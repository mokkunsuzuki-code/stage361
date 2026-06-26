# Stage361: Revocation Proof Injection Gate

Stage361 adds a revocation proof injection gate on top of Stage360.

## Purpose

Stage360 binds external timestamp proof metadata.

Stage361 adds the next missing security question:

> Is the key or certificate revoked?

## What Stage361 Adds

- Stage360 result hash binding
- Stage359 public key fingerprint as revocation target
- OCSP proof receiver
- CRL proof receiver
- signed revocation metadata receiver
- pending_revocation_proof decision
- fake verified claim detection
- fail-closed block conditions

## Decision

Stage361 returns:

- `pending_revocation_proof`
- `accept_revocation_binding`
- `block`

At this stage, the default correct decision is:

```text
pending_revocation_proof

because Stage361 does not yet perform real OCSP or CRL cryptographic verification.

Safety Boundary

Stage361 does not include:

private keys
raw secrets
raw QKD key material
real OCSP verified claims
real CRL verified claims
Meaning

Stage361 does not say:

This certificate is definitely good.

Stage361 says:

The QSP evidence rail now has a safe place to inject and verify revocation proof later.

