---
document:
  id: AI-MOS-FND-0002
  title: AI-MOS Metadata Standard
  type: Foundation Specification
  status: Approved
  version:
    epoch: E001
    semantic: 0.2.0
    full: E001-v0.2.0

ownership:
  organization: Inovador Tech
  owner: AI-MOS Architecture

architecture:
  layer: Foundation
  module: Metadata Governance

lifecycle:
  state: active
  maturity: foundation
  review_required: true

metadata:
  created: 2026-08-07
  updated: 2026-08-07
  language: en-US
  tags:
    - ai-mos
    - foundation
    - metadata
    - yaml
    - governance
    - source-of-truth
    - schema
    - validation

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
  related_documents:
    - ./01_DOCUMENT_TEMPLATE.md
    - ./02_NAMING_CONVENTIONS.md
    - ./03_DIRECTORY_STRUCTURE.md
    - ./04_DOCUMENTATION_PRINCIPLES.md

compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.2.0 <2.0.0"

ai:
  source_of_truth: true
  authority_scope: metadata-standard
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
  last_review: 2026-08-07
  review_cycle: annual
---

# AI-MOS Metadata Standard

## 1. Purpose

This document defines the canonical metadata contract for all Markdown documents maintained within the AI Marketing Operating System (AI-MOS).

It establishes the required structure for:

- YAML Front Matter;
- document identity;
- versioning;
- ownership;
- architectural placement;
- lifecycle state;
- descriptive metadata;
- inter-document relations;
- compatibility declarations;
- machine-oriented AI metadata;
- security classification;
- auditability;
- validation rules.

This document is normative.

The terms **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are to be interpreted as normative requirements when used in this standard.

---

## 2. Scope

This standard applies to all canonical Markdown documents inside the AI-MOS repository, including:

- system governance documents;
- foundation specifications;
- core specifications;
- bootstrap specifications;
- client implementation documents;
- architectural decisions;
- operational standards;
- templates;
- roadmaps;
- knowledge documents;
- workflow documents;
- agent specifications.

This standard does not govern binary assets, compiled artifacts, transient runtime files, or external systems unless those systems explicitly consume AI-MOS metadata.

---

## 3. Canonical Metadata Principle

Every canonical AI-MOS Markdown document MUST begin with YAML Front Matter.

No content may appear before the opening delimiter.

The canonical structure is:

```yaml
---
<metadata>
---
```

The front matter is the authoritative machine-readable contract for the document.

The body of the document MUST not contradict the approved front matter.

---

## 4. Metadata Domains

The canonical top-level metadata domains are:

- `document`
- `ownership`
- `architecture`
- `lifecycle`
- `metadata`
- `relations`
- `compatibility`
- `ai`
- `security`
- `audit`

A document MUST NOT introduce a new top-level canonical metadata domain without an approved schema revision.

Client-specific or extension-specific metadata MUST be namespaced to avoid collisions with canonical AI-MOS fields.

---

## 5. Required Domains

The following domains are REQUIRED for canonical AI-MOS documents:

- `document`
- `ownership`
- `architecture`
- `lifecycle`
- `metadata`
- `relations`
- `ai`

The following domains are REQUIRED for enterprise-ready documents unless explicitly exempted by governance:

- `compatibility`
- `security`
- `audit`

---

## 6. Document Domain

The `document` domain identifies the document as an object in the AI-MOS ecosystem.

Canonical structure:

```yaml
document:
  id:
  title:
  type:
  status:
  version:
    epoch:
    semantic:
    full:
```

### 6.1 `document.id`

Type: string  
Required: YES

`document.id` is the immutable canonical identifier of the document.

Requirements:

- MUST be unique across the AI-MOS ecosystem;
- MUST remain stable for the entire lifetime of the document;
- MUST NOT depend on filename, title, or directory position;
- MUST NOT contain spaces;
- MUST NOT contain accents;
- MUST NOT be reused after retirement;
- MUST be machine-parseable;
- SHOULD encode the functional domain.

