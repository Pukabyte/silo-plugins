# Mediux Artwork proposal

- Plugin ID: `community.mediux`
- Source: [Pukabyte/silo-plugin-mediux](https://github.com/Pukabyte/silo-plugin-mediux)
- Release: [v0.1.6](https://github.com/Pukabyte/silo-plugin-mediux/releases/tag/v0.1.6)
- Maintainer: [Pukabyte](https://github.com/Pukabyte)
- Support: [GitHub issues](https://github.com/Pukabyte/silo-plugin-mediux/issues)
- License: AGPL-3.0-or-later; embedded Outfit uses SIL OFL 1.1.

## Behavior and setup

Mediux supplies movie and series posters, backdrops, logos, season posters, and episode title cards. Existing TMDB/TVDB IDs bootstrap its identity; other Silo providers continue supplying text. Configure a Mediux API token, add the provider to applicable library chains, and open its administrator settings page for creator order and independent season/title-card consistency settings. Preference saves preserve the token and apply without a Silo restart. Refresh an item to apply artwork changes.

Metadata requests contact `https://images.mediux.io/graphql` with the saved token. Creator search uses the same API. The plugin returns credential-free `mediux://` references resolved to `https://images.mediux.io/assets/`; Silo controls direct delivery or image caching. A separate Mediux container is unnecessary. Settings styling reads Silo's public theme endpoint.

## Evidence and limits

The source uses tagged SDK v0.24.0 without local replacements. GitHub CI runs Go race tests, vet, packaging, a native SDK runtime smoke check, and isolated browser checks. Releases include all declared supported-platform binaries, installable ZIPs, manifests with binary SHA-256 checksums, and `checksums.txt`. CODEOWNERS names the maintainer.

The preceding local version 0.1.5 was exercised through Silo's native upload/configuration/provider path on Linux amd64: authenticated metadata lookup, movie posters, series/season posters, title cards, creator lookup, token-preserving preference saves and restart persistence. Sampled client-visible artwork returned valid images. Version 0.1.6 adds regression-tested language matching fixes; its local native runtime smoke verifies handshake, version, checksum, configuration, administrator access, private-token responses and resolution. These checks are maintainer evidence, not an independent Silo approval.

Linux arm64/macOS arm64 are cross-built; their runtime acceptance and cache-enabled end-to-end delivery remain outstanding. Set coverage uses Mediux artwork scopes rather than local library inventory. Metadata cache bounds entries rather than decoded bytes; oversized API responses fail at 2 MiB. Manual image-picker visibility depends on the host forwarding Mediux identity or implementing external-ID image lookup. These limits are documented in the plugin README and design notes.

## Before catalog inclusion

The [approval policy](../APPROVAL_POLICY.md) requires the source repository to belong to `Silo-Community`. The published repository currently belongs to `Pukabyte`. A repository transfer or maintainer-managed adoption is needed before approval.

Silo maintainers must independently review the documented setup and behavior against a supported server, resolve repository ownership, and connect the release workflow's catalog dispatch. Only after that review should an approval date/evidence URL be recorded in `approved-plugins.json` and the catalog regenerated from the approved release. This PR leaves the approval registry and generated catalog unchanged.
