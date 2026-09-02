---
document:
  id: AI-MOS-FND-0002
  title: AI-MOS Metadata Standard
  type: Foundation Specification
  status: Approved
  version:
    epoch: E001
    semantic: 0.1.0
    full: E001-v0.1.0

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
    core: ">=0.1.0 <2.0.0"

ai:
  source_of_truth: true
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

This document defines the canonical metadata contract for all Markdown documents within the AI Marketing Operating System (AI-MOS).

It establishes:

- the mandatory YAML Front Matter structure;
- the semantic meaning of each metadata field;
- field types and accepted values;
- mandatory and optional fields;
- identifier rules;
- lifecycle rules;
- versioning rules;
- document relationship rules;
- compatibility declarations;
- AI and RAG metadata requirements;
- security classification metadata;
- auditability requirements;
- validation requirements.

This document is normative.

Where this specification uses the terms **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, or **MAY**, those terms are to be interpreted as normative requirements.

---

# 2. Scope

This standard applies to every canonical Markdown document maintained inside the AI-MOS repository.

It applies to:

- AI-MOS Core documentation;
- AI-MOS Foundation documentation;
- AI-MOS Bootstrap Kit documentation;
- AI-MOS Client Implementation documentation;
- system specifications;
- architectural decisions;
- operational specifications;
- agent specifications;
- workflow specifications;
- knowledge documents;
- governance documents;
- implementation documentation.

This standard does not require every non-documentary artifact to contain YAML Front Matter.

Binary assets, generated artifacts, temporary files and external dependencies are governed separately.

---

# 3. Canonical Metadata Format

The canonical metadata format is:

```yaml
---
<metadata>
---
```

YAML Front Matter MUST appear at the beginning of the Markdown file.

No content may precede the opening `---` delimiter.

The closing `---` delimiter MUST appear before the first Markdown heading.

---

# 4. Canonical Metadata Domains

AI-MOS metadata is divided into the following domains:

```text
document
ownership
architecture
lifecycle
metadata
relations
compatibility
ai
security
audit
```

Each domain has a defined responsibility.

A document MUST NOT introduce a new top-level metadata domain without an approved change to this standard.

---

# 5. Required Domains

The following domains are REQUIRED:

```yaml
document:
ownership:
architecture:
lifecycle:
metadata:
relations:
ai:
```

The following domains are REQUIRED when applicable to the document:

```yaml
compatibility:
security:
audit:
```

For AI-MOS canonical documents, `compatibility`, `security`, and `audit` SHOULD be present by default.

---

# 6. `document` Domain

The `document` domain identifies the document itself.

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

## 6.1 `document.id`

### Type

`string`

### Required

YES

### Purpose

Provides the immutable identity of the document.

The ID identifies the document independently from its filename.

### Requirements

The ID:

- MUST be unique within the AI-MOS ecosystem;
- MUST remain stable throughout the document lifecycle;
- MUST NOT contain spaces;
- MUST NOT contain accented characters;
- MUST NOT depend on the filename;
- MUST NOT be reused after document retirement;
- MUST NOT change merely because the document title changes.

Recommended format:

```text
AI-MOS-<DOMAIN>-<SEQUENCE>
```

Example:

```text
AI-MOS-FND-0002
```

---

# 7. `document.title`

### Type

`string`

### Required

YES

### Purpose

Defines the canonical human-readable title.

The title SHOULD correspond semantically to the document filename.

Example:

```yaml
title: AI-MOS Metadata Standard
```

---

# 8. `document.type`

### Type

`string`

### Required

YES

### Purpose

Defines the semantic category of the document.

Initial controlled vocabulary:

```text
System Manifest
Foundation Specification
Architecture Specification
Project Specification
Development Rule
Governance Policy
Reference
Decision Record
Implementation Specification
Operational Specification
Agent Specification
Workflow Specification
Knowledge Document
Template
Roadmap
```

New document types SHOULD be added only through an explicit governance change.

---

# 9. `document.status`

### Type

`string`

### Required

YES

### Controlled Vocabulary

