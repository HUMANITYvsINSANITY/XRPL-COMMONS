# HVI Platform — Humanity vs. Insanity

> **Institutional-grade education and credentialing, powered by XRPL.**
> *Where learning becomes a permanent, verifiable, on-chain achievement.*

---

## The Problem

Education credentials are broken.

Certificates get lost, forged, and ignored. Digital badges live in siloed platforms that shut down, change ownership, or simply don't communicate with each other. Employers can't verify them. Learners can't own them. Institutions can't trust them.

At the same time, the Web3 ecosystem is brimming with NFT infrastructure — but almost none of it is connected to real learning outcomes. NFTs are minted for art and speculation, not for the thing that actually changes lives: **verified knowledge and achievement**.

Meanwhile, millions of families, schools, and community groups are locked out of Web3 entirely because the on-ramp requires crypto wallets, seed phrases, and technical know-how that most people don't have.

**The gap:** institutions need verifiable, tamper-proof credentials. Learners need a seamless experience. Web3 needs a legitimate use case grounded in real human achievement.

---

## The Solution

**HVI Platform** is a multi-tenant education and credentialing platform that issues NFT-powered credentials anchored to the XRP Ledger — with a frictionless Web2 on-ramp so anyone can participate, regardless of their crypto knowledge.

When a learner completes a course, earns a milestone, or receives an award:

1. A credential is minted as an NFT on the XRPL using **NFTokenMint** or **CredentialCreate**
2. The metadata — including achievement details, tier, version, and collection context — is pinned to **IPFS** for permanent decentralized storage
3. The credential is **publicly verifiable** via QR code, NFC badge, or Xaman wallet scan
4. As the learner progresses, credentials can be updated on-chain via **NFTokenModify** — turning static NFTs into living records of growth

No crypto wallet needed to sign up. Every new user gets an XRPL wallet generated automatically and silently on registration, with the seed phrase encrypted and shown exactly once.

---

## Key Features

### For Learners
- **Frictionless onboarding** — sign up with email, get an XRPL wallet automatically. No MetaMask required.
- **NFT credentials** — every achievement is a real, on-chain token you own forever
- **Dynamic credentials** — credentials can receive "waves" of new data as you level up, without re-issuing
- **Cross-chain wallet identity** — connect MetaMask (EVM) or Phantom (Solana) alongside your XRPL wallet
- **Age-adaptive dashboards** — Junior, Youth, and Elder variants optimised for different learner profiles

### For Institutions & Workspaces
- **Multi-tenant isolation** — Schools, enterprises, NFT projects, family groups, and event organizers each get their own fully isolated workspace
- **Adaptive learning engine** — structured content hierarchy: Modules → Lessons → Quizzes → Milestones
- **Bulk credential issuance** — issue credentials to entire cohorts in one action
- **Credential programs** — learners enroll in structured programs with auto-credentialing on completion
- **QR / NFC verification** — physical badge generation for in-person check-in and credential verification
- **Role-based access control** — Platform Owner, Tenant Admin, Instructor, Employee, Parent, Learner with granular permissions

### For NFT Collection Managers
- **Collection-first mint hardening** — collections must be established on-chain (taxon claimed and conflict-checked) before any NFT can be minted
- **Art Generator** — generate NFT artwork from layered traits
- **Batch minting** — mint entire collections with a single SSE-streamed batch operation
- **Dynamic NFTs (dNFT)** — XLS-46d compliant, supporting on-chain metadata updates via NFTokenModify
- **Live Stream → NFT pipeline** — live recordings are automatically sealed to IPFS and minted as NFTs
- **Concert Stream Tags** — lightweight broadcast credential type linking live events to NFT collections

### For Platform Operators
- **Opulence X Marketplace API** — partner REST API for marketplace integrations (NFT + credential data)
- **XRP Portal payment gateway** — dual Stripe + XRP payment options; XRP payments via Xaman (XUMM SDK)
- **Admin Console** — full audit logs, member management, workspace provisioning, wallet scanning
- **FAQ & Support system** — public FAQ, admin manager, support inbox, and user feedback widget
- **Trial systems** — MEME_COIN trial invites and free trial links for onboarding new workspaces

---

## Technical Architecture

### Stack

| Layer | Technology |
|-------|-----------|
| **Backend** | Express.js + TypeScript |
| **Frontend** | React + Vite + TanStack Query + wouter + shadcn/ui |
| **Database** | PostgreSQL with Drizzle ORM |
| **Auth** | JWT + bcrypt + server-side logout logging |
| **Blockchain** | XRPL (xrpl.js v4) |
| **Wallet Signing** | Xaman / XUMM SDK |
| **Storage** | IPFS (Pinata + backup gateway) |
| **Payments** | Stripe + XRP via Xaman |
| **Video** | Cloudflare Stream + Mux + Livepeer (multi-provider) |
| **Email** | SMTP (nodemailer) |

