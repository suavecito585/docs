# Source: https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/Makefile

.PHONY: help
.DEFAULT\_GOAL := help

# initialise .env file for all targets if it exists
-include .env

help: ## Show this help.
	@grep -E '^\[a-zA-Z\_-\]+:.\*?## .\*$$' $(MAKEFILE\_LIST) | awk 'BEGIN {FS = ":.\*?## "}; {printf "\\033\[36m%-30s\\033\[0m %s\\n", $$1, $$2}'

# Document each target that should appear in help using a comment placed after the target's colon, starting with '##' (as shown above).
# Targets without such a comment will not appear in the help output.

run-inspector: ## Run the MCP inspector.
	@npx @modelcontextprotocol/inspector -e DISCORD\_TOKEN=$(DISCORD\_TOKEN)