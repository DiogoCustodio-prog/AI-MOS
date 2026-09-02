---
document:
  id: AI-MOS-FND-0007
  title: AI-MOS Governance Approval Process
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
  module: Governance Approval

lifecycle:
  state: active
  maturity: foundation
  review_required: true

metadata:
  created: 2026-08-12
  updated: 2026-08-12
  language: en-US
  tags:
    - ai-mos
    - foundation
    - governance
    - approval
    - review
    - ratification
    - decision-records

relations:
  depends_on:
    - ../SYSTEM/SYSTEM_MANIFEST.md
    - ./00_METADATA_STANDARD.md
    - ./01_DOCUMENT_TEMPLATE.md
    - ./04_DOCUMENTATION_PRINCIPLES.md
  related_documents: []

compatibility:
  ai_mos:
    epoch: E001
    core: ">=0.2.0 <2.0.0"

ai:
  source_of_truth: true
  authority_scope: governance-approval-process
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
  last_review: 2026-08-12
  review_cycle: annual
---

# AI-MOS Governance Approval Process

## 1. Document Status and Authority

This document defines the approval process for proposed changes to canonical AI-MOS documentation and for other governed decisions that require formal review.

Its current editorial status is **In Review**. It is the canonical candidate for the `governance-approval-process` authority scope and becomes the approved governance-process authority only after review and explicit human ratification.

The [AI-MOS System Manifest](../SYSTEM/SYSTEM_MANIFEST.md) remains authoritative for system identity, architectural boundaries, permanent principles, and system-level governance direction. The [AI-MOS Metadata Standard](00_METADATA_STANDARD.md) remains authoritative for metadata fields, types, status vocabulary, lifecycle semantics, relationships, and extensions. The [AI-MOS Document Template](01_DOCUMENT_TEMPLATE.md) remains authoritative for the practical arrangement of canonical document metadata. The [AI-MOS Documentation Principles](04_DOCUMENTATION_PRINCIPLES.md) remains authoritative for documentation quality, traceability, human review, and the distinction between proposals and approved rules.

This document specializes those authorities for approval workflow. It MUST NOT silently amend the metadata contract, create a new canonical top-level metadata domain, or promote a document without the human ratification required here.

While this document is In Review, it defines a proposed governance baseline. The initial adoption of this process is a bootstrap case: this specification may be used to organize its own review, but its authority is not considered approved until the Project Owner explicitly ratifies the recorded recommendation.

The terms **MUST**, **MUST NOT**, **REQUIRED**, **SHALL**, **SHALL NOT**, **SHOULD**, **SHOULD NOT**, and **MAY** are normative terms in this document.

## 2. Purpose

The purpose of this process is to make approval decisions:

- explicit;
- proportional to impact;
- attributable to defined human roles;
- auditable through preserved records;
- resistant to silent AI inference;
- compatible with document status and versioning;
- safe for architectural, security, and client-isolation boundaries.

The process separates analysis from authority. AI may assist with classification, evidence gathering, consistency checks, drafting, and record preparation, but AI MUST NOT represent a human vote, presume human approval, or promote a document to `Approved` without explicit human ratification.

## 3. Scope

This process applies to proposed changes involving:

- canonical documents in `SYSTEM/`, `FOUNDATION/`, `CORE/`, `BOOTSTRAP/`, `CLIENTS/`, and `KNOWLEDGE/`;
- document status promotion or demotion;
- new or changed normative rules;
- changes to authority, dependencies, compatibility, language, security, isolation, versioning, or governed structure;
- exceptions to approved documentation or architectural rules;
- coherent packages of related documents reviewed as one decision set.

It does not make the following items canonical or approved by themselves:

- historical exports in `source-material/`;
- local session memory in `memory/`;
- informal conversation;
- an AI-generated recommendation;
- an unratified decision record;
- a document that merely has valid Front Matter.

A decision record in `KNOWLEDGE/` preserves evidence and outcome. It does not silently replace the Source of Truth owned by the affected canonical document.

## 4. Governance Principles

### 4.1 Human accountability

