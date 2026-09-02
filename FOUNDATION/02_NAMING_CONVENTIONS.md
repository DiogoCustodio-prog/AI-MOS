---
document:
  id: AI-MOS-FND-0004
  title: AI-MOS Naming Conventions
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
  module: Naming Governance

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
    - naming
    - conventions
    - identifiers
    - filenames
    - directories

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ./00_METADATA_STANDARD.md
    - ./01_DOCUMENT_TEMPLATE.md
  related_documents: []

compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.2.0 <2.0.0"

ai:
  source_of_truth: true
  authority_scope: naming-conventions
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

# AI-MOS Naming Conventions

## 1. Document Status and Authority

This document defines the naming conventions for canonical AI-MOS documents, directories, and governed documentation artifacts.

Its current editorial status is **In Review**. It is the canonical candidate for the `naming-conventions` authority scope and becomes the approved naming authority only after architectural review and explicit approval.

The [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) remains authoritative for system identity, architectural boundaries, permanent principles, and governance direction. The [AI-MOS Metadata Standard](00_METADATA_STANDARD.md) remains authoritative for metadata fields, document identity requirements, and metadata types. The [AI-MOS Document Template](01_DOCUMENT_TEMPLATE.md) remains authoritative for the practical authoring arrangement of a canonical document.

This document specializes those contracts for naming. It MUST NOT redefine the meaning of canonical metadata fields, create a second document identity mechanism, or imply that a proposed filename or artifact directory already exists.

The conventions in this document are normative when expressed with **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, and **MAY**.

## 2. Purpose

Consistent naming makes AI-MOS content:

- identifiable by humans and machines;
- stable under Git-based review and future renames;
- navigable in Obsidian and ordinary file browsers;
- predictable for Claude Code and other AI consumers;
- suitable for future retrieval and indexing;
- resistant to ambiguous duplicates and accidental collisions.

Naming is a governance concern, not merely a cosmetic preference. A name must communicate enough context for navigation without becoming a substitute for metadata, architectural placement, or document authority.

## 3. Scope

This specification applies to naming decisions for:

- canonical Markdown document IDs;
- canonical document titles;
- canonical Markdown filenames;
- canonical directory names;
- decision records;
- agent specifications;
- skill specifications;
- workflow specifications;
- templates and other governed documentation artifacts;
- references to those artifacts in Markdown relationships.

It applies to governed areas:

- `SYSTEM/`;
- `FOUNDATION/`;
- `CORE/`;
- `BOOTSTRAP/`;
- `CLIENTS/`;
- `KNOWLEDGE/`.

Historical exports in `source-material/` and Claude session memory in `memory/` are not retroactively governed by these naming rules. Their existing names MUST be preserved unless a separate preservation decision explicitly authorizes a change. A historical filename is not evidence that a corresponding canonical artifact exists.

This document does not define the complete directory tree. Directory ownership, placement, and creation rules are defined by [AI-MOS Directory Structure](03_DIRECTORY_STRUCTURE.md).

## 4. Naming Layers

AI-MOS uses several naming layers with different responsibilities:

| Layer | Purpose | Authority |
| --- | --- | --- |
| `document.id` | Stable logical identity across the document lifecycle | Metadata Standard, specialized by this document |
| `document.title` | Human-readable semantic name | Metadata Standard and document author |
| Filename | Repository navigation and tool compatibility | This document |
| Directory path | Architectural and operational placement | Directory Structure |
| Heading | Human-readable body navigation | Document authoring and documentation principles |

These layers MUST remain distinct.

In particular:

```text
document.id != filename != directory path
```

A rename or move MAY change the filename or path while preserving `document.id`. A change of conceptual identity MUST NOT be hidden behind a simple rename; it requires a new document ID and an explicit relationship such as `supersedes` or `derived_from` when applicable.

## 5. General Character Rules

Canonical names MUST be portable across common filesystems, Git, GitHub, Obsidian, Claude Code, and future indexing tools.

Unless a more specific rule in this document applies, a canonical name MUST:

- use ASCII characters;
- avoid accents and other locale-dependent characters;
- avoid leading or trailing whitespace;
- avoid repeated separators;
- avoid control characters;
- avoid path traversal elements such as `.` and `..` as names;
- avoid reserved filesystem names such as `CON`, `PRN`, `AUX`, and `NUL` when a platform may interpret them specially;
- avoid names that differ only by letter case;
- avoid ambiguous abbreviations when a governed vocabulary exists.

