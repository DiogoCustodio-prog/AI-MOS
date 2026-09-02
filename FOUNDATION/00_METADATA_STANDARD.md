---
document:
  id: AI-MOS-FND-0002
  title: AI-MOS Metadata Standard
  type: Foundation Specification
  status: In Review
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
  created: 2026-08-10
  updated: 2026-08-10
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
  related_documents: []

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
  last_review: 2026-08-10
  review_cycle: annual
---

# AI-MOS Metadata Standard

## 1. Document Status and Authority

This document defines the metadata contract for canonical Markdown documents in the AI Marketing Operating System (AI-MOS).

Its current editorial status is **In Review**. It is the canonical candidate for the `metadata-standard` authority scope and becomes the approved metadata authority only after architectural review and explicit approval.

This specification is subordinate to the [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) for system identity, architectural boundaries, permanent principles, and system-level governance. This specification owns the detailed contract for document metadata. Neither document silently replaces the authority of the other.

While this document is In Review, it is a proposed normative baseline. New canonical documents should follow it, but the repository must not represent the standard as formally approved until its review is complete.

The terms **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are normative terms in this document:

- **MUST**, **REQUIRED**, and **SHALL** indicate an absolute requirement.
- **MUST NOT** and **SHALL NOT** indicate an absolute prohibition.
- **SHOULD** indicates a strong recommendation that may be overridden only with a recorded reason.
- **SHOULD NOT** indicates a strong recommendation against an action.
- **MAY** indicates a permitted option.

## 2. Scope

This standard applies to every **canonical Markdown document** maintained in the governed AI-MOS areas:

- `SYSTEM/`;
- `FOUNDATION/`;
- `CORE/`;
- `BOOTSTRAP/`;
- `CLIENTS/`;
- `KNOWLEDGE/`.

It applies to:

- system manifests;
- Foundation specifications;
- Core specifications;
- Bootstrap specifications;
- Client Implementation documents;
- architecture specifications;
- governance policies;
- decision records;
- development rules;
- operational specifications;
- agent specifications;
- workflow specifications;
- templates;
- roadmaps;
- knowledge and evolution records.

This standard does not require metadata front matter on every repository artifact. The following are not canonical documents unless explicitly promoted through governance:

- historical exports in `source-material/`;
- local Claude session memory in `memory/`;
- temporary files;
- generated artifacts;
- binary assets;
- tool configuration files;
- external systems and their native records.

A repository navigation README MAY be non-canonical when it only explains an empty or reserved directory. If it defines an AI-MOS rule or claims authority over a concept, it MUST be promoted to a canonical document and comply with this standard.

## 3. Canonical Document Requirements

A canonical AI-MOS Markdown document MUST:

1. begin with YAML Front Matter;
2. have no content before the opening `---` delimiter;
3. contain a stable document ID;
4. declare its document type, status, and version;
5. declare ownership and architectural placement;
6. declare lifecycle state and maturity;
7. declare creation and update metadata;
8. declare document relationships;
9. declare the official document language;
10. preserve native YAML data types;
11. avoid secrets and private authentication material;
12. avoid redefining another document's Source of Truth;
13. use deterministic structure and terminology;
14. use relative paths for internal document relationships;
15. remain suitable for human review, Claude Code, Git-based workflows, Obsidian, and future retrieval systems.

A document is not canonical merely because it has front matter. Canonical status depends on its location, declared authority, lifecycle, and governance state.

## 4. Front Matter Format

YAML Front Matter MUST appear at the beginning of the Markdown file and MUST close before the first Markdown heading.

The canonical form is:

```yaml
---
<metadata>
---
```

The opening and closing delimiters MUST be standalone lines containing exactly three hyphens, apart from the line ending.

The recommended top-level domain order is:

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
extensions
```

Consumers SHOULD preserve this order. A validator MAY enforce it for canonical documents.

Top-level domains MUST NOT be duplicated. A canonical field MUST NOT be represented under two different canonical domains.

## 5. Canonical Metadata Domains

The canonical top-level domains are:

- `document` — identity, type, editorial status, and document version;
- `ownership` — accountable organization and owner;
- `architecture` — architectural layer and module;
- `lifecycle` — operational state, maturity, and review requirement;
- `metadata` — dates, language, and retrieval tags;
- `relations` — dependencies and document relationships;
- `compatibility` — AI-MOS Epoch and Core compatibility;
- `ai` — machine-oriented authority and consumer compatibility;
- `security` — classification and confidentiality;
- `audit` — creation, update, review, and review cycle;
- `extensions` — explicitly namespaced optional extensions.

A canonical document MUST NOT introduce another unapproved top-level domain.

Client, vendor, or future extension fields MUST be placed under `extensions` unless an approved revision adds a dedicated canonical domain.

Example:

```yaml
extensions:
  client:
    namespace: inovador-tech
    field: value
  vendor:
    provider: example-provider
    field: value