A human decision-maker MUST retain final authority over approval. The committee recommendation is advisory until ratified by the Project Owner.

AI systems MUST NOT:

- cast or simulate a human vote;
- treat silence, elapsed time, or lack of a comment as approval;
- alter `document.status` from `In Review` to `Approved` based only on a recommendation;
- resolve a recorded architectural or security objection by inference;
- suppress dissent, conditions, risks, or uncertainty from the decision record.

### 4.2 Proportional review

The required review effort MUST correspond to the potential impact of the change. When classification is uncertain, the higher impact level MUST be used until the committee records a justified reclassification.

### 4.3 Traceability

Every formal decision MUST identify the affected document or documents, exact versions, impact level, reviewers, votes, objections, conditions, risks, result, and human ratification state.

### 4.4 One decision authority per scope

This process governs how a decision is reviewed; it does not make the approval record a second Source of Truth for the affected subject. The affected canonical document remains authoritative for its own scope after approval.

### 4.5 No silent promotion

A document remains in its current valid status until all required conditions for the selected result are satisfied. A recommendation to approve is not an approval.

## 5. Permanent Committee Roles

The governance committee uses four standing roles. A person may perform more than one role only when the applicable impact level, independence requirements, and conflict-of-interest constraints are explicitly recorded. Combining roles MUST NOT be used to manufacture quorum.

### 5.1 AI-MOS Architecture

Responsible for:

- architecture and system boundaries;
- authority scopes and Sources of Truth;
- dependencies and compatibility;
- layer placement and structural impact;
- versioning implications;
- confirmation or correction of Level 2 and Level 3 classification;
- architectural objections and escalation.

### 5.2 Project Owner

Responsible for:

- product direction and priorities;
- human accountability for the decision;
- explicit final ratification;
- accepting, rejecting, or returning the committee recommendation;
- veto or escalation;
- deciding an impasse after risks and dissent have been recorded.

The Project Owner's committee vote at Level 3 does not replace their separate ratification action.

### 5.3 Documentation Governance

Responsible for:

- document quality and completeness;
- metadata and relationship consistency;
- traceability and record completeness;
- initial impact classification;
- controlled vocabulary and status checks;
- confirming that the proposal is in the correct repository area;
- identifying missing evidence or documentation gaps.

### 5.4 Security and Operations

Responsible for:

- secrets and sensitive-data boundaries;
- client isolation;
- security classification and confidentiality;
- operational impact and implementation feasibility;
- access, deployment, and maintenance concerns;
- operational objections and mitigations.

## 6. Impact Classification

Every proposal MUST receive an initial impact classification before the committee issues a final result.

### 6.1 Level 1 — Editorial

Level 1 changes are non-normative editorial changes that do not alter architectural boundaries, authority, rule meaning, security expectations, or operational behavior.

Examples include:

- spelling and grammar corrections;
- formatting improvements;
- corrected links;
- terminology clarification that does not change a rule;
- navigation or presentation improvements;
- removal of an accidental duplication that has no normative effect.

A change MUST NOT be treated as Level 1 merely because its diff is small. A short change to a dependency, security rule, authority field, or status meaning is not editorial.

### 6.2 Level 2 — Normative

Level 2 changes add or alter rules within an existing authority scope without changing the system's architectural boundaries.

Examples include:

- adding a documentation rule within an approved Foundation authority;
- changing a checklist requirement without changing the metadata contract;
- clarifying a normative procedure within its existing owner and layer;
- changing a controlled rule that does not alter architecture, security boundaries, client isolation, or language policy.

A Level 2 proposal MUST be escalated to Level 3 when it changes the authority, dependency direction, contract boundary, or other architectural assumption.

### 6.3 Level 3 — Architectural

Level 3 changes affect system structure, authority, or protected boundaries.

Examples include changes to:

- authority scopes or Sources of Truth;
- normative dependencies or dependency direction;
- official language policy;
- security or confidentiality expectations;
- client isolation;
- governed directory structure;
- versioning or identity semantics;
- layer boundaries or product boundaries;
- canonical metadata contracts or top-level domains;
- compatibility contracts with architectural effect.

