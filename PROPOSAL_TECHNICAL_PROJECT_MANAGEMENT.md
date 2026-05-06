# Technical Proposal: Unified Project Management & Architecture Tracking
**Status:** Draft for Community Review  
**Target Audience:** Core Library Maintainers, Player Toolkit Contributors, Implementation Partners  

---

## 1. Executive Summary & Purpose

The Open Health Stack (OHS) ecosystem consists of two distinct engineering layers:
1. **The Foundational Core Libraries:** Engineering-driven, specification-anchored modules (such as `kotlin-fhir`) focused on HL7 FHIR compliance, performance, platform portability, and strict API stability.
2. **The OHS Player Reference Toolkit:** Application-level codebases designed to consolidate community learnings into a "next-layer" implementation framework. The Player acts as an adaptable, multiplatform configuration container allowing implementers to deploy cross-platform health solutions with minimal overhead.

As our distributed community grows, our GitHub organization must adapt to eliminate information silos, safeguard core framework velocity, protect developer context windows, and cleanly orchestrate cross-repository releases. This document defines our formalized project management strategy, repository boundaries, issue schemas, and roadmap structures.

---

## 2. Structural Repository Architecture

To maintain clear separation of concerns, optimize CI/CD pipelines, and prevent code bloat, the OHS Foundation rejects the single-monorepo approach. Instead, we enforce a **Decoupled Multi-Repository Layout** unified by centralized coordination hubs.

```
                    ┌──────────────────────────────┐
                    │     ohs-foundation/.github   │  ◄─── Org-Wide Global Default Settings
                    └──────────────┬───────────────┘
                                   │
         ┌─────────────────────────┴─────────────────────────┐
         ▼                                                   ▼
┌─────────────────────────────────┐                 ┌─────────────────────────────────┐
│     OHS Player Layer            │                 │     Core Libraries Layer        │
├─────────────────────────────────┤                 ├─────────────────────────────────┤
│ • ohs-player (Epic / Spec Hub)  │                 │ • kotlin-fhir                   │
│ • ohs-player-ref-client-app     │                 │ • fhir-info-gateway             │
│ • ohs-player-ref-backend        │                 │ • fhir-data-pipes               │
│ • ohs-player-ref-infrastructure │                 │                                 │
└─────────────────────────────────┘                 └─────────────────────────────────┘
         ▲                                                   ▲
         │                                                   │
┌─────────────────────────────────┐                 ┌─────────────────────────────────┐
│ GitHub Project 1: Release Train │                 │ GitHub Project 2: Core Engine   │
└─────────────────────────────────┘                 └─────────────────────────────────┘
```

### The OHS Player Stack Layout
* **`ohs-player`:** The central administrative repository. It contains **no execution code**. It is exclusively used for tracking cross-repository Features (Epics), architectural specs, user stories, and global documentation.
* **`ohs-player-reference-client-app`:** The codebase for the Kotlin Multiplatform (KMP) runtime container executing app configurations.
* **`ohs-player-reference-backend`:** The web administration framework exposing core configuration APIs.
* **`ohs-player-reference-infrastructure`:** The orchestration layer containing Docker Compose bundles, deployment scripts, and provisioning logic.

### The Core Libraries Layer
* Maintained in external repositories (e.g., `kotlin-fhir`, `fhir-info-gateway`). These follow an independent versioning, deployment, and testing lifecycle.

---

## 3. GitHub Projects Configuration

We maintain two isolated GitHub Project Spaces (Beta/V2) to match the distinct engineering velocities of our contributor segments.

### Project 1: OHS Player Release Train
* **Scope:** Aggregates issues from `ohs-player`, `ohs-player-reference-client-app`, `-backend`, and `-infrastructure`.
* **Primary View:** **Roadmap (Timeline Layout)**, filtered strictly via `repo:ohs-foundation/ohs-player label:"type: feature"`. This isolates high-level milestones from tactical task clutter.
* **Execution View:** **Board Layout**, grouped vertically by a custom single-select metadata field titled `Release Milestone` (e.g., `v1.0.0-Alpha`, `v1.1.0-Beta`). This offers visual clarity on how frontend, backend, and infrastructure tasks sync toward target shipments.

### Project 2: Core Libraries Engine
* **Scope:** Aggregates issues from foundational libraries like `kotlin-fhir` and `fhir-info-gateway`.
* **Primary View:** **Kanban Board Layout** using custom technical state columns:
  `Backlog` ➔ `Triage / Spec Verification` ➔ `Ready for Dev` ➔ `In Progress` ➔ `Review & API Stability Validation` ➔ `Done`
