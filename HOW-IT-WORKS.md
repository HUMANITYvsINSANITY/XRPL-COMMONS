# How It Works — HVI Platform on XRPL

The HVI Platform connects real-world institutions — schools, communities, enterprise organizations — to the XRP Ledger. Here is exactly how that connection works from the moment a user joins to the moment their credential is verified on-chain.

---

## 1. Workspace Provisioning

Every institution on HVI runs in its own isolated workspace (multi-tenant). When a workspace is created:

- A **treasury wallet** is generated and a `SetRegularKey` transaction is submitted on-chain
- The server stores only the Regular Key — the master seed never touches the server
- All subsequent automated signing (minting, credential issuance, domain management) flows through this Regular Key

This means every institution has its own on-chain signing identity, and HVI never holds master seeds in production.

---

## 2. User Registration via Xaman

New members join through an invite link scanned with the Xaman mobile wallet. On confirmation:

**a. XLS-40 DID anchored**
A `DIDSet` Xaman payload is presented immediately after registration. The user signs it with their own wallet. Their DID document includes:
- Their HVI profile endpoint
- The workspace they joined

The user's on-chain identity is anchored in one scan — before they ever touch the platform.

**b. XLS-80 Permissioned Domain fired server-side**
Simultaneously (non-blocking, no user action), the server fires a `PermissionedDomainSet` transaction using the workspace treasury Regular Key. This creates an on-chain access domain scoped to the `HVIWorkspaceMember` credential type. It only fires once per workspace — subsequent registrations skip it if the domain already exists.

After these two steps: the user has an on-chain identity. The workspace has an on-chain access domain. Neither required any admin configuration.

---

## 3. Learning and Achievement

Inside the platform, learners move through modules, lessons, quizzes, and milestones. The content hierarchy is:

```
Program → Modules → Lessons → Quizzes → Milestones
```

As learners progress, the Achievement Milestone System triggers automated on-chain events:

- **New milestone reached** → the learner's credential NFT URI is updated via `NFTokenModify` (XLS-46d)
- **Program completed** → a completion credential is issued (XLS-20 NFT or XLS-70 native credential, admin's choice)
- **Wave data pushed** → incremental updates anchored to issued credentials over time

The credential NFT is not static. It evolves as the learner grows.

---

## 4. Credential Issuance

Instructors and admins issue credentials from templates. Two issuance modes:

| Mode | Transaction | Use Case |
|---|---|---|
| NFT | `NFTokenMint` (XLS-20) | Transferable achievement tokens |
| Native Credential | `CredentialCreate` (XLS-70) | Structured on-chain credential records |

Both modes support:
- Batch issuance (entire cohort at once)
- Verification codes tied to the issued credential
- QR/NFC badge generation for physical events
- Auto-credentialing on program completion

---

## 5. Verification

Credentials can be verified through multiple channels:

- **Public portal** at `/verify/:code` — anyone with the code can check authenticity
- **QR scan check-in** — physical event entry, scanned at the door
- **Xaman wallet sign** — holder signs with their wallet to prove ownership
- **NFC badge tap** — for persistent physical badges

All verification paths resolve back to the on-chain record. No central registry. No trust in HVI required.

---

## 6. Live Streaming → Dynamic NFTs

When a workspace streams live content (Cloudflare, Mux, or Livepeer), the stream is represented as an NFT. When the stream ends:

1. The recording is sealed to IPFS (permanent, content-addressed)
2. The stream NFT's URI is updated via `NFTokenModify` to point to the IPFS archive
3. The NFT is now a permanent, verifiable record of the event

Concert streams, community events, and educational sessions all become dNFTs automatically.

---

## The Stack

```
User (Xaman) → DIDSet → On-chain identity
Workspace → SetRegularKey → Automated signing
             PermissionedDomainSet → Access control
Learning → NFTokenModify → Evolving credential NFTs  
Completion → NFTokenMint / CredentialCreate → Issued credential
Stream end → NFTokenModify → Sealed recording NFT
Verification → Public portal / QR / Xaman sign
```

Everything flows through XRPL. Nothing is simulated or mocked.
