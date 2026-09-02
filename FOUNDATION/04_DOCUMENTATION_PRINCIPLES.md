---
document:
  id: AI-MOS-FND-0006
  title: AI-MOS Documentation Principles
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
  module: Documentation Governance

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
    - documentation
    - principles
    - governance
    - knowledge
    - quality

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ./00_METADATA_STANDARD.md
    - ./01_DOCUMENT_TEMPLATE.md
    - ./02_NAMING_CONVENTIONS.md
    - ./03_DIRECTORY_STRUCTURE.md
  related_documents: []

compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.2.0 <2.0.0"

ai:
  source_of_truth: true
  authority_scope: documentation-principles
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

# AI-MOS Documentation Principles

## 1. Document Status and Authority

This document defines the principles for creating, reviewing, maintaining, and evolving canonical AI-MOS documentation.

Its current editorial status is **In Review**. It is the canonical candidate for the `documentation-principles` authority scope and becomes the approved documentation-principles authority only after architectural review and explicit approval.

The [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) remains authoritative for system identity, boundaries, permanent principles, and governance direction. The [AI-MOS Metadata Standard](00_METADATA_STANDARD.md) remains authoritative for metadata. The [AI-MOS Document Template](01_DOCUMENT_TEMPLATE.md), [AI-MOS Naming Conventions](02_NAMING_CONVENTIONS.md), and [AI-MOS Directory Structure](03_DIRECTORY_STRUCTURE.md) remain authoritative for their specialized subjects.

This document defines how AI-MOS documentation should be reasoned about and maintained. It MUST NOT silently replace the contracts owned by those documents or turn an unvalidated experiment into an approved rule.

The principles in this document are normative when expressed with **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, and **MAY**.

## 2. Documentation as System Infrastructure

AI-MOS is documentation-first and AI-native. Markdown is not merely a report about an implementation; it is the primary governed representation of system knowledge, operating models, decisions, contracts, and reusable instructions.

Documentation enables AI-MOS to:

- preserve institutional knowledge;
- make reasoning inspectable;
- coordinate human and AI work;
- convert validated practices into reusable assets;
- support future automation and retrieval;
- expose uncertainty, ownership, dependencies, and review state;
- evolve without silently losing historical context.

Durable capabilities SHOULD be documented before they are automated or treated as reusable system behavior. Documentation does not prove that an implementation exists. Conversely, a tool or experiment does not become an architectural capability until it is documented, reviewed, and approved within the correct boundary.

## 3. Scope

These principles apply to canonical documentation in:

- `SYSTEM/`;
- `FOUNDATION/`;
- `CORE/`;
- `BOOTSTRAP/`;
- `CLIENTS/`;
- `KNOWLEDGE/`.

They also guide the treatment of source material, client evidence, proposals, experiments, and future documentation artifacts.

They do not turn historical exports in `source-material/` or local Claude memory in `memory/` into canonical knowledge. Those areas retain their separate preservation and operational roles.

## 4. Documentation Precedes Implementation

A reusable capability SHOULD have an explicit documented contract before durable implementation begins.

The minimum contract should make clear, as applicable:

- purpose and scope;
- ownership;
- inputs and outputs;
- dependencies;
- constraints and security boundaries;
- lifecycle and review state;
- compatibility assumptions;
- measurement or acceptance criteria;
- authority and relationship to existing Sources of Truth.

This principle does not prohibit exploratory coding, prototyping, or research. It requires that a prototype be labeled as an experiment or proposal and not be represented as a production capability before the applicable review.

A document may describe a planned capability without claiming that its tools or implementation already exist. Statements about current workspace state MUST be verified against the actual repository.

## 5. One Source of Truth per Scope

Each canonical concept MUST have one authoritative Source of Truth within a declared `ai.authority_scope`.

Other documents MUST:

- reference the owning Source of Truth;
- avoid copying its normative definition;
- preserve their own narrower responsibility;
- state a conflict rather than silently selecting a preferred interpretation.

`ai.source_of_truth: true` grants authority only within the declared scope. It does not grant universal authority over AI-MOS.

