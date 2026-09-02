---
document:
  id: AI-MOS-FND-0003
  title: AI-MOS Document Template
  type: Template
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
  module: Document Authoring

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
    - document-template
    - authoring
    - yaml
    - governance

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ./00_METADATA_STANDARD.md
  related_documents: []

compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.2.0 <2.0.0"

ai:
  source_of_truth: true
  authority_scope: document-template
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

# AI-MOS Document Template

## 1. Document Status and Authority

This document provides the canonical authoring template for AI-MOS Markdown documents.

Its current editorial status is **In Review**. It is the canonical candidate for the `document-template` authority scope and becomes the approved document-authoring reference only after architectural review and explicit approval.

This document applies the metadata contract defined by the [AI-MOS Metadata Standard](00_METADATA_STANDARD.md). It does not replace, amend, or independently redefine that standard. The metadata standard remains authoritative for field meaning, required fields, data types, controlled vocabularies, relationship semantics, language policy, and validation behavior.

The [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) remains authoritative for system identity, architectural boundaries, permanent principles, and system-level governance.

The template's authority is limited to the practical arrangement and authoring procedure for a canonical document. `ai.source_of_truth: true` in this document does not grant universal authority over the repository.

## 2. Purpose

The purpose of this template is to provide a repeatable starting point for creating a canonical AI-MOS Markdown document.

It helps an author to:

- place YAML Front Matter before all Markdown content;
- use the canonical top-level metadata domains in a predictable order;
- preserve native YAML data types;
- declare identity, ownership, architecture, lifecycle, language, relationships, compatibility, security, and audit information;
- distinguish document-level authority from ordinary document content;
- prepare a document for human review, Claude Code, Git-based workflows, Obsidian, and future retrieval systems.

The template is an authoring aid. It is not a substitute for architectural review, governance approval, or future automated validation.

## 3. Scope

This template is intended for canonical Markdown documents in the governed AI-MOS areas:

- `SYSTEM/`;
- `FOUNDATION/`;
- `CORE/`;
- `BOOTSTRAP/`;
- `CLIENTS/`;
- `KNOWLEDGE/`.

It may be adapted for system manifests, Foundation specifications, Core specifications, Bootstrap documents, Client Implementation documents, Knowledge records, decision records, agent specifications, workflow specifications, templates, and other document types recognized by the Metadata Standard.

It does not govern:

- historical exports in `source-material/`;
- Claude session memory in `memory/`;
- temporary files;
- generated artifacts;
- binary assets;
- external systems and their native records.

A repository navigation README may remain non-canonical when it only describes a reserved area and does not claim authority over an AI-MOS concept.

## 4. Relationship with the Metadata Standard

The Metadata Standard and this template have different responsibilities:

| Document | Responsibility |
| --- | --- |
| [AI-MOS Metadata Standard](00_METADATA_STANDARD.md) | Defines the metadata contract and normative field behavior |
| AI-MOS Document Template | Applies that contract in a copyable authoring structure |
| [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) | Defines system identity, boundaries, permanent principles, and governance direction |

The template MUST remain compatible with the Metadata Standard. It MUST NOT:

- introduce an unapproved top-level metadata domain;
- introduce a new canonical field;
- change a field's meaning or data type;
- create a new controlled vocabulary;
- redefine the relationship between `document.status` and `lifecycle.state`;
- broaden a Source-of-Truth authority scope;
- replace the official canonical language policy;
- silently convert an example into an approved specification.

The future Foundation documents for naming conventions, directory structure, and documentation principles own their respective subjects. This template should reference those documents when available instead of preemptively redefining their rules.

## 5. Canonical Authoring Rules

### 5.1 File opening and Front Matter

A canonical document MUST:

1. begin with the opening `---` delimiter;
2. contain valid YAML Front Matter;
3. close the Front Matter with a standalone `---` delimiter;
4. place the closing delimiter before the first Markdown heading;
5. contain no content before the opening delimiter.

The top-level domains SHOULD appear in the following order:

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

`extensions` is conditional and is omitted from the default template. When used, it MUST be the final top-level domain and MUST follow the extension rules in the Metadata Standard.

### 5.2 Identity and version

Every canonical instance MUST receive its own stable `document.id`.

The ID is independent of the filename and title. It MUST follow the governed ID format and MUST NOT be copied from this template or another document.

Document version values belong under `document.version`. The values `epoch`, `semantic`, and `full` MUST remain consistent according to the Metadata Standard.

### 5.3 Editorial status and operational lifecycle