Canonical names MUST NOT contain secrets, credentials, access tokens, personal data, or client-confidential facts.

Names SHOULD be concise, semantically specific, and stable. A name SHOULD describe the artifact's responsibility rather than its current implementation detail.

## 6. Document Identity

### 6.1 Canonical ID format

Every canonical AI-MOS document MUST have a unique `document.id` assigned according to the Metadata Standard.

The recommended format is:

```text
AI-MOS-<DOMAIN>-<SEQUENCE>
```

The current machine-parseable pattern is:

```text
^AI-MOS-[A-Z]{3}-[0-9]{4}$
```

Examples:

```text
AI-MOS-SYS-0001
AI-MOS-FND-0004
AI-MOS-COR-0010
```

The ID MUST:

- be unique across the AI-MOS ecosystem;
- remain stable for the lifetime of the document;
- contain exactly one governed three-letter domain code in the current format;
- contain a four-digit zero-padded sequence in the current format;
- contain no spaces, accents, or additional separators;
- remain independent of filename, title, directory, and language;
- never be reassigned after retirement.

The sequence is an identity allocation sequence, not a count of files in a directory. Deleting, archiving, superseding, or renaming a document MUST NOT make its sequence available for reuse.

### 6.2 Initial domain code catalog

The following catalog is the current proposed vocabulary for the E001 architecture:

| Code | Primary scope | Example use |
| --- | --- | --- |
| `SYS` | System identity and constitutional governance | System Manifest |
| `FND` | Foundation contracts and standards | Metadata Standard |
| `COR` | Reusable AI-MOS Core assets | Core specification |
| `BST` | Bootstrap initialization and deployment assets | Bootstrap procedure |
| `CLI` | Client Implementation material | Client-specific specification |
| `KNO` | Governed knowledge and evolution records | Decision or lesson |
| `OPS` | Cross-cutting operational specifications | Operational rule |
| `INT` | Integration contracts and specifications | Integration contract |

These codes identify the primary naming domain; they do not replace `architecture.layer` or `architecture.module`. A new code MUST be introduced through a versioned governance change and MUST be checked against the three-letter ID pattern.

A document that concerns multiple areas MUST use the code for its primary authority and responsibility, not an arbitrary code for every subject mentioned in its body.

### 6.3 ID allocation and uniqueness

Before creating a canonical document, the author MUST:

1. identify the document's primary authority scope;
2. select the applicable domain code;
3. allocate a sequence that is not already used;
4. verify that no historical or retired canonical ID is being reused;
5. record the ID in the new document's front matter;
6. check for duplicates across all governed areas.

The current workspace has no automated duplicate-ID validator. Until one exists, duplicate detection is a manual repository-wide review responsibility.

A future validator SHOULD detect:

- duplicate active IDs;
- duplicate IDs involving archived or superseded documents;
- malformed domain codes;
- malformed sequences;
- IDs that do not agree with the declared architecture or authority scope;
- reuse of retired IDs.

### 6.4 Identity changes

The following actions MUST preserve `document.id` when the conceptual document remains the same:

- correcting a filename;
- moving the document to an approved location;
- changing a human-readable title without changing the concept;
- translating the document into an identified derivative;
- correcting non-identity metadata.

The following conditions MAY require a new ID:

- the document's primary responsibility changes materially;
- the authority scope is split into independent concepts;
- the document is replaced by a separate conceptual object rather than revised;
- governance explicitly determines that the original identity must be retired.

When a new ID is assigned, the relationship to the former document MUST be recorded when the relationship vocabulary applies.

## 7. Document Titles

`document.title` is the authoritative human-readable title in front matter. The first top-level Markdown heading SHOULD match it exactly unless a documented editorial reason requires a different presentation.

A canonical title MUST:

- be written in the document's declared language;
- describe the document's actual semantic responsibility;
- avoid version numbers, dates, status labels, or path fragments unless they are part of the concept itself;
- avoid claiming approval, authority, or implementation status that the metadata does not support;
- avoid unexplained acronyms when a governed title is available;
- remain consistent with the body and filename.

Recommended form for Foundation specifications:

```text
AI-MOS <Subject>
```

Examples:

```text
AI-MOS Metadata Standard
AI-MOS Document Template
AI-MOS Naming Conventions
```

A title change does not change `document.id`, but a material change in meaning requires the identity analysis described in Section 6.4.

## 8. Markdown Filenames

### 8.1 General canonical filename rules

Canonical Markdown filenames MUST:

- use the `.md` extension in lowercase;
- use ASCII characters only;
- use uppercase letters for governed document words;
- use underscores as word separators;
- avoid spaces, accents, and punctuation not required by a defined artifact pattern;
- be semantically recognizable without relying on a numeric ID;
- be unique within their directory without case-only distinctions;
- remain short enough for reliable navigation and tool display.

Canonical filenames SHOULD match the document title semantically but MUST NOT be required to duplicate the title character-for-character. The `document.id` remains authoritative when filename and metadata differ.

### 8.2 Ordered Foundation filenames

Foundation documents that form an intentional construction sequence use a two-digit navigation prefix followed by an uppercase descriptive name:

```text
NN_DESCRIPTIVE_NAME.md
```

Examples:

```text
00_METADATA_STANDARD.md
01_DOCUMENT_TEMPLATE.md
02_NAMING_CONVENTIONS.md
03_DIRECTORY_STRUCTURE.md
04_DOCUMENTATION_PRINCIPLES.md
05_GOVERNANCE_APPROVAL_PROCESS.md
```

The numeric prefix communicates reading order only. It is not the document ID, does not replace the front matter, and MUST NOT be interpreted as a global sequence.

A change to the sequence prefix does not by itself require a new `document.id`. When a prefix changes, all affected internal links and navigation references MUST be reviewed.

### 8.3 General canonical filenames

For canonical documents outside an ordered sequence, use a descriptive uppercase snake-case filename:

```text
DESCRIPTIVE_NAME.md
```

Examples:

```text
SYSTEM_MANIFEST.md
PROJECT_SPECIFICATION.md
DEVELOPMENT_RULES.md
```

`README.md` MAY be used for repository navigation or a governed area overview. A README that defines normative AI-MOS rules MUST comply with the Metadata Standard and receive a canonical ID.

### 8.4 Filename stability and renames

A filename SHOULD remain stable after publication to reduce link churn. A rename MAY be performed when it improves semantic accuracy, removes ambiguity, or corrects a naming violation.

A rename MUST:

- preserve `document.id` when the concept is unchanged;
- update all relative references that point to the old path;
- preserve or update the title only when semantically justified;
- be recorded in the repository history once Git is available;
- be reviewed for Obsidian and future index compatibility.

A filename MUST NOT be used to silently change a document's authority or architectural layer.

## 9. Directory Names

Canonical top-level directory names are governed by the System Manifest and currently use uppercase ASCII names:

```text
SYSTEM/
FOUNDATION/
CORE/
BOOTSTRAP/
CLIENTS/
KNOWLEDGE/
```

Canonical directory names MUST:

- use uppercase ASCII letters for the established top-level areas;
- use underscores for multi-word names when a nested directory is approved;
- avoid spaces, accents, and hyphens unless an approved compatibility rule requires one;
- represent a stable architectural or operational responsibility;
- not encode document status, version, or temporary workflow state;
- not duplicate an existing area under a case variant;
- not contain secrets or client-sensitive facts in Core or Foundation paths.

A directory name is a placement signal, not a Source of Truth. The front matter's `architecture.layer`, `architecture.module`, and relationships remain authoritative for document semantics.

Auxiliary paths have separate preservation rules:

- `source-material/` contains historical source material and is not a canonical architecture layer;
- `source-material/chatgpt-exports/` contains preserved exports and MUST NOT be renamed or edited as part of ordinary canonical documentation work;
- `memory/` contains local Claude session memory and is not AI-MOS canonical knowledge.

These existing auxiliary names are preserved even though they do not use the canonical naming style.

## 10. Names for Specialized Artifacts

The following patterns are conventions for future governed artifacts. They describe names; they do not claim that the corresponding directories, automation, validators, or runtime capabilities currently exist.

### 10.1 Decision records

Decision records SHOULD use:

```text
ADR-YYYYMMDD-short-decision-name.md
```

The date is a navigation aid and does not replace the stable `document.id`. If multiple decisions are created on the same date, the short name MUST distinguish them. A decision record that becomes a canonical document MUST use the full AI-MOS front matter contract.