If two approved documents appear to own the same scope, the conflict MUST be resolved through governance. AI MUST NOT choose based solely on recency, filename, document length, or textual confidence.

A document that is informative, derivative, translated, experimental, or client-specific MUST NOT claim a canonical authority scope without an explicit decision.

## 6. Modularity and Single Responsibility

Each canonical document SHOULD have one primary responsibility and enough context for independent interpretation.

A document SHOULD:

- define its purpose and boundaries;
- name its owner and architectural layer;
- reference dependencies instead of reproducing them;
- separate normative rules from examples and commentary;
- use headings that support direct navigation;
- avoid becoming a monolithic playbook for unrelated subjects.

When a subject requires multiple documents, split it by stable responsibility and connect the documents through explicit relationships. A shorter document is not automatically better; the goal is coherent modularity, not arbitrary fragmentation.

The same principle applies to agents, skills, workflows, templates, and knowledge records. Each should have explicit responsibility, inputs, outputs, and escalation boundaries when those concepts are applicable.

## 7. Deterministic Knowledge

Canonical documentation MUST be sufficiently deterministic for humans and machines to interpret it consistently.

Deterministic documentation uses:

- stable document identity;
- governed metadata and controlled vocabulary;
- explicit language;
- predictable headings and terminology;
- relative internal relationships;
- unambiguous normative verbs;
- explicit status and lifecycle;
- stated assumptions and boundaries;
- reproducible examples where examples are needed.

A document MUST distinguish:

- normative requirements;
- recommendations;
- illustrative examples;
- proposals;
- unresolved questions;
- historical evidence;
- implementation status.

AI systems MUST not fill missing authority, dates, dependencies, or capabilities through silent inference. When a required fact is unknown, the document or decision MUST expose the gap and remain in an appropriate non-production state.

## 8. Official Language and Editorial Clarity

The official language of canonical AI-MOS documentation is `en-US`.

Canonical documents in the governed areas MUST declare:

```yaml
metadata:
  language: en-US
```

A localized derivative MAY use another language only when it:

1. declares its actual language;
2. identifies the canonical en-US document from which it derives;
3. remains structurally aligned with the canonical document;
4. does not silently replace the en-US Source of Truth.

Historical exports and operational conversations may use other languages because they are not canonical AI-MOS documents.

Canonical prose SHOULD be clear, precise, and direct. Avoid ambiguous pronouns, unexplained jargon, excessive rhetorical language, and claims stronger than the available evidence. A document should be understandable without requiring the reader to reconstruct hidden transcript context.

## 9. Traceability and Evidence

A governed document SHOULD make its origin and rationale traceable when the content affects architecture, governance, security, compatibility, client isolation, or long-term operations.

Traceability may include:

- `relations.depends_on` and `related_documents`;
- decision records;
- knowledge and evolution records;
- audit metadata;
- explicit source-material references;
- affected-document lists;
- measurement results;
- migration or supersession relationships.

Source material is evidence, not authority. A historical export may explain why an idea was considered, but only a reviewed canonical document can define the current rule.

When a change affects an authoritative Source of Truth, the author MUST show:

- the rationale;
- the affected files and scopes;
- compatibility and migration implications;
- the requested approval state;
- the validation performed and any remaining gaps.

## 10. Human Review and Accountability

AI may research, draft, classify, summarize, compare, validate, and propose documentation changes. AI MUST NOT silently promote a proposal, experiment, or client result into an authoritative Source of Truth.

Human review is required before:

- approving a new canonical authority;
- changing architectural boundaries;
- changing metadata semantics or controlled vocabulary;
- promoting a client-specific result into Core;
- introducing a new directory or artifact class with architectural implications;
- changing security or isolation rules;
- declaring a previously unimplemented capability as available.

The editorial field `document.status` MUST represent the actual approval state. `lifecycle.state` MUST represent operational status. They MUST NOT be collapsed into one label.

A document may be detailed and internally consistent while still being `Draft`, `Proposed`, or `In Review`. Completeness is not approval.