```text
Draft
Proposed
In Review
Approved
Active
Deprecated
Superseded
Archived
Rejected
```

### Rules

A document MUST have exactly one lifecycle status.

`Approved` indicates that the content has been formally accepted.

`Active` indicates that the document is currently authoritative for operational use.

`Deprecated` indicates that the document remains available but SHOULD NOT be used for new implementations.

`Superseded` indicates that another document has replaced it.

`Archived` indicates historical preservation without current authority.

---

# 10. `document.version`

The `version` object implements the AI-MOS hybrid versioning model.

```yaml
version:
  epoch: E001
  semantic: 0.1.0
  full: E001-v0.1.0
```

## 10.1 Epoch

### Type

`string`

### Format

```text
E###
```

Example:

```text
E001
```

The Epoch represents the architectural generation of AI-MOS.

An Epoch change indicates architectural evolution rather than ordinary document revision.

---

## 10.2 Semantic Version

### Type

`string`

### Format

```text
MAJOR.MINOR.PATCH
```

Example:

```text
1.4.2
```

Semantic versioning follows:

### MAJOR

Increment when compatibility is broken.

### MINOR

Increment when backward-compatible capabilities are introduced.

### PATCH

Increment for backward-compatible corrections or refinements.

---

## 10.3 Full Version

### Type

`string`

### Format

```text
E###-vMAJOR.MINOR.PATCH
```

Example:

```text
E001-v1.4.2
```

The `full` field MUST correspond exactly to:

```text
<epoch>-v<semantic>
```

Example:

```yaml
epoch: E001
semantic: 1.4.2
full: E001-v1.4.2
```

Invalid:

```yaml
epoch: E001
semantic: 1.4.2
full: E002-v1.4.2
```

---

# 11. `ownership` Domain

Defines organizational ownership.

```yaml
ownership:
  organization:
  owner:
```

## 11.1 `organization`

### Type

`string`

### Required

YES

Defines the organization responsible for the document.

For proprietary AI-MOS Core documentation:

```yaml
organization: Inovador Tech
```

---

## 11.2 `owner`

### Type

`string`

### Required

YES

Identifies the responsible team, function or accountable role.

Example:

```yaml
owner: AI-MOS Architecture
```

Individual personal names SHOULD NOT be used unless required for formal accountability.

---

# 12. `architecture` Domain

Defines the document's position in the AI-MOS architecture.

```yaml
architecture:
  layer:
  module:
```

## 12.1 `layer`

### Type

`string`

### Required

YES

Initial controlled vocabulary:

```text
System
Foundation
Core
Bootstrap
Client
Knowledge
Operations
Integration
```

---

## 12.2 `module`

### Type

`string`

### Required

YES

Defines the logical module to which the document belongs.

Example:

```yaml
architecture:
  layer: Foundation
  module: Metadata Governance
```

---

# 13. `lifecycle` Domain

Defines the operational lifecycle of the document.

```yaml
lifecycle:
  state:
  maturity:
  review_required:
```

## 13.1 `state`

### Type

`string`

### Required

YES

Controlled vocabulary:

```text
active
inactive
deprecated
superseded
archived
```

The lifecycle state MUST remain semantically consistent with `document.status`.

---

## 13.2 `maturity`

### Type

`string`

### Required

YES

Controlled vocabulary:

```text
draft
foundation
experimental
production
enterprise
legacy
```

---

## 13.3 `review_required`

### Type

`boolean`

### Required

YES

Indicates whether the document requires periodic architectural or governance review.

Example:

```yaml
review_required: true
```

---

# 14. `metadata` Domain

Contains descriptive metadata.

```yaml
metadata:
  created:
  updated:
  language:
  tags:
```

## 14.1 Dates

### Type

`date`

### Format

```text
YYYY-MM-DD
```

Example:

```yaml
created: 2026-08-07
updated: 2026-08-07
```

Datetime values SHOULD be used only when timestamp precision is required.

---

## 14.2 `language`

### Type

`string`

### Format

BCP 47 language tag.

Example:

```yaml
language: en-US
```

