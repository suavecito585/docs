# Source: https://github.com/suavecito585/docs/blob/main/agent-ready/visibility.mdx

[suavecito585](https://github.com/suavecito585) / **[docs](https://github.com/suavecito585/docs)** Public

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
 

 

## FilesExpand file tree

 main

/

# visibility.mdx

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

[![suavecito585](https://avatars.githubusercontent.com/u/216850138?v=4&size=40)](https://github.com/suavecito585) [suavecito585](https://github.com/suavecito585/docs/commits?author=suavecito585)

[Initial commit from Mintlify hosted docs](https://github.com/suavecito585/docs/commit/7dab2d003d4fa310aaf3e9a581859dc321793595)

May 12, 2026

[7dab2d0](https://github.com/suavecito585/docs/commit/7dab2d003d4fa310aaf3e9a581859dc321793595) · May 12, 2026

## History

[History](https://github.com/suavecito585/docs/commits/main/agent-ready/visibility.mdx)

Open commit details

History

85 lines (67 loc) · 3.13 KB

## FilesExpand file tree

 main

/

# visibility.mdx

Copy path

Top

## File metadata and controls

- Preview
 
- Code
 
- Blame
 

85 lines (67 loc) · 3.13 KB

[Raw](https://github.com/suavecito585/docs/raw/refs/heads/main/agent-ready/visibility.mdx)

Copy raw file

Download raw file

Outline

Edit and raw actions

<table><tbody><tr><th>title</th><td>Visibility</td></tr><tr><th>description</th><td>Show different content to humans and AI agents</td></tr><tr><th>icon</th><td>eye</td></tr></tbody></table>

The `Visibility` component lets a single page serve two audiences: humans reading on the web and AI agents processing the Markdown output. Content marked `for="humans"` appears on the rendered page but is excluded from Markdown exports. Content marked `for="agents"` is hidden on the web but included in Markdown.

This means you can write conversational, UI-centric instructions for humans and structured, machine-readable instructions for AI — without maintaining two separate pages.

## How it works

Mintlify serves every page at two URLs:

- `https://docs.example.com/page` — the rendered site, for humans
- `https://docs.example.com/page.md` — the raw Markdown, for AI agents

`Visibility` controls what appears at each URL.

## Example

```mdx
<Visibility for="humans">
  <Steps>
    <Step title="Open the dashboard">
      Navigate to [dashboard.example.com](https://dashboard.example.com) and sign in.
    </Step>
    <Step title="Create an API key">
      Go to **Settings → API Keys** and click **New key**.
    </Step>
  </Steps>
</Visibility>

<Visibility for="agents">
  To authenticate, send a POST request to `/v1/auth/token` with the user's
  email and password in the request body. The response includes a bearer token
  valid for 24 hours. Pass this token as `Authorization: Bearer <token>` on
  all subsequent requests.
</Visibility>
```

Human readers see the step-by-step UI walkthrough. AI agents processing the Markdown get the direct API instructions instead.

## Props

\- \`"humans"\` — visible on the rendered web page, excluded from \`.md\` export - \`"agents"\` — hidden on the rendered web page, included in \`.md\` export

## When to use it

Show UI screenshots and button clicks to humans. Give agents the equivalent API calls. Show a visual settings panel to humans. Give agents the equivalent JSON or CLI flags. Show a friendly explanation to humans. Give agents structured error codes and remediation steps. Include rich diagrams and narrative for humans. Provide a concise structured summary for agents.

## Combining with Prompt

`Visibility` and `Prompt` complement each other well. Use `Visibility` to give agents structured context, then use `Prompt` to give human readers a prompt they can use to ask an AI about that same content.

```mdx
<Visibility for="agents">
  ## Authentication schema
  - Method: Bearer token
  - Header: `Authorization: Bearer <token>`
  - Token TTL: 86400 seconds
  - Refresh endpoint: POST /v1/auth/refresh
</Visibility>

<Prompt description="Ask about authentication" icon="lock">
  Explain how authentication works in this API and show me example code for
  getting a token and making an authenticated request.
</Prompt>
```