Level 3 review requires all four standing roles.

### 6.4 Classification procedure

`Documentation Governance` assigns the initial level and records the rationale. `AI-MOS Architecture` MUST confirm or correct any Level 2 or Level 3 classification before the final result. Any reviewer MAY request escalation.

The committee MAY reclassify a proposal before deciding it. A reclassification MUST be recorded with its reason, evidence, and effect on quorum. A proposal MUST NOT be downgraded without a written rationale. If uncertainty remains, the higher level applies.

## 7. Quorum and Participation

Quorum is progressive and is defined by impact level:

| Impact level | Required reviewers | Required roles and conditions |
| --- | ---: | --- |
| Level 1 — Editorial | 2 | Documentation Governance and one additional qualified reviewer |
| Level 2 — Normative | 3 | AI-MOS Architecture, Documentation Governance, and one additional qualified reviewer |
| Level 3 — Architectural | 4 | AI-MOS Architecture, Project Owner, Documentation Governance, and Security and Operations |

The additional reviewer at Level 1 or Level 2 MUST be identified in the decision record. A reviewer is qualified when they have sufficient knowledge of the affected scope and no unrecorded conflict of interest.

Quorum means that the required reviewers participated and recorded a decision or abstention. An abstention does not count as a favorable vote and does not replace a required role. If a required role is absent, the committee MUST NOT issue an approval recommendation; it may issue `Escalate` or `Defer` while preserving the reason.

For consistency with the official language policy, the formal result vocabulary used in a record MUST be written in English. The controlled result values are defined in Section 9.

## 8. Review Procedure

A proposal proceeds through the following stages:

1. **Submit** — identify the proposal, affected scope, author, exact document versions, and requested outcome.
2. **Screen** — Documentation Governance checks structural completeness and assigns the initial impact level.
3. **Confirm** — AI-MOS Architecture confirms or corrects Level 2 and Level 3 classification; any reviewer may request escalation.
4. **Review** — required reviewers inspect the proposal, dependencies, evidence, security boundaries, client-isolation implications, compatibility, and versioning.
5. **Record** — each reviewer records a vote, comments, risks, conditions, objections, or abstention.
6. **Recommend** — the committee selects one formal result from Section 9.
7. **Ratify** — the Project Owner explicitly ratifies, rejects, returns, or escalates the recommendation.
8. **Apply** — only after required conditions and ratification are complete may the document status, version, or relationship be updated.
9. **Verify** — Documentation Governance checks the applied state against the decision record and confirms that no unrelated file or Source of Truth was changed.

AI may prepare drafts for stages 1 through 5 and assist with stage 9, but every human action that is required for quorum or ratification MUST be attributable to the responsible human role.

## 9. Formal Results

The committee MUST select exactly one of the following result values for each decision item:

### 9.1 `Approve`

The committee recommends approval because quorum is valid, required reviews are complete, and no unresolved blocking objection remains.

The affected document MAY be promoted to `Approved` only after:

- the decision record is complete;
- the exact document version is identified;
- the Project Owner explicitly ratifies the recommendation;
- all required record and metadata updates are applied and verified.

### 9.2 `Approve with conditions`

The committee recommends approval subject to explicit conditions.

The affected document MUST remain `In Review` until each condition has an owner, acceptance criterion, due or review point when applicable, and verification recorded. The Project Owner may ratify the conditional recommendation, but ratification alone does not authorize promotion before the conditions are satisfied.

### 9.3 `Request changes`

The proposal requires revision before a final approval recommendation. The affected document remains `In Review` or retains its current status when no status change was requested.

The record MUST identify the requested changes and the evidence needed for resubmission.

### 9.4 `Reject`

The proposal is not accepted. A document MAY be moved to `Rejected` when that result applies to the document itself. Rejection does not grant authority and does not authorize implementation as an approved rule.

The record MUST state the rationale, affected version, and any follow-up or resubmission conditions.

### 9.5 `Escalate`