`document.status` and `lifecycle.state` represent different dimensions:

- `document.status` identifies editorial and approval state;
- `lifecycle.state` identifies operational state.

A new document normally begins with `status: Draft` and `state: active`, unless the applicable governance process requires another valid combination. A document MUST NOT use `Active` as an editorial status.

### 5.4 Language

Canonical AI-MOS documentation MUST use:

```yaml
metadata:
  language: en-US
```

A localized derivative MUST declare its actual language and identify its canonical en-US source through the relationship rules defined by the Metadata Standard. A translation MUST NOT silently replace the en-US Source of Truth.

### 5.5 Relationships

Both relationship arrays MUST be present in every canonical instance:

```yaml
relations:
  depends_on: []
  related_documents: []
```

`depends_on` is for documents that are structurally or normatively necessary to interpret, validate, or implement the instance. `related_documents` is for semantically connected documents that are not mandatory dependencies.

Internal relationship values MUST be relative Markdown paths resolved from the directory containing the current document. The author MUST verify that every declared internal path exists.

Optional relationship fields such as `supersedes`, `superseded_by`, `implements`, `implemented_by`, `references`, `derived_from`, and `translated_from` MAY be added only when applicable and according to the Metadata Standard.

### 5.6 Authority

The default for a new document is:

```yaml
ai:
  source_of_truth: false
```

A document MUST use `source_of_truth: true` only when it is intended to be authoritative within a specific conceptual scope and that authority has been identified for governance review. When the value is `true`, `ai.authority_scope` MUST be present, non-empty, and specific.

A document must not claim an authority scope already owned by another approved Source of Truth without an explicit governance decision.

### 5.7 YAML types and prohibited values

Values MUST preserve the types defined by the Metadata Standard:

- booleans MUST be native YAML booleans;
- arrays MUST remain arrays, including empty relationship arrays;
- structured values MUST remain objects;
- versions MUST remain strings;
- dates MUST use the declared ISO-compatible representation.

Required production fields MUST NOT be empty, null, or populated with prohibited placeholders such as `TBD`, `UNKNOWN`, or `N/A`.

The copyable block below contains illustrative markers because it is a template. Every marker and example value MUST be reviewed and replaced before the resulting document is treated as a production or enterprise document.

### 5.8 Security

The document body and its metadata MUST NOT contain passwords, API keys, authentication tokens, session cookies, private credentials, secrets, or ungoverned sensitive personal data.

The `security` domain describes governance expectations. It does not itself enforce access control.

## 6. Copyable Canonical Document Template

The following block is the default authoring template. It is **illustrative and non-normative as an instance**: the Metadata Standard remains the normative authority. Copy it only as a starting point, then replace every document-specific value and remove comments that are not needed in the resulting document.

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
    - canonical
    - documentation

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
  last_review: YYYY-MM-DD
  review_cycle: annual
---

# Document Title

Document content begins here.
```

### 6.1 Required adaptation of the block

Before using the block as a canonical instance, the author MUST:

1. assign a new, unique `document.id`;
2. replace the title with the actual document title;
3. select a valid `document.type` from the controlled vocabulary;
4. select the actual editorial status and compatible lifecycle state;
5. set the document's actual version and keep `version.full` synchronized;
6. identify the accountable organization and owner;
7. set the actual architectural layer and module;
8. replace the illustrative dates with the actual creation, update, and review dates;
9. use relevant lowercase tags without duplicates, accents, secrets, or private data;
10. replace the relationship arrays with the actual dependencies and related documents;
11. confirm the applicable Epoch and Core compatibility range;
12. keep `ai.source_of_truth: false` unless the document has a defined authority scope;
13. add a specific `ai.authority_scope` when `source_of_truth` is `true`;
14. select the actual security classification and confidentiality level;
15. identify the actual audit roles and review cycle;
16. replace the body heading and all document-specific explanatory content.

`AI-MOS-XXX-0000`, `Document Title`, `Module Name`, `YYYY-MM-DD`, and similar values are instructional markers. They MUST NOT remain in a production or enterprise document.

### 6.2 Optional `extensions` block

Client, vendor, or future extension data MAY be added only under an explicit namespace:

```yaml
extensions:
  client:
    namespace: client-identifier
    field: value
```

Extensions MUST remain subordinate to the canonical contract. They MUST NOT change the meaning of canonical fields, claim a canonical authority scope, collide with canonical names, or contain secrets.

### 6.3 Optional relationship fields

Add optional relationship fields only when their semantics apply to the instance:

```yaml
relations:
  depends_on: []
  related_documents: []
  supersedes: []
  superseded_by: []
  implements: []
  implemented_by: []
  references: []
  derived_from: []
  translated_from: []
