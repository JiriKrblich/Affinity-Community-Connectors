# Affinity Community Connectors

The public registry used by **Discover** in Connector for Affinity. It lists
connectors the community can install from the app; it does not run any code on
GitHub or bundle Connector for Affinity itself.

## Using the registry

Open **Discover** in Connector for Affinity to browse and install connectors.
The app reads `connectors.json`, then reads each connector's own `app.json` at
the published tag or commit. The manifest remains the source of truth for its
name, description, author, version, icon, image, supported environment and
files.

## Publishing a connector

1. Build and test a connector. Follow [CONTRIBUTING.md](CONTRIBUTING.md).
2. Put it in its own GitHub repository, or a folder inside a repository you
   maintain. Do not submit credentials, generated output or user data.
3. Tag a release (for example `v1.0.0`) or choose an immutable commit SHA.
4. Add one entry to `connectors.json` and open a pull request.

The registry entry points to an exact tag or commit, never a moving branch.
That lets reviewers see exactly what Connector for Affinity will install.

## Repository files

- `connectors.json` — the Discover registry.
- `featured.json` — optional IDs to show first in Discover.
- `CONTRIBUTING.md` — connector format and submission rules.

To propose a connector or report a registry issue, open an issue or pull
request in this repository.
