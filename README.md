# Edgestream Marketplace

Install agent plugins from the stable or development channel. This repository
owns marketplace installation, updates, and [release promotion](docs/PROMOTION.md).
Plugin repositories own their capabilities, local development, and release builds.

This repository follows the [Agent Plugins specification](https://agent-plugins.org/).

## Channels

| Channel | Marketplace branch | Marketplace ID | Directory display name |
| --- | --- | --- | --- |
| Stable | `main` | `edgestream` | Edgestream |
| Development | `development` | `edgestream-dev` | Edgestream Lab |

Stable entries point to published release tags; development entries follow the
plugin repository's development branch. The catalogs are authoritative:
[stable](https://github.com/edgestream/agent-marketplace/blob/main/.agents/plugins/marketplace.json)
and [development](https://github.com/edgestream/agent-marketplace/blob/development/.agents/plugins/marketplace.json).
Use the entry's `name` for CLI installation; the plugin manifest supplies its
display name. Available plugins may differ between channels.

## Installation

### Codex CLI

For the stable channel:

```bash
codex plugin marketplace add edgestream/agent-marketplace --ref main
codex plugin add feeds@edgestream
```

For the development channel:

```bash
codex plugin marketplace add edgestream/agent-marketplace --ref development
codex plugin add feeds-dev@edgestream-dev
```

The second command in each example installs the social-media plugin. For another
plugin, use `<plugin-name>@<marketplace-id>` from the selected catalog.
Register each marketplace once. Run `codex plugin list` to confirm installation,
then start a new task and request the installed plugin explicitly.

### ChatGPT desktop

When this marketplace is available in your workspace's **Plugins Directory**,
select **Edgestream** for stable plugins or **Edgestream Lab** for development.
Choose the desired plugin and select **Install**, then start a new chat and
request it explicitly. If the marketplace is absent, your workspace administrator
must make it available first; CLI registration alone does not import it into a
ChatGPT workspace. See the [official plugin documentation](https://developers.openai.com/plugins)
for host setup and availability.

For the social-media plugin, try “Read the feed at https://x.com/OpenAI”. Its
package includes companion skills; check for an actual tool call when verifying
retrieval. See the [plugin README](https://github.com/edgestream/feeds-plugin)
for capabilities and standalone CLI/MCP use.

## Updates and channel changes

Refresh the selected Codex marketplace snapshot:

```bash
codex plugin marketplace upgrade edgestream
# Or, for development:
codex plugin marketplace upgrade edgestream-dev
```

Reinstall the desired plugin using the installation command above when a new
version is available, then start a fresh task and verify the installed version.
Refreshing the catalog alone is not proof that an installed plugin was updated.
In ChatGPT, use the workspace's plugin refresh/update controls and verify the
result in a new chat; catalog syncing and local CLI snapshots are separate.

Changing channels installs a different plugin identity. Do not assume settings
or existing installations migrate automatically. Verify the new installation
before removing the old one, and select the intended plugin explicitly if both
are installed.

## Maintenance

Use the [promotion guide](docs/PROMOTION.md) for listing changes, verification,
retries, and rollback. Keep installation guidance here and link to it from plugin
repositories. Maintain shared guides on `main`; development-branch documentation
should link to this canonical guide rather than carry a second installation guide.