## 11. Status, Lifecycle, and Maturity

Every canonical document MUST distinguish at least three questions:

1. Has the document been editorially approved?
2. Is the document operationally current?
3. How mature is the asset or capability?

These questions are represented by:

- `document.status` for editorial approval;
- `lifecycle.state` for operational state;
- `lifecycle.maturity` for maturity level.

Examples of semantically coherent combinations include:

| Editorial status | Operational state | Interpretation |
| --- | --- | --- |
| `Draft` | `active` | Current working draft, not approved |
| `In Review` | `active` | Candidate under review |
| `Approved` | `active` | Approved and currently used |
| `Deprecated` | `deprecated` | Retained but not recommended for new use |
| `Superseded` | `superseded` | Replaced by another document |
| `Archived` | `archived` | Preserved for historical reference |
| `Rejected` | `inactive` | Not accepted and not operational |

A document MUST NOT claim current approved authority through prose when its metadata says it is unapproved, superseded, archived, or rejected.

## 12. Security and Safe Content

AI-MOS Markdown is not a secret store.

Canonical and auxiliary documentation MUST NOT contain:

- passwords;
- API keys;
- authentication tokens;
- session cookies;
- private credentials;
- secret material;
- ungoverned sensitive personal data.

Security classification metadata describes governance expectations; it does not enforce access control.

Documentation SHOULD use abstract examples, redacted values, and placeholders that are explicitly identified as illustrative. Production metadata MUST NOT use prohibited placeholders such as `TBD`, `UNKNOWN`, or `N/A` to conceal missing required decisions.

Client-specific confidential facts MUST remain in the appropriate Client Implementation or governed restricted record. They MUST NOT be copied into Core, Foundation, public examples, or shared templates without explicit authorization and generalization.

## 13. Client Isolation and Vendor Independence

AI-MOS has separate boundaries for Core, Bootstrap, and Client Implementations.

Core documentation MUST remain customer-independent. Client documentation MAY contain organization-specific context, branding, campaigns, integrations, metrics, operational memory, and experiments within its isolated boundary.

A validated client result is evidence for possible reuse, not automatically a Core rule. The promotion path is:

```text
client problem
  → evidence
  → research
  → hypothesis
  → implementation
  → test
  → measurement
  → learning
  → generalization
  → review
  → approved reusable asset
```

Vendor tools and providers are implementation environments or integrations, not permanent architectural authorities. Documentation MAY specify an integration when the integration is part of the governed scope, but it MUST distinguish a vendor-specific implementation from a vendor-independent contract.

A document MUST NOT turn an available tool into a system capability without evidence that the tool is configured, supported, and within the applicable boundary.

## 14. Experiments, Proposals, and Rules

AI-MOS MUST distinguish the following states of knowledge:

- **Historical source material** — preserved evidence from prior work;
- **Observation** — a recorded fact about an environment or result;
- **Experiment** — a bounded hypothesis and test;
- **Proposal** — a candidate rule or design awaiting review;
- **Approved rule** — a governed normative requirement;
- **Implementation** — an actual capability verified in the workspace;
- **Lesson or pattern** — a documented learning that may inform future work.

A transcript, example, screenshot, command, architecture sketch, or successful one-off result MUST NOT be presented as an implemented capability without verification.

Experiments SHOULD record their hypothesis, scope, inputs, method, outcome, limitations, and next decision. Proposals SHOULD identify their owner, rationale, affected Sources of Truth, and requested review. Approved rules SHOULD identify the document that owns them.

When evidence conflicts with a current Source of Truth, preserve the evidence and route the conflict for review. Do not silently edit the Source of Truth to match the evidence.

## 15. Markdown, Git, Obsidian, and RAG

### 15.1 Markdown

Markdown is the primary canonical knowledge representation. Canonical files MUST use the metadata contract and SHOULD use focused headings, relative links, deterministic terminology, and explicit examples.

### 15.2 Git and GitHub

Git provides history, review, and auditability in this workspace. Documentation MUST NOT claim that pull requests, hooks, CI checks, builds, linting, automated tests, or an automated metadata validator exist unless they are actually configured and verified.