```

Extension fields MUST NOT change the meaning of canonical fields. Canonical fields always take precedence over extension fields.

## 6. Required Domains

The following domains and fields are REQUIRED for every canonical AI-MOS document:

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

ownership:
  organization:
  owner:

architecture:
  layer:
  module:

lifecycle:
  state:
  maturity:
  review_required:

metadata:
  created:
  updated:
  language:
  tags:

relations:
  depends_on:
  related_documents:

ai:
  source_of_truth:
  claude_code_compatible:
  github_compatible:
  obsidian_compatible:
  rag_ready:
```

The following domains SHOULD be present in every canonical document and MUST be present in enterprise-ready documents unless an approved exemption exists:

```yaml
compatibility:
security:
audit:
```

The `authority_scope` field is REQUIRED when `ai.source_of_truth` is `true` and SHOULD be present for every canonical document when a machine consumer needs to determine its conceptual scope.

## 7. `document` Domain

The `document` domain identifies the document as a governed object in the AI-MOS ecosystem.

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

### 7.1 `document.id`

Type: string.

Required: yes.

`document.id` is the stable logical identity of the document. It is independent of the filename, title, directory position, and document language.

The ID MUST:

- be unique across the AI-MOS ecosystem;
- remain stable throughout the document lifecycle;
- be machine-parseable;
- contain no spaces;
- contain no accented characters;
- not depend on the filename;
- not depend on the title;
- not be reused after retirement;
- not change solely because the file is renamed or translated.

The recommended pattern is:

```text
AI-MOS-<DOMAIN>-<SEQUENCE>
```

The current recommended machine-parseable form is:

```text
^AI-MOS-[A-Z]{3}-[0-9]{4}$
```

The domain code is a governed vocabulary. The definitive domain catalog belongs to the naming conventions document and MUST be kept consistent with this pattern.

Example:

```yaml
id: AI-MOS-FND-0002
```

A retired ID MUST NOT be reassigned to a different document.

### 7.2 `document.title`

Type: string.

Required: yes.

`document.title` is the canonical human-readable title. It SHOULD describe the semantic purpose of the document and SHOULD remain aligned with the body and filename.

The title MAY change during the document lifecycle. A title change does not change `document.id`.

### 7.3 `document.type`

Type: string.

Required: yes.

`document.type` identifies the controlled semantic category of the document.

The initial controlled vocabulary is:

- `System Manifest`;
- `Foundation Specification`;
- `Architecture Specification`;
- `Project Specification`;
- `Development Rule`;
- `Governance Policy`;
- `Reference`;
- `Decision Record`;
- `Implementation Specification`;
- `Operational Specification`;
- `Agent Specification`;
- `Workflow Specification`;
- `Knowledge Document`;
- `Template`;
- `Roadmap`.

A new document type MUST be introduced through a versioned governance change to this standard.

### 7.4 `document.status`

Type: string.

Required: yes.

`document.status` represents the editorial and approval state of the document. It MUST NOT be used as a substitute for `lifecycle.state`.

The controlled vocabulary is:

- `Draft` — being authored and not yet submitted for review;
- `Proposed` — submitted for consideration but not yet in formal review;
- `In Review` — under technical, architectural, or governance review;
- `Approved` — formally accepted for use within its authority scope;
- `Deprecated` — retained but not recommended for new use;
- `Superseded` — replaced by another document;
- `Archived` — retained for historical reference without current authority;
- `Rejected` — reviewed and not accepted.

`Active` is not a valid value for `document.status`. Operational activity belongs to `lifecycle.state: active`.

A document MUST have exactly one editorial status.

### 7.5 `document.version`

The `version` object implements AI-MOS hybrid versioning for the document.

Canonical structure:

```yaml
version:
  epoch: E001
  semantic: 0.2.0
  full: E001-v0.2.0
```

#### 7.5.1 `version.epoch`

Type: string.

Required: yes.

Format:

```text
E###
```

The Epoch identifies the architectural generation against which the document was authored.

