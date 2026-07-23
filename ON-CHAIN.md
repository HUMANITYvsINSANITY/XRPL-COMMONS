# On-Chain — What Lives on the Ledger

Every meaningful event in the HVI Platform produces an on-chain record. This document is a reference of what is anchored, why, and how it can be verified.

---

## Verified Live Examples

Not a testnet demo. These four transactions fired for real against the founder's own live production account (`r9avT7NURuqC7jbVxUjcrMkHAr5aqmHkSN`) as part of HVI's actual identity ceremony. Every hash below was checked directly against `xrplcluster.com` and confirmed `validated: true`, `tesSUCCESS` before this document was written — look them up yourself, no trust required:

| What fired | Transaction | Hash |
|---|---|---|
| `AccountSet` (Domain → hvi3.com) | tesSUCCESS | `E5CD6C68232D16F75D903CE30022432185606F7C09B01AF697F5D0DBE764B18D` |
| `DIDSet` (XLS-40) | tesSUCCESS | `B66E804182B61B3CB72D546CCF2B3470B4644E7704F021C578102460B7892228` |
| `PermissionedDomainSet` (XLS-80) | tesSUCCESS | `90C8E08C035875899FD2BBC440EF3317F2D34F74486F4D6F0949EF4DF927CBB0` |
| `CredentialCreate` (XLS-70) | tesSUCCESS | `69E2A01CADA72309076F75E30C9763A5B5A3F49CA68117EAC0EB38A0784F0649` |

```bash
curl -X POST https://xrplcluster.com -H "Content-Type: application/json" \
  -d '{"method":"tx","params":[{"transaction":"E5CD6C68232D16F75D903CE30022432185606F7C09B01AF697F5D0DBE764B18D"}]}'
```

---

## Identity Layer

### User DID (XLS-40)
**Transaction:** `DIDSet`
**Who signs:** The user, via Xaman
**When:** At the moment of invite-link registration

Each user's DID document contains:
- Their W3C DID identifier: `did:xrpl:1:<wallet-address>`
- HVI profile service endpoint
- Workspace membership service endpoint

**Verify:** `GET /did/<wallet-address>` on the platform, or query the XRPL ledger directly for the DID object on the account.

---

### Workspace Permissioned Domain (XLS-80)
**Transaction:** `PermissionedDomainSet`
**Who signs:** Workspace treasury (Regular Key, server-side)
**When:** First member registers in a workspace

Each workspace has one Permissioned Domain scoped to the `HVIWorkspaceMember` credential type. This is the on-chain gate for workspace-level access control.

**Verify:** Query the workspace account on the XRPL ledger for its PermissionedDomain object.

---

## Signing Infrastructure

### Regular Key (SetRegularKey)
**Transaction:** `SetRegularKey`
**Who signs:** Workspace treasury master key (one-time, during provisioning)
**When:** Workspace setup

Enables the server to sign `NFTokenMint`, `PermissionedDomainSet`, `CredentialCreate`, and `NFTokenModify` transactions without exposing the master seed. The master seed is used once to set the Regular Key and then discarded from the system.

---

## Credential Layer

### NFT Credential (XLS-20)
**Transaction:** `NFTokenMint`
**Who signs:** Workspace treasury (Regular Key)
**When:** Instructor issues a credential

Minted with `tfMutable` flag enabled, allowing future URI updates as the credential evolves. The NFT URI points to the full credential metadata hosted on IPFS.

**Verify:** Look up the NFTokenID on the XRPL ledger. The URI decodes to the credential metadata.

---

### Native XRPL Credential (XLS-70)
**Transaction:** `CredentialCreate`
**Who signs:** Workspace treasury (Regular Key)
**When:** Instructor issues a credential in native mode

A structured credential record directly on the ledger, tied to the holder's wallet address. Supports expiration dates and credential type codes.

**Verify:** Query the XRPL ledger for CredentialObject by issuer + subject + credential type.

---

### Dynamic Credential Update (XLS-46d)
**Transaction:** `NFTokenModify`
**Who signs:** Workspace treasury (Regular Key, auto-signed)
**When:** Learner reaches a milestone, or a live stream ends

Updates the URI of an existing NFT without burning and reminting. Used for:
- Achievement milestones (credential evolves as learner progresses)
- Stream recordings (NFT URI updated to sealed IPFS archive at stream end)

**Verify:** The current URI on the NFT reflects the latest state. Historical states are in the IPFS content at each URI.

---

## Payment Layer

### RLUSD Trust Line
**Transaction:** `TrustSet`
**Who signs:** Workspace treasury (Regular Key)
**When:** Workspace treasury is provisioned

Enables the workspace to receive RLUSD (Ripple USD) for subscription and service payments. Set automatically — no manual admin step.

---

## Escrow Layer

### Native Token Escrow (XLS-85)
**Transaction:** `EscrowCreate` / `EscrowFinish`
**Who signs:** Treasury (Regular Key)
**When:** Fired as a deliberate protocol-proof action, treasury-to-treasury

A real, time-triggered escrow — not a simulated or described one. This is not a holder payout mechanism; it's a live demonstration that the escrow primitive itself works end-to-end against real ledger conditions, exercised on both testnet and mainnet.

**Verify:** Query the treasury account for its Escrow ledger objects, or look up the `EscrowCreate`/`EscrowFinish` transaction pair directly.

---

## What Is NOT on the Ledger

To be explicit about what stays off-chain:

- User profile data, course content, quiz answers — stored in PostgreSQL
- IPFS CIDs are anchored *by reference* in NFT URIs, not stored on the ledger
- Video recordings stream through Cloudflare/Mux/Livepeer and are sealed to IPFS at end; only the final IPFS URI is on-chain
- Payment processing (Stripe card path) is fully off-chain; only XRP/RLUSD paths settle on-chain

---

## Querying the Ledger

All HVI on-chain records are queryable through standard XRPL APIs:

```bash
# Check a user DID
curl -X POST https://xrplcluster.com -d '{"method":"account_objects","params":[{"account":"<wallet>","type":"did"}]}'

# Check an NFT
curl -X POST https://xrplcluster.com -d '{"method":"nft_info","params":[{"nft_id":"<token-id>"}]}'

# Check a Permissioned Domain
curl -X POST https://xrplcluster.com -d '{"method":"account_objects","params":[{"account":"<workspace-treasury>","type":"permissioned_domain"}]}'

# Check a native credential
curl -X POST https://xrplcluster.com -d '{"method":"account_objects","params":[{"account":"<holder-wallet>","type":"credential"}]}'
```

Everything here is on the public ledger. No API key required.
