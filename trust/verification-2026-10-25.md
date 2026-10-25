# Threat-list V1 client trust handoff — 2026-10-25

This is a non-secret, versioned review record for client builds. Static trust
data is in [threat-list-v1-roots.json](threat-list-v1-roots.json).
Do **not** fetch either file at runtime to establish trust, and do not derive a
trusted key from `latest.psc` or a delivery provider.

## Root and provenance

- Purpose: `ThreatListManifest`; Ed25519 public key
  `8c9efcf0d50babd63d2aaaf03fbcdb3d08aacccaaef511997bcd213fd4d560de`.
- Inclusive active sequence window: `1..9223372036854775807`.
- A reviewed one-time production threat-only provisioning ceremony was recorded
  on 2026-09-30. Its public record and the VPS's live `[signing]` configuration
  matched on 2026-10-25. The owner approved pinning this public root in the
  Apple client and publishing this handoff on 2026-10-25.
- No independent high-window recovery root is provisioned in the live VPS
  configuration. Leave that client slot unset; never use a placeholder or an
  unrelated binary-signing root.

The client must embed the reviewed root and bounds at build time. JSON bounds
are decimal strings because the upper bound exceeds JavaScript's exact integer
range; parse them as unsigned 64-bit integers.

## Time-qualified public release evidence

At about 2026-10-25 20:27 UTC, the backend's pinned Rust helper authenticated
Cloudflare's public `latest.psc` under this root after bounded TLS 1.3, header
and Brotli checks:

| Field | Observed value |
| --- | --- |
| Sequence | `36` |
| Issued / expires | `2026-10-25T06:01:05Z` / `2026-10-26T06:01:05Z` |
| Compressed latest SHA-256 | `364ed82984e1fd7b4276fed3d6e96b227371d59cbd6e2347afc5195cce8d1f09` |
| Signed payload SHA-256 | `f4521ca50e9cd5be009a938c742ed54b0b7ff4c1b7928b7cb776144caf3e15ae` |
| Content version / ID | `3` / `dcbef6a54907d26e5085e25a64d45c751554323c5edf20a543d7ac2367eb5181` |
| Source IDs | `1, 4..15` (13 sources) |
| Portable `PTHI0001` index SHA-256 / bytes | `f29fa338a58eccf40cfabb18fac8502b930f1a99996ac24b885fc0a137311fdc` / `86749227` |

GitHub release metadata listed a 1,074-byte `latest.psc` with the same SHA-256
under tag `head-364ed82984e1fd7b4276fed3d6e96b227371d59cbd6e2347afc5195cce8d1f09`.
Earlier public monitors authenticated sequence 36 on Cloudflare, GitHub and
Bunny. These are snapshots, not permanent trust configuration.

At 2026-10-25T20:53:36Z, a fresh read-only probe authenticated all three
public `latest.psc` objects under the active root at sequence 36; each was
1,074 bytes with the exact SHA-256 above. The verified signed payload hash
matched exact `manifest.payload` bytes. Its frozen-V1 manifest referenced
`threat-lists/v1/full/cafea15a21b3acef37ddf7b1450b467cd91b4a649b2a37d63b1a10ac99eedf17.tar.br`
with 27,669,757 wire bytes and 86,844,416 decoded bytes. Fresh Cloudflare,
GitHub and Bunny downloads each matched the descriptor's exact wire size and
SHA-256. The pinned Rust helper validated the signed channel and Cloudflare's
full package under the frozen V1 contract; the other two mirrors served
byte-identical full packages. No mirror was unavailable in this probe.

## Remaining gates

1. Map only the approved active root and inclusive window into the Apple
   build's static trust configuration. Keep recovery unset.
2. Qualify expiry, rollback, mirror failure, stale-list warning and clean-install
   activation in the client before claiming release readiness. A later release
   needs its own fresh manifest/package verification.

The frozen transport and archive contract is
[backend threat-list V1 protocol](https://github.com/pailebotedigital/pailebot-backend/blob/153621e09be4763bb885af0fd503ec1459dad191/docs/threat-list-v1-protocol.md).