Recommended pattern:

```text
AI-MOS-<DOMAIN>-<SEQUENCE>
```

The domain code MUST be controlled by governance.

The sequence SHOULD be zero-padded.

Example:

```text
AI-MOS-FND-0002
```

---

### 6.2 `document.title`

Type: string  
Required: YES

`document.title` is the canonical human-readable title of the document.

The title SHOULD reflect the semantic purpose of the file.

The title MUST remain consistent with the document body and filename naming convention, but the metadata value is authoritative.

---

### 6.3 `document.type`

Type: string  
Required: YES

`document.type` identifies the controlled category of the document.

Controlled vocabulary:

- `System Manifest`
- `Foundation Specification`
- `Architecture Specification`
- `Project Specification`
- `Development Rule`
- `Governance Policy`
- `Reference`
- `Decision Record`
- `Implementation Specification`
- `Operational Specification`
- `Agent Specification`
- `Workflow Specification`
- `Knowledge Document`
- `Template`
- `Roadmap`

New types MUST be introduced only through governance revision.

---

### 6.4 `document.status`

Type: string  
Required: YES

`document.status` represents the editorial and approval state of the document.

Controlled vocabulary:

- `Draft`
- `Proposed`
- `In Review`
- `Approved`
- `Deprecated`
- `Superseded`
- `Archived`
- `Rejected`

Meaning:

- `Draft` = under construction;
- `Proposed` = submitted for consideration;
- `In Review` = under technical or governance review;
- `Approved` = formally accepted as valid;
- `Deprecated` = still present but not recommended for new use;
- `Superseded` = replaced by another document;
- `Archived` = preserved for historical reference;
- `Rejected` = not accepted.

`document.status` MUST be treated as the editorial approval state, not as the operational lifecycle state.

---

### 6.5 `document.version`

The `version` object implements the AI-MOS hybrid versioning model.

Canonical structure:

```yaml
version:
  epoch:
  semantic:
  full:
```

#### 6.5.1 `version.epoch`

Type: string  
Required: YES

Format:

```text
E###
```

Example:

```text
E001
```

The epoch identifies the architectural generation of AI-MOS.

An epoch change indicates structural or conceptual evolution that may affect compatibility at a platform level.

#### 6.5.2 `version.semantic`

Type: string  
Required: YES

Format:

```text
MAJOR.MINOR.PATCH
```

Semantic versioning rules:

- `MAJOR` increments for incompatible changes;
- `MINOR` increments for backward-compatible additions;
- `PATCH` increments for backward-compatible fixes or refinements.

#### 6.5.3 `version.full`

Type: string  
Required: YES

Format:

```text
E###-vMAJOR.MINOR.PATCH
```

Example:

```text
E001-v0.2.0
```

`version.full` MUST equal the exact concatenation of `epoch` and `semantic` using the canonical format above.

---

## 7. Ownership Domain

The `ownership` domain defines accountability.

Canonical structure:

```yaml
ownership:
  organization:
  owner:
```

### 7.1 `ownership.organization`

Type: string  
Required: YES

The organization responsible for the document.

Example:

```yaml
organization: Inovador Tech
```

### 7.2 `ownership.owner`

Type: string  
Required: YES

The accountable team, function, or governance role responsible for the document.

Individual personal names SHOULD be avoided unless governance requires explicit personal accountability.

Example:

```yaml
owner: AI-MOS Architecture
```

---

## 8. Architecture Domain

The `architecture` domain defines where the document sits in the AI-MOS system.

Canonical structure:

```yaml
architecture:
  layer:
  module:
```

### 8.1 `architecture.layer`

Type: string  
Required: YES

Controlled vocabulary:

- `System`
- `Foundation`
- `Core`
- `Bootstrap`
- `Client`
- `Knowledge`
- `Operations`
- `Integration`

### 8.2 `architecture.module`

