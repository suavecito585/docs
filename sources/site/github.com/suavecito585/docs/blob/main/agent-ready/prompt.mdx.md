# Source: https://github.com/suavecito585/docs/blob/main/agent-ready/prompt.mdx

[suavecito585](https://github.com/suavecito585) / **[docs](https://github.com/suavecito585/docs)** Public

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
 

 

## FilesExpand file tree

 main

/

# prompt.mdx

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/docs/commits/main/agent-ready/prompt.mdx)

History

75 lines (59 loc) · 2.88 KB

## FilesExpand file tree

 main

/

# prompt.mdx

Copy path

Top

## File metadata and controls

- Preview
 
- Code
 
- Blame
 

75 lines (59 loc) · 2.88 KB

[Raw](https://github.com/suavecito585/docs/raw/refs/heads/main/agent-ready/prompt.mdx)

Copy raw file

Download raw file

Outline

Edit and raw actions

<table><tbody><tr><th>title</th><td>Prompt component</td></tr><tr><th>description</th><td>Embed shareable AI prompts readers can copy or open in Cursor</td></tr><tr><th>icon</th><td>robot</td></tr></tbody></table>

The `Prompt` component displays a pre-built AI prompt with one-click actions to copy it to the clipboard or open it directly in Cursor. It's ideal for any docs page where you want to hand readers a ready-to-use prompt.

## Basic usage

You are a technical writer. Given the following API endpoint documentation, write a one-paragraph summary that explains what the endpoint does, what inputs it requires, and what it returns. Be concise and use plain language.

```mdx
<Prompt description="Summarize this API endpoint">
You are a technical writer. Given the following API endpoint documentation,
write a one-paragraph summary that explains what the endpoint does, what
inputs it requires, and what it returns. Be concise and use plain language.
</Prompt>
```

## With Cursor integration

Add `actions={["copy", "cursor"]}` to also surface an "Open in Cursor" button. This is especially useful for prompts readers will use in their editor.

<Prompt description="Generate a typed API client" icon="code" actions={\["copy", "cursor"\]}

You are an expert TypeScript developer. Given the following OpenAPI specification, generate a fully-typed API client using native fetch. Include:

- A base client class with configurable baseUrl and auth headers
- One method per endpoint, with typed request parameters and response types
- JSDoc comments on each method Do not use any third-party HTTP libraries.

```mdx
<Prompt
  description="Generate a typed API client"
  icon="code"
  actions={["copy", "cursor"]}
>
You are an expert TypeScript developer. Given the following OpenAPI
specification, generate a fully-typed API client using native fetch...
</Prompt>
```

## Props

Heading text shown above the prompt content. Supports Markdown. The prompt text that gets copied or sent to Cursor. Which action buttons to show. Options: \`"copy"\`, \`"cursor"\`. Defaults to \`\["copy"\]\`. An icon displayed alongside the description. Supports Font Awesome, Lucide, and Tabler icon names, image URLs, or inline SVG.

## When to use it

The `Prompt` component works well anywhere you're teaching readers to work with AI:

- **Quickstart guides** — give readers a prompt to generate their first integration
- **API reference pages** — include a prompt for generating client code from the spec
- **Troubleshooting guides** — embed a debugging prompt readers can run against their own error logs
- **Conceptual pages** — add a prompt for exploring the topic further with an AI assistant