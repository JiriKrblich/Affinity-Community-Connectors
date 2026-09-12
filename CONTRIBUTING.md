# Contributing a connector

Connector for Affinity connects an Affinity document to an API, local tool or
service. A connector runs locally in its own Node.js process; it is not an
Affinity plugin.

## Before you submit

Use the **Create with AI** tab in Connector for Affinity or the complete
[authoring guide](https://github.com/JiriKrblich/Connector-for-Affinity/blob/main/AUTHORING.md).
It defines the full API and the current compatibility rules.

Your connector must:

- have a stable `id`, `name`, `description`, `version`, `author`, `testedWith`
  declaration and a semantic Tabler icon in `app.json`;
- use an optional HTTPS `url` for the author's or project's contact page; it is
  shown as a clickable link in Discover;
- use a folder with `app.json` and `index.js` whenever it needs settings,
  secrets, image fields, dropdowns or other rich inputs;
- define every reasonable Affinity input in the manifest. Use `select` and
  `optionsFrom` for structured or discovered values, `image` for artwork from
  Affinity, and put one-time setup in `settings` and credentials in `secrets`;
- never include a key, token, private artwork or user data in the repository;
- work from a version tag or immutable commit that reviewers can inspect.

### Affinity-aware inputs

Do not ask people to type a workflow name, model ID, export source or file path
when the connector can offer it as an Affinity control. Use the appropriate
manifest fields: `select`, `textarea`, `number`, `slider`, `checkbox`, `image`,
`note`, `showIf`, `dependsOn` and `optionsFrom`.

An `image` field should list every source the connector genuinely supports, for
example `selection`, `artboard`, `layer`, `spread`, `document` or `file`.
Dynamic selects return strings or `{ value, label }` entries from
`options.<name>(ctx)`. The Connector desktop app and the Affinity helper can
both populate these lists.

## Connector layout

Use this structure for a normal connector:

```
my-connector/
  app.json
  index.js
  icon.svg              # optional, only for a custom icon
```

The relevant parts of `app.json` look like this:

```json
{
  "id": "my-connector",
  "name": "My Connector",
  "description": "What it does for Affinity users.",
  "version": "1.0.0",
  "testedWith": "Affinity version not recorded · Connector for Affinity 1.0.0",
  "author": "Your name",
  "url": "https://your-site.example",
  "bar": { "icon": "sparkles" },
  "main": "index.js",
  "fields": []
}
```

Do not invent a tested Affinity version. Replace `Affinity version not
recorded` only after a real test. Include any extra source files under `files`
in `app.json`; Connector for Affinity reads text assets only, so host preview
images remotely and reference them by URL.

## Add it to Discover

Add one object to `connectors.json` in this repository:

```json
{
  "id": "my-connector",
  "repository": "github-account/my-connector",
  "ref": "v1.0.0",
  "category": "Images"
}
```

Use `path` when the connector lives inside a larger repository:

```json
{
  "id": "my-connector",
  "repository": "github-account/design-tools",
  "ref": "v1.0.0",
  "path": "connectors/my-connector",
  "category": "Production"
}
```

`ref` must be a tag or commit SHA, never `main`, `master` or another moving
branch. The `id` must match `app.json` exactly. Choose a clear category such as
`Images`, `Sharing`, `Production`, `Utilities` or `Learning`.

When updating a connector, publish the new tag first, then change only the
`ref` in a pull request. Connector for Affinity keeps each user's settings and
secrets outside the connector folder when it installs the update.