---

## 14.3 `tags`

### Type

`array[string]`

Tags MUST:

- use lowercase;
- use hyphens instead of spaces;
- avoid accents;
- be semantically relevant;
- avoid duplicate terms.

Example:

```yaml
tags:
  - ai-mos
  - foundation
  - metadata
```

---

# 15. `relations` Domain

Defines explicit relationships between documents.

```yaml
relations:
  depends_on:
  related_documents:
```

Both fields MUST contain relative paths.

Example:

```yaml
relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
  related_documents:
    - ./01_DOCUMENT_TEMPLATE.md
```

Absolute URLs MUST NOT be used for internal repository relationships.

---

## 15.1 Dependency Rules

`depends_on` identifies documents required to correctly interpret or implement the current document.

Dependencies MUST NOT be circular unless explicitly authorized by architecture governance.

Example of prohibited dependency cycle:

```text
A → B → C → A
```

---

## 15.2 Related Documents

`related_documents` identifies relevant documents that do not constitute mandatory dependencies.

---

# 16. Recommended Relationship Extensions

The following relationship fields MAY be used:

```yaml
relations:
  depends_on:
  related_documents:
  supersedes:
  superseded_by:
  implements:
  implemented_by:
  references:
```

When used, all values MUST be relative repository paths unless the relationship explicitly targets an external system.

---

# 17. `compatibility` Domain

Defines compatibility requirements.

Canonical structure:

```yaml
compatibility:
  ai_mos:
    epoch:
    core:
```

Example:

```yaml
compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.1.0 <2.0.0"
```

---

## 17.1 Epoch Compatibility

A document MUST declare the Epoch against which it was designed when compatibility is relevant.

Example:

```yaml
epoch: E001
```

---

## 17.2 Version Ranges

Version ranges SHOULD use explicit comparison operators.

Examples:

```text
>=1.0.0 <2.0.0
>=1.2.0
=1.4.2
```

Ambiguous declarations such as:

```text
1.x
latest
current
stable
```

MUST NOT be used in normative compatibility metadata.

---

# 18. `ai` Domain

Defines machine-oriented compatibility and semantic status.

Canonical structure:

```yaml
ai:
  source_of_truth:
  claude_code_compatible:
  github_compatible:
  obsidian_compatible:
  rag_ready:
```

All fields are boolean.

---

## 18.1 `source_of_truth`

Indicates whether the document is authoritative for the concepts it defines.

Only one canonical document SHOULD define a specific concept as Source of Truth.

---

## 18.2 `claude_code_compatible`

Indicates that the document follows the conventions required for reliable use by Claude Code.

---

## 18.3 `github_compatible`

Indicates that the document conforms to repository and Git-based documentation standards.

---

## 18.4 `obsidian_compatible`

Indicates that the document can participate safely in the Obsidian knowledge graph.

---

## 18.5 `rag_ready`

Indicates that the document satisfies the minimum structural requirements for future RAG ingestion.

RAG readiness requires:

- explicit metadata;
- stable identity;
- semantic headings;
- deterministic terminology;
- explicit relationships;
- absence of critical contextual dependencies.

---

# 19. `security` Domain

Defines document classification.

Canonical structure:

```yaml
security:
  classification:
  confidentiality:
```

## 19.1 Classification

Initial vocabulary:

```text
public
internal
restricted
confidential
```

---

## 19.2 Confidentiality

Initial vocabulary:

```text
standard
sensitive
high
```

Security classification MUST NOT be interpreted as an access-control mechanism by itself.

It is metadata for governance and future policy enforcement.

---

# 20. `audit` Domain

Provides document traceability.

Canonical structure:

```yaml
audit:
  created_by:
  updated_by:
  last_review:
  review_cycle:
```

## 20.1 `created_by`

Identifies the role, system or organizational function responsible for creation.

---

## 20.2 `updated_by`

Identifies the role, system or function responsible for the latest update.

---

## 20.3 `last_review`

Date of the most recent formal review.

Format:

```text
YYYY-MM-DD
```

---

## 20.4 `review_cycle`

