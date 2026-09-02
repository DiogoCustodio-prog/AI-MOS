# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository state

This checkout is currently a documentation workspace, not an executable application. The historical exports are preserved under `source-material/chatgpt-exports/`, with the explanation of that boundary in `source-material/README.md`. The initial canonical areas now exist as `SYSTEM/`, `FOUNDATION/`, `CORE/`, `BOOTSTRAP/`, `CLIENTS/`, and `KNOWLEDGE/`. `SYSTEM/SYSTEM_MANIFEST.md` and the Foundation specifications through `FOUNDATION/05_GOVERNANCE_APPROVAL_PROCESS.md` are canonical candidates and are currently `In Review`; the remaining areas contain scope READMEs and no approved specifications. The local `memory/` directory contains Claude session memory, not AI-MOS canonical knowledge.

There is no application code, package manifest, build configuration, test runner, linter, or metadata validator at present. The root `CLAUDE.md` is operational guidance for Claude Code, while the future Core documentation will define the product itself.

Files under `source-material/` are source material and decision history, not automatically canonical specifications. They contain repeated drafts, proposed directory trees, and aspirational commands. Do not treat a quoted example as an existing file or capability. Before promoting an idea into a canonical document, reconcile it with the latest approved architectural decisions and the actual workspace.

## Commands

No build, lint, test, or application-run command is currently defined. Do not invent one or report a validation command as passing until the corresponding tooling exists.

Useful inspection commands from the repository root (PowerShell):

```powershell
Get-ChildItem -Force
Get-ChildItem -Recurse -File
Get-Content .\path\to\document.md
```

Historical exports are under `source-material\chatgpt-exports`; canonical documents belong in the governed areas, not in the source-material directory.

`git` is the intended future source-control and audit mechanism, but this checkout is not currently a Git repository. Once the repository is initialized, use `git status --short` before and after changes. When scripts and validation are added, record their exact build, lint, test, and single-test commands in this section rather than relying on the examples embedded in exported conversations.

## Architectural model

AI-MOS is intended to be a documentation-first, AI-native operating system for marketing and organizational intelligence. Markdown is the primary knowledge representation; automation, agents, prompts, and integrations are downstream consumers of governed knowledge.

The primary product boundary has three layers:

- **AI-MOS Core** — Inovador Tech intellectual property: architecture, governance, standards, reusable operating models, agent patterns, and documentation contracts. It must remain customer-independent.
- **AI-MOS Bootstrap Kit** — templates, repository initialization, onboarding, checklists, and validation needed to create a new implementation without modifying Core.
- **AI-MOS Client Implementation** — an isolated workspace containing a client’s business context, branding, personas, campaigns, workflows, integrations, metrics, and client-specific agents. Client content must not contaminate Core.

Inovador Tech is the first **Reference Implementation** and the dogfooding environment. Real problems are solved there first; validated, generalizable solutions are then extracted into Core as reusable skills, workflows, templates, agents, or standards. Do not assume an unvalidated Inovador Tech experiment is a framework rule.

The planned functional subsystems are complementary views of that architecture:

- **Core OS**: architecture, governance, documentation, memory, and versioning.
- **Branding OS**: positioning, visual identity, voice, personas, and messaging.
- **Marketing OS**: campaigns, content, ads, SEO, funnels, landing pages, and prompt libraries.
- **Automation OS**: Claude Code, MCP integrations, browser/tool workflows, n8n, and external platforms.
- **Knowledge OS**: decisions, ADRs, lessons, experiments, patterns, metrics, feedback, and evolution history.
- **AI Agent OS**: specialized agents with explicit missions, scope, tools, memory, constraints, and metrics.

## Canonical documentation contract

When canonical AI-MOS documents are created, follow the approved metadata standard represented in the source material:

- Begin with YAML front matter; nothing may precede the opening `---`.
- Use the governed top-level domains: `document`, `ownership`, `architecture`, `lifecycle`, `metadata`, `relations`, `compatibility`, `ai`, `security`, and `audit` as applicable.
- Give every canonical document a stable, unique ID independent of filename, normally `AI-MOS-<DOMAIN>-<SEQUENCE>`.
- Use hybrid versioning: architecture epoch plus SemVer, for example `E001-v0.2.0`; keep `epoch`, `semantic`, and `full` consistent.
- Use relative paths for internal document relationships. Keep `depends_on` distinct from non-normative related references, and avoid circular dependencies.
- Preserve one Source of Truth per concept. Reference it instead of copying normative definitions into multiple documents.
- Keep metadata types native to YAML: booleans as booleans, arrays as arrays, and ISO dates as dates/strings in the documented format. Do not use placeholders such as `TBD`, `UNKNOWN`, or `N/A` for required production fields.
- Keep canonical documents deterministic, modular, independently understandable, and suitable for Claude Code, Git-based review, Obsidian navigation, and future RAG indexing.
- Treat `document.id`, creation metadata, and creator attribution as stable after assignment. Changes to normative metadata require architectural review and a version update.

