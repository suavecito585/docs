# Source: https://github.com/suavecito585/mcp-discord/blob/main/src/server.ts

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# server.ts

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/src/server.ts)

History

354 lines (300 loc) · 12.6 KB

## FilesExpand file tree

 main

/

# server.ts

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

354 lines (300 loc) · 12.6 KB

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/src/server.ts)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

import { Server } from "@modelcontextprotocol/sdk/server/index.js"; import { Client } from "discord.js"; import { z } from "zod"; import { CallToolRequestSchema, ListToolsRequestSchema, } from "@modelcontextprotocol/sdk/types.js"; import { toolList } from './toolList.js'; import { createToolContext, loginHandler, sendMessageHandler, getForumChannelsHandler, createForumPostHandler, getForumPostHandler, listForumThreadsHandler, replyToForumHandler, deleteForumPostHandler, getForumTagsHandler, setForumTagsHandler, updateForumPostHandler, editMessageHandler, createTextChannelHandler, createForumChannelHandler, editChannelHandler, deleteChannelHandler, readMessagesHandler, getServerInfoHandler, addReactionHandler, addMultipleReactionsHandler, removeReactionHandler, getReactionUsersHandler, deleteMessageHandler, createWebhookHandler, sendWebhookMessageHandler, editWebhookHandler, deleteWebhookHandler, createCategoryHandler, editCategoryHandler, deleteCategoryHandler, createVoiceChannelHandler, setChannelPermissionsHandler, removeChannelPermissionsHandler, listRolesHandler, createRoleHandler, editRoleHandler, deleteRoleHandler, assignRoleHandler, removeRoleHandler, listMembersHandler, getMemberHandler, listServersHandler, searchMessagesHandler } from './tools/tools.js'; import { MCPTransport } from './transport.js'; import { info, error } from './logger.js'; export class DiscordMCPServer { private server: Server; private toolContext: ReturnType<typeof createToolContext>; private clientStatusInterval: NodeJS.Timeout | null = null; constructor( private client: Client, private transport: MCPTransport ) { this.server = new Server( { name: "MCP-Discord", version: "1.0.0" }, { capabilities: { tools: {} } } ); this.toolContext = createToolContext(client); this.setupHandlers(); } private setupHandlers() { // Set up the tool list this.server.setRequestHandler(ListToolsRequestSchema, async () => { return { tools: toolList }; }); // Handle tool execution requests this.server.setRequestHandler(CallToolRequestSchema, async (request) => { const { name, arguments: args } = request.params; try { let toolResponse; switch (name) { case "discord\_create\_category": toolResponse = await createCategoryHandler(args, this.toolContext); return toolResponse; case "discord\_edit\_category": toolResponse = await editCategoryHandler(args, this.toolContext); return toolResponse; case "discord\_delete\_category": toolResponse = await deleteCategoryHandler(args, this.toolContext); return toolResponse; case "discord\_login": toolResponse = await loginHandler(args, this.toolContext); this.logClientState("after discord\_login handler"); return toolResponse; case "discord\_send": this.logClientState("before discord\_send handler"); toolResponse = await sendMessageHandler(args, this.toolContext); return toolResponse; case "discord\_get\_forum\_channels": this.logClientState("before discord\_get\_forum\_channels handler"); toolResponse = await getForumChannelsHandler(args, this.toolContext); return toolResponse; case "discord\_create\_forum\_post": this.logClientState("before discord\_create\_forum\_post handler"); toolResponse = await createForumPostHandler(args, this.toolContext); return toolResponse; case "discord\_get\_forum\_post": this.logClientState("before discord\_get\_forum\_post handler"); toolResponse = await getForumPostHandler(args, this.toolContext); return toolResponse; case "discord\_list\_forum\_threads": this.logClientState("before discord\_list\_forum\_threads handler"); toolResponse = await listForumThreadsHandler(args, this.toolContext); return toolResponse; case "discord\_reply\_to\_forum": this.logClientState("before discord\_reply\_to\_forum handler"); toolResponse = await replyToForumHandler(args, this.toolContext); return toolResponse; case "discord\_delete\_forum\_post": this.logClientState("before discord\_delete\_forum\_post handler"); toolResponse = await deleteForumPostHandler(args, this.toolContext); return toolResponse; case "discord\_get\_forum\_tags": this.logClientState("before discord\_get\_forum\_tags handler"); toolResponse = await getForumTagsHandler(args, this.toolContext); return toolResponse; case "discord\_set\_forum\_tags": this.logClientState("before discord\_set\_forum\_tags handler"); toolResponse = await setForumTagsHandler(args, this.toolContext); return toolResponse; case "discord\_update\_forum\_post": this.logClientState("before discord\_update\_forum\_post handler"); toolResponse = await updateForumPostHandler(args, this.toolContext); return toolResponse; case "discord\_edit\_message": this.logClientState("before discord\_edit\_message handler"); toolResponse = await editMessageHandler(args, this.toolContext); return toolResponse; case "discord\_create\_text\_channel": this.logClientState("before discord\_create\_text\_channel handler"); toolResponse = await createTextChannelHandler(args, this.toolContext); return toolResponse; case "discord\_create\_forum\_channel": this.logClientState("before discord\_create\_forum\_channel handler"); toolResponse = await createForumChannelHandler(args, this.toolContext); return toolResponse; case "discord\_edit\_channel": this.logClientState("before discord\_edit\_channel handler"); toolResponse = await editChannelHandler(args, this.toolContext); return toolResponse; case "discord\_delete\_channel": this.logClientState("before discord\_delete\_channel handler"); toolResponse = await deleteChannelHandler(args, this.toolContext); return toolResponse; case "discord\_read\_messages": this.logClientState("before discord\_read\_messages handler"); toolResponse = await readMessagesHandler(args, this.toolContext); return toolResponse; case "discord\_get\_server\_info": this.logClientState("before discord\_get\_server\_info handler"); toolResponse = await getServerInfoHandler(args, this.toolContext); return toolResponse; case "discord\_add\_reaction": this.logClientState("before discord\_add\_reaction handler"); toolResponse = await addReactionHandler(args, this.toolContext); return toolResponse; case "discord\_add\_multiple\_reactions": this.logClientState("before discord\_add\_multiple\_reactions handler"); toolResponse = await addMultipleReactionsHandler(args, this.toolContext); return toolResponse; case "discord\_remove\_reaction": this.logClientState("before discord\_remove\_reaction handler"); toolResponse = await removeReactionHandler(args, this.toolContext); return toolResponse; case "discord\_get\_reaction\_users": this.logClientState("before discord\_get\_reaction\_users handler"); toolResponse = await getReactionUsersHandler(args, this.toolContext); return toolResponse; case "discord\_delete\_message": this.logClientState("before discord\_delete\_message handler"); toolResponse = await deleteMessageHandler(args, this.toolContext); return toolResponse; case "discord\_create\_webhook": this.logClientState("before discord\_create\_webhook handler"); toolResponse = await createWebhookHandler(args, this.toolContext); return toolResponse; case "discord\_send\_webhook\_message": this.logClientState("before discord\_send\_webhook\_message handler"); toolResponse = await sendWebhookMessageHandler(args, this.toolContext); return toolResponse; case "discord\_edit\_webhook": this.logClientState("before discord\_edit\_webhook handler"); toolResponse = await editWebhookHandler(args, this.toolContext); return toolResponse; case "discord\_delete\_webhook": this.logClientState("before discord\_delete\_webhook handler"); toolResponse = await deleteWebhookHandler(args, this.toolContext); return toolResponse; case "discord\_list\_servers": this.logClientState("before discord\_list\_servers handler"); toolResponse = await listServersHandler(args, this.toolContext); return toolResponse; case "discord\_search\_messages": this.logClientState("before discord\_search\_messages handler"); toolResponse = await searchMessagesHandler(args, this.toolContext); return toolResponse; case "discord\_list\_roles": toolResponse = await listRolesHandler(args, this.toolContext); return toolResponse; case "discord\_create\_role": toolResponse = await createRoleHandler(args, this.toolContext); return toolResponse; case "discord\_edit\_role": toolResponse = await editRoleHandler(args, this.toolContext); return toolResponse; case "discord\_delete\_role": toolResponse = await deleteRoleHandler(args, this.toolContext); return toolResponse; case "discord\_assign\_role": toolResponse = await assignRoleHandler(args, this.toolContext); return toolResponse; case "discord\_remove\_role": toolResponse = await removeRoleHandler(args, this.toolContext); return toolResponse; case "discord\_list\_members": toolResponse = await listMembersHandler(args, this.toolContext); return toolResponse; case "discord\_get\_member": toolResponse = await getMemberHandler(args, this.toolContext); return toolResponse; case "discord\_create\_voice\_channel": toolResponse = await createVoiceChannelHandler(args, this.toolContext); return toolResponse; case "discord\_set\_channel\_permissions": toolResponse = await setChannelPermissionsHandler(args, this.toolContext); return toolResponse; case "discord\_remove\_channel\_permissions": toolResponse = await removeChannelPermissionsHandler(args, this.toolContext); return toolResponse; default: throw new Error(\`Unknown tool: ${name}\`); } } catch (error) { if (error instanceof z.ZodError) { return { content: \[{ type: "text", text: \`Invalid arguments: ${error.errors .map((e: z.ZodIssue) => \`${e.path.join(".")}: ${e.message}\`) .join(", ")}\` }\], isError: true }; } const errorMessage = error instanceof Error ? error.message : 'Unknown error'; return { content: \[{ type: "text", text: \`Error executing tool: ${errorMessage}\` }\], isError: true }; } }); } private logClientState(context: string) { info(\`Discord client state \[${context}\]: ${JSON.stringify({ isReady: this.client.isReady(), hasToken: !!this.client.token, user: this.client.user ? { id: this.client.user.id, tag: this.client.user.tag, } : null })}\`); } async start() { // Add client to server context so transport can access it (this.server as any).\_context = { client: this.client }; (this.server as any).client = this.client; // Setup periodic client state logging this.clientStatusInterval = setInterval(() => { this.logClientState("periodic check"); }, 10000); await this.transport.start(this.server); } async stop() { // Clear the periodic check interval if (this.clientStatusInterval) { clearInterval(this.clientStatusInterval); this.clientStatusInterval = null; } await this.transport.stop(); } }

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

281

282

283

284

285

286

287

288

289

290

291

292

293

294

295

296

297

298

299

300

301

302

303

304

305

306

307

308

309

310

311

312

313

314

315

316

317

318

319

320

321

322

323

324

325

326

327

328

329

330

331

332

333

334

335

336

337

338

339

340

341

342

343

344

345

346

347

348

349

350

351

352

353

354

import { Server } from "@modelcontextprotocol/sdk/server/index.js";

import { Client } from "discord.js";

import { z } from "zod";

import {

CallToolRequestSchema,

ListToolsRequestSchema,

} from "@modelcontextprotocol/sdk/types.js";

import { toolList } from './toolList.js';

import {

createToolContext,

loginHandler,

sendMessageHandler,

getForumChannelsHandler,

createForumPostHandler,

getForumPostHandler,

listForumThreadsHandler,

replyToForumHandler,

deleteForumPostHandler,

getForumTagsHandler,

setForumTagsHandler,

updateForumPostHandler,

editMessageHandler,

createTextChannelHandler,

createForumChannelHandler,

editChannelHandler,

deleteChannelHandler,

readMessagesHandler,

getServerInfoHandler,

addReactionHandler,

addMultipleReactionsHandler,

removeReactionHandler,

getReactionUsersHandler,

deleteMessageHandler,

createWebhookHandler,

sendWebhookMessageHandler,

editWebhookHandler,

deleteWebhookHandler,

createCategoryHandler,

editCategoryHandler,

deleteCategoryHandler,

createVoiceChannelHandler,

setChannelPermissionsHandler,

removeChannelPermissionsHandler,

listRolesHandler,

createRoleHandler,

editRoleHandler,

deleteRoleHandler,

assignRoleHandler,

removeRoleHandler,

listMembersHandler,

getMemberHandler,

listServersHandler,

searchMessagesHandler

} from './tools/tools.js';

import { MCPTransport } from './transport.js';

import { info, error } from './logger.js';

export class DiscordMCPServer {

private server: Server;

private toolContext: ReturnType<typeof createToolContext\>;

private clientStatusInterval: NodeJS.Timeout | null \= null;

constructor(

private client: Client,

private transport: MCPTransport

) {

this.server \= new Server(

{

name: "MCP-Discord",

version: "1.0.0"

},

{

capabilities: {

tools: {}

}

}

);

this.toolContext \= createToolContext(client);

this.setupHandlers();

}

private setupHandlers() {

// Set up the tool list

this.server.setRequestHandler(ListToolsRequestSchema, async () \=> {

return {

tools: toolList

};

});

// Handle tool execution requests

this.server.setRequestHandler(CallToolRequestSchema, async (request) \=> {

const { name, arguments: args } \= request.params;

try {

let toolResponse;

switch (name) {

case "discord\_create\_category":

toolResponse \= await createCategoryHandler(args, this.toolContext);

return toolResponse;

case "discord\_edit\_category":

toolResponse \= await editCategoryHandler(args, this.toolContext);

return toolResponse;

case "discord\_delete\_category":

toolResponse \= await deleteCategoryHandler(args, this.toolContext);

return toolResponse;

case "discord\_login": toolResponse \= await loginHandler(args, this.toolContext);

this.logClientState("after discord\_login handler");

return toolResponse;

case "discord\_send":

this.logClientState("before discord\_send handler");

toolResponse \= await sendMessageHandler(args, this.toolContext);

return toolResponse;

case "discord\_get\_forum\_channels":

this.logClientState("before discord\_get\_forum\_channels handler");

toolResponse \= await getForumChannelsHandler(args, this.toolContext);

return toolResponse;

case "discord\_create\_forum\_post":

this.logClientState("before discord\_create\_forum\_post handler");

toolResponse \= await createForumPostHandler(args, this.toolContext);

return toolResponse;

case "discord\_get\_forum\_post":

this.logClientState("before discord\_get\_forum\_post handler");

toolResponse \= await getForumPostHandler(args, this.toolContext);

return toolResponse;

case "discord\_list\_forum\_threads":

this.logClientState("before discord\_list\_forum\_threads handler");

toolResponse \= await listForumThreadsHandler(args, this.toolContext);

return toolResponse;

case "discord\_reply\_to\_forum":

this.logClientState("before discord\_reply\_to\_forum handler");

toolResponse \= await replyToForumHandler(args, this.toolContext);

return toolResponse;

case "discord\_delete\_forum\_post":

this.logClientState("before discord\_delete\_forum\_post handler");

toolResponse \= await deleteForumPostHandler(args, this.toolContext);

return toolResponse;

case "discord\_get\_forum\_tags":

this.logClientState("before discord\_get\_forum\_tags handler");

toolResponse \= await getForumTagsHandler(args, this.toolContext);

return toolResponse;

case "discord\_set\_forum\_tags":

this.logClientState("before discord\_set\_forum\_tags handler");

toolResponse \= await setForumTagsHandler(args, this.toolContext);

return toolResponse;

toolResponse \= await getMemberHandler(args, this.toolContext);

return toolResponse;

case "discord\_create\_voice\_channel":

toolResponse \= await createVoiceChannelHandler(args, this.toolContext);

return toolResponse;

case "discord\_set\_channel\_permissions":

toolResponse \= await setChannelPermissionsHandler(args, this.toolContext);

return toolResponse;

case "discord\_remove\_channel\_permissions":

toolResponse \= await removeChannelPermissionsHandler(args, this.toolContext);

return toolResponse;

default:

throw new Error(\`Unknown tool: ${name}\`);

}

} catch (error) {

if (error instanceof z.ZodError) {

return {

content: \[{

type: "text",

text: \`Invalid arguments: ${error.errors

.map((e: z.ZodIssue) \=> \`${e.path.join(".")}: ${e.message}\`)

.join(", ")}\`

}\],

isError: true

};

}

const errorMessage \= error instanceof Error ? error.message : 'Unknown error';

return {

content: \[{ type: "text", text: \`Error executing tool: ${errorMessage}\` }\],

isError: true

};

}

});

}

private logClientState(context: string) {

info(\`Discord client state \[${context}\]: ${JSON.stringify({

isReady: this.client.isReady(),

hasToken: !!this.client.token,

user: this.client.user ? {

id: this.client.user.id,

tag: this.client.user.tag,

} : null

})}\`);

}

async start() {

// Add client to server context so transport can access it

(this.server as any).\_context \= { client: this.client };

(this.server as any).client \= this.client;

// Setup periodic client state logging

this.clientStatusInterval \= setInterval(() \=> {

this.logClientState("periodic check");

}, 10000);

await this.transport.start(this.server);

}

async stop() {

// Clear the periodic check interval

if (this.clientStatusInterval) {

clearInterval(this.clientStatusInterval);

this.clientStatusInterval \= null;

}

await this.transport.stop();

}

}