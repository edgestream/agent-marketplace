# Hosted Feeds workspace plugin

The Edgestream workspace already contains the Feeds app-generated plugin with
ID `plugin_asdk_app_6ac49879ccc481918f51562ec1d84797`. The catalog at
`workspace-feeds/.agents/plugins/marketplace.json` is solely for adopting that
plugin into GitHub management. It does not create or register another MCP app.

In **Admin > Plugins > Add > Import marketplace**, use Source
`https://github.com/edgestream/agent-marketplace`, Path `workspace-feeds`, and
Branch, tag, or commit `main`. The catalog has one Feeds entry, pinned to the
published `feeds-plugin` tag `0.2.9` and its MCP-free `web/` package. Do not
import the repository root for this workspace Feeds workflow: the root catalog
contains a separate Recipes entry.

Check the import report before installing or syncing anything else. The Feeds
plugin must retain the ID above, the existing workspace availability, and each
user's individual OAuth connection. Stop if a second Feeds plugin is created or
the existing ID is not adopted. A failed takeover needs investigation; another
import is not a recovery step. The package should display Feeds by Edgestream,
version `0.2.9`, and expose the `read-feeds` skill and existing hosted app.

After a successful takeover, verify the same plugin in ChatGPT Web and Desktop,
Chat and Work, for both intended users. Use bounded X and Bluesky requests and
inspect actual tool calls. Record the import result and user-visible evidence in
[`feeds-plugin#53`](https://github.com/edgestream/feeds-plugin/issues/53).

For updates, publish and verify a new `feeds-plugin` release, change only this
catalog's `source.ref` in a reviewed PR, merge, then sync this marketplace.
Review the saved sync report and plugin ID after each update. If a sync rejects
an invalid package, keep the last working version and correct the source; do not
create another workspace plugin. Removing a catalog entry does not delete its
managed workspace copy, while deleting the marketplace does.
