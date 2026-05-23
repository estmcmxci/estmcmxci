# estmcmxci.eth

Building ENS as the authority-policy substrate for the managed agent runtime platform (MARP) era.
Identity protocol & trust architecture — ENS-native, runtime-portable, audit-grade.

> *"Generation is abundant; verification is scarce."*

I ship to ENS's canonical contracts, publish ENS-native specs through the Public Goods program, and operate live ENS-bound agent deployments on mainnet and Base. 

Current work: an ENS verification and revocation toolkit (Verifier + AuthResolver + SDK + conformance suite) for managed agent runtime platforms — **submitted to the ENS Service Provider Program (SPP3), July 2026 – July 2027 cycle, currently under review**.

---

## Upstream ENS Contributions

### Canonical ENS Contracts — PR #509 (merged, v1.7.0)

Replaced software-implemented `EllipticCurve` verification with the **EIP-7951 P-256 precompile** in ENS's DNSSEC oracle (Algorithm 13). ~98% gas reduction (~200k+ → ~3,500 per verification). Merged by Makoto Inoue (ENS Labs) 26 Jan 2026; shipped to production in v1.7.0 on 13 Mar 2026.

- PR: https://github.com/ensdomains/ens-contracts/pull/509
- Release: https://github.com/ensdomains/ens-contracts/releases/tag/v1.7.0
- Contribution trail: https://github.com/ensdomains/ens-contracts/pulls?q=is%3Apr+author%3Aestmcmxci

### ENS Public Goods Grant — "ENS v2 Interop Research" (Sep 2025, Stage 1 completed)

Two committed deliverables, both shipped:

- **Universal Resolver Matrix (URM)** — a reference framework that reframes ENS as *"a trust-routing system and compiler that anchors heterogeneous namespaces to Ethereum as the root of trust,"* organizing resolver architectures into a matrix (trust model, proof system, lifecycle, verification path). Convened with Kernel and Nick Johnson (ENS Labs). Published Dec 2025.
  - https://discuss.ens.domains/t/universal-resolver-matrix-a-design-framework-for-heterogeneous-resolver-architecture/21734
- **WebAuthn-for-ENS specification** — a productionizable design for the agent-authority / WebAuthn-verifier cell URM identified. The technical foundation for the SPP3 proposal.
  - https://docs.steg.eth.link/specifications/webauthn-specification/
