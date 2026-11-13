# The 40 Thieves docs

The Mintlify site for The 40 Thieves open-source projects. This repository is the hub: it holds
the site settings (`docs.base.json`) and the landing page, and pulls each project's docs in from
its own repository.

| Project | Source | Published at |
|---|---|---|
| Reliquary-TC | `docs-site` branch of [The-40-Thieves/reliquary-tc](https://github.com/The-40-Thieves/reliquary-tc) | `/reliquary-tc` |

## How it works

`.github/workflows/multirepo.yml` runs [`mintlify/multirepo-action`](https://github.com/mintlify/multirepo-action)
every hour and on demand. It copies each child listed in `.github/mintlify-multirepo.yml` into its
destination folder, rewrites the child's links under that path, and generates `docs.json` from
`docs.base.json` with each child's navigation in place of its `sourceRef`. It commits the result to
`main`, and Mintlify deploys it.

Do not edit synced folders or `docs.json` here: the next sync overwrites them. Change a project's
docs in its own repository, and change site settings in `docs.base.json`.

To sync now: Actions → Combine docs → Run workflow, or `gh workflow run multirepo.yml -R suavecito585/docs`.

## Add a project

1. In the project's repository, publish a Mintlify site (a folder with `docs.json` and pages) to a
   branch or folder.
2. Add it to `.github/mintlify-multirepo.yml` with a `destination`.
3. Add a tab with `{ "sourceRef": "<owner>/<repo>" }` to `docs.base.json`, and a card to `index.mdx`.
