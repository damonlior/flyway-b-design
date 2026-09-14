---
name: flyway-b-design
description: Apply the Flyway B-end design system to design, revise, review, document, or specify enterprise product pages and Figma screens. Use whenever a request involves 飞来汇/Flyway B端 page design, transaction or fund-management interfaces, component and token selection, page patterns, Figma design-document organization, review-ready delivery, responsive behavior, interaction states, permissions, risk controls, or checking whether a design complies with the Flyway design system.
---

# Flyway B Design

Apply the bundled Flyway B-end governance documents as one mandatory rule set. Do not invent a separate visual language or page structure.

## REFERENCE LOADING POLICY (highest priority)

Do not preload all reference files. `references/` totals roughly 124 KB; loading it on every task wastes context and quota for no benefit.

Use progressive disclosure:

1. Determine the task.
2. Use existing context first.
3. Identify the minimum reference required.
4. Search for the relevant section or keyword first.
5. Read only the required section when possible.
6. Load additional references only if the current information is insufficient.

Never read every file in `references/` by default.

Hard consequences of this policy:

- If the current context already answers the question, read nothing.
- Never read the same reference twice in one task; reuse what you already read.
- Never read a reference "just to be safe"; read it when the task creates a real question.
- Locating a section means `grep -n '^#' <file>` (or a keyword search) first, then reading only that range. Never read a whole file to find one fact.

## Reference Router

Match the task to exactly one row and load only what that row lists.

### A. Simple UI edits — load nothing

Examples: change spacing, change width/height, change copy, adjust alignment, swap a component the user already specified.

Default: **load no reference.** Apply the edit directly.

Only when a value is genuinely undetermined, search `Design-System.md` for that single fact instead of loading a file. Do not open a reference merely to confirm something the context already settles.

### B. Component design / component usage

Examples: Button, Input, Select, Table, Modal, Form, Navigation.

1. `Design-System.md` first — §4 Component Library holds one section per component (Button, Input, Select, Date Picker, Dropdown, Checkbox / Radio, Switch, Table, Pagination, Modal, Drawer, Tooltip, Tag, Notification, Empty State). Read only the component in question; add §2 Foundations only when tokens are in question.
2. Only if the task involves a composition pattern, also load `Pattern-Library.md` §17 (Cross-pattern Component Rules).

Do not read either file in full.

### C. Page design / page refactor

Examples: Dashboard, List, Detail, Form, Workspace.

1. `Pattern-Library.md` first — read §18 (Pattern Selection Matrix), which is short, to pick the pattern.
2. Then read only the selected pattern's section (for example §5 Data List, §7 Detail).
3. Then, only for the specific Token / Component facts that page needs, search `Design-System.md` for those facts.

Do not load both files completely. Do not read patterns that were not selected.

### D. AI generation principles / design decisions

Load `AI-Design-Skill.md` only when the task involves:

- how AI should generate a page
- design decision principles
- design quality judgement
- AI behaviour boundaries

### E. Skill workflow / execution constraints

Load `AGENTS.md` only when the task involves:

- how this skill itself works
- file maintenance
- the Figma execution flow
- special agent constraints

### F. Figma design-document output

Load `Design-Document-Output-Rules.md` only when producing or revising a Figma design document. Start with §4 File Structure, §8 Task Flow Completeness, §9 Required State Coverage and §14 Review-ready Output Contract; add §5 Version Management, §10 Interaction Annotation or §18 Recommended Figma Skeleton only if the task touches them.

### Reading a reference in full

Escalate to a full read only when:

- the task is high-risk (financial submission, permissions, risk control) and needs cross-section consistency, or
- the user explicitly asks for a full-document compliance audit.

## FIGMA CONTEXT POLICY

Do not inspect the entire Figma document by default. A full document tree is large and rarely needed.