The official language for canonical AI-MOS documentation is `en-US`; every governed canonical document must declare `metadata.language: en-US`. Translations may exist only as explicitly identified derivatives of the en-US Source of Truth. The metadata standard separates editorial approval (`document.status`) from operational lifecycle (`lifecycle.state`). Do not collapse those meanings or silently resolve conflicts by inference. The documented authority order is canonical metadata, the metadata standard, the system manifest, document body, filename/location, then AI inference.

## Document construction order

The intended Foundation sequence is:

1. `SYSTEM_MANIFEST.md` — system identity, scope, governance, macro-architecture, and permanent principles.
2. `00_METADATA_STANDARD.md` — the metadata contract consumed by all other canonical documents.
3. `01_DOCUMENT_TEMPLATE.md`.
4. `02_NAMING_CONVENTIONS.md`.
5. `03_DIRECTORY_STRUCTURE.md`.
6. `04_DOCUMENTATION_PRINCIPLES.md`.
7. `05_GOVERNANCE_APPROVAL_PROCESS.md` — the review, quorum, decision-record, and human-ratification process.

Only after Foundation is reviewed should Core documents such as `README.md`, `CLAUDE.md`, `VISION.md`, `PROJECT_SPECIFICATION.md`, `DEVELOPMENT_RULES.md`, and `ROADMAP.md` be treated as the next construction phase. The current root `CLAUDE.md` is operational guidance for Claude Code; it should remain aligned with the eventual Core documentation rather than duplicating the full specification.

Before implementing a new capability, establish which canonical document owns the requirement, read its dependencies and related decisions, and determine whether the requested change belongs to Core, Bootstrap, or a client implementation. If the required governing document does not yet exist, document the gap instead of fabricating authority.

## Memory and evolution

The intended memory design is layered:

- Git is the historical source of truth for Markdown, prompts, agents, skills, campaigns, and decisions.
- Markdown is the canonical, searchable, versionable representation.
- Obsidian is a human navigation and graph interface, not a separate authority.
- Drive/Notion may support storage or operations but must not become the only canonical source.
- A vector database/RAG layer is a later optimization for a substantially larger corpus, not an initial prerequisite.

Organize future operational memory by knowledge type, such as `decisions`, `lessons`, `patterns`, `anti-patterns`, `experiments`, `metrics`, `feedback`, and `evolution`. Each record should identify its origin, conclusion, affected documents/agents, and review state. A curator or evolution workflow may create records and propose changes, but AI must not silently modify an authoritative Source of Truth: record the rationale, show affected files, and obtain human approval before promoting the change.

Use the evolution loop as the operating model:

```text
problem → research → hypothesis → implementation → test → measurement
→ learning → documentation → standardization → reuse → new version
```

Every reusable solution discovered in the Reference Implementation should be evaluated for extraction into a Core skill, workflow, template, library, or agent. Keep client-specific facts and experimental results in the client/reference implementation unless they have been explicitly generalized and approved.

## Working principles for Claude Code

- Read the governing and dependency documents before editing a canonical specification. In the planned repository, the normal reading order is README, CLAUDE, project specification, development rules, relevant knowledge, ADRs, and lessons.
- Prefer small, single-responsibility Markdown documents over one large playbook. Use explicit relative links and metadata relationships to compose them.
- Distinguish approved decisions from proposals, experiments, and transcript commentary. State uncertainty when the source material conflicts or an implementation is missing.
- When a task solves a real Reference Implementation problem, preserve the client result first, then identify the generalizable rule separately; do not copy private client context into Core.
- When a future task introduces code or automation, add the corresponding validation and update this command section with verified commands. Until then, repository validation is limited to document review, YAML/front-matter consistency, relationship/path checks, duplicate-ID checks, and architectural cross-checks performed manually.