Type: string  
Required: YES

`architecture.module` identifies the logical module or subdomain to which the document belongs.

The value SHOULD be specific enough to support filtering and navigation.

Example:

```yaml
architecture:
  layer: Foundation
  module: Metadata Governance
```

---

## 9. Lifecycle Domain

The `lifecycle` domain defines the operational state of the document as an authoritative asset.

Canonical structure:

```yaml
lifecycle:
  state:
  maturity:
  review_required:
```

### 9.1 `lifecycle.state`

Type: string  
Required: YES

Controlled vocabulary:

- `active`
- `inactive`
- `deprecated`
- `superseded`
- `archived`

`lifecycle.state` represents whether the document is operationally current.

This field is distinct from `document.status`.

### 9.2 `lifecycle.maturity`

Type: string  
Required: YES

Controlled vocabulary:

- `draft`
- `foundation`
- `experimental`
- `production`
- `enterprise`
- `legacy`

### 9.3 `lifecycle.review_required`

Type: boolean  
Required: YES

Indicates whether the document requires periodic formal review.

Booleans MUST be stored as native YAML booleans.

---

## 10. Metadata Domain

The `metadata` domain contains descriptive metadata.

Canonical structure:

```yaml
metadata:
  created:
  updated:
  language:
  tags:
```

### 10.1 Dates

`metadata.created` and `metadata.updated` MUST use ISO-compatible date format:

```text
YYYY-MM-DD
```

Datetime precision MAY be used only when operationally necessary.

### 10.2 `metadata.language`

Type: string  
Required: YES

`metadata.language` MUST use a valid BCP 47 language tag.

Examples:

- `en-US`
- `pt-BR`

### 10.3 `metadata.tags`

Type: array[string]  
Required: YES

Tags MUST:

- be lowercase;
- use hyphens instead of spaces;
- avoid accents;
- be semantically relevant;
- avoid duplicates;
- be stable enough for retrieval.

Example:

```yaml
tags:
  - ai-mos
  - foundation
  - metadata
```

---

## 11. Relations Domain

The `relations` domain defines document-to-document relationships.

Canonical structure:

```yaml
relations:
  depends_on:
  related_documents:
```

### 11.1 Relative Path Requirement

All internal relation values MUST be relative paths.

Absolute URLs MUST NOT be used for internal repository relations.

### 11.2 `depends_on`

`depends_on` identifies documents that are structurally necessary to interpret the current document correctly.

This relationship is normative and implies dependency.

### 11.3 `related_documents`

`related_documents` identifies documents that are semantically connected but not mandatory dependencies.

### 11.4 Circular Dependency Rule

Circular dependencies SHOULD be avoided.

If a cycle is architecturally unavoidable, it MUST be explicitly documented and approved.

---

## 12. Compatibility Domain

The `compatibility` domain declares platform and version compatibility.

Canonical structure:

```yaml
compatibility:
  ai_mos:
    epoch:
    core:
```

### 12.1 `compatibility.ai_mos.epoch`

Type: string  
Required: YES when compatibility is declared

The AI-MOS epoch against which the document is compatible.

### 12.2 `compatibility.ai_mos.core`

Type: string  
Required: YES when compatibility is declared

Version range for the AI-MOS Core.

Version ranges SHOULD use explicit comparison operators.

Examples:

- `>=0.2.0 <2.0.0`
- `>=1.0.0`
- `=1.4.2`

Ambiguous values such as `latest`, `current`, `stable`, or `1.x` MUST NOT be used in normative compatibility metadata.

---

## 13. AI Domain

The `ai` domain defines machine-oriented authority and compatibility.

Canonical structure:

```yaml
ai:
  source_of_truth:
  authority_scope:
  claude_code_compatible:
  github_compatible:
  obsidian_compatible:
  rag_ready:
```

### 13.1 `ai.source_of_truth`

Type: boolean  
Required: YES

