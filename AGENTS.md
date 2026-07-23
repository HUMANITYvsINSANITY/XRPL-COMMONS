# HVI — AI Agents & Assistants
### Built with AI. Operated by AI. Grounded in truth, not the open web.

---

> **HVI isn't just built on XRPL — it's built and run by an AI-augmented team, and it ships
> AI assistants grounded in a private knowledge base of its own code and the XRPL/XLS
> standards.**

This document describes the AI that builds HVI and the AI that HVI ships to its users. It
complements `README.md` (the XLS stack), `HOW-IT-WORKS.md`, and `ON-CHAIN.md`.

---

## Two kinds of agent

**1. The persona team — how HVI is built.** A team of specialized AI agents, each an expert
in one discipline, collaborates to design, build, and review the platform. Every agent has
persistent memory and a clear mandate, and load-bearing changes pass a release gate.

**2. The shipped assistants — what HVI's users get.** Every user has an AI assistant that
answers questions and guides them — grounded in a private knowledge base of HVI's own code
and the XRPL/XLS standards. **These assistants never use the open web.** If the answer isn't
in the knowledge base, they say so and ask, rather than inventing it.

---

## The persona team

| Discipline | Owns |
|---|---|
| **Architect** | Multi-tenant + cross-chain design, domain model, architecture decisions, the preservation mandate |
| **Developer** | Code, tests, review — test-driven on money, on-chain, auth, and healthcare paths |
| **Compliance** | HIPAA / FERPA / AML-KYC posture, SOC 2, breach runbook, "no medical data on-chain" |
| **Legal** | Contracts, ToS/Privacy, settlement terms, the securities firewall |
| **Designer** | Multi-audience adaptive UI, accessibility, UX preservation |
| **Brand** | Positioning, voice, protecting the meme + marketplace value |
| **BizDev** | Partner & distributor program, Opulence X |
| **End-user advocate** | User journeys, microcopy, the use-case quality bar |
| **Finance** | Settlement/retainage/treasury, unit economics, payments & on-ramp |

Supported by function templates for Marketing, Customer Success, Support, Community, Sales,
and People Ops as those functions come online.

**Release gate.** Nothing load-bearing ships without Finance + Compliance sign-off, founder-final.

---

## The shipped assistants

### In-platform assistant
Every signed-in user sees one assistant — a floating button on every page. It does two things:

- **Guide** — answers how-to questions and walks the user to the action in as few clicks as
  possible, always using the platform's real navigation labels.
- **Report** — one tap files a structured issue straight into the team's tracker.

It supports **voice both ways** — speak to it, and it can speak back — using
privacy-preserving, self-hosted speech-to-text so audio never leaves HVI's infrastructure.
By design it has exactly two capabilities (answer, report) and cannot change platform state
— a deliberate guardrail against prompt-injection from untrusted input.

### Grounded in truth, not the web
Both the in-platform assistant and HVI's operator assistant read from a shared knowledge
base built from local clones of:

- HVI's own repositories
- The **XRPL / XLS standards** (`XRPL-Standards`, `xrpl.js`, `xrpl-dev-portal`, `rippled`)
- Curated HVI reference docs

The knowledge base refreshes on a schedule and is **read-only** — the assistants can search
and read it, never write to it. This is why HVI's assistants don't hallucinate XLS numbers,
transaction types, or nav labels: they're answering from the source, or not at all.

---

*Humanity vs. Insanity Platform — hvi3.com*
*HUMANITYvsINSANITY GitHub Organization*
