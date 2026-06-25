# Source: https://github.com/suavecito585/mcp-discord/blob/main/Makefile

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# Makefile

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/Makefile)

History

14 lines (10 loc) · 580 Bytes

 main

/

# Makefile

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

14 lines (10 loc) · 580 Bytes

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/Makefile)

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

.PHONY: help

.DEFAULT\_GOAL := help

# initialise .env file for all targets if it exists

\-include .env

help: #\# Show this help.

@grep -E '^\[a-zA-Z\_-\]+:.\*?## .\*$$' $(MAKEFILE\_LIST) | awk 'BEGIN {FS = ":.\*?## "}; {printf "\\033\[36m%-30s\\033\[0m %s\\n", $$1, $$2}'

# Document each target that should appear in help using a comment placed after the target's colon, starting with '##' (as shown above).

# Targets without such a comment will not appear in the help output.

run-inspector: #\# Run the MCP inspector.

@npx @modelcontextprotocol/inspector -e DISCORD\_TOKEN=$(DISCORD\_TOKEN)