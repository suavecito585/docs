# Source: https://github.com/suavecito585/mcp-discord/blob/main/src/transport.ts

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# transport.ts

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/src/transport.ts)

History

162 lines (145 loc) · 5.4 KB

 main

/

# transport.ts

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

162 lines (145 loc) · 5.4 KB

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/src/transport.ts)

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

143

144

145

146

147

148

149

150

151

152

153

154

155

156

157

158

159

160

161

162

import { Server } from "@modelcontextprotocol/sdk/server/index.js";

import { StreamableHTTPServerTransport } from "@modelcontextprotocol/sdk/server/streamableHttp.js";

import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

import express, { Request, Response } from "express";

import { toolList } from './toolList.js';

import {

createToolContext,

loginHandler,

sendMessageHandler,

getForumChannelsHandler,

createForumPostHandler,

getForumPostHandler,

replyToForumHandler,

deleteForumPostHandler,

createTextChannelHandler,

deleteChannelHandler,

readMessagesHandler,

getServerInfoHandler,

addReactionHandler,

addMultipleReactionsHandler,

removeReactionHandler,

deleteMessageHandler,

createWebhookHandler,

sendWebhookMessageHandler,

editWebhookHandler,

deleteWebhookHandler,

editCategoryHandler,

createCategoryHandler,

deleteCategoryHandler,

listServersHandler,

searchMessagesHandler

} from './tools/tools.js';

import { Client, GatewayIntentBits } from "discord.js";

import { info, error } from './logger.js';

export interface MCPTransport {

start(server: Server): Promise<void\>;

stop(): Promise<void\>;

}

export class StdioTransport implements MCPTransport {

private transport: StdioServerTransport | null \= null;

async start(server: Server): Promise<void\> {

this.transport \= new StdioServerTransport();

await server.connect(this.transport);

}

async stop(): Promise<void\> {

if (this.transport) {

await this.transport.close();

this.transport \= null;

}

}

}

export class StreamableHttpTransport implements MCPTransport {

private app: express.Application;

private server: Server | null \= null;

private httpServer: any \= null;

private transport: StreamableHTTPServerTransport | null \= null;

private toolContext: ReturnType<typeof createToolContext\> | null \= null;

private sessionId: string \= '';

constructor(private port: number \= 8080) {

this.app \= express();

this.app.use(express.json());

this.sessionId \= \`session\_${Date.now()}\_${Math.random().toString(36).substring(2, 10)}\`;

info(\`Created HTTP transport with session ID: ${this.sessionId}\`);

}

async start(server: Server): Promise<void\> {

this.server \= server;

info('Starting HTTP transport with server: ' + String(!!this.server));

// Try to get client from the DiscordMCPServer instance

if (server) {

const anyServer \= server as any;

let client: Client | undefined;

if (anyServer.\_context?.client) {

client \= anyServer.\_context.client;

info('Found client in server.\_context');

}

else if (anyServer.client instanceof Client) {

client \= anyServer.client;

info('Found client directly on server object');

}

else if (anyServer.\_parent?.client instanceof Client) {

client \= anyServer.\_parent.client;

info('Found client in server.\_parent');

}

if (client) {

this.toolContext \= createToolContext(client);

info('Tool context initialized with Discord client');

} else {

info('Creating new Discord client for transport');

const newClient \= new Client({

intents: \[

GatewayIntentBits.Guilds,

GatewayIntentBits.GuildMessages,

GatewayIntentBits.MessageContent,

GatewayIntentBits.GuildMessageReactions

\]

});

this.toolContext \= createToolContext(newClient);

info('Tool context initialized with new Discord client');

}

}

// Create transport

this.transport \= new StreamableHTTPServerTransport({

sessionIdGenerator: undefined // stateless

});

// Connect the transport

await this.server.connect(this.transport);

info('Transport connected');

// Setup /mcp endpoint to use transport.handleRequest()

this.app.all('/mcp', async (req: Request, res: Response) \=> {

try {

await this.transport!.handleRequest(req, res, req.body);

} catch (err) {

error('Error handling MCP request: ' + String(err));

if (!res.headersSent) {

res.status(500).json({ error: 'Internal server error' });

}

}

});

return new Promise((resolve) \=> {

this.httpServer \= this.app.listen(this.port, '0.0.0.0', () \=> {

info(\`MCP Server listening on 0.0.0.0:${this.port}\`);

resolve();

});

});

}

async stop(): Promise<void\> {

if (this.transport) {

await this.transport.close();

this.transport \= null;

}

if (this.server) {

await this.server.close();

this.server \= null;

}

if (this.httpServer) {

return new Promise((resolve) \=> {

this.httpServer.close(() \=> {

info('HTTP server closed');

this.httpServer \= null;

resolve();

});

});

}

}

}