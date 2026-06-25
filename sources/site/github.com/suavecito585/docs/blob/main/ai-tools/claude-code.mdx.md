# Source: https://github.com/suavecito585/docs/blob/main/ai-tools/claude-code.mdx

[suavecito585](https://github.com/suavecito585) / **[docs](https://github.com/suavecito585/docs)** Public

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
 

 

## FilesExpand file tree

 main

/

# claude-code.mdx

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/docs/commits/main/ai-tools/claude-code.mdx)

History

43 lines (33 loc) · 906 Bytes

 main

/

# claude-code.mdx

Copy path

Top

## File metadata and controls

- Preview
 
- Code
 
- Blame
 

43 lines (33 loc) · 906 Bytes

[Raw](https://github.com/suavecito585/docs/raw/refs/heads/main/ai-tools/claude-code.mdx)

Copy raw file

Download raw file

Outline

Edit and raw actions

<table><tbody><tr><th>title</th><td>Claude Code setup</td></tr><tr><th>description</th><td>Configure Claude Code for your documentation workflow</td></tr><tr><th>icon</th><td>asterisk</td></tr></tbody></table>

Set up Claude Code to help you write and maintain your Mintlify documentation.

## Prerequisites

- Active Claude subscription (Pro, Max, or API access)

## Setup

\`\`\`bash npm install -g @anthropic-ai/claude-code \`\`\` In your docs directory, run:

```shell
npx skills add https://mintlify.com/docs
```

This gives Claude Code Mintlify's component reference, writing standards, and workflow guidance.

Edit \`AGENTS.md\` in your project root to add project-specific terminology, style preferences, and content boundaries. \`\`\`bash claude \`\`\`