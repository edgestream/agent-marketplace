# Edgestream Marketplace

This repository follows the [Agent Plugins specification](https://agent-plugins.org/).

Install agent plugins from the stable or development channel. This repository
owns marketplace installation, updates, and [release promotion](docs/PROMOTION.md).
Plugin repositories own their capabilities, local development, and release builds.

## Channels

| Channel | Marketplace branch | Marketplace ID | Directory display name |
| --- | --- | --- | --- |
| Stable | `main` | `edgestream` | Edgestream |
| Development | `development` | `edgestream-dev` | Edgestream Lab |

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

### ChatGPT desktop

When this marketplace is available in your workspace's **Plugins Directory**,
select **Edgestream** for stable plugins or **Edgestream Lab** for development.
Choose the desired plugin and select **Install**, then start a new chat and
request it explicitly. If the marketplace is absent, your workspace administrator
must make it available first; CLI registration alone does not import it into a
ChatGPT workspace. See the [official plugin documentation](https://developers.openai.com/plugins)
for host setup and availability.

## Updates and channel changes

Refresh the selected Codex marketplace snapshot:

```bash
codex plugin marketplace upgrade edgestream
# Or, for development:
codex plugin marketplace upgrade edgestream-dev
```

## Maintenance

Use the [promotion guide](docs/PROMOTION.md) for listing changes, verification,
retries, and rollback. Keep installation guidance here and link to it from plugin
repositories.