Indicates whether the document is the authoritative source for the concepts it defines.

More than one document MUST NOT claim authority over the same canonical concept without a governance decision.

### 13.2 `ai.authority_scope`

Type: string  
Required: YES

Defines the exact conceptual scope of the document’s authority.

Example:

```yaml
authority_scope: metadata-standard
```

This field prevents the boolean `source_of_truth` from becoming semantically broad or ambiguous.

### 13.3 Compatibility Flags

All of the following MUST be booleans:

- `claude_code_compatible`
- `github_compatible`
- `obsidian_compatible`
- `rag_ready`

Meaning:

- `claude_code_compatible` = suitable for deterministic AI-assisted editing and reasoning;
- `github_compatible` = suitable for Git-based repository workflows;
- `obsidian_compatible` = suitable for graph-based document linking;
- `rag_ready` = suitable for future retrieval augmentation.

`rag_ready: true` requires explicit metadata, stable identity, and deterministic structure.

---

## 14. Security Domain

The `security` domain defines document classification.

Canonical structure:

```yaml
security:
  classification:
  confidentiality:
```

### 14.1 `security.classification`

Controlled vocabulary:

- `public`
- `internal`
- `restricted`
- `confidential`

### 14.2 `security.confidentiality`

Controlled vocabulary:

- `standard`
- `sensitive`
- `high`

This field does not itself implement access control. It is metadata for governance and future policy enforcement.

Metadata MUST NOT be used to store secrets, credentials, tokens, passwords, or private authentication material.

---

## 15. Audit Domain

The `audit` domain provides traceability.

Canonical structure:

```yaml
audit:
  created_by:
  updated_by:
  last_review:
  review_cycle:
```

### 15.1 `audit.created_by`

Identifies the role, system, or function responsible for document creation.

### 15.2 `audit.updated_by`

Identifies the role, system, or function responsible for the latest approved update.

### 15.3 `audit.last_review`

Type: date  
Format:

```text
YYYY-MM-DD
```

### 15.4 `audit.review_cycle`

Controlled vocabulary:

- `quarterly`
- `semiannual`
- `annual`
- `biennial`
- `event-driven`
- `none`

---

## 16. Canonical Metadata Baseline

Every canonical AI-MOS Markdown document SHOULD conform to the following baseline structure:

```yaml
---
document:
  id: AI-MOS-XXX-0000
  title: Document Title
  type: Foundation Specification
  status: Draft
  version:
    epoch: E001
    semantic: 0.2.0
    full: E001-v0.2.0

ownership:
  organization: Inovador Tech
  owner: AI-MOS Architecture

architecture:
  layer: Foundation
  module: Module Name

lifecycle:
  state: active
  maturity: foundation
  review_required: true

metadata:
  created: YYYY-MM-DD
  updated: YYYY-MM-DD
  language: en-US
  tags:
    - ai-mos
    - example

relations:
  depends_on: []
  related_documents: []

compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.2.0 <2.0.0"

ai:
  source_of_truth: false
  authority_scope: example-scope
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
  last_review: YYYY-MM-DD
  review_cycle: annual
---
```

This example is illustrative.

It is not a universal default for all document types.

---

## 17. YAML Type Rules

AI-MOS metadata MUST preserve native YAML types.

Correct:

```yaml
review_required: true
```

Incorrect:

```yaml
review_required: "true"
```

Correct:

```yaml
tags:
  - ai-mos
  - architecture
```

Incorrect:

```yaml
tags: "ai-mos, architecture"
```

Correct:

```yaml
depends_on: []
```

Incorrect:

```yaml
depends_on:
```

---

## 18. Empty and Placeholder Values

Empty or placeholder values MUST NOT be used to obscure missing mandatory information.

The following values MUST NOT be used as production placeholders for required fields:

- `TBD`
- `UNKNOWN`
- `N/A`

If a required value is not known, the document MUST remain in a non-production state until the value is resolved.

---

## 19. Immutability Rules

