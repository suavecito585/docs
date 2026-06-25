# Source: https://github.com/suavecito585/mcp-discord/blob/main/src/notifications.ts

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# notifications.ts

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

[![barryyip0625](https://avatars.githubusercontent.com/u/111196081?v=4&size=40)](https://github.com/barryyip0625) [barryyip0625](https://github.com/suavecito585/mcp-discord/commits?author=barryyip0625)

[fix:](https://github.com/suavecito585/mcp-discord/commit/188d3c173829da1b04feed1af709004515886c34) [resolve](https://github.com/suavecito585/mcp-discord/commit/188d3c173829da1b04feed1af709004515886c34) [barryyip0625#27](https://github.com/barryyip0625/mcp-discord/issues/27) [and refresh README](https://github.com/suavecito585/mcp-discord/commit/188d3c173829da1b04feed1af709004515886c34)

Open commit details

Mar 18, 2026

[188d3c1](https://github.com/suavecito585/mcp-discord/commit/188d3c173829da1b04feed1af709004515886c34) · Mar 18, 2026

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/src/notifications.ts)

Open commit details

History

46 lines (38 loc) · 1.21 KB

## FilesExpand file tree

 main

/

# notifications.ts

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

46 lines (38 loc) · 1.21 KB

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/src/notifications.ts)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

import { Server } from '@modelcontextprotocol/sdk/server/index.js' export type Level = 'debug' | 'info' | 'notice' | 'warning' | 'error' | 'critical' | 'alert' | 'emergency'; const levelPriority: Record<Level, number> = { debug: 0, info: 1, notice: 2, warning: 3, error: 4, critical: 5, alert: 6, emergency: 7, }; export let currentLevel: Level = 'info'; export function setLevel(level: Level) { if (!levelPriority.hasOwnProperty(level)) return false; currentLevel = level; return true; } export function log(server: Server | null | undefined, message: string, level: Level = 'info') { if (levelPriority\[level\] < levelPriority\[currentLevel\]) return; if (!server?.transport) return; server.sendLoggingMessage( { level: level, logger: 'mcp-discord', data: { text: message }, } ); } export function info(server: Server | null | undefined, message: string) { log(server, message, 'info'); } export function warning(server: Server | null | undefined, message: string) { log(server, message, 'warning'); } export function error(server: Server | null | undefined, message: string) { log(server, message, 'error'); }

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

import { Server } from '@modelcontextprotocol/sdk/server/index.js'

export type Level \= 'debug' | 'info' | 'notice' | 'warning' | 'error' | 'critical' | 'alert' | 'emergency';

const levelPriority: Record<Level, number\> \= {

debug: 0,

info: 1,

notice: 2,

warning: 3,

error: 4,

critical: 5,

alert: 6,

emergency: 7,

};

export let currentLevel: Level \= 'info';

export function setLevel(level: Level) {

if (!levelPriority.hasOwnProperty(level)) return false;

currentLevel \= level;

return true;

}

export function log(server: Server | null | undefined, message: string, level: Level \= 'info') {

if (levelPriority\[level\] < levelPriority\[currentLevel\]) return;

if (!server?.transport) return;

server.sendLoggingMessage(

{

level: level,

logger: 'mcp-discord',

data: { text: message },

}

);

}

export function info(server: Server | null | undefined, message: string) {

log(server, message, 'info');

}

export function warning(server: Server | null | undefined, message: string) {

log(server, message, 'warning');

}

export function error(server: Server | null | undefined, message: string) {

log(server, message, 'error');

}