# Source: https://github.com/suavecito585/mcp-discord/blob/main/src/logger.ts

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# logger.ts

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

[![barryyip0625](https://avatars.githubusercontent.com/u/111196081?v=4&size=40)](https://github.com/barryyip0625) [barryyip0625](https://github.com/suavecito585/mcp-discord/commits?author=barryyip0625)

[feat: add logger utility and improve Discord login error message for …](https://github.com/suavecito585/mcp-discord/commit/e10d5166bc9697887dd193a339f153cecc1b2993)

Open commit details

May 11, 2025

[e10d516](https://github.com/suavecito585/mcp-discord/commit/e10d5166bc9697887dd193a339f153cecc1b2993) · May 11, 2025

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/src/logger.ts)

Open commit details

History

19 lines (17 loc) · 422 Bytes

## FilesExpand file tree

 main

/

# logger.ts

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

19 lines (17 loc) · 422 Bytes

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/src/logger.ts)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

export function log(message: string, level: 'info' | 'error' = 'info') { const logMessage = { jsonrpc: '2.0', method: 'log', params: { level, message } }; process.stdout.write(JSON.stringify(logMessage) + '\\n'); } export function info(message: string) { log(message, 'info'); } export function error(message: string) { log(message, 'error'); }

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

export function log(message: string, level: 'info' | 'error' \= 'info') {

const logMessage \= {

jsonrpc: '2.0',

method: 'log',

params: {

level,

message

}

};

process.stdout.write(JSON.stringify(logMessage) + '\\n');

}

export function info(message: string) {

log(message, 'info');

}

export function error(message: string) {

log(message, 'error');

}