The following fields SHOULD be treated as immutable after initial assignment:

- `document.id`
- `metadata.created`
- `audit.created_by`

Changing any of these fields requires explicit governance approval.

The following fields are expected to change over time:

- `document.version`
- `document.status`
- `lifecycle.state`
- `metadata.updated`
- `audit.updated_by`
- `audit.last_review`

---

## 20. Filename Independence

The canonical document identity is independent from the filename.

A filename MAY change while `document.id` remains unchanged.

The filename is a navigation aid.

The metadata identity is the authoritative identifier.

---

## 21. Authority Precedence

When metadata conflicts with inferred information, the following order of authority applies:

1. Approved front matter metadata
2. This metadata standard
3. `SYSTEM_MANIFEST.md`
4. Document body
5. Filename
6. Directory position
7. AI inference

AI systems MUST NOT silently override authoritative metadata with inferred values.

---

## 22. Source of Truth Rules

A document declaring `ai.source_of_truth: true` assumes authoritative responsibility only within the defined `authority_scope`.

Other documents MUST reference the canonical Source of Truth instead of redefining the same concept.

If two documents claim authority over the same scope, the conflict MUST be resolved through governance before publication.

---

## 23. Validation Requirements

A compliant AI-MOS repository SHOULD support automated validation for:

- missing front matter;
- invalid YAML syntax;
- missing required fields;
- incorrect data types;
- invalid controlled vocabulary values;
- malformed document IDs;
- invalid version fields;
- inconsistent `version.full`;
- broken relative paths;
- duplicate document IDs;
- incompatible epoch declarations;
- invalid security classifications;
- invalid lifecycle/status combinations.

Validation SHOULD be available both for human review and automated pipelines.

---

## 24. Compatibility and Evolution

This standard itself is versioned.

A change is:

### PATCH
A wording correction or clarification that does not change structure or validation behavior.

### MINOR
A backward-compatible addition, such as a new optional field or controlled value.

### MAJOR
A breaking change, such as a required field removal, semantic change, or incompatible validation revision.

An Architecture Epoch change MAY supersede this standard if the AI-MOS architecture itself evolves fundamentally.

---

## 25. Backward Compatibility

Unknown optional fields SHOULD be ignored by consumers when feasible.

Unknown fields MUST NOT silently override canonical fields.

Canonical fields always take precedence over extension fields.

---

## 26. Extension Mechanism

Client-specific or future extension metadata SHOULD be namespaced.

Example:

```yaml
client:
  namespace:
    field: value
```

Extensions MUST NOT alter the meaning of canonical AI-MOS metadata fields.

---

## 27. Client Isolation

Client implementations MAY extend the metadata model, but they MUST NOT redefine canonical AI-MOS fields.

Client metadata MUST remain subordinate to core governance and must not contaminate the canonical schema.

---

## 28. Repository Language Policy

The repository MAY contain documents in multiple languages, but each document MUST declare its language explicitly through `metadata.language`.

The canonical language of a document is the language declared in its metadata.

Localized documents MUST remain structurally aligned with the canonical schema.

---

## 29. Security Boundary

Metadata MUST NOT be used to store:

- passwords;
- API keys;
- tokens;
- private credentials;
- secrets;
- session values;
- sensitive personal data unless explicitly governed.

Metadata describes the document. It is not a secret store.

---

## 30. Compliance Levels

AI-MOS defines three compliance levels:

### Level 1 — Structural
The document contains valid YAML and the required fields.

### Level 2 — Semantic
The field values are valid, consistent, and conform to controlled vocabulary.

### Level 3 — Enterprise
The document satisfies:

- structural validation;
- semantic validation;
- relationship validation;
- version validation;
- lifecycle validation;
- security classification;
- audit metadata;
- AI compatibility;
- RAG readiness where applicable.

Production Core documents SHOULD reach Level 3 compliance.

---

## 31. Formal Validation Profile

