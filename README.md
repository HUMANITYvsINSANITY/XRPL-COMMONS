# HVI Platform — Humanity vs. Insanity
### Built on the XRP Ledger. Live in Production. Covering the Full XLS Stack.

---

## What This Is

The HVI Platform is an institutional-grade, multi-tenant infrastructure system built entirely on the XRP Ledger. It was not built to demo one standard. It was built to solve real problems for schools, institutions, NFT communities, families, and enterprise organizations — and in doing so, it ended up implementing the entire modern XLS stack in a single cohesive platform.

This is not a proof-of-concept. This is production infrastructure, live at **hvi3.com**, being used today.

---

## XRPL Standards Implemented

### XLS-20 — Native NFTs
Full NFT lifecycle: mint, burn, transfer, offer creation. Used as the primary credentialing and achievement token across all platform workspaces. Every credential issued, every milestone achieved, every course completed is backed by an on-chain NFT.

- `NFTokenMint` with `tfMutable` and `tfTransferable` flags for upgradeable credentials
- `NFTokenBurn` for revocation
- `NFTokenCreateOffer` for credential transfer workflows
- Batch minting for class-level and cohort-level issuance
- Bulk import/export pipeline for enterprise onboarding

---

### XLS-40 — Decentralized Identifiers (DIDs)
Every user who joins the HVI Platform gets a W3C-compatible DID anchored on-chain via `DIDSet`. This fires automatically at the point of wallet-linked registration — no extra step required from the user. They scan Xaman once. That's it. Their identity is on the ledger.

The DID document includes:
- Their HVI profile endpoint
- Their workspace membership endpoint (anchoring *which* institution they belong to)

This means every learner, instructor, and administrator has a verifiable on-chain identity tied to a real institution — not just a wallet address.

---

### XLS-46d — Dynamic NFTs (dNFTs)
NFTs on HVI are not static. They evolve. When a learner completes a new module, their credential NFT updates on-chain without burning and reminting. When a live stream ends, the recording is sealed to IPFS and the stream NFT's URI is updated to point to the permanent archive.

- `NFTokenModify` for non-destructive URI updates
- Achievement Milestone System triggers automatic on-chain updates
- Live stream recordings become dynamic NFTs sealed to IPFS at stream end
- "Wave" system: incremental credential data pushed to issued tokens over time

This is the standard that makes credentials *alive* rather than frozen snapshots.

---

### XLS-70 — Native XRPL Credentials
Beyond NFTs, the platform supports native `CredentialCreate` transactions for issuing structured, verifiable credentials directly on the ledger. These can be verified publicly through the platform's credential verification portal, via QR scan, or via Xaman wallet signature check-in.

- Private credential issuance with on-chain security anchoring
- Public credential catalog and verification endpoint
- QR/NFC badge generation for physical check-in scenarios
- Program enrollment with auto-credentialing on completion

---

### XLS-80 — Permissioned Domains
Every provisioned workspace on HVI fires a `PermissionedDomainSet` transaction at the point of first member registration. This creates an on-chain domain scoped to the `HVIWorkspaceMember` credential type. No manual setup. No admin action required.

- Server-side treasury signing via `SetRegularKey` — no seed stored online
- Domain ID persisted per workspace and enforced at the API layer
- Fires automatically, non-blocking, on invite-link registration
- Enables credential-gated access control at the XRPL protocol level

This means every school, institution, or community on the HVI Platform has its own permissioned access domain on the XRP Ledger — automatically.

---

### XLS-85 — Native Token Escrow
The platform fires real `EscrowCreate`/`EscrowFinish` transactions, treasury-to-treasury, as a live protocol-proof action — not a simulated demo. Time-triggered release, verifiable on-ledger, exercised end-to-end against real testnet and mainnet conditions.

---

### SetRegularKey — Automated Treasury Signing
To enable server-side signing without exposing master seeds, the platform uses XRPL's `SetRegularKey` transaction to provision per-workspace signing keys. The treasury wallet stores only a Regular Key on the server. All automated transactions — NFT mints, credential issuance, domain creation, dNFT updates — sign through this key.

This is the architecture that makes server-automated XRPL operations safe at scale.

---

### TrustSet — RLUSD Integration
The platform automatically configures RLUSD (Ripple USD) trust lines for workspace treasury wallets, enabling stablecoin payments and reward flows without manual setup. Payment options include both Stripe (Web2) and XRP/RLUSD (Web3) at the point of subscription and service billing.

---

### Xaman (XUMM) — Deep Integration
Xaman is the signing layer for all user-facing XRPL operations:

- Login via wallet signature (replacing passwords entirely)
- DID anchoring at registration
- `SetRegularKey` provisioning for workspace admins
- Credential verification check-in
- Live stream permission flows
- Cosigning for treasury operations

Users never see a transaction hash. They see a QR code or a mobile deep link. The complexity is invisible.

---

## What This Platform Actually Does

| Layer | What Is Built |
|---|---|
| **Identity** | W3C DID per user, anchored on XRPL at registration |
| **Access Control** | XLS-80 Permissioned Domain per workspace, auto-provisioned |
| **Credentials** | XLS-20 NFT + XLS-70 native credential, dual-mode issuance |
| **Dynamic Records** | XLS-46d dNFT updates on milestone, module completion, and stream end |
| **Escrow** | XLS-85 native token escrow, live protocol-proof action |
| **Payments** | Stripe + XRP + RLUSD, dual-path checkout |
| **Streaming** | Multi-provider live streaming (Cloudflare, Mux, Livepeer) sealed to IPFS as dNFTs |
| **Multi-tenancy** | Schools, institutions, families, NFT projects, enterprise — each with isolated data |
| **Roles** | Platform Owner, Tenant Admin, Instructor, Employee, Parent, Learner |
| **Cross-chain** | EVM (MetaMask) and Solana (Phantom) wallet identity alongside XRPL primary |
| **Verification** | Public credential portal, QR scan, NFC badge, Xaman sign check-in |

See `ON-CHAIN.md` for real, independently-verifiable mainnet transaction hashes for the identity and access-control layers — not just a description of what the code does, but proof it actually happened.

---

## The Point

Most teams pick one XLS standard and build around it. We took the full stack — XLS-20, XLS-40, XLS-46d, XLS-70, XLS-80, XLS-85 — and wired it into a single platform that a school administrator, a parent, a learner, or an enterprise customer can use without knowing what a transaction is.

That's the work. That's what's live.

---

*Humanity vs. Insanity Platform — hvi3.com*
*HUMANITYvsINSANITY GitHub Organization*
