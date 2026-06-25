# Source: https://github.com/suavecito585/mcp-discord/blob/main/src/errorHandler.ts

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# errorHandler.ts

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/src/errorHandler.ts)

History

80 lines (69 loc) · 2.62 KB

 main

/

# errorHandler.ts

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

80 lines (69 loc) · 2.62 KB

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/src/errorHandler.ts)

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

// Discord API error handler for MCP tools

import { ToolResponse } from './tools/types.js';

/\*\*

\* A unified error handler for Discord API errors

\* @param error - The error object from Discord API calls

\* @param clientId - Optional Discord Client ID for custom invite links

\* @returns A standard tool response with error message and potential solution

\*/

export function handleDiscordError(error: any, clientId?: string): ToolResponse {

// Ensure error is in the expected format for checking

const errorMessage \= typeof error \=== 'string'

? error

: error?.message || String(error);

const errorCode \= error?.code;

// Generate invite link based on client ID if provided

const inviteLink \= clientId

? \`https://discord.com/oauth2/authorize?client\_id=${clientId}&scope=bot&permissions=8\`

: "https://discord.com/oauth2/authorize?client\_id=YOUR\_CLIENT\_ID&scope=bot&permissions=52076489808";

// Check for privileged intents errors

if (errorMessage.includes('Privileged intent provided is not enabled or whitelisted')) {

return {

content: \[{

type: "text",

text: \`Error: Privileged intents are not enabled.

Solution: Please enable the required intents (Message Content, Server Members, Presence) in the Discord Developer Portal for your bot application.

For detailed instructions, check the Prerequisites section in our README.\`

}\],

isError: true

};

}

// Check for unauthorized/bot not in server errors

if (

errorCode \=== 50001 || // Missing Access

errorCode \=== 10004 || // Unknown Guild

errorMessage.includes('Missing Access') ||

errorMessage.includes('Unknown Guild') ||

errorMessage.includes('Missing Permissions')

) {

return {

content: \[{

type: "text",

text: \`Error: The bot is not a member of the target Discord server or lacks required permissions.

Solution: Please add the bot to the target server using this Discord invite link:

${inviteLink}

According to Discord's security model, a bot can only access information from servers it has been explicitly added to.\`

}\],

isError: true

};

}

// Check for rate limiting

if (errorCode \=== 429 || errorMessage.includes('rate limit')) {

return {

content: \[{

type: "text",

text: \`Error: Discord API rate limit reached.

Solution: Please wait a moment before trying again. If this persists, consider spacing out your requests.\`

}\],

isError: true

};

}

// General error response for other cases

return {

content: \[{

type: "text",

text: \`Discord API Error: ${errorMessage}\`

}\],

isError: true

};

}