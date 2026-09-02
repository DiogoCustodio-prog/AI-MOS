---
document:
  id: AI-MOS-FND-0005
  title: AI-MOS Directory Structure
  type: Foundation Specification
  status: In Review
  version:
    epoch: E001
    semantic: 0.1.0
    full: E001-v0.1.0

ownership:
  organization: Inovador Tech
  owner: AI-MOS Architecture

architecture:
  layer: Foundation
  module: Repository Structure

lifecycle:
  state: active
  maturity: foundation
  review_required: true

metadata:
  created: 2026-08-11
  updated: 2026-08-11
  language: en-US
  tags:
    - ai-mos
    - foundation
    - directory-structure
    - repository
    - architecture
    - isolation

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ./00_METADATA_STANDARD.md
    - ./01_DOCUMENT_TEMPLATE.md
    - ./02_NAMING_CONVENTIONS.md
  related_documents: []

compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.2.0 <2.0.0"

ai:
  source_of_truth: true
  authority_scope: directory-structure
  claude_code_compatible: true
  github_compatible: true
  obsidian_compatible: true
  rag_ready: true

security:
  classification: internal
  confidentiality: standard

audit:
  created_by: AI-MOS Architecture
  updated_by: AI-MOS Architecture
  last_review: 2026-08-11
  review_cycle: annual
---

# AI-MOS Directory Structure

## 1. Document Status and Authority

This document defines the governed repository areas, their responsibilities, dependency direction, and rules for placing canonical and auxiliary material in AI-MOS.

Its current editorial status is **In Review**. It is the canonical candidate for the `directory-structure` authority scope and becomes the approved directory authority only after architectural review and explicit approval.

The [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) remains authoritative for system identity, architectural boundaries, permanent principles, and the primary repository areas. The [AI-MOS Metadata Standard](00_METADATA_STANDARD.md) remains authoritative for canonical document metadata and relationships. The [AI-MOS Naming Conventions](02_NAMING_CONVENTIONS.md) remains authoritative for names, IDs, filenames, and naming-layer separation. This document specializes those contracts for placement and repository organization.

The actual workspace state is the source of truth for what currently exists. A structure shown as planned or future in this document MUST NOT be interpreted as an existing directory, tool, validator, or runtime capability.

## 2. Purpose

A governed directory structure makes AI-MOS:

- architecturally legible;
- safe for Core, Bootstrap, and Client isolation;
- predictable for human and AI navigation;
- compatible with relative Markdown relationships;
- suitable for future Git review and retrieval indexing;
- explicit about the boundary between canonical documents, source material, and local session memory.

Directories provide placement and navigation. They do not replace document metadata, authority scope, or human review.

## 3. Scope

This specification applies to the current AI-MOS documentation workspace and to future canonical repository structures derived from it.

It governs:

- canonical top-level areas;
- auxiliary non-canonical areas;
- responsibility boundaries;
- dependency direction;
- creation of new areas;
- placement of canonical Markdown documents;
- isolation of Core, Bootstrap, Client, and Knowledge content;
- relative path interpretation.

It does not define:

- a build system;
- a package manager;
- a test runner;
- a metadata validator;
- a Git workflow that is not currently implemented;
- a complete future tree for agents, skills, prompts, integrations, or runtime automation.

Those capabilities require their own approved specifications and actual implementation.

## 4. Current Workspace Structure

The current workspace contains the following principal areas:

```text
AI-MOS/
├── CLAUDE.md
├── SYSTEM/
│   ├── README.md
│   └── SYSTEM_MANIFEST.md
├── FOUNDATION/
│   ├── README.md
│   ├── 00_METADATA_STANDARD.md
│   ├── 01_DOCUMENT_TEMPLATE.md
│   ├── 02_NAMING_CONVENTIONS.md
│   ├── 03_DIRECTORY_STRUCTURE.md
│   ├── 04_DOCUMENTATION_PRINCIPLES.md
│   └── 05_GOVERNANCE_APPROVAL_PROCESS.md
├── CORE/
│   └── README.md
├── BOOTSTRAP/
│   └── README.md
├── CLIENTS/
│   └── README.md
├── KNOWLEDGE/
│   └── README.md
├── source-material/
│   ├── README.md
│   └── chatgpt-exports/
└── memory/
    ├── MEMORY.md
    └── user-language-preference.md
```