The current AI-MOS architecture is `E001`. An Epoch change indicates structural or conceptual evolution that may affect platform-level compatibility.

#### 7.5.2 `version.semantic`

Type: string.

Required: yes.

Format:

```text
MAJOR.MINOR.PATCH
```

Within the same Epoch:

- MAJOR increments for incompatible contract or semantic changes;
- MINOR increments for backward-compatible additions or capabilities;
- PATCH increments for backward-compatible corrections and refinements.

#### 7.5.3 `version.full`

Type: string.

Required: yes.

Format:

```text
E###-vMAJOR.MINOR.PATCH
```

`version.full` MUST equal the exact concatenation of `version.epoch`, the literal `-v`, and `version.semantic`.

Valid:

```yaml
epoch: E001
semantic: 0.2.0
full: E001-v0.2.0
```

Invalid:

```yaml
epoch: E001
semantic: 0.2.0
full: E002-v0.2.0
```

## 8. `ownership` Domain

The `ownership` domain defines accountability for the document.

Canonical structure:

```yaml
ownership:
  organization:
  owner:
```

### 8.1 `ownership.organization`

Type: string.

Required: yes.

The organization responsible for the document.

For AI-MOS Core and Foundation documents, the organization is normally:

```yaml
organization: Inovador Tech
```

### 8.2 `ownership.owner`

Type: string.

Required: yes.

The accountable team, function, or governance role responsible for the document.

Individual names SHOULD be avoided unless formal accountability requires them.

Recommended value for system and Foundation specifications:

```yaml
owner: AI-MOS Architecture
```

## 9. `architecture` Domain

The `architecture` domain identifies the document's position in the AI-MOS architecture.

Canonical structure:

```yaml
architecture:
  layer:
  module:
```

### 9.1 `architecture.layer`

Type: string.

Required: yes.

Initial controlled vocabulary:

- `System`;
- `Foundation`;
- `Core`;
- `Bootstrap`;
- `Client`;
- `Knowledge`;
- `Operations`;
- `Integration`.

The layer value MUST match the document's governed repository area and architectural responsibility. A document in `SYSTEM/` must not declare `layer: Foundation` merely because it is part of the Foundation phase.

### 9.2 `architecture.module`

Type: string.

Required: yes.

The module identifies the logical subdomain to which the document belongs.

The value SHOULD be specific enough for filtering, navigation, and dependency analysis.

Example:

```yaml
architecture:
  layer: Foundation
  module: Metadata Governance
```

## 10. `lifecycle` Domain

The `lifecycle` domain defines the operational state of a document as a governed asset.

Canonical structure:

```yaml
lifecycle:
  state:
  maturity:
  review_required:
```

### 10.1 `lifecycle.state`

Type: string.

Required: yes.

Controlled vocabulary:

- `active` — current and available for operational use within its editorial status;
- `inactive` — retained but not currently used;
- `deprecated` — retained but not recommended for new use;
- `superseded` — replaced by another document;
- `archived` — preserved for historical reference.

`lifecycle.state` is distinct from `document.status`.

### 10.2 `lifecycle.maturity`

Type: string.

Required: yes.

Controlled vocabulary:

- `draft`;
- `foundation`;
- `experimental`;
- `production`;
- `enterprise`;
- `legacy`.

A document marked `enterprise` MUST have passed the applicable structural, semantic, relationship, security, and governance checks.

### 10.3 `lifecycle.review_required`

Type: boolean.

Required: yes.

Indicates whether the document requires periodic formal review.

The value MUST be a native YAML boolean, not a quoted string.

### 10.4 Status and lifecycle consistency

`document.status` and `lifecycle.state` represent different dimensions but MUST remain semantically consistent.

The following combinations are valid examples:

| Editorial status | Operational state | Meaning |
| --- | --- | --- |
| `Draft` | `active` | Current working draft, not approved |
| `In Review` | `active` | Current candidate under review |
| `Approved` | `active` | Approved and currently used |
| `Deprecated` | `deprecated` | Retained but not recommended for new use |
| `Superseded` | `superseded` | Replaced by another document |
| `Archived` | `archived` | Historical preservation |
| `Rejected` | `inactive` | Not accepted and not operational |

A validator SHOULD reject combinations that imply current authority for a rejected, archived, or superseded document.

## 11. `metadata` Domain

The `metadata` domain contains descriptive and retrieval-oriented metadata.

Canonical structure:

```yaml
metadata:
  created:
  updated:
  language:
  tags:
```

