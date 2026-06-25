# Source: https://github.com/suavecito585/docs/blob/main/api-reference/introduction.mdx

[suavecito585](https://github.com/suavecito585) / **[docs](https://github.com/suavecito585/docs)** Public

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
 

 

## FilesExpand file tree

 main

/

# introduction.mdx

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

[History](https://github.com/suavecito585/docs/commits/main/api-reference/introduction.mdx)

Open commit details

History

33 lines (26 loc) · 875 Bytes

## FilesExpand file tree

 main

/

# introduction.mdx

Copy path

Top

## File metadata and controls

- Preview
 
- Code
 
- Blame
 

33 lines (26 loc) · 875 Bytes

[Raw](https://github.com/suavecito585/docs/raw/refs/heads/main/api-reference/introduction.mdx)

Copy raw file

Download raw file

Outline

Edit and raw actions

<table><tbody><tr><th>title</th><td>Introduction</td></tr><tr><th>description</th><td>Example section for showcasing API endpoints</td></tr></tbody></table>

If you're not looking to build API reference documentation, you can delete this section by removing the api-reference folder.

## Welcome

There are two ways to build API documentation: [OpenAPI](https://mintlify.com/docs/api-playground/openapi/setup) and [MDX components](https://mintlify.com/docs/api-playground/mdx/configuration). For the starter kit, we are using the following OpenAPI specification.

<Card title="Plant Store Endpoints" icon="leaf" href="[https://github.com/mintlify/starter/blob/main/api-reference/openapi.json](https://github.com/mintlify/starter/blob/main/api-reference/openapi.json)"

View the OpenAPI specification file

## Authentication

All API endpoints are authenticated using Bearer tokens and picked up from the specification file.

```json
"security": [
  {
    "bearerAuth": []
  }
]
```