- If the user identifies a specific frame, component, selection, or page, inspect only that scope (`get_selection`, `get_node`, or `get_design_context` with a specific `nodeId`).
- Only expand the inspected scope when required to complete the task.
- Do not call Figma tools when the task needs no current Figma state — for example a spacing or copy change on a node the user already described.
- Do not re-inspect the same node twice in one task.
- Do not call Figma at all unless the task requires reading the current design context or performing a Figma operation.

## Resolve authority

- Treat actual Figma Component, Variables, and Styles as facts when they are available.
- Use `Design-System.md` for appearance, tokens, component capabilities, and asset existence.
- Use `Pattern-Library.md` for page structure, flow, module order, and responsive transformation.
- Use `AI-Design-Skill.md` for method, component selection, states, interaction, risk, permission, and delivery requirements.
- Use `Design-Document-Output-Rules.md` for Figma document structure, naming, versioning, task-flow presentation, annotations, review readiness, history, and change synchronization.
- Use `AGENTS.md` for mandatory execution, conflict, exception, audit, and Figma change-boundary rules.
- Report unresolved conflicts. Never silently bypass them by creating new tokens, components, or patterns.

## Execute every task

1. Identify the business goal, user role, permissions, primary task, risk level, target viewport, and whether the request authorizes Figma changes.
2. Select exactly one Primary Pattern and the necessary Supporting Patterns.
3. Map every UI element to an existing Component, Variant, Property, semantic Token, Style, Grid, or a declared Composition Pattern.
4. Define information architecture and separate page-level, module-level, row-level, and field-level actions.
5. Use Auto Layout and the documented responsive transformations. Never treat mobile as a scaled desktop frame.
6. Cover Default, Hover, Active, Focus, Disabled, Loading, Error, Empty, Permission, and relevant business states; mark genuinely irrelevant states as `N/A`.
7. Check financial data formatting, risk confirmation, permission expression, error recovery, accessibility, Light/Dark, and Desktop/Compact/Mobile behavior.
8. Complete the Definition of Done in `AGENTS.md` before calling the work compliant or complete.
9. When producing or revising a Figma design document, organize it as Module → Scenario / Task Flow → Screen / State, add local interaction annotations, maintain version/history boundaries, and complete the Review Ready checklist in `Design-Document-Output-Rules.md`.

Each step applies at the depth the task requires. A simple edit does not trigger the full page-design workflow; the router decides how much of it applies.

## Handle missing assets

- Reuse an existing component or supported composition when possible.
- Label a supported page-level combination as `Composition Pattern`.
- Label an unavailable capability as `Needs Extension` and provide the extension proposal required by `AGENTS.md`.
- Do not create or modify formal Component masters, Variables, Styles, or tokens without explicit component-library maintenance authorization.
- Do not claim that Card, Slider, KPI Card, Chart, or a complete Empty State container master exists when the references say otherwise.

## Respect the Figma boundary

- Keep analysis, scanning, specification, and review tasks read-only.
- Modify Figma only when the user explicitly requests creation or changes.
- Treat page-design authorization as separate from component-library maintenance authorization.
- Before writing, confirm the target file, page, frame, and change scope.
- After writing, report changed frames, reused components, untouched library assets, exceptions, missing assets, and remaining issues.

## Deliver the result

Include, at minimum:

1. Business Goal, User Role, and Page Type.
2. Primary Pattern and Supporting Patterns.
3. Information Architecture / Layout Structure.
4. Component, Variant, and Property Mapping.
5. Token Mapping.
6. Interaction and State Matrix.
7. Error, Empty, Permission, and Risk Handling.
8. Desktop, Compact Desktop, and Mobile rules.
9. Reused Assets.
10. Missing Assets / Extension Proposal.
11. Approved Exceptions.
12. Validation Result.
13. Design-document version, module/task-flow structure, change summary, and Review Ready result when the deliverable is a Figma design proposal.

For a short user request, compress the presentation and load fewer references — but still perform every check the task actually requires.