* **Custom Field Metric:** `Component Impact` (Single-Select) with values: `Engine Core`, `Structured Data / Mapping`, `Sync / Network`, `Multiplatform (KMP)`.

---

## 4. OHS Player Layer: Detailed Issue & Workflow Setup

The Player layer utilizes a strict Parent-Child relationship pattern. Features (Epics) are decomposed into fine-grained Tasks (Sub-tasks) to support explicit task delegation.

### 4.1 Feature (Epic) Layout Format
Features are initialized *exclusively* inside the root `ohs-player` repository using the `type: feature` label. They anchor user requirements and explicitly list technical steps across repositories via Markdown task lists.

```markdown
---
name: "🚀 Feature (Epic)"
description: Define a high-level feature that spans multiple sub-tasks or repositories.
title: "Feature: [Short, Descriptive Title]"
labels: ["type: feature", "status: backlog"]
---

## 🎯 User Story / Objective
**As a** [user/role],
**I want to** [action/capability],
**So that** [benefit/value].

---

## 📋 High-Level Acceptance Criteria
- [ ] Criterion 1 (e.g., "User can see real-time updates without refreshing")
- [ ] Criterion 2 (e.g., "Data adheres to FHIR profiling specifications")

---

## 🛠️ Cross-Repository Task List
*Track execution across the ohs-player stack by linking sub-tasks below using the `org/repo#issue` syntax.*

### Client UI / Frontend (`ohs-player-reference-client-app`)
- [ ] #<!-- Link local repository task issue here -->

### Backend Services (`ohs-player-reference-backend`)
- [ ] ohs-foundation/ohs-player-reference-backend#<!-- Link backend task issue here -->

### Infrastructure & Deployment (`ohs-player-reference-infrastructure`)
- [ ] ohs-foundation/ohs-player-reference-infrastructure#<!-- Link infra task issue here -->

---

## 🎨 Design / UX Architecture Notes
*(Optional) Add links to Figma, architectural diagrams, or state-machine flows here.*
```

### 4.2 Tactical Task Layout Format
Tasks are created directly inside their execution codebases (`-client-app`, `-backend`, `-infrastructure`) using the `type: task` label. They are explicitly scoped to prevent context drift.

```markdown
---
name: "🛠️ Execution Task"
description: A tightly scoped, isolated technical task.
title: "Task: [Component] - [Action]"
labels: ["type: task", "status: ready-for-dev"]
---

## 📍 Context
- **Parent Feature:** ohs-foundation/ohs-player#<!-- Link back to the main Feature epic issue here -->
- **Target Component:** [e.g., KMP UI Screen, DB Migration, Proxy Handler]

---

## 💻 Technical Requirements
*Developer Note: Adhere strictly to the scope boundaries detailed below.*

### Reference Files / Context Scope
- `path/to/target/file.kt`
- `path/to/related/interface.kt`

### Specific Instructions
1. [ ] Implement the following interface logic...
2. [ ] Ensure errors are caught and logged via the standard logger framework.
3. [ ] Avoid changing public API signatures unless explicitly required.

---

## ✅ Definition of Done (DoD)
- [ ] Code compiles without errors or warnings.
- [ ] Unit tests cover edge cases for this change.
- [ ] No regression introduced to existing components.
```

---

## 5. Core Libraries Layer: Detailed Issue Setup

Core library issues avoid end-user terminology, focusing instead on specification guidelines, benchmarking constraints, platform abstraction boundaries, and deterministic acceptance definitions.

### Core Technical Task Format
```markdown
---
name: "🧬 Core Framework Task"
description: Foundational engineering component modification anchored in specification metrics.
title: "Core Engine: [Layer] - [Technical Scope]"
labels: ["type: core-engineering", "status: triage"]
---

## 📋 Technical Objective
Provide a concise explanation of the optimization, bug resolution, or specification compliance update required within the shared framework layer.