### Multi-Tenancy

Every workspace (tenant) is fully isolated at the data layer. Each tenant can have its own:
- Branding (logo, colours, theme — Classic / Dark / Light)
- XRPL signing wallet (treasury key)
- Pinata IPFS credentials
- Member roster with role assignments
- NFT collections, credential templates, content library, and service jobs

Workspace types: `SCHOOL`, `HOME`, `NFT_PROJECT`, `ENTERPRISE`, `EVENTS`, `HVI`

### Security Model
- JWT tokens with server-side revocation
- bcrypt password hashing
- AES-256-GCM encryption for stored XRPL seed phrases
- Seed phrases returned exactly once (on registration) and never again
- Role-based API guards on every endpoint
- Tenant-scoped data access enforced at the storage layer

---

## XRPL & Web3 Integration

This is where HVI goes beyond any existing education platform.

### On-Chain Credentials
- **NFTokenMint** — credentials minted with `tfTransferable` + optional `tfMutable` flag
- **CredentialCreate** — native XRPL credential objects for institutional issuance
- **NFTokenModify** — update credential metadata on-chain without burning (requires `tfMutable`)
- **NFTokenCreateOffer / NFTokenAcceptOffer** — credential transfer to learner wallet after mint

### Collection-First Mint Hardening
Before any NFT can be minted, the collection must be **established on-chain**:
1. The platform scans the issuer wallet's existing NFTs to detect taxon conflicts
2. If the taxon is free, the collection is marked on-chain and the taxon is locked
3. Only then are mint buttons enabled — preventing orphaned or mixed-collection NFTs

### Dynamic Credentials ("Waves")
Credentials aren't static. Institutions can push incremental data updates — called *waves* — to already-issued credentials. Each wave triggers an `NFTokenModify` transaction, updating the on-chain metadata URI to point to a new IPFS pin that includes the new achievement data.

### Web2 On-Ramp
Every user who registers gets an XRPL wallet generated silently using `Wallet.generate()`. The seed is encrypted with AES-256-GCM and stored securely. The user sees their seed phrase exactly once on a dedicated confirmation screen. From that point on, they have a real XRPL identity — without ever having visited an exchange or crypto app.

### Cross-Chain Identity
Users can connect EVM wallets (MetaMask) and Solana wallets (Phantom) alongside their primary XRPL wallet. Only public addresses are stored (privacy-first). The XRPL wallet is always shown with a "Primary Chain" badge.

### Live Stream → NFT
When a workspace hosts a live stream (via Cloudflare, Mux, or Livepeer), the recording is:
1. Pinned to IPFS with full metadata
2. Minted as a dynamic NFT
3. Linked to the relevant NFT collection via Concert Stream Tag
4. Optionally encrypted for private/gated playback

---

## Demo Flow

1. **Sign up** at `/get-started` — 3-step education gate explaining wallets and what you unlock → register → XRPL wallet auto-generated
2. **Create a workspace** — choose workspace type (school, family, enterprise, NFT project)
3. **Set up a credential template** — name it, add a cover image, link to an NFT collection
4. **Issue a credential** — select a learner, issue — NFT minted on XRPL, metadata pinned to IPFS
5. **Verify the credential** — scan the QR code on the public verification page — on-chain confirmed
6. **Push a wave** — learner completes the next module → credential updated on-chain via NFTokenModify
7. **NFT Gallery** — view the full collection, establish it on-chain, batch mint, manage dynamic metadata

---

## Roadmap

- **Mobile app** (iOS + Android) — credential wallet and learning companion
- **Expanded Marketplace API** — deeper Opulence X integration, secondary market hooks
- **Community governance** — on-chain voting for curriculum decisions using credential-weighted votes
- **Credential stacking** — combine multiple credentials into a composite "degree" NFT
- **Open API** — allow third-party LMS integrations to push credentials via REST
- **Decentralized verifier network** — anyone can run a verification node, reducing reliance on centralised check-in

---

## Why XRPL?

- **Low fees** — minting and modifying NFTs costs fractions of a cent, making mass credentialing economically viable
- **Speed** — 3-5 second settlement, fast enough for real-time credential issuance during live events
- **NFTokenModify** — unique to XRPL; no other major chain supports mutable NFT metadata without a burn-and-remint cycle
- **CredentialCreate** — native credential primitive built into the ledger, not a smart contract workaround
- **Xaman ecosystem** — seamless mobile signing without exposing seed phrases
- **Sustainability** — carbon-neutral, no proof-of-work energy cost

---

## Team

*[Add team member names, roles, and backgrounds here]*

---

## Links

- **Live app**: [humanityvsinsanity.tech](https://humanityvsinsanity.tech)
- **GitHub**: *[Add repository link]*
- **Demo video**: *[Add Loom / YouTube link]*

---

*Built with purpose. Anchored on-chain. Owned by learners.*