### 11.1 `metadata.created` and `metadata.updated`

Type: ISO-compatible date or datetime string, according to repository validation support.

Required: yes.

The preferred date form is:

```text
YYYY-MM-DD
```

Datetime precision MAY be used when operationally necessary, but documents SHOULD use date precision unless timestamps are required.

`metadata.created` records the canonical document's creation date and SHOULD remain immutable after assignment.

`metadata.updated` records the latest approved or proposed document update, according to the document's governance state.

### 11.2 `metadata.language`

Type: string.

Required: yes.

The value MUST be a valid BCP 47 language tag.

The official language of canonical AI-MOS documentation is:

```yaml
language: en-US
```

Canonical documents created in `SYSTEM/`, `FOUNDATION/`, `CORE/`, `BOOTSTRAP/`, `CLIENTS/`, and `KNOWLEDGE/` MUST use `en-US` unless an explicit governance decision creates a localized derivative.

A localized derivative MUST:

1. declare its actual language;
2. identify the canonical en-US document it derives from;
3. remain structurally aligned with the canonical document;
4. never silently replace the en-US Source of Truth.

Historical exports and operational conversations may use other languages without violating this standard because they are not canonical AI-MOS documents.

### 11.3 `metadata.tags`

Type: array of strings.

Required: yes.

Tags MUST:

- be lowercase;
- use hyphens instead of spaces;
- avoid accents;
- be semantically relevant;
- avoid duplicates;
- be stable enough to support retrieval;
- not contain secrets or private data.

Example:

```yaml
tags:
  - ai-mos
  - foundation
  - metadata
```

## 12. `relations` Domain

The `relations` domain defines explicit relationships between documents.

Canonical minimum structure:

```yaml
relations:
  depends_on: []
  related_documents: []
```

Both fields MUST be present and MUST contain YAML arrays, including when empty.

### 12.1 Internal path rules

Values in internal document relationship fields MUST be repository-relative Markdown paths.

They MUST NOT be absolute filesystem paths.

They MUST NOT use a repository-specific absolute URL when a relative path is available.

A relationship path MUST resolve from the directory containing the current document.

Example for a Foundation document:

```yaml
relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
```

### 12.2 `relations.depends_on`

`depends_on` identifies documents that are structurally or normatively necessary to interpret, validate, or implement the current document.

Dependencies are normative relationships. Missing dependencies are a validation failure for a production or enterprise document.

Dependencies SHOULD form an acyclic graph. A circular dependency requires explicit architectural justification and approval.

### 12.3 `relations.related_documents`

`related_documents` identifies documents that are semantically connected but not mandatory dependencies.

A related document is not automatically authoritative for the current document.

### 12.4 Optional relationship fields

The following relationship fields MAY be used when they are defined and applicable:

```yaml
relations:
  supersedes: []
  superseded_by: []
  implements: []
  implemented_by: []
  references: []
  derived_from: []
  translated_from: []
```

When these fields refer to internal documents, their values MUST follow the same relative-path rules.

`translated_from` SHOULD be used by a localized derivative to identify the canonical en-US document.

A document marked `Superseded` SHOULD declare `superseded_by` unless the replacement is external and documented elsewhere.

## 13. `compatibility` Domain

The `compatibility` domain declares the AI-MOS architecture and Core version range against which a document is designed.

Canonical structure:

```yaml
compatibility:
  ai_mos:
    epoch:
    core:
```

### 13.1 `compatibility.ai_mos.epoch`

Type: string.

Required when compatibility is declared; recommended for every canonical document.

The value MUST use the current AI-MOS Epoch format:

```text
E###
```

Example:

```yaml
epoch: E001
```

### 13.2 `compatibility.ai_mos.core`

Type: string.

Required when compatibility is declared.

The value declares the supported AI-MOS Core semantic version range within the specified Epoch.

Version ranges SHOULD use explicit comparison operators, for example:

```text
>=0.2.0 <2.0.0
>=1.0.0
=1.4.2
```

The following ambiguous values MUST NOT be used in normative compatibility metadata:

```text
latest
current
stable
1.x
```

A compatibility declaration that omits the Epoch is incomplete when the AI-MOS architecture supports multiple Epochs.

## 14. `ai` Domain

The `ai` domain describes machine-oriented authority and compatibility properties.

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

### 14.1 `ai.source_of_truth`

Type: boolean.

Required: yes.

Indicates whether the document is authoritative for the concepts within its declared scope.

