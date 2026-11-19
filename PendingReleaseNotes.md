# v1.22 Pending Release Notes

Notes for the v1.22.0 release, including breaking changes and new features.
Changes should *not* be included here if they are backported to previous releases.

## Breaking Changes

- When updating OSDs in parallel, Rook now restricts each batch to a single bucket of the narrowest failure domain used
  by the pools' CRUSH rules (typically `host`), so that an update never takes down OSDs from more than one failure
  domain. Batches may be smaller than before, in particular for OSDs on portable PVCs, which each have their own `host`
  bucket. Set `storage.osdUpdateFailureDomain` to choose another failure domain, or to `root` to keep the previous
  behavior.

## Features

- `CephObjectStoreUser` gained `spec.secretTemplate`, which adds labels and annotations to the Secret that holds the
  user's credentials, for example to opt the Secret in to a tool that copies Secrets into other namespaces. Keys that
  Rook sets or acts on are reserved.
- RGW SSE-S3 accepts `VAULT_TRANSIT_BACKEND_PATH` in `security.s3.connectionDetails` for a Vault transit engine that is
  not mounted at the default `transit` path. RGW SSE-KMS with the `transit` engine accepts it in
  `security.kms.connectionDetails` too.
