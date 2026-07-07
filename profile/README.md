<!--
  This file renders as the OHS Software Foundation GitHub org landing page.
  Place it at:  .github/profile/README.md
  Replace placeholder links (ohs.dev, docs, chat, calendar) with real URLs before publishing.
  Confirm partner names, WHO framing, and impact metrics are cleared for public use.
-->

<div align="center">

<!-- TODO: replace with hosted logo, e.g. ./assets/ohs-logo.svg -->
<img src="https://github.com/ohs-foundation/.github/blob/main/ohs-logo-horizontal-transparent.png" alt="OHS Software Foundation" width="480" />

# Open Health Stack Software Foundation (OHS-SF)

**A [Linux Foundation](https://www.linuxfoundation.org/) project · Built on open standards for advancing next-gen global digital health** 

[Intro](#what-is-the-ohs-sf) · [Start Here](#start-here) · [Contributing](#contributing) · [Community](#community) · [hello@ohs.foundation](mailto:hello@ohs.foundation)

</div>

---

## What is the OHS-SF?

The OHS Software Foundation builds and maintains **open, reusable building blocks for digital health** — standards-based libraries, SDKs, and reference tooling that make it dramatically easier to build interoperable, AI-ready solutions.

The idea is simple: stop rebuilding the same plumbing. When the foundational components are open, shared, and maintained in common, developers everywhere spend less time wiring up infrastructure and more time on the parts of a solution that actually improve care — and they keep ownership of what they build.

> **The shift we're built for:**
> - from vertical, single-program solutions → **reusable building blocks** ·
> - from external vendor lock-in → **locally-owned innovation** ·
> - from bespoke integrations → **open standards & interoperability**.

These building blocks are designed for the realities of global health — secure, offline-capable, and built to work in low-resource and low-connectivity settings — and are stewarded in a neutral, community-owned home at the Linux Foundation.

## The three pillars

OHS-SF work is organized into three pillars. Each repository in this organization belongs to one of them (filterable via the `pillar` property and `ohs-*` topics).

| | Pillar | What it covers | Status |
|---|---|---|---|
| **01** | **[FHIR Foundations](#01--fhir-foundations)** | Standards-based building blocks — libraries, SDKs, and components that make it easier to build with HL7 FHIR | Active |
| **02** | **[OHS Player](#02--ohs-player)** | A Multiplatform (Android, iOS, Web) reference toolkit to build and deploy FHIR — and, soon, AI — solutions faster | Active |
| **03** | **[AI Commons](#03--ai-commons)** | A neutral space for safe, verifiable, model-agnostic AI for global health — evals, benchmarks, and tooling | Forming |

## Start here

| If you want to… | Begin with |
|---|---|
| Build a FHIR-native **Android app** (data capture, offline sync, decision support) | [`android-fhir`](https://github.com/ohs-foundation/android-fhir) |
| Build **cross-platform** (Android, iOS, JVM, Web) on FHIR | the [`kotlin-*` libraries](#01--fhir-foundations) *(next-generation, evolving)* |
| Add **access control / privacy** in front of a FHIR store | [`fhir-gateway`](https://github.com/ohs-foundation/fhir-gateway) |
| Run **analytics** and query FHIR data with SQL | [`fhir-data-pipes`](https://github.com/ohs-foundation/fhir-data-pipes) |
| See a **reference toolkit** assembled end-to-end | [`"OHS Player" Toolkit`](#02--ohs-player) |
| **Contribute** to the community | [`Contributing`](#contributing) |

---

### 01 · FHIR Foundations 
**Standards-based building blocks.** Foundational libraries, SDKs, and components for building with HL7 FHIR — the consolidated "plumbing" so you don't rebuild it | [View Collection](https://github.com/orgs/ohs-foundation/repositories?q=topic:ohs-fhir-foundations)

> **Choosing a generation:** `android-fhir` is the mature, production-proven stack for Android. The `kotlin-*` libraries are a Kotlin Multiplatform next generation under active development — ideal for cross-platform work, but APIs may still change.

| Repository | Component | Maturity |
|---|---|---|
| [`android-fhir`](https://github.com/ohs-foundation/android-fhir) | **Android FHIR SDK** — Kotlin libraries for offline-capable, mobile-first FHIR apps (Structured Data Capture, FHIR Engine, Workflow) | Maintenance |
| [`fhir-gateway`](https://github.com/ohs-foundation/fhir-gateway) | **FHIR Info Gateway** — reverse proxy for access-control and privacy policies in front of any FHIR store | Stable |
| [`fhir-data-pipes`](https://github.com/ohs-foundation/fhir-data-pipes) | **FHIR Analytics** — pipelines that transform FHIR into SQL-on-FHIR for scalable querying & dashboards | Stable |
| [`kotlin-fhir`](https://github.com/ohs-foundation/kotlin-fhir) | **Kotlin FHIR** — lean FHIR data model on Kotlin Multiplatform | Beta |
| [`kotlin-fhirpath`](https://github.com/ohs-foundation/kotlin-fhirpath) | **Kotlin FHIRPath** — FHIRPath on Kotlin Multiplatform | Beta |
| [`kotlin-fhir-data-capture`](https://github.com/ohs-foundation/kotlin-fhir-data-capture) | **Kotlin SDC** — Multiplatform data capture from FHIR Questionnaires | Alpha |
| [`kotlin-fhir-engine`](https://github.com/ohs-foundation/kotlin-fhir-engine) | **Kotlin FHIR Engine** — Multiplatform on-device FHIR storage & sync | Evolving |

### 02 · OHS Player
**A Multiplatform reference toolkit** that shows how to assemble FHIR Foundations components into working solutions across Android, iOS, and Web — so teams build and deploy faster | | [View Collection](https://github.com/orgs/ohs-foundation/repositories?q=topic:ohs-player)

| Repository | Role |
|---|---|
| [`ohs-player`](https://github.com/ohs-foundation/ohs-player) | Reference toolkit overview & entry point |
| [`ohs-player-reference-client-app`](https://github.com/ohs-foundation/ohs-player-reference-client-app) | Configurable Kotlin Multiplatform client app |
| [`ohs-player-reference-web-portal`](https://github.com/ohs-foundation/ohs-player-reference-web-portal) | Web portal for managing workforce hierarchies |
| [`ohs-player-reference-infrastructure`](https://github.com/ohs-foundation/ohs-player-reference-infrastructure) | Deployment scripts & container images |

> **Reference, not product.** The Foundation publishes building blocks and reference toolkits — not standalone, deployable end-user products. Player is a starting point you adapt and own.

### 03 · AI Commons (Launching)
**A neutral space for safe, effective AI in global health** — *forming.* Model-agnostic collaboration on evals, benchmarks, verifiable AI, and supporting tooling (skills, MCPs), in partnership with the WHO and the wider ecosystem.

Repositories will appear here as the pillar takes shape. Have a project to donate or an idea to support? [Let's talk](mailto:hello@ohs.foundation).

---
## Contributing

We welcome contributions of every kind — code, documentation, testing, design, and field feedback from real deployments. Contributing to technical projects does **not** require Foundation membership.

- **New here?** Browse [`good first issue`](https://github.com/search?q=org%3Aohs-foundation+label%3A%22good+first+issue%22+state%3Aopen&type=issues) across the org.
- **Each repository** has its own contribution and build instructions in its README and `CONTRIBUTING.md`.
- **Reporting a vulnerability?** Healthcare software deserves extra care — please follow each repo's security policy and do not open public issues for security reports.

## Code of Conduct
This project follows the [OHS Software Foundation Code of Conduct](https://github.com/ohs-foundation/.github/blob/main/CODE_OF_CONDUCT.md). By participating, you agree to uphold these standards.

## Community

- 💬 Chat : [Join on Discord](https://discord.com/invite/Uyxn5YDvUW)
- 📅 Community calls: [Subscribe to the Community Calendar](https://shorturl.at/VMmJa)
- 📨 General contact: [hello@ohs.foundation](mailto:hello@ohs.foundation)

## Governance

OHS-SF is a community-driven, vendor-neutral project hosted by the Linux Foundation, with open governance set by the community doing the work. The formal charter and governance model are being finalized by the formation group and will be published here as the Foundation launches.

## Project History

Open Health Stack launched in 2023 — created at Google in collaboration with the WHO and a global developer community — as a suite of Digital Public Goods for FHIR-native digital health. 

OHS transitioned from a Google-led project into an independent, community-owned **umbrella project at the Linux Foundation** — a neutral home built to steward these building blocks for the long term and to serve the global health ecosystem that depends on them.

## License

OHS components are released under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) unless a repository states otherwise.

<sub>HL7® and FHIR® are registered trademarks of Health Level Seven International. Use does not constitute endorsement.</sub>