`source_of_truth: true` MUST NOT be interpreted as universal authority over the entire repository.

A document declaring `source_of_truth: true` MUST declare a non-empty `authority_scope`.

Two approved documents MUST NOT claim the same authority scope unless an explicit governance decision defines their relationship.

### 14.2 `ai.authority_scope`

Type: string.

Required when `source_of_truth: true`; recommended for all canonical documents.

The value identifies the exact conceptual scope governed by the document.

Examples:

```yaml
authority_scope: system-manifest
authority_scope: metadata-standard
authority_scope: naming-conventions
authority_scope: campaign-workflow
```

Authority scopes MUST be specific enough to prevent overlapping Sources of Truth.

### 14.3 Consumer compatibility flags

The following fields are booleans:

- `claude_code_compatible`;
- `github_compatible`;
- `obsidian_compatible`;
- `rag_ready`.

They MUST use native YAML booleans.

Meanings:

- `claude_code_compatible` — the document is structured for deterministic AI-assisted reading and editing;
- `github_compatible` — the document is suitable for Git-based repository review and history;
- `obsidian_compatible` — the document is suitable for graph-based navigation and linking;
- `rag_ready` — the document has stable identity, explicit metadata, deterministic structure, and relationships sufficient for future retrieval ingestion.

A compatibility flag is a declared property, not proof that the corresponding integration has already been implemented.

### 14.4 RAG readiness minimum

A document marked `rag_ready: true` MUST provide:

- stable identity;
- clear title and headings;
- declared architectural layer and module;
- version and lifecycle metadata;
- explicit language;
- explicit relationships;
- deterministic terminology;
- sufficient context for independent interpretation;
- no secret material.

## 15. `security` Domain

The `security` domain declares document classification and confidentiality expectations.

Canonical structure:

```yaml
security:
  classification:
  confidentiality:
```

### 15.1 `security.classification`

Initial controlled vocabulary:

- `public`;
- `internal`;
- `restricted`;
- `confidential`.

### 15.2 `security.confidentiality`

Initial controlled vocabulary:

- `standard`;
- `sensitive`;
- `high`.

Security metadata does not itself enforce access control. It describes governance expectations for future or external policy enforcement.

### 15.3 Security boundary

Metadata and document bodies MUST NOT contain:

- passwords;
- API keys;
- authentication tokens;
- session cookies;
- private credentials;
- secrets;
- ungoverned sensitive personal data.

AI-MOS Markdown is not a secret-storage mechanism.

## 16. `audit` Domain

The `audit` domain provides traceability for document creation and review.

Canonical structure:

```yaml
audit:
  created_by:
  updated_by:
  last_review:
  review_cycle:
```

### 16.1 `audit.created_by`

Type: string.

Required for enterprise-ready canonical documents.

Identifies the role, system, or organizational function responsible for creating the document.

### 16.2 `audit.updated_by`

Type: string.

Required for enterprise-ready canonical documents.

Identifies the role, system, or organizational function responsible for the latest approved or proposed update, consistent with the document status.

### 16.3 `audit.last_review`

Type: ISO-compatible date.

Required for enterprise-ready canonical documents.

Records the date of the most recent formal review. It MUST NOT be represented by placeholders such as `TBD`.

### 16.4 `audit.review_cycle`

Type: string.

Required for enterprise-ready canonical documents.

Controlled vocabulary:

- `quarterly`;
- `semiannual`;
- `annual`;
- `biennial`;
- `event-driven`;
- `none`.

## 17. Canonical Baseline

The following is the recommended baseline for a canonical AI-MOS document. It is illustrative and must be adapted to the document's actual authority, layer, status, and relationships.

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
  created: 2026-08-10
  updated: 2026-08-10
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
  last_review: 2026-08-10
  review_cycle: annual
---
```

The baseline is not permission to copy an incorrect authority scope, status, layer, or compatibility range into a new document.

## 18. YAML Type Rules

AI-MOS metadata MUST preserve native YAML types.

Correct:

```yaml
review_required: true
source_of_truth: false
tags:
  - ai-mos
  - foundation
depends_on: []
```

Incorrect:

```yaml
review_required: "true"
source_of_truth: "false"
tags: "ai-mos, foundation"
depends_on:
```

Boolean values MUST be booleans.

Arrays MUST be arrays, including empty arrays.

Structured values MUST be objects.

Dates MUST use the declared ISO-compatible representation.

Version values MUST remain strings, even when they contain only numbers and periods, so that version semantics are not lost during parsing.

## 19. Empty, Null, and Placeholder Values

Required metadata MUST NOT be empty or null.

An empty array is valid where a relationship or collection is genuinely empty:

```yaml
relations:
  depends_on: []
  related_documents: []