Controlled vocabulary:

```text
quarterly
semiannual
annual
biennial
event-driven
none
```

---

# 21. Canonical Front Matter

The following structure is the canonical baseline for AI-MOS documents:

```yaml
---
document:
  id: AI-MOS-XXX-0000
  title: Document Title
  type: Foundation Specification
  status: Draft
  version:
    epoch: E001
    semantic: 0.1.0
    full: E001-v0.1.0

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
    core: ">=0.1.0 <2.0.0"

ai:
  source_of_truth: false
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

---

# 22. YAML Type Rules

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

Boolean values MUST be YAML booleans.

Dates MUST be ISO-compatible dates.

Lists MUST be YAML arrays.

Structured metadata MUST use YAML objects.

---

# 23. Null and Empty Values

Empty values MUST NOT be used to disguise unknown information.

Preferred:

```yaml
relations:
  depends_on: []
```

Not:

```yaml
relations:
  depends_on:
```

If a REQUIRED value is genuinely unknown, the document MUST remain in an appropriate non-production lifecycle state until the value is resolved.

Placeholder values such as:

```text
TBD
UNKNOWN
N/A
```

MUST NOT be used for mandatory production metadata.

---

# 24. Immutability Rules

The following metadata SHOULD be treated as immutable after document creation:

```text
document.id
metadata.created
audit.created_by
```

Changing any of these fields requires explicit governance approval.

The following fields are expected to change during the lifecycle:

```text
document.version
document.status
metadata.updated
lifecycle.state
audit.updated_by
audit.last_review
```

---

# 25. Filename Independence

The document ID and filename are separate identifiers.

A filename MAY change while the document ID remains unchanged.

Example:

```text
old:
00_METADATA_STANDARD.md

new:
00_METADATA_SPECIFICATION.md
```

The document identity remains:

```yaml
id: AI-MOS-FND-0002
```

This allows Git history and external references to remain stable.

---

# 26. Source of Truth Rules

A document declaring:

```yaml
ai:
  source_of_truth: true
```

assumes authoritative responsibility for the concepts defined within its scope.

Other documents MUST reference the Source of Truth rather than reproduce normative definitions.

If two documents claim authority over the same concept, the conflict MUST be resolved through architectural governance.

---

# 27. RAG Metadata Requirements

Documents intended for RAG ingestion SHOULD provide enough metadata to support:

- identity filtering;
- architectural filtering;
- version filtering;
- lifecycle filtering;
- security filtering;
- dependency traversal;
- semantic retrieval;
- temporal reasoning.

At minimum, RAG-ready documents MUST contain:

```yaml
document:
  id:
  title:
  version:

architecture:
  layer:
  module:

lifecycle:
  state:

relations:

ai:
  rag_ready: true
```

---

# 28. Claude Code Requirements

Claude Code MUST be able to determine from metadata:

1. What document it is reading.
2. What architectural layer it belongs to.
3. Who owns it.
4. What version it represents.
5. Whether it is authoritative.
6. What documents it depends on.
7. What documents relate to it.
8. Whether it is active.
9. Whether it is compatible with the current AI-MOS Epoch.

Claude Code SHOULD NOT infer these properties from filename conventions when the metadata provides an authoritative value.

---

# 29. Obsidian Requirements

Obsidian-compatible documents SHOULD:

- use stable IDs;
- use relative Markdown links;
- use descriptive headings;
- avoid unnecessary embedded HTML;
- maintain predictable metadata structures.

Internal relationships SHOULD be represented through relative Markdown links and metadata relationship fields where appropriate.

---

# 30. Git and GitHub Requirements

Metadata changes are subject to normal Git version control.

Changes to normative metadata MUST be visible in Git history.

Generated metadata MUST NOT overwrite authoritative metadata without an explicit governance process.

Pull requests modifying the metadata contract SHOULD trigger automated validation.

---

# 31. Validation Requirements

A compliant AI-MOS repository SHOULD eventually provide automated validation capable of detecting:

- missing Front Matter;
- invalid YAML;
- missing required fields;
- invalid field types;
- invalid controlled vocabulary;
- malformed document IDs;
- invalid versions;
- inconsistent `full` version values;
- broken relative references;
- duplicate document IDs;
- incompatible Epoch declarations;
- invalid relationship paths;
- invalid security classifications.

---

# 32. Metadata Schema Evolution

Changes to this metadata standard are themselves versioned.

A change is:

### PATCH

When correcting wording or documentation without changing schema behavior.

### MINOR

When adding backward-compatible optional metadata.

### MAJOR

When changing or removing required fields, changing field semantics, or breaking validation compatibility.

An architectural Epoch change MAY supersede the entire metadata schema when the underlying architecture fundamentally changes.

---

# 33. Backward Compatibility

Metadata consumers MUST ignore unknown optional fields rather than failing whenever technically feasible.

However, unknown fields MUST NOT silently override canonical fields.

Example:

```yaml
document:
  title: Canonical Title

