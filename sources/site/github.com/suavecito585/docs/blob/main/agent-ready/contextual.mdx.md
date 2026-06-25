# Source: https://github.com/suavecito585/docs/blob/main/agent-ready/contextual.mdx

[suavecito585](https://github.com/suavecito585) / **[docs](https://github.com/suavecito585/docs)** Public

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
 

 

## FilesExpand file tree

 main

/

# contextual.mdx

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/docs/commits/main/agent-ready/contextual.mdx)

History

91 lines (71 loc) · 2.76 KB

 main

/

# contextual.mdx

Copy path

Top

## File metadata and controls

- Preview
 
- Code
 
- Blame
 

91 lines (71 loc) · 2.76 KB

[Raw](https://github.com/suavecito585/docs/raw/refs/heads/main/agent-ready/contextual.mdx)

Copy raw file

Download raw file

Outline

Edit and raw actions

<table><tbody><tr><th>title</th><td>Contextual menu</td></tr><tr><th>description</th><td>Give readers one-click access to AI tools and integrations</td></tr><tr><th>icon</th><td>bolt</td></tr></tbody></table>

The contextual toolbar is a floating action bar that appears on every page of your docs. It lets readers instantly copy page content, open it in an AI assistant, or add your docs as an MCP server — without leaving the page.

Configure it in `docs.json` under `contextual.options`:

```json
{
  "contextual": {
    "options": ["copy", "view", "claude", "chatgpt", "mcp", "cursor", "vscode"]
  }
}
```

## Available options

### Content actions

| Option | Description |
| --- | --- |
| `copy` | Copies the page as Markdown to the clipboard |
| `view` | Opens the raw Markdown version of the page (`.md` URL) |

### AI assistants

| Option | Description |
| --- | --- |
| `claude` | Opens the page in Claude |
| `chatgpt` | Opens the page in ChatGPT |
| `perplexity` | Opens the page in Perplexity |
| `grok` | Opens the page in Grok |
| `aistudio` | Opens the page in Google AI Studio |

### Editor integrations

| Option | Description |
| --- | --- |
| `cursor` | Adds the page to Cursor's context |
| `vscode` | Adds the page to VS Code Copilot |
| `windsurf` | Adds the page to Windsurf's Cascade |
| `devin` | Opens the page in Devin |

### MCP

| Option | Description |
| --- | --- |
| `mcp` | Shows instructions for using your docs as an MCP server |
| `add-mcp` | Provides a one-click prompt to add your docs MCP server to an AI tool |

The \`mcp\` and \`add-mcp\` options are especially powerful — they let developers connect your entire docs site to any MCP-compatible AI assistant, so it can answer questions about your product directly.

## Custom options

You can add custom entries to the toolbar with a title, description, icon, and link. The `href` supports dynamic placeholders:

| Placeholder | Resolves to |
| --- | --- |
| `$page` | The current page's full URL |
| `$path` | The current page's path |
| `$mcp` | Your docs MCP server URL |

```json
{
  "contextual": {
    "options": [
      "copy",
      "claude",
      {
        "title": "Open issue",
        "description": "Report a problem with this page",
        "icon": "github",
        "href": "https://github.com/your-org/docs/issues/new?title=Issue+on+$path"
      }
    ]
  }
}
```

The contextual toolbar is only visible on preview and production deployments, not in \`mint dev\` local preview.

## Pairing with Visibility

The toolbar's `copy` and `view` options expose your page's Markdown content directly. If you use the [`Visibility`](https://github.com/suavecito585/docs/blob/main/agent-ready/visibility) component, the `for="agents"` blocks will be included in that Markdown — giving AI assistants structured context that human readers don't see.