```

The following values MUST NOT be used as production placeholders for required fields:

```text
TBD
UNKNOWN
N/A
```

If a required value is not known, the document MUST remain in an appropriate non-production status and the missing decision must be recorded for resolution.

A placeholder in an illustrative example MUST be clearly marked as illustrative and MUST NOT be copied into a production document.

## 20. Immutability and Change Rules

The following fields SHOULD be treated as immutable after initial assignment:

- `document.id`;
- `metadata.created`;
- `audit.created_by`.

Changing one of these fields requires explicit governance approval and a recorded reason.

The following fields are expected to change during the document lifecycle:

- `document.title`;
- `document.status`;
- `document.version`;
- `lifecycle.state`;
- `lifecycle.maturity`;
- `metadata.updated`;
- `metadata.tags`;
- `audit.updated_by`;
- `audit.last_review`;
- `relations` as the document graph evolves.

Normative changes MUST increment the document version according to the hybrid versioning rules and MUST be visible in the repository's Git history.

## 21. Filename Independence

The canonical identity of a document is its `document.id`, not its filename.

A filename MAY change while `document.id` remains unchanged.

Example:

```text
old: 00_METADATA_STANDARD.md
new: 00_METADATA_SPECIFICATION.md
```

The logical identity remains:

```yaml
id: AI-MOS-FND-0002
```

A filename is a navigation aid and SHOULD follow the naming conventions, but it is not the authoritative identity.

## 22. Authority and Source-of-Truth Rules

A Source of Truth is authoritative only within its declared `authority_scope`.

The following rules apply:

1. Every canonical concept SHOULD have one approved authoritative document.
2. A document claiming `source_of_truth: true` MUST declare `authority_scope`.
3. Other documents MUST reference the Source of Truth instead of reproducing its normative definition.
4. Two documents MUST NOT claim overlapping authority without an approved governance decision.
5. Historical exports, drafts, experiments, and AI inferences cannot override an approved Source of Truth.
6. A proposed document in review is not equivalent to an approved document.
7. A client implementation cannot redefine the meaning of Core or Foundation canonical fields.
8. A knowledge record may propose a change but cannot silently promote it.

The `SYSTEM_MANIFEST.md` is authoritative for the `system-manifest` scope. This document is authoritative for the `metadata-standard` scope once approved. Specialized documents own their declared scopes.

## 23. Authority Resolution

Authority is scoped, not determined by one universal document ranking.

When interpreting a canonical document:

1. Validate the current front matter against this standard.
2. Use the current document's valid metadata to identify its ID, version, language, layer, lifecycle, relationships, and declared authority.
3. Use the approved Source of Truth for the concept being interpreted.
4. Use the approved System Manifest for system identity, boundaries, and permanent system principles.
5. Use the document body as implementation or explanatory content within the authority established above.
6. Use filename and directory only as navigation aids when metadata is absent or incomplete.
7. Use AI inference only to propose clarification, never to silently override authoritative information.

A malformed or unapproved front matter block is not made authoritative merely by appearing at the top of a file. It must be reported for correction.

If two approved documents conflict, the conflict MUST be recorded and resolved through architectural governance. An AI system MUST NOT silently choose one based only on filename, recency, or textual confidence.

## 24. Compatibility with Consumers

### 24.1 Claude Code

A Claude Code-compatible document SHOULD allow an agent to determine from metadata:

1. what document it is reading;
2. what concept or scope it governs;
3. where it belongs architecturally;
4. who owns it;
5. what version it represents;
6. whether it is approved and operationally active;
7. what documents it depends on;
8. what documents relate to it;
9. which language is canonical;
10. which Epoch and Core range it supports.

Claude Code SHOULD NOT infer these properties from filenames when the metadata provides them.

### 24.2 Git and GitHub

Canonical metadata changes MUST be reviewable in the repository's Git history.

Generated metadata MUST NOT overwrite authoritative metadata without a documented governance process.

Pull requests that modify this standard or other normative metadata SHOULD run structural, semantic, relationship, and duplicate-ID validation when tooling is available.

### 24.3 Obsidian

Obsidian-compatible documents SHOULD:

- use stable IDs;
- use relative Markdown links;
- use descriptive headings;
- avoid unnecessary embedded HTML;
- maintain predictable metadata structures;
- keep the canonical language and derivative relationships explicit.

### 24.4 RAG

RAG readiness is a structural property. It does not require a vector database and does not authorize indexing of restricted information.

A future retrieval system SHOULD be able to filter documents by:

- ID;
- authority scope;
- layer and module;
- version and Epoch;
- lifecycle state;
- status;
- language;
- security classification;
- dependency relationships;
- tags.

## 25. Extension and Client Metadata

Client and vendor metadata MAY extend a document, but it MUST remain subordinate to the canonical contract.

Preferred form:

```yaml
extensions:
  client:
    namespace: client-identifier
    field: value