## 📑 Specification Context & References
- **Target Submodule:** [e.g., `:engine-core:shared`, `:fhir-structures`]
- **HL7 FHIR Specification Link:** [e.g., https://hl7.org/fhir/R4/auditargument.html]
- **Target Standards:** [e.g., FHIR SDK v2.0 KMP compliance requirements]

## 🛠️ Implementation Constraints
- Must remain strictly independent of Android platform JVM packages to guarantee uncompromised iOS native compilation capability.
- Memory consumption allocations must not exceed defined boundary tolerances during parsing executions of large-scale bundles.

## ✅ Acceptance Criteria
- [ ] Implement architecture modifications conforming to the specified HL7 guidelines.
- [ ] Execute localized cross-platform unit validations simulating high concurrency loads.
- [ ] Verify that public API binary signatures remain stable or register intentional changes with deprecation annotations.
```

---

## 6. Upstream Boundary Intersections: Shadow Tracking Pattern

Because the OHS Player's config-driven execution engine depends heavily on foundational updates in the `kotlin-fhir` repository (such as KMP engine stabilization), we manage these inter-team intersections via the **Shadow Tracking Pattern**.

### Rule Framework
1. **Do Not Pull External Tickets Directly Into Player Tasks:** Avoid importing raw, unresolved core library tracking cards into everyday Player feature lists. This isolates player developers from upstream engineering noise.
2. **Instantiate a Local Shadow Issue:** Create an issue inside the `ohs-player` repo labeled `type: dependency` to represent the core blocker.
3. **Explicit Cross-Referencing:** Use markdown links inside the shadow issue to point out the actual external library ticket.

### Shadow Tracking Blueprint
```markdown
---
title: "🔗 [Upstream Dependency] Kotlin-FHIR SDK v2.0 KMP Engine Baseline"
labels: ["type: dependency", "status: blocked"]
---

## 📍 Upstream Context
This issue tracks the foundational readiness of the Kotlin Multiplatform (KMP) engine from the core library team. We cannot implement local configuration parsing until this is stable.

* **Upstream Target:** ohs-foundation/kotlin-fhir#124 <!-- External Reference -->
* **Expected Delivery:** Q2 2026

## 🛑 Blocked Player Epics
The following local player features are blocked by this tracking issue:
- [ ] ohs-foundation/ohs-player#42 <!-- Link to local Feature Epic -->
```

---

## 7. Delivery Lifecycles & Release Horizons

### OHS Player Toolkit Horizons
The Player toolkit lifecycle coordinates multi-repo releases using high-level thematic horizons focused on sandbox access, framework maturity, and cloud templates.



*   **Horizon 1: Milestone v1.0.0-Alpha ("The Sandbox")**
    * *Focus:* Deliver single-command local sandbox environments.
    * *Client App:* Hardcoded configuration parsing from local asset roots.
    * *Backend/Gateway:* Baseline Info Gateway proxies configured without multi-tenant authentication patterns.
    * *Infrastructure:* Unified local Docker Compose scripts linking core services.
*   **Horizon 2: Milestone v1.1.0-Beta ("Interoperable Validation")**
    * *Focus:* Introduce dynamic form rendering engines and visibility controls.
    * *Client App:* Integrated dynamic KMP form rendering parsing direct from loaded FHIR Questionnaire resources.
    * *Backend/Gateway:* Operationalized audit trails tracking proxy flows via FHIR `AuditEvent` resource processing.
    * *Infrastructure:* Auto-populating data seeds injecting synthetic clinical configurations upon initialization workflows.
*   **Horizon 3: Milestone v1.2.0-GA ("Production Blueprints")**
    * *Focus:* Scalable cloud architecture validation and analytics data extraction pipelines.
    * *Client App:* Full orchestration executing applications entirely from remote configurations.
    * *Backend/Gateway:* Data pipeline integrations streaming resources to an analytical SQL data warehouse.
    * *Infrastructure:* Formalized deployment profiles tailored for target cloud providers (e.g., AWS/GCP execution templates).

---

### Core Libraries Release Lifecycle
The core library framework operates independently of application-level timelines, shipping releases along strict engineering gates.



*   **Stage 1: Multiplatform Target Parity (Alpha Target)**
    * Complete extraction of legacy Android JVM dependencies out from internal storage models.
    * Implement native database target processing engines across iOS platforms.
*   **Stage 2: Specification Alignment Validation (Beta Target)**
    * Update definitions to guarantee parsing compatibility against emerging HL7 profiles.
    * Complete benchmark passes optimizing parsing performance constraints on resource bundles.
*   **Stage 3: API Freeze & GA Publication (GA Target)**
    * Seal public API structures and apply strict semantic versioning constraints.
    * Push stable artifacts to standard deployment networks for downstream consumer integration.