This tree documents the workspace at the time of this specification. Files may be added through governed work without implying that every possible future artifact class has been created.

The root `CLAUDE.md` is operational guidance for Claude Code. It is not a substitute for the future canonical Core documentation set.

## 5. Canonical Repository Areas

### 5.1 `SYSTEM/`

`SYSTEM/` owns system identity, constitutional scope, macro-architecture, permanent principles, and system-level governance.

Current canonical candidate:

```text
SYSTEM/SYSTEM_MANIFEST.md
```

A document in `SYSTEM/` MUST have `architecture.layer: System` and MUST remain independent of lower-level implementation details. It MUST NOT become a container for detailed Foundation, Core, Bootstrap, or Client rules that belong to their specialized Sources of Truth.

### 5.2 `FOUNDATION/`

`FOUNDATION/` owns cross-cutting documentation contracts consumed by the other governed areas.

The intended construction sequence is:

```text
FOUNDATION/00_METADATA_STANDARD.md
FOUNDATION/01_DOCUMENT_TEMPLATE.md
FOUNDATION/02_NAMING_CONVENTIONS.md
FOUNDATION/03_DIRECTORY_STRUCTURE.md
FOUNDATION/04_DOCUMENTATION_PRINCIPLES.md
FOUNDATION/05_GOVERNANCE_APPROVAL_PROCESS.md
```

A document in `FOUNDATION/` MUST have `architecture.layer: Foundation`. Foundation documents define reusable contracts; they MUST NOT contain client-specific business facts.

### 5.3 `CORE/`

`CORE/` owns reusable AI-MOS intellectual property and product specifications that are independent of a particular client.

It may eventually contain approved architecture specifications, operating models, reusable agent patterns, skills, workflows, integration contracts, and generalized knowledge. The current workspace contains only a scope README; no future artifact class should be assumed to exist until created and governed.

A document in `CORE/` MUST have `architecture.layer: Core` and MUST NOT contain private client facts, secrets, unapproved client campaigns, or ungeneralized experiments.

### 5.4 `BOOTSTRAP/`

`BOOTSTRAP/` owns initialization and deployment assets used to create an implementation without modifying Core.

It may eventually contain repository initialization procedures, templates, onboarding, checklists, configuration boundaries, and validation procedures. The current workspace contains only a scope README.

A document in `BOOTSTRAP/` MUST have `architecture.layer: Bootstrap` and MUST reference the Core and Foundation contracts it consumes.

### 5.5 `CLIENTS/`

`CLIENTS/` is the boundary for isolated Client Implementations.

A Client Implementation may contain organization-specific context, branding, personas, products, campaigns, workflows, integrations, metrics, operational memory, client-specific agents, and experiments. Each client MUST remain isolated from other clients and from reusable Core content.

A document in a Client Implementation MUST have `architecture.layer: Client` and MUST identify the applicable client scope through governed metadata or an approved extension. Client facts MUST NOT be copied into Core merely because they may be useful as examples.

The current workspace contains only a scope README. No client implementation is implied by the existence of this directory.

### 5.6 `KNOWLEDGE/`

`KNOWLEDGE/` owns governed records of decisions, evidence, lessons, experiments, patterns, anti-patterns, metrics, feedback, and evolution history.

Knowledge records may inform changes to any architectural layer, but they do not silently modify a Source of Truth. A record may propose extraction into Core, Bootstrap, or Foundation; the extraction requires explicit review and approval.

A document in `KNOWLEDGE/` MUST have `architecture.layer: Knowledge` and SHOULD identify its origin, conclusion, affected artifacts, and review state.

## 6. Auxiliary Areas

### 6.1 `source-material/`

`source-material/` contains historical exports and reference material used as input for architectural work. It is non-normative and is not an AI-MOS product layer.

Its current preserved export location is:

