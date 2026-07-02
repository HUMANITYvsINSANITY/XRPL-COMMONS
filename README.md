# XRPL-COMMONS

**Humanity vs Insanity (HVI)** — an institutional-grade, multi-tenant education and credentialing platform built on the XRP Ledger.

This repository is the public showcase for the HVI Platform: an overview of what it does, how it's built, and how its XRPL integrations work.

## What is HVI?

HVI combines an adaptive learning engine with NFT-powered, on-chain credentials. It's designed for schools, institutions, parent/youth groups, and NFT project communities that need verifiable digital credentials and tailored educational experiences — all anchored to the XRP Ledger for authenticity and portability.

## Core Capabilities

- **Multi-Tenancy** — Isolated workspaces for different tenant types: `SCHOOL`, `HOME`, `NFT_PROJECT`, `ENTERPRISE`, `EVENTS`, `HVI`.
- **Role-Based Access Control** — Granular roles: Platform Owner, Tenant Admin, Instructor, Employee, Parent, Learner.
- **Adaptive Learning Engine** — Structured modules, lessons, and quizzes that adapt to the learner.
- **On-Chain Credentialing** — Credential templates, verification codes, a public verification catalog, and enrollment-based programs. Credentials are issued via XRPL `CredentialCreate` or `NFTokenMint`, with QR/Xaman-wallet check-in for verification.
- **NFT Metadata Engine** — Dynamic NFT metadata (XLS-46d dNFT), on-chain updates via `NFTokenModify`, batch operations, and an achievement milestone system.
- **XRPL Ecosystem Tools** — An integrated wallet scanner and multi-blockchain wallet management (XRPL, EVM via MetaMask, Solana via Phantom), with XRPL always treated as the primary chain.
- **Web2 On-Ramp** — New users get an auto-generated XRPL wallet on registration (via `xrpl.js`), with a one-time encrypted seed reveal flow — no prior crypto experience required.
- **Live Streaming → Sealed NFTs** — Multi-provider streaming (Cloudflare, Mux, Livepeer) with recordings sealed to IPFS as dynamic NFTs, including encrypted playback for sensitive content.
- **Payments** — Dual Stripe + XRP payment paths, with XRP payments handled through Xaman (XUMM).

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Express.js, TypeScript, JWT, PostgreSQL + Drizzle ORM |
| Frontend | React, Vite, TanStack Query, wouter, shadcn/ui |
| Shared | Drizzle schema, Zod validation, shared TypeScript types |
| Ledger | XRP Ledger (`xrpl.js`), Xaman/XUMM wallet integration |

## XRPL Integration Highlights

- **On-chain credentials** via `CredentialCreate` and `NFTokenMint`, with public verification.
- **Dynamic NFTs (dNFT)** following XLS-46d, updated on-chain through `NFTokenModify`.
- **Auto-provisioned wallets** for every new user, generated with `xrpl.js` and encrypted at rest.
- **Cross-chain identity layer** — XRPL as the primary chain, with optional EVM and Solana wallet linking for broader NFT project support.

## Status

This repository documents the platform's architecture and capabilities as a public reference. It does not contain the production application source.

## License

MIT
