# Edgestream Marketplace

The hosted workspace distribution of Feeds and Recipes is retired. The `main`
catalog retains its `edgestream` identity but contains no plugin entries. Do not
use it for new installations.

Removing catalog entries does not uninstall existing workspace copies. A workspace
administrator must delete the Edgestream marketplace from **Admin > Plugins >
Marketplaces** and remove the associated connected MCP apps. Follow the
[retirement procedure](docs/PROMOTION.md#retire-the-hosted-workspace-marketplace).

The separate `development` catalog is not changed by this retirement. Removing a
workspace marketplace does not remove local Codex installations or delete plugin
source repositories. Private Feeds deployment is documented in the
[Feeds operator guide](https://github.com/edgestream/feeds-plugin/pull/83).