```text
source-material/chatgpt-exports/
```

Files in this area may contain repeated drafts, proposals, revised decisions, transcript commentary, aspirational trees, or examples of commands and integrations. They MUST NOT be treated as canonical merely because they are detailed or have metadata-like text.

Historical material MUST remain preserved without ordinary editing or cleanup. A validated idea is promoted by creating or updating a canonical document in the appropriate governed area, not by rewriting the historical export.

### 6.2 `memory/`

`memory/` contains local Claude session memory. It is not AI-MOS canonical knowledge, not a product layer, and not a Source of Truth for repository architecture.

Memory files MUST NOT be used as substitutes for canonical decisions, specifications, or client knowledge. Durable AI-MOS knowledge belongs in an appropriate governed document after review.

### 6.3 Root operational files

Root operational files such as `CLAUDE.md` may guide tooling behavior without becoming canonical AI-MOS specifications. If a root file later claims authority over an AI-MOS concept, it MUST be reconciled with the canonical area and Metadata Standard.

## 7. Dependency Direction

The intended architectural dependency direction is:

```text
SYSTEM
  ↓
FOUNDATION
  ↓
CORE
  ↓
BOOTSTRAP
  ↓
CLIENTS
```

`KNOWLEDGE/` is cross-cutting. It records evidence and evolution across the system but does not become a lower-level implementation dependency merely by documenting an observation.

The rules are:

1. `SYSTEM/` defines system-level authority and must not depend on lower layers.
2. `FOUNDATION/` consumes system authority and defines contracts consumed downstream.
3. `CORE/` consumes System and Foundation contracts and remains client-independent.
4. `BOOTSTRAP/` consumes approved Foundation and Core assets to initialize implementations.
5. `CLIENTS/` consumes approved Foundation, Core, and Bootstrap assets and remains isolated by client.
6. `KNOWLEDGE/` may reference any layer as evidence, but a knowledge record does not silently become an authority.
7. Lower layers MUST NOT redefine a concept owned by an approved higher or specialized Source of Truth.
8. A dependency relationship MUST be represented in `relations.depends_on` when the dependency is required to interpret or implement the document.

A lower layer may be referenced from a higher layer as evidence or a future proposal only when the relationship is semantically justified and does not create an architectural dependency cycle.

## 8. Placement and Metadata Consistency

A canonical document's directory and metadata MUST tell a consistent story.

At minimum:

- a file in `SYSTEM/` declares `architecture.layer: System`;
- a file in `FOUNDATION/` declares `architecture.layer: Foundation`;
- a file in `CORE/` declares `architecture.layer: Core`;
- a file in `BOOTSTRAP/` declares `architecture.layer: Bootstrap`;
- a file in `CLIENTS/` declares `architecture.layer: Client`;
- a file in `KNOWLEDGE/` declares `architecture.layer: Knowledge`.

A path mismatch is a review finding, not an invitation to infer which value is correct. The author MUST reconcile the conflict with the applicable Source of Truth before promotion.

A directory MUST NOT be used to infer:

- document approval status;
- operational lifecycle;
- authority scope;
- version;
- language;
- security classification;
- whether an integration or validator exists.

Those properties belong in governed metadata and approved document content.

## 9. File and Path Rules

Canonical path and filename rules are defined by [AI-MOS Naming Conventions](02_NAMING_CONVENTIONS.md). The principal placement rules are:

- canonical Markdown documents belong in the governed area that owns their architectural responsibility;
- internal relationships use relative Markdown paths resolved from the current file's directory;
- a file move MUST preserve `document.id` when the conceptual document remains the same;
- a file move MUST update affected relationship paths;
- a file move MUST NOT silently change authority, layer, or client boundary;
- paths MUST NOT contain secrets, credentials, or ungoverned sensitive personal information;
- temporary, generated, or tool-specific files MUST not be presented as canonical without governance.

Example:

```yaml
relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ./00_METADATA_STANDARD.md
```

These values identify paths, not logical IDs. The corresponding document IDs must be read from the target documents' front matter.