The committee cannot or should not resolve the matter at the current level. The affected document normally remains `In Review`, or retains its current status when no status change was requested.

The record MUST identify the receiving authority, unresolved question, risk, and information required for the next decision.

### 9.6 `Defer`

The decision is postponed because of missing evidence, dependency, priority, capacity, or another explicitly recorded reason. The affected document normally remains `In Review`, or retains its current status when no status change was requested.

Defer is not approval by delay. The record SHOULD identify a review trigger or next review point when one can be established.

## 10. Blocking Objections, Dissent, and Impasse

A reasoned objection blocks immediate approval when it concerns:

- architecture or dependency direction;
- security or sensitive-data handling;
- authority or Source-of-Truth ownership;
- official language policy;
- client isolation;
- a required compatibility or versioning boundary.

A blocking objection MUST remain visible in the decision record until it is:

- resolved with evidence;
- mitigated and formally accepted by the accountable human authority;
- escalated to the appropriate authority;
- or addressed by a recorded human decision that explicitly accepts the residual risk.

The Project Owner MUST NOT silently ignore a technical or security objection. A veto or decision to accept residual risk MUST identify the objection, rationale, affected scope, and any conditions or monitoring required.

A non-blocking concern does not prevent a result, but it MUST be recorded with its owner and disposition when the committee relies on it.

If reviewers disagree, the record MUST preserve the distinct positions. A majority recommendation does not erase a minority objection. If the disagreement prevents a responsible recommendation, the committee selects `Escalate` or `Defer` rather than treating disagreement as approval.

An impasse is resolved by the Project Owner only after the risks, objections, alternatives, and dissenting views are recorded. For Level 3 decisions, the Project Owner's final human decision MUST be explicit and separate from their committee vote.

## 11. Human Ratification and Status Transitions

The Project Owner's ratification is a distinct human action. It MUST identify:

- the decision record;
- the exact document or package version;
- the committee result;
- the ratification decision;
- the human decision-maker;
- the date of ratification;
- any accepted conditions or residual risks.

The ratification field in a decision record is a record structure, not a new canonical Front Matter field. Until the Metadata Standard formally defines a dedicated field, canonical documents MUST NOT add `audit.approval_record` as though it were already part of the standard.

A document MAY reference its approval record through an applicable existing relationship or body section only when the relationship is valid for that document and the change is itself reviewed. A record reference that does not fit the existing canonical relationship vocabulary MUST be kept in the decision record and body text, or placed under an explicitly namespaced `extensions` field that is governed for that use. The existence of a decision record MUST NOT be represented by inventing an unapproved top-level field.

The status effects are:

| Committee result | Normal document effect |
| --- | --- |
| `Approve` | After explicit human ratification and verification, the document MAY change to `Approved`. |
| `Approve with conditions` | Remains `In Review` until all conditions are verified; only then may it change to `Approved` after ratification requirements are satisfied. |
| `Request changes` | Remains `In Review` and returns to revision. |
| `Reject` | MAY change to `Rejected` when the document itself is rejected. |
| `Escalate` | Remains at its current status, normally `In Review`, pending the higher decision. |
| `Defer` | Remains at its current status, normally `In Review`, pending the deferred review. |

For an already approved document, any normative change MUST create a new version that starts `In Review`. The previously approved version remains valid until the new version is approved. After the new version is approved, the previous version MAY be marked `Superseded` with an explicit relationship and recorded rationale. A non-normative editorial change MAY follow a lower-impact path when it does not alter the approved rule, authority, dependency, security expectation, or status meaning.

Promotion to `Approved` requires all of the following:

1. valid quorum;
2. no unresolved blocking objection;
3. a complete formal decision record;
4. explicit Project Owner ratification;
5. exact document identity and version;
6. individual identification of every document in a reviewed package;
7. completion and verification of any conditions.

## 12. Decision Records in `KNOWLEDGE/`

Formal approval decisions MUST be preserved as canonical knowledge records in `KNOWLEDGE/` when the decision affects canonical status, normative content, architecture, security, client isolation, authority, or another governed boundary.

