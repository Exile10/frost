# Spark SDK compatible FROST 2.2 update

This maintenance branch starts at the revision pinned by Breez SDK 0.19.4,
`9aaf1b6b9fa3c2c3c2c7c70da83061deda1a9180`, and merges upstream FROST 2.2
`3ffc19d8f473d5bc4e07ed41bc884bdb42d6c29f`. The release includes
`379ef689c733b3d9c80fd409071d4f3af4dafed2`, which validates refresh thresholds
for dealer and distributed key generation paths (GHSA-wgq8-vr6r-mqxm).

The merge retains the existing Spark participant-group signing changes in
frost-core and frost-secp256k1-tr. Consumers must pin the resulting commit;
Lightspark's current main has a separate major-version API and is not a
substitute for this SDK-compatible branch.

Local validation on macOS: secp256k1-tr integration tests (34), BIP340
interoperability tests (3), key recreation tests (11), and taproot tweaking
(1) passed. Integration tests include invalid refresh-threshold rejection.
Formatting passed. Parent SDK compilation and application tests are tracked
in the consuming repository PR. No live wallet transaction or Jetson device
signing is claimed.

This update cannot repair keys previously refreshed with an unsafe threshold.
See the upstream advisory for affected-key handling:
https://github.com/advisories/GHSA-wgq8-vr6r-mqxm
