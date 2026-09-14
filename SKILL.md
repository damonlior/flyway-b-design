---
name: flyway-b-design
description: Apply the Flyway B-end design system to design, revise, review, document, or specify enterprise product pages and Figma screens. Use whenever a request involves 飞来汇/Flyway B端 page design, transaction or fund-management interfaces, component and token selection, page patterns, Figma design-document organization, review-ready delivery, responsive behavior, interaction states, permissions, risk controls, or checking whether a design complies with the Flyway design system.
---

# Flyway B Design

Apply the bundled Flyway B-end governance documents as one mandatory rule set. Do not invent a separate visual language or page structure.

## Load the rules

Before analyzing, proposing, reviewing, or editing any page:

1. Read [references/AGENTS.md](references/AGENTS.md) completely.
2. Read [references/Design-System.md](references/Design-System.md) completely for visual foundations, components, variants, properties, assets, and known gaps.
3. Read [references/AI-Design-Skill.md](references/AI-Design-Skill.md) completely for the design workflow, selection rules, interaction, risk, permissions, responsive behavior, and validation.
4. Read [references/Pattern-Library.md](references/Pattern-Library.md) completely to select the page shell, primary pattern, supporting patterns, and cross-device transformations.
5. Read [references/Design-Document-Output-Rules.md](references/Design-Document-Output-Rules.md) completely for Figma file structure, version management, module/task-flow organization, interaction annotations, review-ready state coverage, and delivery governance.

When a reference is long, read it in successive chunks until EOF. Do not rely on memory, general B-end conventions, or only one reference.

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

For a short user request, compress the presentation but still perform every required check.