### 10.2 Agent specifications

Agent specifications SHOULD use:

```text
AGENT-short-agent-name.md
```

The name SHOULD identify the agent's mission or role, not a model vendor or temporary implementation. Examples:

```text
AGENT-content-strategist.md
AGENT-metadata-curator.md
```

### 10.3 Skill specifications

Skill specifications SHOULD use:

```text
SKILL-short-skill-name.md
```

Examples:

```text
SKILL-document-review.md
SKILL-campaign-briefing.md
```

### 10.4 Workflow specifications

Workflow specifications SHOULD use:

```text
WORKFLOW-short-workflow-name.md
```

Examples:

```text
WORKFLOW-document-promotion.md
WORKFLOW-client-bootstrap.md
```

### 10.5 Templates and operational artifacts

Reusable Markdown templates SHOULD use:

```text
TEMPLATE-short-template-name.md
```

Other governed artifact patterns MUST be defined by the owning specification before they are used at scale. A proposed pattern MUST NOT be presented as an existing repository capability.

## 11. Relationship and Link Naming

Internal document relationships in front matter MUST use repository-relative Markdown paths, as required by the Metadata Standard. The path is a reference to a file location; it is not the document's logical identity.

Body links SHOULD:

- use relative paths for internal Markdown documents;
- use the document's human-readable title as link text when practical;
- avoid link text that implies approval or authority not present in metadata;
- be updated when a referenced filename changes;
- avoid links to preserved historical exports when a reviewed canonical Source of Truth exists, unless the historical source is intentionally cited as evidence.

Examples:

```markdown
[AI-MOS Metadata Standard](00_METADATA_STANDARD.md)
[AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md)
```

A link label, filename, or path MUST NOT override authoritative front matter.

## 12. Naming and Architectural Boundaries

Names MUST support the separation between:

- System governance;
- Foundation contracts;
- reusable Core intellectual property;
- Bootstrap initialization assets;
- isolated Client Implementations;
- governed Knowledge records.

Client-specific names, company identifiers, campaign names, or private operational facts MUST NOT be placed in reusable Core filenames or IDs unless the artifact is explicitly a client implementation or a generalized reference with approval.

A client directory or filename MUST NOT be used to imply that its content is reusable Core knowledge. Conversely, a Core filename MUST NOT conceal client-specific content.

The `CLI` domain code is appropriate for a Client Implementation document. It does not authorize copying that document into `CORE/`.

## 13. Compatibility Guidance

### 13.1 Claude Code

Predictable names help Claude Code locate and classify documents, but Claude Code MUST use front matter and applicable Sources of Truth rather than infer identity from a filename alone. A name is an input to navigation, not a license to invent missing metadata.

### 13.2 Git and GitHub

Portable ASCII names, stable paths, and focused renames reduce merge conflicts and make review history easier to understand. A future Git workflow SHOULD treat a rename that preserves `document.id` as an identity-preserving change.

The current workspace is not a Git repository. These are compatibility goals and conventions, not evidence that Git history, branches, hooks, or CI validation are currently available.

### 13.3 Obsidian

Relative Markdown links and descriptive filenames support graph navigation. Case-only filename differences SHOULD be avoided because filesystem and indexing behavior may vary by platform.

### 13.4 RAG and indexing

Stable IDs, descriptive names, explicit layer names, and predictable artifact prefixes provide useful retrieval signals. A filename alone is never sufficient for authority, lifecycle, language, or security classification. Future indexing MUST preserve `document.id` as the primary logical key when available.

## 14. Examples

### 14.1 Valid canonical names

```text
SYSTEM/SYSTEM_MANIFEST.md
FOUNDATION/00_METADATA_STANDARD.md
FOUNDATION/02_NAMING_CONVENTIONS.md
CORE/PROJECT_SPECIFICATION.md
KNOWLEDGE/ADR-20260811-document-identity.md
```

The last example is valid as a proposed decision-record filename only when the path has been approved for that purpose and the document has compliant metadata.

### 14.2 Invalid or discouraged names

