# Tuist plugins for Cursor

The Cursor marketplace for [Tuist](https://tuist.dev). It packages the Tuist agent skills and the hosted Tuist MCP server so Cursor can work with your Apple and Android projects: migrate to generated projects, debug generation, and pull build, test, bundle, and cache data straight from your Tuist dashboard.

## Install

Add this repository as a marketplace from your Cursor organization dashboard: **Settings → Plugins → Team Marketplaces → Import Marketplace**, then paste `https://github.com/tuist/cursor-plugin`. Cursor reads `.cursor-plugin/marketplace.json` and lists the plugins it finds.

Once it is listed on the [Cursor marketplace](https://cursor.com/marketplace), open **Customize** in the sidebar, search for **Tuist**, then **Install** and pick a project or user scope. Typing `/add-plugin` in the editor gets you to the same place.

Most skills drive the `tuist` CLI, so run `tuist auth login` once to give them access to your project's data. The bundled MCP server covers what the CLI does not expose yet and prompts for sign-in from inside Cursor.

## Plugins

| Plugin | Description |
| --- | --- |
| [`tuist`](plugins/tuist) | Agent skills and MCP access for Tuist projects |

## Layout

```text
.cursor-plugin/marketplace.json   marketplace manifest
plugins/tuist/                    the Tuist plugin
scripts/validate-template.mjs     manifest and frontmatter validator
```

## Skills come from tuist/tuist

`plugins/tuist/skills` mirrors [`skills/skills`](https://github.com/tuist/tuist/tree/main/skills/skills) in the Tuist monorepo, the same source that publishes [tuist/agent-skills](https://github.com/tuist/agent-skills). Edit skills there so every agent gets the change, not just Cursor.

## Adding a plugin

1. Create `plugins/<name>/.cursor-plugin/plugin.json` with a lowercase kebab-case `name`.
2. Add the components you need. Cursor discovers `skills/<name>/SKILL.md`, `rules/*.mdc`, `agents/*.md`, `commands/*.md`, `hooks/hooks.json`, and `mcp.json` by convention, so you only declare paths in the manifest when they live elsewhere.
3. Append an entry to `.cursor-plugin/marketplace.json` with `name`, `source`, and `description`.
4. Run the validator.

## Validate

```bash
node scripts/validate-template.mjs
```

CI runs the same check on every push and pull request.

## License

MIT. See [LICENSE.md](LICENSE.md).
