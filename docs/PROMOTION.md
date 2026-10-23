# Marketplace promotion

The hosted `main` catalog is retired; the procedure below is retained for
separate development/future distribution work and does not authorize republishing
the retired integrations.

Plugin repositories own release preparation, builds, tests, tags, and GitHub
releases. This repository owns listing changes and installed-host verification.
For installation commands and channel selection, see [README.md](../README.md#installation).

## Promote a release

1. Obtain the published release tag and exact verified commit from the plugin
   repository. A published release alone does not update the marketplace.
2. Create a separate branch and PR targeting this repository's `main`. Update
   only the relevant entry in `.agents/plugins/marketplace.json`: its repository
   URL, plugin identity, and `source.ref`. Stable entries must reference a
   published tag, never a moving maintenance branch. Preserve unrelated entries and
   existing policy fields.
3. Verify the tag resolves to the supplied commit and both plugin manifests at
   that commit declare the expected identity and matching release version.
   Review the current stable reference: an older maintenance-line patch must
   not displace a newer stable minor release unless an explicit rollback is
   intended.
4. Record the repository, tag, commit, previous reference, and validation in the
   PR. Review and merge the listing change, then verify installation below.

The development catalog lives on `development`; its entries follow the plugin
repository's development branch and use the development identity. Stable
promotion does not require changing that catalog. Do not merge entire marketplace
branches into one another: their catalogs intentionally differ.

## Retire the hosted workspace marketplace

The hosted workspace distribution of Feeds and Recipes is abandoned. The `main`
catalog has no entries; do not promote new releases to it. This decision replaces
the former exception that followed `feeds-plugin/main` through its `web/` package.
Published tags and source repositories remain available for historical reference.

A workspace administrator completes retirement:

1. Open **Admin > Plugins > Marketplaces**, select the Edgestream import and
   inspect its imported plugins. The retired catalog previously contained Recipes
   and the hosted Feeds plugin
   `plugin_asdk_app_6ac49879ccc481918f51562ec1d84797`.
2. Delete that marketplace import. According to the
   [official management guide](https://learn.chatgpt.com/docs/enterprise/plugin-management),
   this deletes all plugins imported from it. Removing entries in Git alone only
   marks workspace copies as **No longer in source** and is not an uninstall.
3. Inspect **Workspace apps** and remove the retired Feeds MCP app and any
   remaining integration belonging to these retired plugins. Revoke associated
   OAuth grants and service credentials in the owning authorization system.
   Personal plugin removal does not establish workspace-wide app removal.
4. Verify from an ordinary member account that neither retired workspace plugin
   can be installed or invoked. Check the marketplace import and associated MCP
   apps are absent. Record the date, workspace and safe evidence; never record
   tokens or keys.
5. Decommission the retired hosted Feeds endpoint and its dedicated credentials
   through the infrastructure owner. Preserve any shared identity infrastructure
   still used by other services. Catalog removal does not stop a server.

Deleting this workspace import does not delete the GitHub repository or remove
local clients' configured marketplaces. Do not recreate the retired import to
reconnect GitHub. A new private Feeds tunnel connection is a separate rollout;
this retirement does not create or publish it.

### Recorded status

- Feeds personal/plugin uninstall: management tool confirmed uninstall of
  `plugin_asdk_app_6ac49879ccc481918f51562ec1d84797` on 2026-10-23.
- Recipes personal/plugin uninstall: management tool reported `not_installed`
  for `recipes` on 2026-10-23; no workspace-wide absence is inferred.
- Workspace marketplace deletion, connected app removal, OAuth revocation,
  ordinary-member denial and hosted infrastructure shutdown: **Unverified**.
  The available plugin tool does not administer workspace marketplace imports
  or the hosting infrastructure.

## Installation verification

After promotion, test a fresh installation and an update from the previous
stable version in supported hosts. Confirm displayed identity and version, MCP
startup, an actual tool call, and companion skill discovery where supplied.
For a first stable release, record that no previous stable update path exists and
verify the development-to-stable transition. Distinct plugin identities do not
imply automatic migration of installations or settings.

Record host/version, release tag/commit, and results in the promotion PR. A natural
language answer alone is not evidence of tool use. Plugin-specific model-routing
evidence belongs in the plugin repository's skill verification documentation.

## Retries and rollback

Serialize promotion for the stable channel. Before retrying, inspect existing
releases, catalog references, and marketplace PRs. Reuse matching work; stop on
conflicting versions or commits. If publication succeeded but promotion failed,
retry promotion against the existing release rather than recreating that release.

For a defective release, restore the previous known-good reference through a PR
and arrange a corrected patch release in the plugin repository. A catalog rollback
does not downgrade already installed clients: verify and communicate the recovery
steps for each affected host. If there is no previous stable release, withdraw
the broken listing until a correction is available. Keep published tags and release
history intact.