```

Extensions MUST:

- use an explicit namespace;
- avoid collisions with canonical field names;
- not alter canonical semantics;
- not claim a canonical authority scope without governance;
- not contain secrets;
- remain compatible with client isolation.

A client implementation may add facts required for its operation. It must not redefine `document`, `ownership`, `architecture`, `lifecycle`, `metadata`, `relations`, `compatibility`, `ai`, `security`, or `audit` semantics.

## 26. Repository Language Policy

The official language of canonical AI-MOS documentation is `en-US`.

Every canonical document MUST declare:

```yaml
metadata:
  language: en-US
```

This policy is compatible with multilingual client operations. A translation or localized derivative MAY use `pt-BR` or another valid BCP 47 language tag, but it MUST declare `relations.translated_from` pointing to the canonical source and MUST not claim to replace the en-US Source of Truth.

Source material may remain in its original language. It is not subject to canonical language enforcement because it is not a canonical specification.

## 27. Compliance Levels

AI-MOS defines three compliance levels.

### Level 1 — Structural

The document has:

- valid Front Matter delimiters;
- parseable YAML;
- required domains and fields;
- correct basic data types;
- a valid document ID format;
- a consistent `version.full` value.

### Level 2 — Semantic

The document satisfies Level 1 and also has:

- valid controlled vocabulary values;
- consistent status and lifecycle state;
- valid language declaration;
- valid relationships and relative paths;
- a coherent layer and module;
- a valid authority scope when required;
- compatible Epoch declarations;
- no duplicate document ID.

### Level 3 — Enterprise

The document satisfies Levels 1 and 2 and also has:

- security classification;
- audit metadata;
- review-cycle declaration;
- explicit ownership;
- dependency validation;
- client-isolation compliance where applicable;
- AI compatibility flags;
- RAG readiness where declared;
- governance approval appropriate to its status;
- no prohibited secret material.

Production and enterprise Core documents SHOULD achieve Level 3 compliance.

## 28. Validation Requirements

A compliant AI-MOS validation process SHOULD detect:

- missing Front Matter;
- content before the opening delimiter;
- missing closing delimiter;
- invalid YAML syntax;
- duplicate top-level domains;
- missing required domains;
- missing required fields;
- incorrect YAML data types;
- invalid controlled vocabulary values;
- malformed document IDs;
- duplicate document IDs;
- invalid Epoch values;
- invalid semantic versions;
- inconsistent `version.full`;
- invalid status and lifecycle combinations;
- invalid or missing language declarations;
- broken relative relationship paths;
- absolute internal relationship paths;
- circular dependencies;
- invalid authority scopes;
- overlapping approved Source-of-Truth scopes;
- incompatible Epoch declarations;
- invalid security classifications;
- missing audit fields for enterprise documents;
- prohibited placeholders in production metadata;
- secrets in metadata;
- unauthorized top-level extension domains.

Validation SHOULD be available both as a human-review checklist and as automated tooling when implementation support exists.

This repository currently has no automated metadata validator. Until one is implemented, validation is manual and its limitations must be reported accurately.

## 29. Metadata Schema Evolution

This standard is itself versioned.

### PATCH

A wording correction or clarification that does not change field structure, semantics, controlled values, or validation behavior.

### MINOR

A backward-compatible addition, such as an optional field, optional relationship, extension rule, or controlled value that does not invalidate compliant documents.

### MAJOR

A breaking change, such as:

- removing a required field;
- changing the meaning of a field;
- changing a required field type;
- invalidating existing compliant documents;
- changing relationship semantics;
- changing compatibility behavior.

An Architecture Epoch change MAY supersede this standard when the underlying AI-MOS architecture changes fundamentally.

Any change to this standard MUST be reviewed and recorded before promotion to an approved status.

## 30. Backward Compatibility

Metadata consumers SHOULD ignore unknown optional fields when technically feasible.

Unknown fields MUST NOT silently override canonical fields.

Canonical fields always take precedence over extensions.

A consumer that cannot safely ignore an unknown field MUST report the incompatibility rather than silently interpreting it as a canonical field.

## 31. Non-Compliance

A canonical document is non-compliant if it:

- omits required metadata;
- contains invalid YAML;
- uses invalid data types;
- uses an invalid controlled value;
- declares an inconsistent version;
- declares a duplicate document ID;
- uses an invalid internal reference;
- violates the official language policy without being a declared derivative;
- claims an overlapping Source-of-Truth scope;
- contradicts an approved authority without a recorded decision;
- exposes secrets through metadata or document content;
- violates lifecycle or client-isolation rules;
- introduces an unauthorized top-level domain;
- violates the System Manifest or other applicable governance.

A non-compliant document MUST NOT be promoted to production or enterprise authority until the non-compliance is resolved or explicitly excepted through governance.

## 32. Canonical Example

The following example is non-normative and demonstrates a valid approved document. `status: Approved` is paired with `lifecycle.state: active`; `Active` is not used as an editorial status.

```yaml
---
document:
  id: AI-MOS-CORE-0010
  title: Example Core Specification
  type: Architecture Specification
  status: Approved
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
  created: 2026-08-10
  updated: 2026-08-10
  language: en-US
  tags:
    - ai-mos
    - core
    - architecture

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ../FOUNDATION/00_METADATA_STANDARD.md
  related_documents: []

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
  last_review: 2026-08-10
  review_cycle: annual