```text
Foundation Metadata Standard.md       # spaces and mixed style
fundação.md                           # accents and unclear responsibility
SYSTEM/system_manifest.md             # case inconsistency
AI-MOS-FND-0004.md                    # hides the semantic filename
02.naming.conventions.md              # wrong separator and lowercase style
FINAL_APPROVED_VERSION.md             # encodes status in the filename
client-secret-api-key.md              # secret or sensitive content in a name
```

The invalid examples are naming violations or discouraged patterns; they are not claims about files currently present in the workspace.

## 15. Exceptions and Governance

An exception MAY be granted when a tool, external standard, migration, preservation requirement, or client boundary makes the standard naming pattern unsuitable.

An exception MUST:

- identify the affected path or artifact class;
- state the reason and compatibility impact;
- preserve stable `document.id` rules whenever possible;
- avoid creating ambiguity with an existing canonical name;
- be recorded in an approved decision or governance record;
- define whether the exception is temporary, permanent, or migration-only.

Historical preservation is an exception category. Preserving source material does not make the historical names canonical, and canonical work MUST NOT rewrite the historical exports merely to make them stylistically consistent.

If a naming rule conflicts with an approved higher-authority document, the conflict MUST be escalated. AI MUST NOT silently resolve the conflict by changing IDs, filenames, or directories.

## 16. Versioning and Change Handling

A wording clarification that does not change a naming rule MAY be a PATCH revision. A backward-compatible naming addition, such as a new specialized artifact pattern or governed domain code, is a MINOR revision. A change to the ID format, identity semantics, established top-level names, or non-reusable ID rule is a MAJOR revision within the current Epoch unless an Epoch change is required.

Changes to `document.id` allocation, domain codes, filename semantics, or directory naming MUST be reviewed against:

- the Metadata Standard;
- the Document Template;
- the Directory Structure;
- existing canonical relationships;
- historical preservation requirements;
- future validation and indexing needs.

A naming revision MUST NOT retroactively rename preserved historical material without an explicit preservation decision.

## 17. Manual Review Checklist

Before creating or promoting a governed artifact, confirm:

- [ ] The artifact has a clearly identified primary responsibility.
- [ ] The correct architectural area and naming domain have been selected.
- [ ] The `document.id` follows the current format and is unique.
- [ ] The ID is not copied from another document and has not been reused.
- [ ] The ID is independent of the filename, title, and path.
- [ ] The title accurately describes the document's semantic purpose.
- [ ] The filename uses the correct extension, separators, case, and artifact pattern.
- [ ] An ordered prefix is used only as a navigation aid.
- [ ] The filename does not encode status, version, or temporary workflow state.
- [ ] The directory is an approved architectural or operational location.
- [ ] The path does not expose secrets or client-confidential facts.
- [ ] Existing auxiliary source material and Claude memory have not been renamed or edited unintentionally.
- [ ] Internal links and relationship paths use relative Markdown paths.
- [ ] A rename preserves `document.id` when the concept remains the same.
- [ ] A conceptual split or replacement has an explicit identity and relationship decision.
- [ ] The name is portable for Claude Code, GitHub, Obsidian, and future indexing.
- [ ] Any exception has a recorded reason and approval path.

The repository currently has no automated naming validator. This checklist is a manual review aid, not an automated validation result.

## 18. Normative Summary

AI-MOS naming MUST preserve the following principles:

1. `document.id` is the stable logical identity.
2. IDs follow the governed `AI-MOS-<DOMAIN>-<SEQUENCE>` format and are never reused.
3. Domain codes are controlled vocabulary, not ad hoc abbreviations.
4. Titles describe semantic responsibility.
5. Filenames support navigation but do not define authority or identity.
6. Ordered prefixes communicate reading order only.
7. Canonical names are portable, deterministic, and free of secrets.
8. Directory names communicate approved placement but do not replace metadata.
9. Client-specific content remains isolated from reusable Core content.
10. Historical source material remains preserved and non-canonical.
11. Renames preserve identity when the concept is unchanged and update relationships.
12. Exceptions require recorded governance rather than silent inference.

This document defines naming conventions for the current E001 architecture. It remains a review candidate until explicit architectural approval is recorded.

## 19. Naming Conventions Status

```text
Document: AI-MOS Naming Conventions
Document ID: AI-MOS-FND-0004
Architecture Epoch: E001
Current Version: E001-v0.1.0
Status: In Review
Authority Scope: naming-conventions
Official Documentation Language: en-US
Owner: AI-MOS Architecture
```