## 10. Core, Bootstrap, and Client Isolation

The directory structure enforces product boundaries:

```text
CORE/       reusable, customer-independent intellectual property
BOOTSTRAP/  initialization and deployment assets
CLIENTS/    isolated organization-specific implementations
```

Rules:

1. Core MUST NOT depend on a specific Client Implementation.
2. Bootstrap MAY consume Core and Foundation assets but MUST NOT modify their Source of Truth.
3. A Client Implementation MAY specialize approved Core and Bootstrap patterns within its own boundary.
4. One client MUST NOT read another client's private operational material as though it were reusable Core knowledge.
5. Client-specific credentials, integrations, metrics, campaigns, and facts MUST remain within the applicable client boundary.
6. Client results that may be generalized MUST first be recorded as evidence and then reviewed for extraction; direct copying is prohibited.
7. A client directory does not make its contents private automatically; access control remains an external operational concern.

## 11. Creating New Directories

A new top-level or nested directory MUST NOT be created solely because a historical export, tool example, or aspirational tree mentions it.

Before creating a new governed directory, the author MUST:

1. state the responsibility and architectural owner;
2. determine whether an existing area already owns the concept;
3. verify that the new area does not duplicate or split an existing Source of Truth without a decision;
4. define its dependency direction and client-isolation behavior;
5. define naming and placement rules;
6. identify the document types it may contain;
7. identify the metadata and validation implications;
8. create or update the applicable governing specification;
9. record the decision when it changes the architecture;
10. create the directory only when the repository work actually requires it.

A new directory SHOULD begin with a scope README or governing document only when that artifact provides real navigation value. Empty future directories MUST NOT be represented as implemented capabilities.

A nested directory MUST have a single primary responsibility and MUST remain subordinate to its owning top-level area. A nested directory that requires independent authority may need its own specification and explicit metadata scope.

## 12. Planned and Unimplemented Structures

Historical material may mention directories such as agents, skills, workflows, prompts, memory, branding, marketing, integrations, or automation. Those names are proposals unless the corresponding area exists in the current workspace and has an approved responsibility.

The following are not currently established by this workspace as implemented product directories:

- `agents/`;
- `skills/`;
- `workflows/`;
- `prompts/`;
- `templates/`;
- `integrations/`;
- `automation/`;
- any vendor-specific or runtime directory.

Future directories MAY be created when their ownership, scope, naming, dependencies, isolation, and validation requirements are documented. This document does not create them by mentioning them.

## 13. Compatibility Guidance

### 13.1 Claude Code

The structure gives Claude Code stable areas for reading and editing, but Claude Code MUST verify actual paths before acting. It MUST NOT invent a file because a path appears in a proposal or historical export.

### 13.2 Git and GitHub

The current workspace is a Git repository with a `main` branch, an initial commit, and a configured `origin` remote. The structure supports version control through small, reviewable areas, stable paths, explicit relationships, and clear ownership. The existence of Git does not imply that branch protection, pull requests, hooks, CI, build, lint, test runner, or automated metadata validation is currently configured.

### 13.3 Obsidian

Uppercase governed areas and relative Markdown paths provide predictable navigation. Obsidian is a navigation interface, not an authority over placement or document meaning.

### 13.4 RAG

Top-level architectural areas, explicit metadata, relative relationships, and client boundaries provide useful retrieval filters. A future indexer MUST preserve area and metadata distinctions, especially between canonical documents, source material, local memory, Core, and Client content.

`rag_ready: true` declares structural suitability; it does not mean that a vector database, embedding process, graph, or retrieval pipeline exists.

## 14. Valid and Invalid Placement Examples

### 14.1 Valid examples

```text
SYSTEM/SYSTEM_MANIFEST.md
FOUNDATION/00_METADATA_STANDARD.md
FOUNDATION/03_DIRECTORY_STRUCTURE.md
CORE/PROJECT_SPECIFICATION.md
BOOTSTRAP/README.md
CLIENTS/<client-implementation>/
KNOWLEDGE/<knowledge-record>.md
source-material/chatgpt-exports/<preserved-export>.md
memory/<claude-session-memory>.md
```

