# Marketplace promotion

Plugin repositories own release preparation, builds, tests, tags, and GitHub
releases. This repository owns listing changes and installed-host verification.
For installation commands and channel selection, see [README.md](../README.md#installation).

## Promote a release

1. Obtain the published release tag and exact verified commit from the plugin
   repository. A published release alone does not update the marketplace.
2. Create a separate branch and PR targeting this repository's `main`. Update
   only the relevant entry in `.agents/plugins/marketplace.json`: its repository
   URL, plugin identity, and `source.ref`. Stable entries must reference a
   published tag, never a moving maintenance branch. Preserve unrelated entries
   and existing policy fields.
3. Verify the tag resolves to the supplied commit and both plugin manifests at
   that commit declare the expected identity and matching release version.
   Review the current stable reference: an older maintenance-line patch must not
   displace a newer stable minor release unless an explicit rollback is intended.
4. Record the repository, tag, commit, previous reference, and validation in the
   PR. Review and merge the listing change, then verify installation below.

The development catalog lives on `development`; its entries follow the plugin
repository's development branch and use the development identity. Stable
promotion does not require changing that catalog. Do not merge entire marketplace
branches into one another: their catalogs intentionally differ.

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
