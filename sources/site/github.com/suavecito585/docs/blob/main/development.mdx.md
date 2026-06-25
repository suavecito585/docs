# Source: https://github.com/suavecito585/docs/blob/main/development.mdx

[suavecito585](https://github.com/suavecito585) / **[docs](https://github.com/suavecito585/docs)** Public

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fdocs)
 

 

## FilesExpand file tree

 main

/

# development.mdx

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/docs/commits/main/development.mdx)

History

95 lines (64 loc) · 2.71 KB

 main

/

# development.mdx

Copy path

Top

## File metadata and controls

- Preview
 
- Code
 
- Blame
 

95 lines (64 loc) · 2.71 KB

[Raw](https://github.com/suavecito585/docs/raw/refs/heads/main/development.mdx)

Copy raw file

Download raw file

Outline

Edit and raw actions

<table><tbody><tr><th>title</th><td>Development</td></tr><tr><th>description</th><td>Preview changes locally to update your docs</td></tr><tr><th>icon</th><td>terminal</td></tr></tbody></table>

\*\*Prerequisites\*\*: - Node.js version 19 or higher - A docs repository with a \`docs.json\` file

Follow these steps to install and run Mintlify on your operating system.

```shell
npm i -g mint
```

Navigate to your docs directory where your `docs.json` file is located, and run the following command:

```shell
mint dev
```

A local preview of your documentation will be available at `http://localhost:3000`.

## Custom ports

By default, Mintlify uses port 3000. You can customize the port Mintlify runs on by using the `--port` flag. For example, to run Mintlify on port 3333, use this command:

```shell
mint dev --port 3333
```

If you attempt to run Mintlify on a port that's already in use, it will use the next available port:

```md
Port 3000 is already in use. Trying 3001 instead.
```

## Mintlify versions

Please note that each CLI release is associated with a specific version of Mintlify. If your local preview does not align with the production version, please update the CLI:

```shell
npm mint update
```

## Validating links

The CLI can assist with validating links in your documentation. To identify any broken links, use the following command:

```shell
mint broken-links
```

## Deployment

If the deployment is successful, you should see the following:

[![Screenshot of a deployment confirmation message that says All checks have passed.](https://github.com/suavecito585/docs/raw/main/images/checks-passed.png)](https://github.com/suavecito585/docs/blob/main/images/checks-passed.png)

## Code formatting

We suggest using extensions on your IDE to recognize and format MDX. If you're a VSCode user, consider the [MDX VSCode extension](https://marketplace.visualstudio.com/items?itemName=unifiedjs.vscode-mdx) for syntax highlighting, and [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) for code formatting.

## Troubleshooting

```
This may be due to an outdated version of node. Try the following:
1. Remove the currently-installed version of the CLI: `npm remove -g mint`
2. Upgrade to Node v19 or higher.
3. Reinstall the CLI: `npm i -g mint`
```

```
Solution: Go to the root of your device and delete the `~/.mintlify` folder. Then run `mint dev` again.
```

Curious about what changed in the latest CLI version? Check out the [CLI changelog](https://www.npmjs.com/package/mintlify?activeTab=versions).