The record is the audit and reasoning history for the decision. It is not a replacement for the affected Source of Truth.

### 12.1 Event and package granularity

The process supports a hybrid model:

- a record MAY describe one decision event for one document;
- a record MAY describe one coherent package containing multiple related documents;
- each document in a package MUST be listed individually with its own ID, exact version, impact level, result, conditions, objections, and status after decision;
- documents with different impact levels, results, unresolved conditions, or materially different decisions SHOULD be separated into different records.

A package MUST have one coherent decision purpose. Grouping documents for convenience MUST NOT hide different outcomes or bypass the quorum required by the highest-impact item.

### 12.2 Minimum record content

A formal record MUST contain, in its body or governed metadata:

- a stable record identity when the record is canonical;
- decision title and purpose;
- date of submission and decision;
- author or submitting role;
- affected architectural area and authority scope;
- affected document ID, path, and exact version for each item;
- initial and final impact classification with rationale;
- evidence and dependencies reviewed;
- required quorum and participating roles;
- each reviewer's role, vote, comments, risks, conditions, and objections;
- abstentions and conflicts of interest, when applicable;
- the committee's formal result for each document or package item;
- unresolved issues and their disposition;
- Project Owner ratification or rejection, including explicit human attribution and date;
- exact status and version after the decision;
- conditions, owners, verification criteria, and completion state;
- dissent, escalation, veto, impasse, or residual-risk acceptance when applicable;
- links to affected documents and supporting evidence;
- follow-up review trigger or next action when applicable.

A record MUST NOT state or imply that an AI system supplied a human vote or ratification. AI assistance MAY be acknowledged as preparation, analysis, or consistency checking, but human decisions MUST remain distinguishable.

### 12.3 Record status and authority

A decision record MAY begin as `Draft` or `In Review` according to the record's actual state. An unratified record MUST NOT claim that the affected document is approved. A record that documents a ratified decision MUST preserve the exact evidence and decision state; later corrections MUST be handled through a governed update rather than silent rewriting.

The record's `ai.authority_scope`, when present, MUST be limited to the record's own decision-record responsibility. It MUST NOT claim the authority scope of the affected canonical document.

### 12.4 Record reference without an unapproved field

The current Metadata Standard defines `audit` fields for creation, update, review date, and review cycle, but it does not define `audit.approval_record`. This process therefore does not require that field.

Until a formal Metadata Standard revision is approved, the record-to-document connection MUST use existing relative links and the record body, with optional existing relationship fields only when their semantics apply. A future schema change MAY define a dedicated approval-record relationship, but that change itself MUST follow this process at the appropriate impact level.

## 13. Initial Adoption and Bootstrap Exception

This process is itself a Foundation specification and begins with `document.status: In Review`. Its initial adoption MUST NOT be described as proof that the process was already approved.

For the bootstrap review of this document:

1. the proposal and exact version are identified;
2. Documentation Governance assigns the initial impact level;
3. the required reviewers review the process and record their positions;
4. the committee issues a recommendation;
5. the Project Owner explicitly ratifies, rejects, returns, escalates, or defers that recommendation;
6. only after ratification may this document be promoted to `Approved`.

If the existing process is not yet approved, the Project Owner's explicit ratification is the human authority for the initial adoption decision. The record MUST clearly label this as initial adoption and MUST NOT claim that an already-approved process authorized the decision retroactively.

The bootstrap exception is limited to establishing this process. It MUST NOT waive review for unrelated canonical documents, erase the requirement for human ratification, or authorize silent status promotion.

## 14. Exceptions and Escalation

An exception to this process MUST:

- identify the affected document, package, or decision;
- state the reason and scope;
- identify the risk and compatibility impact;
- preserve the human accountability requirement unless a higher approved authority explicitly changes it;
- record duration or review trigger when the exception is temporary;
- be preserved in `KNOWLEDGE/` when it affects a canonical boundary.

No exception may authorize secrets in Markdown, client contamination of Core, silent changes to a Source of Truth, or representation of an AI action as human approval.