Normative changes SHOULD be reviewed as focused, traceable changes with preserved history in Git.

### 15.3 Obsidian

Obsidian MAY provide navigation and graph exploration. It is an interface, not an independent Source of Truth. Relative links and stable IDs SHOULD be preserved so navigation remains useful across compatible tools.

### 15.4 RAG and future retrieval

Canonical documentation SHOULD be ready for future retrieval through:

- stable identity;
- explicit language;
- architecture and lifecycle metadata;
- security classification;
- deterministic headings;
- clear relationships;
- scope-aware authority;
- separation of canonical, client, historical, and session content.

`rag_ready: true` indicates structural suitability. It does not mean that embeddings, a vector database, an indexer, a knowledge graph, or a retrieval pipeline has been implemented.

A future retrieval system MUST preserve authority, language, lifecycle, security, and client-boundary metadata rather than flattening all Markdown into undifferentiated content.

## 16. Documentation Quality Principles

A canonical document SHOULD satisfy the following quality properties:

### 16.1 Correctness

Claims match the governing documents, actual workspace, and available evidence. Unknowns are identified rather than invented.

### 16.2 Completeness

The document includes the context required for its declared responsibility, dependencies, ownership, and review state without duplicating unrelated contracts.

### 16.3 Coherence

Terms, statuses, versions, links, metadata, and body content do not contradict one another or the applicable Sources of Truth.

### 16.4 Clarity

A human reader can understand purpose, scope, authority, and actions without reconstructing hidden context.

### 16.5 Determinism

Two qualified authors should produce materially compatible interpretations from the same requirements.

### 16.6 Maintainability

The document is modular, versionable, navigable, and small enough to review without losing its primary responsibility.

### 16.7 Security

The document contains no secrets or ungoverned sensitive information and respects client boundaries.

### 16.8 Machine readability

Metadata, relationships, headings, and terminology are structured for future automated inspection without making unsupported claims about current tooling.

## 17. Evolution Loop

AI-MOS uses the following evolution loop:

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

Each stage has a distinct purpose:

1. **Problem** — identify a real operational or architectural need.
2. **Research** — gather evidence and understand constraints.
3. **Hypothesis** — state the proposed explanation or solution.
4. **Implementation** — apply the hypothesis in a bounded context.
5. **Test** — inspect behavior against defined expectations.
6. **Measurement** — collect evidence of outcome and limitations.
7. **Learning** — record what changed in understanding.
8. **Documentation** — make the learning explicit and traceable.
9. **Standardization** — generalize and govern the reusable rule.
10. **Reuse** — apply the approved asset in an appropriate boundary.
11. **New version** — version the affected document or artifact when its contract changes.

The loop does not authorize automatic promotion. Standardization requires appropriate human review and must respect Core, Bootstrap, Client, and Source-of-Truth boundaries.

## 18. Compatibility with AI-MOS Layers

Documentation principles apply differently by layer:

- `SYSTEM/` documents define identity and constitutional direction.
- `FOUNDATION/` documents define cross-cutting contracts.
- `CORE/` documents define reusable customer-independent capabilities.
- `BOOTSTRAP/` documents define initialization and deployment behavior.
- `CLIENTS/` documents define isolated organization-specific implementations.
- `KNOWLEDGE/` documents record evidence, decisions, lessons, and evolution.

A document MUST remain within its layer's responsibility and MUST declare dependencies appropriate to its interpretation. A Knowledge record may describe a Core proposal, but it does not become a Core specification by describing it. A Client document may use a Core pattern, but it does not change the Core pattern by specializing it locally.

When a requirement does not have an appropriate owner, the gap MUST be documented and routed for architectural decision. The author MUST NOT place the rule in a convenient directory solely to avoid an unresolved ownership question.

## 19. Manual Quality Checklist

Before submitting a canonical document for review, confirm:

- [ ] The document has one primary responsibility.
- [ ] Its purpose, scope, owner, layer, and authority boundary are explicit.
- [ ] It begins with valid YAML Front Matter and follows the Metadata Standard.
- [ ] Its ID, title, filename, path, version, status, lifecycle, and language are coherent.
- [ ] Canonical language is `en-US`, or the derivative language and source are explicitly identified.
- [ ] Required dependencies and related references are correctly classified.
- [ ] Internal paths are relative and resolve from the current document.
- [ ] It references Sources of Truth instead of duplicating their normative definitions.
- [ ] It distinguishes requirements, recommendations, examples, proposals, experiments, and observations.
- [ ] Claims about current files, commands, integrations, validators, or runtime behavior have been verified.
- [ ] It contains no secrets or ungoverned sensitive personal data.
- [ ] Client-specific information remains isolated from Core and other clients.
- [ ] Vendor-specific details are not presented as permanent architecture without an explicit decision.
- [ ] Approval status reflects actual human review.
- [ ] The document is deterministic, understandable, and suitable for future retrieval.
- [ ] Normative changes have a versioning and traceability rationale.
- [ ] Remaining gaps and uncertainties are visible.

The current workspace has no automated documentation-quality validator. This checklist and manual cross-document review are the available validation method; neither is an automated pass.

## 20. Exceptions and Governance

An exception to these principles MAY be accepted for historical preservation, exploratory work, client-specific requirements, legal obligations, migration, or an explicitly bounded architectural experiment.

An exception MUST:

- identify the principle and affected scope;
- explain the reason and expected duration;
- identify security, compatibility, isolation, and maintenance effects;
- preserve the document's actual status and lifecycle;
- be recorded in an appropriate knowledge or decision record;
- receive the required human approval before it is treated as normative.

Exceptions MUST NOT be used to conceal missing ownership, unverified capabilities, secrets, broken relationships, or unauthorized client contamination.

If this document conflicts with an approved higher-authority specification, the conflict MUST be escalated. AI MUST NOT silently modify the Source of Truth or treat an unapproved interpretation as final.

## 21. Versioning and Change Handling

A clarification that does not alter a principle MAY be a PATCH revision. A backward-compatible addition of a principle or quality criterion is a MINOR revision. A change to the meaning of documentation authority, Source-of-Truth behavior, client isolation, language policy, or the distinction between evidence and approved rules is a MAJOR revision within the current Epoch unless an Epoch change is required.

Changes MUST be reviewed against:

- the System Manifest;
- the Metadata Standard;
- the Document Template;
- the Naming Conventions;
- the Directory Structure;
- existing approved or review-stage documents;
- actual workspace capabilities and boundaries.

A revision MUST preserve historical rationale and MUST NOT turn the presence of a rule in a historical export into evidence that it is currently approved.

## 22. Normative Summary

AI-MOS documentation MUST:

1. precede durable implementation of reusable capabilities where a contract is required;
2. maintain one Source of Truth per declared scope;
3. preserve modularity and single responsibility;
4. be deterministic, explicit, and suitable for human and machine interpretation;
5. use `en-US` for canonical documentation;
6. preserve traceability to decisions, evidence, dependencies, and review state;
7. require human approval for authority, architectural, security, isolation, and promotion changes;
8. distinguish editorial status from operational lifecycle and maturity;
9. exclude secrets and ungoverned sensitive data;
10. isolate Client Implementation content from Core and other clients;
11. distinguish experiments, proposals, observations, evidence, implementations, and approved rules;
12. treat Markdown as canonical knowledge while keeping Git, Obsidian, and RAG in their proper roles;
13. follow the documented evolution loop from problem through reuse and new version;
14. expose gaps and uncertainty instead of inventing capabilities or authority.

These principles define the documentation discipline for the current E001 architecture. This document remains a review candidate until explicit architectural approval is recorded.

## 23. Documentation Principles Status

```text
Document: AI-MOS Documentation Principles
Document ID: AI-MOS-FND-0006
Architecture Epoch: E001
Current Version: E001-v0.1.0
Status: In Review
Authority Scope: documentation-principles
Official Documentation Language: en-US
Owner: AI-MOS Architecture
```