The angle-bracketed names are illustrative placeholders for path patterns, not current files or capabilities.

### 14.2 Invalid or discouraged examples

```text
CORE/client-campaign.md                    # client-specific content in Core
FOUNDATION/client-api-key.md               # secret or client data in Foundation
CLIENTS/shared-core-standard.md            # reusable Core authority in a client area
SYSTEM/FOUNDATION_RULES.md                 # lower-layer detail placed in System
CORE/../CLIENTS/other-client/              # path traversal and client-boundary violation
future/agents/                             # ungoverned future structure
```

These examples describe violations or proposals. They do not assert that the paths currently exist.

## 15. Exceptions and Governance

An exception to the directory structure MAY be granted for historical preservation, external tooling, migration, legal or client boundary requirements, or a documented architectural experiment.

An exception MUST:

- identify the path and owning responsibility;
- state whether the path is canonical, auxiliary, generated, or temporary;
- describe dependency and isolation effects;
- preserve document identity and relative-link correctness where possible;
- be recorded in a decision or approved governance change;
- define whether it is temporary, permanent, or migration-only.

The preservation of `source-material/` and `memory/` is an existing boundary exception: those areas are intentionally outside the canonical product layers and MUST NOT be normalized into them without explicit decisions.

When the path, metadata, and governing documents conflict, the issue MUST be escalated rather than silently resolved by moving files or editing metadata.

## 16. Manual Review Checklist

Before creating, moving, or promoting a directory or document, confirm:

- [ ] The owning architectural area is identified.
- [ ] The path belongs to an approved or explicitly proposed responsibility.
- [ ] The document's `architecture.layer` matches its governed area.
- [ ] The filename follows the Naming Conventions.
- [ ] The document has a stable unique ID independent of its path.
- [ ] Required front matter and relative relationships are present.
- [ ] Every declared internal path resolves from the current document's directory.
- [ ] The move or creation does not introduce a dependency cycle.
- [ ] Core remains client-independent.
- [ ] Bootstrap consumes rather than silently changes Core.
- [ ] Client content remains isolated from Core and other clients.
- [ ] Knowledge records evidence without silently modifying authority.
- [ ] Historical exports remain preserved and unedited.
- [ ] Local Claude memory remains separate from canonical knowledge.
- [ ] No secret, credential, or ungoverned sensitive data appears in a path or document.
- [ ] A future or aspirational directory has not been represented as an existing capability.
- [ ] Any exception has a documented reason and approval path.

The repository currently has no automated directory, relationship, or architecture validator. This checklist is a manual review aid and does not constitute an automated pass.

## 17. Normative Summary

AI-MOS directory structure MUST preserve the following principles:

1. Top-level areas represent distinct architectural responsibilities.
2. `SYSTEM/`, `FOUNDATION/`, `CORE/`, `BOOTSTRAP/`, `CLIENTS/`, and `KNOWLEDGE/` are the current canonical areas.
3. `source-material/` is preserved non-normative source material.
4. `memory/` is local Claude session memory, not canonical AI-MOS knowledge.
5. Directory placement must agree with canonical metadata.
6. Dependencies follow `SYSTEM → FOUNDATION → CORE → BOOTSTRAP → CLIENTS`.
7. Knowledge may inform change but does not silently change authority.
8. Core, Bootstrap, and Client boundaries must remain isolated.
9. A path is not a document identity; `document.id` remains stable across identity-preserving moves.
10. New directories require ownership, scope, naming, dependency, isolation, and governance analysis.
11. Historical and future structures must not be confused with implemented capabilities.
12. Relative paths must remain valid after every move or rename.

This document defines the current E001 directory structure. It remains a review candidate until explicit architectural approval is recorded.

## 18. Directory Structure Status

```text
Document: AI-MOS Directory Structure
Document ID: AI-MOS-FND-0005
Architecture Epoch: E001
Current Version: E001-v0.1.0
Status: In Review
Authority Scope: directory-structure
Official Documentation Language: en-US
Owner: AI-MOS Architecture
```