```

Do not add an optional relationship merely to make the metadata look complete. An empty array is appropriate only when the relationship field is intentionally part of the instance and currently has no values. The required baseline always includes `depends_on` and `related_documents`.

## 7. Authoring Procedure

Create a canonical document in the following order:

### Step 1 — Establish ownership and scope

Determine which governed area owns the document and whether it belongs to System, Foundation, Core, Bootstrap, Client, or Knowledge scope.

Identify the canonical document that owns each requirement the new document will use. Read that document before drafting. Do not promote historical material, an experiment, or an AI inference directly into an authoritative rule.

### Step 2 — Identify dependencies

List the existing documents that are necessary to interpret or implement the new document. Add their repository-relative paths to `relations.depends_on` and verify that each path resolves.

If a required governing document does not exist, record the gap instead of inventing its authority.

### Step 3 — Assign identity and version

Reserve a unique document ID according to the applicable naming conventions. Assign the current Epoch and an initial semantic version appropriate to the document's maturity and governance state.

Keep `document.id` stable. A filename change does not require an ID change.

### Step 4 — Complete metadata domains

Fill the template using the actual values for:

- document identity and type;
- ownership;
- architectural placement;
- lifecycle;
- dates, language, and tags;
- relationships;
- compatibility;
- AI consumer flags and authority;
- security classification;
- audit traceability.

Do not remove a required field to avoid making a decision. If a required value is unknown, keep the document in an appropriate non-production status and record the unresolved decision through the applicable governance process.

### Step 5 — Write the document body

Use deterministic headings and terminology. State the document's purpose, scope, authority boundary, and relationship to other Sources of Truth when those facts are necessary for independent interpretation.

Keep one primary responsibility per document. Reference another Source of Truth instead of duplicating its normative definition.

### Step 6 — Review before promotion

Run the checklist in the next section. Review the document against its dependencies, the System Manifest, the Metadata Standard, and any approved specialized authority.

The document's editorial status MUST reflect its actual approval state. A detailed draft is not an approved standard.

## 8. Canonical Instance Validation Checklist

Before a new instance is submitted for review, confirm the following.

### 8.1 Structural checks

- [ ] The file begins with `---` and contains no preceding content.
- [ ] The closing `---` appears before the first Markdown heading.
- [ ] The YAML parses without duplicate top-level domains.
- [ ] All required domains and fields are present.
- [ ] The recommended domain order is preserved.
- [ ] `extensions`, when used, is namespaced and final.

### 8.2 Identity and semantic checks

- [ ] `document.id` is unique, stable, machine-parseable, and independent of the filename.
- [ ] `document.type` uses the approved controlled vocabulary.
- [ ] `document.status` uses the approved editorial vocabulary.
- [ ] `lifecycle.state` and `document.status` are semantically consistent.
- [ ] `version.epoch`, `version.semantic`, and `version.full` are consistent.
- [ ] The architectural layer matches the governed repository area.
- [ ] The module accurately describes the document's responsibility.

### 8.3 Language and relationship checks

- [ ] The canonical document language is `en-US`.
- [ ] A localized derivative declares its actual language and `translated_from` relationship.
- [ ] `relations.depends_on` and `relations.related_documents` are arrays.
- [ ] Every internal relationship is a relative Markdown path.
- [ ] Every declared internal path resolves to an existing document.
- [ ] Dependencies are necessary and related references are not mislabeled as dependencies.
- [ ] No circular dependency was introduced without explicit architectural justification.

### 8.4 Authority and compatibility checks

- [ ] `ai.source_of_truth` is a native YAML boolean.
- [ ] `ai.authority_scope` is present and specific when `source_of_truth` is `true`.
- [ ] The claimed authority scope does not overlap another approved Source of Truth without a recorded decision.
- [ ] Compatibility declares the applicable Epoch and Core range.
- [ ] Consumer compatibility flags are native YAML booleans.
- [ ] `rag_ready: true` is supported by stable identity, deterministic structure, relationships, language, and safe content.

### 8.5 Security, audit, and governance checks

- [ ] No password, key, token, cookie, credential, secret, or ungoverned sensitive personal data is present.
- [ ] Security classification and confidentiality reflect the actual governance expectation.
- [ ] Audit fields identify the responsible role or function.
- [ ] Review dates and review cycle are real values, not production placeholders.
- [ ] The document status accurately reflects review and approval.
- [ ] Normative changes have an appropriate version update and recorded rationale.
- [ ] Client-specific information is isolated from Core unless explicitly generalized and approved.

The repository currently has no automated metadata validator. Until that tooling exists, this checklist and manual cross-document review are the available validation method; they do not constitute an automated pass.

## 9. Consumer Compatibility

### 9.1 Claude Code

The template gives Claude Code a predictable way to identify a document's purpose, authority, owner, layer, version, lifecycle, language, relationships, and compatibility. Claude Code MUST use valid metadata and applicable Sources of Truth rather than infer these properties from the filename when the metadata is available.

### 9.2 Git and GitHub

The stable ID, explicit version, relative relationships, and audit fields make proposed changes reviewable in repository history once Git is initialized. Generated or inferred metadata MUST NOT silently overwrite authoritative metadata.

### 9.3 Obsidian

Relative Markdown paths, stable IDs, descriptive headings, and predictable domain ordering support navigation and graph-based exploration. The template does not make Obsidian an authority over canonical content.

### 9.4 RAG

The template supports future retrieval by preserving explicit identity, scope, layer, module, version, status, language, tags, security classification, and relationships. `rag_ready: true` describes structural readiness; it does not imply that a vector database, indexer, or RAG pipeline has been implemented.

Compatibility flags describe document properties and intended interfaces. They do not prove that every corresponding integration exists in the current workspace.

## 10. Lifecycle and Change Handling

A template-based document follows the AI-MOS evolution model:

```text
problem
  → research
  → hypothesis
  → implementation
  → test
  → measurement
  → learning
  → documentation
  → standardization
  → reuse
  → new version
