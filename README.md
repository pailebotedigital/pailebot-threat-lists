# Pailebot threat-list releases

This public repository distributes Pailebot's signed threat-list updates. It is a delivery mirror, not the publisher's source code or an API for classifying browsing activity. Pailebot does not collect browsing URLs or telemetry through these release files. GitHub operates this mirror under its own policies.

There are no releases yet. Until the first signed release passes source-rights and deployment review, do not treat any file in this repository as a current threat list.

## Release files

- `latest.psc` is the signed channel metadata at `/releases/latest/download/latest.psc`.
- `full-<sha256>` releases contain complete `<sha256>.tar.br` packages.
- `delta-<sha256>` releases contain adjacent incremental `<sha256>.tar.br` packages.

Package names are content-addressed. The latest metadata is published only after every referenced package is uploaded and checked. Clients must authenticate the signed metadata, verify package digests and sizes, and apply the rollback rules before trusting content. A GitHub download alone is not authentication. The wire contract is maintained with the [Pailebot backend](https://github.com/pailebotedigital/pailebot-backend); this repository contains release assets only.

## Reuse and attribution

The compiled lists are intended to be usable by other projects, subject to each source's own permissions. Each signed package contains `notices.json` with source provenance and attribution. Follow those notices when redistributing or adapting source material. The repository's CC BY 4.0 license covers only Pailebot-authored documentation and original compilation contributions, to the extent Pailebot has rights to license them. It does **not** relicense third-party feeds, site names, logos, or trademarks. No affiliation or endorsement by listed sites is implied.

The lists are advisory and can be incomplete or out of date. They are not a substitute for browser and user security decisions.

Report incorrect entries or broken releases through [Issues](https://github.com/pailebotedigital/pailebot-threat-lists/issues).