- Grant record: [builder.ensgrants.xyz](https://builder.ensgrants.xyz) (grantee: `fundamentalia.eth`). Research thread: https://discuss.ens.domains/t/ens-research-namechain-ensip-19-multichain-interop/21392

### DNSSEC Modernization (EIP-7951 context)

Practical pathways for cheaper cryptographic verification in ENS-adjacent flows — the work that became PR #509.

- Forum: https://discuss.ens.domains/t/updating-dnssec-verification-with-eip-7951/21754
- Demos: https://github.com/steg-eth/dnssec-solutions
- Talk (Devcon SEA, Nov 2024): ["Universal ECCs: Use Cases for the P256 Precompile in Decentralized Internet Infrastructure"](https://www.youtube.com/watch?v=e_QBTQGMxPs) — Ethereum Foundation channel.

---

## ENS-Native Agent Identity (Live)

### Synthesis — Trust Resolution Layer

A verifiable, personhood-anchored, ENS-bound agent identity framework. Five-layer TRL composing ENSIP-25, ENSIP-26, ENSIP-64, ERC-8004, AIP, DVS, and runtime/session attestation paths. MIT-licensed, four packages:

- `@synthesis/resolver` — TypeScript resolution library
- `@synthesis/cli` — **Ensemble CLI** (`issue → pin → publish → verify → rotate`)
- `@synthesis/conformance` — **Ensemble Conformance Suite**
- `@synthesis/site` — explorer at [estmcmxci.co](https://estmcmxci.co)

Repo: https://github.com/estmcmxci/synthesis

**1st Place, ENS Identity track — Synthesis Hackathon (May 2026).** [Track](https://synthesis.mandate.md/tracks/ens-identity-i4jgf3) · [Project](https://synthesis.mandate.md/projects/trust-resolution-layer-b67a)

### Live Reference Deployments

- **emilemarcelagustin.eth** — ENS-bound agent on Ethereum mainnet (nine ENSIP-64 text records) + ERC-8004 agent **#24994** on Base mainnet. Hosted runtime on Pinata Agents.
  - https://estmcmxci.co/agent/emilemarcelagustin.eth
- **alpha-go.bankrtest.eth** — parallel test deployment, ERC-8004 agent **#19327** on Base mainnet.
- Forum post: https://discuss.ens.domains/t/reference-implementation-of-an-ens-bound-agent/22100

### NCCoE Position Paper

ENS as the naming layer for AI agent identity — submitted to NIST's National Cybersecurity Center of Excellence.

- https://nccoe.emilemarcelagustin.eth.link

### Oikonomos — ENS-Integrated Agent Operations

Agent keychain + wallet-oriented operational primitives for autonomous DeFi workflows.

- **Finalist + Integrate ENS bounty winner — ETHGlobal HackMoney 2026** (top-of-hackathon, all sponsor tracks). [Showcase](https://ethglobal.com/showcase/oikonomos-w6z57)
- Repo: https://github.com/estmcmxci/oikonomos

### Trust-Swap — Gate-Then-Execute Pattern

Reference implementation for trust-gated settlement over resolver-based verification.

- Repo: https://github.com/estmcmxci/trust-swap

---

## The MARP Thesis

> The next operator class is managed agent runtime platforms (MARPs).
> ENS should be their authority-policy substrate.

Managed agent runtime platforms — Pinata Agents, Virtuals Protocol, Bankr Agents, Anthropic + Cloudflare's Claude Managed Agents — are moving from pilots to governed production. What they do *not* standardize is a portable authorization layer counterparties can verify independently: no outside service can confirm, in real time, that an agent-signed action came from a credential the operator currently authorizes.

ENS already provides naming, discovery, registry, and typed records (ENSIP-25/26/64, ERC-8004). The missing layer is an **ENS-keyed authority-policy lookup surface** above those primitives. That lookup is the gap. The SPP3 proposal delivers it.

Full positioning: [*The Next Operator Class: Managed Agent Runtime Platforms*](https://discuss.ens.domains/t/the-next-operator-class-managed-agent-runtime-platforms/22121) (May 2026).

---

## Current Focus

**Application status:** Steg SPP3 proposal — *ENS Verification and Revocation Toolkit for MARPs* — **submitted and under review** for the July 2026 – July 2027 cycle.

A defined integration service:

- **Verifier contract** — EIP-7951 P-256 precompile + ecrecover + EIP-1271 staticcall (extensible scheme dispatch)
- **AuthResolver contract** — per-name (UUPS proxies via `VerifiableFactory`), composing ENSv2's EAC + HCA substrate for credential, capability, and revocation records
- **TypeScript SDK** — normalized allow/deny reason codes (`verified` / `unverified` / `stale` / `revoked` / `mismatch` / `policy-denied` / `endpoint-unproven`)
- **Conformance suite** — reproducible test vectors, adversarial mutation cases
- **Three Wave-1 pilot integrations** — Pinata Agents (operator), Virtuals Protocol (protocol-native), x402 (capability publisher); Bankr Agents day-zero compatible
- **Third-party security audit** of Verifier + AuthResolver

A read-only forward-declaring scaffold of this pattern is already running against a live MARP: [BankrBot/skills PR #189](https://github.com/BankrBot/skills/pull/189) — publishes credential / capability / revocation records onto an ENS name via NameStone, resolves and verifies along the `verifyAction` ordering. Validated on `authtest.bankrtest.eth`.

---

## Writing + Ecosystem

- ENS forum: https://discuss.ens.domains/u/estmcmxci
- ENS name: https://ens.app/estmcmxci.eth
- Web: [estmcmxci.co](https://estmcmxci.co) · [steg.eth.link](https://steg.eth.link) · [docs.steg.eth.link](https://docs.steg.eth.link)