An AI-MOS validation pipeline SHOULD enforce the following:

- front matter presence;
- canonical ordering of top-level domains;
- immutable identity protection;
- semantic version consistency;
- epoch consistency;
- lifecycle/status consistency;
- path relativity checks;
- duplicate ID detection;
- controlled vocabulary enforcement;
- authority scope presence when `source_of_truth` is true.

---

## 32. Canonical Example

The following is a valid non-normative example:

```yaml
---
document:
  id: AI-MOS-CORE-0010
  title: Example Core Specification
  type: Architecture Specification
  status: Active
  version:
    epoch: E001
    semantic: 1.2.0
    full: E001-v1.2.0

ownership:
  organization: Inovador Tech
  owner: AI-MOS Architecture

architecture:
  layer: Core
  module: Intelligence Architecture

lifecycle:
  state: active
  maturity: enterprise
  review_required: true

metadata:
  created: 2026-08-07
  updated: 2026-08-07
  language: en-US
  tags:
    - ai-mos
    - core
    - architecture

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ../FOUNDATION/00_METADATA_STANDARD.md
  related_documents:
    - ../FOUNDATION/01_DOCUMENT_TEMPLATE.md

compatibility:
  ai_mos:
    epoch: E001
    core: ">=1.0.0 <2.0.0"

ai:
  source_of_truth: true
  authority_scope: example-core-specification
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
  last_review: 2026-08-07
  review_cycle: annual
---
```

---

## 33. Non-Compliance Definition

A document is non-compliant if it:

- omits required metadata;
- contains invalid YAML;
- uses invalid controlled values;
- declares inconsistent version fields;
- duplicates an existing document ID;
- uses invalid internal references;
- contradicts authoritative metadata;
- exposes secrets in metadata;
- violates lifecycle/status consistency;
- violates repository governance.

Non-compliant documents MUST NOT be promoted to enterprise production status.

---

## 34. Governance Authority

This standard governs metadata across the AI-MOS ecosystem.

Changes to required fields, field semantics, validation rules, or controlled vocabulary MUST be reviewed and versioned.

This document is subordinate only to the AI-MOS System Manifest and any future approved Architecture Epoch that explicitly supersedes it.

---

## 35. Normative Summary

Every canonical AI-MOS Markdown document MUST be:

- identifiable;
- versioned;
- owned;
- classified;
- lifecycle-aware;
- architecturally positioned;
- relationally connected;
- machine-readable;
- auditable;
- AI-compatible;
- validation-ready.

The metadata layer exists to ensure that AI-MOS remains understandable, governable, and automatable over long architectural horizons.

---

## 36. Standard Status

- Standard: AI-MOS Metadata Standard
- Document ID: AI-MOS-FND-0002
- Architecture Epoch: E001
- Current Version: E001-v0.2.0
- Status: Approved
- Authority: AI-MOS Architecture

---

## 37. Appendix A — Canonical Regex Guidance

### Document ID
Recommended pattern:

```text
^AI-MOS-[A-Z]{3}-[0-9]{4}$
```

### Epoch
Recommended pattern:

```text
^E[0-9]{3}$
```

### Semantic Version
Recommended pattern:

```text
^[0-9]+\.[0-9]+\.[0-9]+$
```

### Full Version
Recommended pattern:

```text
^E[0-9]{3}-v[0-9]+\.[0-9]+\.[0-9]+$
```

### Language Tag
Recommended pattern:

```text
^[a-z]{2}-[A-Z]{2}$
```

### Relative Path
Must be a repository-relative Markdown path and SHOULD begin with `./` or `../` when referencing peer documents.

---

## 38. Appendix B — Validation Intent

The purpose of this standard is not only human readability.

Its purpose is also to make AI-MOS:

- deterministic for Claude Code;
- stable for Git workflows;
- navigable in Obsidian;
- indexable for future RAG;
- auditable for enterprise governance;
- resilient to future architectural evolution.