---
```

## 33. Governance Authority

This standard governs the metadata contract for the AI-MOS ecosystem within the `metadata-standard` authority scope.

The [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) remains the higher authority for system identity, product boundaries, permanent principles, and system-level governance.

Changes to required fields, field semantics, data types, controlled vocabulary, relationship behavior, validation behavior, compatibility rules, or language policy MUST undergo architectural review and versioning.

No document, agent, script, integration, or external tool may silently redefine this standard.

## 34. Normative Summary

Every canonical AI-MOS Markdown document MUST be:

- identifiable;
- versioned;
- owned;
- architecturally positioned;
- lifecycle-aware;
- language-declared;
- relationally connected;
- machine-readable;
- auditable when enterprise status requires it;
- compatible with the applicable Epoch;
- safe for governed use;
- explicit about authority;
- validation-ready.

The metadata layer exists to keep AI-MOS understandable, governable, auditable, and automatable over long architectural horizons.

## 35. Standard Status

```text
Standard: AI-MOS Metadata Standard
Document ID: AI-MOS-FND-0002
Architecture Epoch: E001
Current Version: E001-v0.2.0
Status: In Review
Authority Scope: metadata-standard
Official Documentation Language: en-US
Owner: AI-MOS Architecture
```

This status is intentionally aligned with the current review state of `SYSTEM/SYSTEM_MANIFEST.md`. Both documents require explicit architectural approval before being represented as approved Source-of-Truth documents.

## 36. Appendix A — Canonical Regex Guidance

### Document ID

```text
^AI-MOS-[A-Z]{3}-[0-9]{4}$
```

### Architecture Epoch

```text
^E[0-9]{3}$
```

### Semantic Version

```text
^[0-9]+\.[0-9]+\.[0-9]+$
```

### Full Version

```text
^E[0-9]{3}-v[0-9]+\.[0-9]+\.[0-9]+$
```

### Language Tag

The official canonical value is:

```text
en-US
```

General language validation SHOULD use a BCP 47-compatible parser rather than the simplified pattern below:

```text
^[a-z]{2,3}(?:-[A-Z][a-z]{3})?(?:-[A-Z]{2}|-[0-9]{3})?$
```

### Relative Internal Document Path

A relationship value MUST be a repository-relative Markdown path resolved from the current document's directory. It MUST NOT be an absolute filesystem path or an internal repository URL.

## 37. Appendix B — Validation Intent

The purpose of this standard is not only human readability. It is to make AI-MOS:

- deterministic for Claude Code;
- stable for Git and GitHub workflows;
- navigable in Obsidian;
- explicit about authority and dependencies;
- indexable for future RAG;
- auditable for enterprise governance;
- resilient across future architectural evolution.

The executable schema and validator are intentionally separate future artifacts. This Markdown specification defines the contract; a later machine-readable schema and validation pipeline will implement it without silently changing its meaning.