When this process conflicts with an approved higher-authority document, the conflict MUST be escalated and recorded. AI MUST NOT resolve the conflict silently.

## 15. Manual Review Checklist

Before issuing an approval recommendation, confirm:

- [ ] The proposal has a clear purpose, scope, owner, and requested result.
- [ ] Every affected document has an ID, relative path, and exact version.
- [ ] The initial impact level and rationale are recorded.
- [ ] AI-MOS Architecture confirmed or corrected any Level 2 or Level 3 classification.
- [ ] The committee used the quorum required by the final impact level.
- [ ] Required roles participated and any abstention or conflict is recorded.
- [ ] Reviewers recorded votes, risks, conditions, objections, and dissent.
- [ ] Blocking objections are resolved, mitigated and accepted, or escalated.
- [ ] The formal result uses the controlled English vocabulary.
- [ ] The decision record is in `KNOWLEDGE/` when formal preservation is required.
- [ ] The exact document version and status after the decision are explicit.
- [ ] Conditions have owners, criteria, and verification state.
- [ ] Project Owner ratification is explicit, attributable, and separate from AI analysis.
- [ ] No document was promoted to `Approved` before ratification and verification.
- [ ] No unapproved metadata field, top-level domain, or authority scope was introduced.
- [ ] No source material, session memory, secret, or client-confidential content was modified or copied into an inappropriate boundary.
- [ ] Follow-up actions and review triggers are recorded.

The workspace currently has no automated governance, metadata, or decision-record validator. This checklist is a manual review aid and does not constitute an automated validation result.

## 16. Versioning and Change Handling

A wording clarification that does not change the process rule MAY be a PATCH revision. A backward-compatible addition to roles, record guidance, or review procedure MAY be a MINOR revision. A change to human ratification, quorum, impact semantics, blocking objections, status transitions, or authority boundaries is a MAJOR revision within the current Epoch unless an Epoch change is required.

A normative revision to this process MUST begin as a new version in `In Review`. The currently approved version, if one exists, remains the active authority until the revised version is approved. A revision MUST identify its predecessor through an applicable governed relationship when that relationship vocabulary is available and must preserve the decision history.

The stable identity fields `document.id`, `metadata.created`, and `audit.created_by` MUST NOT be changed as part of an ordinary revision. Changes to those fields require explicit governance review and a recorded reason.

## 17. Normative Summary

AI-MOS governance approval MUST preserve these rules:

1. The committee is composed of standing roles and scales with impact.
2. Level 1 requires two reviewers; Level 2 requires three including AI-MOS Architecture; Level 3 requires all four standing roles.
3. Documentation Governance classifies initially; AI-MOS Architecture confirms or corrects Levels 2 and 3; uncertainty uses the higher level.
4. A reasoned architectural, security, authority, language, or isolation objection blocks immediate approval until resolved, accepted with explicit human accountability, or escalated.
5. The committee recommends; the Project Owner explicitly ratifies, rejects, returns, escalates, or defers.
6. AI MUST NOT simulate votes, infer consent, or promote a document to `Approved` without human ratification.
7. Formal results are `Approve`, `Approve with conditions`, `Request changes`, `Reject`, `Escalate`, and `Defer`.
8. Approved-document normative changes begin as new `In Review` versions; the prior approved version remains valid until replacement approval.
9. Formal decisions are preserved in `KNOWLEDGE/` with document-level identity, versions, votes, risks, objections, outcomes, conditions, and ratification.
10. The process does not introduce `audit.approval_record` or another unapproved canonical field.
11. The process itself remains `In Review` until its own recommendation is explicitly ratified.

## 18. Governance Approval Process Status

```text
Document: AI-MOS Governance Approval Process
Document ID: AI-MOS-FND-0007
Architecture Epoch: E001
Current Version: E001-v0.1.0
Status: In Review
Authority Scope: governance-approval-process
Official Documentation Language: en-US
Owner: AI-MOS Architecture
```

This document remains a review candidate until its decision record is complete and the Project Owner provides explicit human ratification. Its current existence does not imply that the process, the Foundation, or any other document has been formally approved.