custom:
  title: Other Title
```

`document.title` remains authoritative.

---

# 34. Extension Mechanism

Future domains MAY be introduced through an approved schema evolution.

Extensions SHOULD follow:

```yaml
extension:
  namespace:
    field:
```

Third-party or client-specific metadata SHOULD NOT modify the semantics of canonical AI-MOS fields.

Client-specific metadata MUST be namespaced when required to avoid collisions.

Example:

```yaml
client:
  namespace:
    field: value
```

---

# 35. Client Isolation

Client implementations MAY extend the metadata model but MUST NOT alter the meaning of Core metadata fields.

Example:

```yaml
client:
  id: CLIENT-001
  implementation: production
```

Client metadata must remain subordinate to AI-MOS Core governance.

---

# 36. Security Boundary

Metadata itself MUST NOT contain:

- passwords;
- API keys;
- authentication tokens;
- session cookies;
- private credentials;
- secrets;
- sensitive personal data unless explicitly required and governed.

Metadata describes a document.

It is not a secret-storage mechanism.

---

# 37. Validation Priority

When metadata conflicts with inferred information, the following authority order applies:

```text
1. Explicit approved metadata
2. This metadata standard
3. SYSTEM_MANIFEST.md
4. Document content
5. Filename
6. Directory location
7. AI inference
```

AI systems MUST NOT silently infer a conflicting value when authoritative metadata exists.

---

# 38. Compliance Levels

AI-MOS defines three compliance levels.

## Level 1 — Structural

The document contains valid YAML and required fields.

## Level 2 — Semantic

The metadata values are valid, consistent and architecturally meaningful.

## Level 3 — Enterprise

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

Production Core documents SHOULD achieve Level 3 compliance.

---

# 39. Canonical Example

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

# 40. Non-Compliance

A document is non-compliant when it:

- omits required metadata;
- contains invalid YAML;
- uses an invalid controlled value;
- contains an inconsistent version;
- declares a duplicate ID;
- uses invalid internal references;
- contradicts authoritative metadata;
- exposes secrets through metadata;
- violates the AI-MOS architecture.

Non-compliant documents MUST NOT be promoted to Enterprise production status.

---

# 41. Governance Authority

This specification governs metadata across the AI-MOS ecosystem.

Changes to this document require architectural review.

Changes that affect required fields, field semantics, validation behavior or interoperability MUST be versioned accordingly.

This document is subordinate only to the AI-MOS System Manifest and any future approved Architecture Epoch that explicitly supersedes it.

---

# 42. Normative Summary

Every canonical AI-MOS Markdown document MUST be:

```text
Identifiable
Versioned
Owned
Classified
Lifecycle-aware
Architecturally positioned
Relationally connected
Machine-readable
Auditable
AI-compatible
```

The metadata layer exists to ensure that AI-MOS remains understandable not only today, but also after years of architectural evolution.

---

# 43. Standard Status

```text
Standard: AI-MOS Metadata Standard
Document ID: AI-MOS-FND-0002
Architecture Epoch: E001
Current Version: E001-v0.1.0
Status: Approved
Authority: AI-MOS Architecture
```