```

The following changes require attention to versioning and governance:

- a normative change to the document body;
- a change to metadata semantics or authority;
- a change to dependencies or relationship meaning;
- a change to compatibility assumptions;
- a change that affects client isolation or security expectations.

The following identity fields should be treated as stable after assignment:

- `document.id`;
- `metadata.created`;
- `audit.created_by`.

Changing one of these fields requires explicit governance approval and a recorded reason. Normal lifecycle changes may update title, status, version, lifecycle state, tags, relationships, update metadata, review metadata, and accountable updater as appropriate.

A template revision that changes the metadata contract belongs in the Metadata Standard and requires its governance and versioning process. This document may not silently amend that contract.

## 11. Non-Compliance and Escalation

A document created from this template is non-compliant when it violates the Metadata Standard, the System Manifest, an applicable approved Source of Truth, the language policy, relationship rules, security boundary, client-isolation rule, or governance state.

Non-compliance MUST be corrected before promotion to production or enterprise authority unless an explicit, recorded governance exception exists.

When the author finds a conflict between approved documents, they MUST record the conflict and request architectural resolution. AI systems MUST NOT silently choose an authority based only on filename, recency, or textual confidence.

When a dependency, controlled vocabulary, field, or rule appears to be missing, the author MUST document the gap and route a proposal to the owner of the governing document. They MUST NOT invent an unapproved canonical field or top-level domain in the new document.

## 12. Normative Summary

A canonical AI-MOS document created from this template MUST:

- begin with valid YAML Front Matter;
- use the metadata domains and field contract defined by the Metadata Standard;
- have a stable unique ID independent of filename;
- declare ownership, architectural placement, lifecycle, language, relationships, and compatibility;
- preserve native YAML types;
- distinguish editorial status from operational lifecycle;
- declare authority only within a specific scope;
- use `en-US` unless it is an explicitly identified localized derivative;
- use relative internal document paths;
- avoid secrets and ungoverned sensitive data;
- remain within its single responsibility;
- accurately represent its review and approval state;
- remain compatible with the System Manifest and applicable Sources of Truth.

This template is an implementation aid for governed document authoring. The [AI-MOS Metadata Standard](00_METADATA_STANDARD.md) remains the Source of Truth for the canonical metadata contract, and the [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) remains the Source of Truth for system-level identity, boundaries, principles, and governance direction.

## 13. Template Status

```text
Document: AI-MOS Document Template
Document ID: AI-MOS-FND-0003
Architecture Epoch: E001
Current Version: E001-v0.1.0
Status: In Review
Authority Scope: document-template
Official Documentation Language: en-US
Owner: AI-MOS Architecture
```

This document remains a review candidate until explicit architectural approval is recorded. Its existence does not imply that the System Manifest or Metadata Standard has been formally approved.
