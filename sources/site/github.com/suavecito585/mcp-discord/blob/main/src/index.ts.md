# Source: https://github.com/suavecito585/mcp-discord/blob/main/src/index.ts

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# index.ts

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/src/index.ts)

History

142 lines (129 loc) · 4.82 KB

 main

/

# index.ts

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

142 lines (129 loc) · 4.82 KB

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/src/index.ts)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

48

49

50

51

52

53

54

55

56

57

58

59

60

61

62

63

64

65

66

67

68

69

70

71

72

73

74

75

76

77

78

79

80

81

82

83

84

85

86

87

88

89

90

91

92

93

94

95

96

97

98

99

100

101

102

103

104

105

106

107

108

109

110

111

112

113

114

115

116

117

118

119

120

121

122

123

124

125

126

127

128

129

130

131

132

133

134

135

136

137

138

139

140

141

142

#!/usr/bin/env node

import { Client, GatewayIntentBits } from "discord.js";

import { config as dotenvConfig } from 'dotenv';

import { DiscordMCPServer } from './server.js';

import { StdioTransport, StreamableHttpTransport } from './transport.js';

import { info, error } from './logger.js';

// Load environment variables from .env file if exists

dotenvConfig();

// Configuration with priority for command line arguments

const config \= {

DISCORD\_TOKEN: (() \=> {

try {

// First try to get from command line arguments

const configIndex \= process.argv.indexOf('--config');

if (configIndex !== \-1 && configIndex + 1 < process.argv.length) {

const configArg \= process.argv\[configIndex + 1\];

// Handle both string and object formats

if (typeof configArg \=== 'string') {

try {

const parsedConfig \= JSON.parse(configArg);

return parsedConfig.DISCORD\_TOKEN;

} catch (err) {

// If not valid JSON, try using the string directly

return configArg;

}

}

}

// Then try environment variable

return process.env.DISCORD\_TOKEN;

} catch (err) {

error('Error parsing config: ' + String(err));

return null;

}

})(),

TRANSPORT: (() \=> {

// Check for transport type argument

const transportIndex \= process.argv.indexOf('--transport');

if (transportIndex !== \-1 && transportIndex + 1 < process.argv.length) {

return process.argv\[transportIndex + 1\];

}

// Default to stdio

return 'stdio';

})(),

HTTP\_PORT: (() \=> {

// Check for port argument

const portIndex \= process.argv.indexOf('--port');

if (portIndex !== \-1 && portIndex + 1 < process.argv.length) {

return parseInt(process.argv\[portIndex + 1\]);

}

// Default port for MCP

return 8080;

})()

};

// Create Discord client

const client \= new Client({

intents: \[

GatewayIntentBits.Guilds,

GatewayIntentBits.GuildMessages,

GatewayIntentBits.MessageContent,

GatewayIntentBits.GuildMembers

\]

});

// Save token to client for login handler

if (config.DISCORD\_TOKEN) {

client.token \= config.DISCORD\_TOKEN;

}

// Auto-login on startup if token is available

const autoLogin \= async () \=> {

const token \= config.DISCORD\_TOKEN;

if (token) {

try {

await client.login(token);

info('Successfully logged in to Discord');

} catch (err: any) {

if (typeof err.message \=== 'string' && err.message.includes('Privileged intent provided is not enabled or whitelisted')) {

error('Login failed: One or more privileged intents are not enabled in the Discord Developer Portal. Please enable the required intents.');

} else {

error('Auto-login failed: ' + String(err));

}

}

} else {

info("No Discord token found in config, skipping auto-login");

}

};

// Initialize transport based on configuration

const initializeTransport \= () \=> {

switch (config.TRANSPORT.toLowerCase()) {

case 'http':

info(\`Initializing HTTP transport on 0.0.0.0:${config.HTTP\_PORT}\`);

return new StreamableHttpTransport(config.HTTP\_PORT);

case 'stdio':

info('Initializing stdio transport');

return new StdioTransport();

default:

error(\`Unknown transport type: ${config.TRANSPORT}. Falling back to stdio.\`);

return new StdioTransport();

}

};

// Start auto-login process

await autoLogin();

// Create and start MCP server with selected transport

const transport \= initializeTransport();

const mcpServer \= new DiscordMCPServer(client, transport);

try {

await mcpServer.start();

info('MCP server started successfully');

// Keep the Node.js process running

if (config.TRANSPORT.toLowerCase() \=== 'http') {

// Send a heartbeat every 30 seconds to keep the process alive

setInterval(() \=> {

info('MCP server is running');

}, 30000);

// Handle termination signals

process.on('SIGINT', async () \=> {

info('Received SIGINT. Shutting down server...');

await mcpServer.stop();

process.exit(0);

});

process.on('SIGTERM', async () \=> {

info('Received SIGTERM. Shutting down server...');

await mcpServer.stop();

process.exit(0);

});

info('Server running in keep-alive mode. Press Ctrl+C to stop.');

}

} catch (err) {

error('Failed to start MCP server: ' + String(err));

process.exit(1);

}