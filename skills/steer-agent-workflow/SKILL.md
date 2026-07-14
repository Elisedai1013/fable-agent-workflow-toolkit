---
name: steer-agent-workflow
description: Steer complex Agent work before, during, and after execution using source-grounded methods from Field Guide to Fable. Use when an Agent needs to find blind spots, explore genuinely different prototypes, interview the user to surface architecture-changing decisions, interpret a reference implementation, track execution deviations, or help the user verify their understanding of completed work before review, merge, or release.
---

# Steer Agent Workflow

Keep the Agent moving while making unknowns, deviations, evidence, and human decisions visible. Select only the smallest method needed for the user's current stage; do not force every task through all six methods.

## Establish the working state

1. Restate the result the user is trying to achieve.
2. Inspect the available task brief, artifacts, implementation state, and verification evidence.
3. Identify the current stage: before execution, during execution, or after completion.
4. Identify any decision that would materially change scope, architecture, permissions, cost, safety, or publication.
5. Continue within the authority already granted. Ask before expanding permissions or taking external, irreversible, or materially different action.

## Route to the smallest useful method

| Current signal | Select | Intended result |
| --- | --- | --- |
| The task has not started and important unknowns may be missing | Blind spot pass | A prioritized unknowns-to-verify list and stronger task brief |
| The goal is known but direction or preference is hard to express | Differentiated prototypes | Meaningfully different options and explicit tradeoffs |
| Important decisions are implicit, contradictory, or absent | Decision interview | Confirmed facts, unresolved questions, and an execution specification |
| The user provides code, a page, product, or other reference | Reference implementation | A semantic map or authorized reimplementation with differences and assumptions |
| A longer autonomous task is underway | Implementation notes | A traceable record of deviations, impacts, and escalation decisions |
| The user explicitly wants to confirm their understanding of completed work | Reverse quiz | A verification summary and the user's remaining understanding gaps |

Combine methods only when the transition is necessary. For example, run a blind spot pass before an interview when the missing decision is not yet visible, or use implementation notes followed by a reverse quiz for a long completed change when the user explicitly asks to check their understanding.

Read the matching section in [references/method-cards.md](references/method-cards.md) before applying a selected method. Do not load unrelated method sections unless the task moves into another stage.

## Separate evidence from judgment

Maintain four distinct layers throughout the work:

- **Verified evidence:** facts supported by inspected files, tool output, primary sources, or tests. Treat user statements as authoritative for their intent and choices; label claims about external state as user-provided until independently checked.
- **AI hypotheses:** possible blind spots, interpretations, risks, or options that still need verification.
- **Human decisions:** value choices, permission changes, scope changes, irreversible actions, or risk acceptance that the user must own.
- **Next step:** the smallest concrete action that advances the work without hiding unresolved decisions.

Never present an AI hypothesis as a verified fact. When the evidence is incomplete, name the gap and explain how to verify it.

## Apply the selected method

### Before execution

- Use **blind spot pass** to challenge the brief, not merely rewrite it.
- Use **differentiated prototypes** to expose preferences through real structural, interaction, or visual differences.
- Use **decision interview** one decision at a time when answers may change the solution. Do not ask questions already answered by the available context.

Do not stop routine progress for every uncertainty. Pause only when the unresolved decision could materially change the result or exceeds the user's granted authority.

### When translating a reference

- Use **reference implementation** before or during implementation when the user provides code, a page, a product, or another concrete map of the intended result.
- Inspect the reference and extract behavior and intent before implementing anything.
- Implement only when the user's request authorizes implementation; otherwise return a semantic map and open questions.
- Do not copy protected code, design, or assets without permission.

### During execution

- Record a deviation when new evidence forces the work away from the agreed plan.
- Prefer conservative and reversible actions while the deviation is unresolved.
- Continue after recording only if the change stays inside the agreed scope and risk boundary.
- Escalate changes to permissions, external systems, publication, security posture, cost, or irreversible state.

### After completion

- When the user explicitly asks to verify their understanding, summarize what changed, why it changed, what evidence verifies it, and what remains unverified.
- Ask questions that test the user's understanding of the actual work, not trivia.
- Withhold answers until the user responds, then identify the specific understanding gaps.
- If the user only asked the Agent to complete and verify work, deliver the evidence-backed completion report without forcing a quiz; offer the reverse quiz as an optional next step.
- Treat the quiz as a comprehension check, never as approval to merge or release.

## Return a decision-ready result

Use the user's language. Adapt the length to the task, but preserve these fields when they are relevant:

```markdown
## 当前阶段
[Before execution / During execution / After completion]

## 采用方法
[Selected method and why it is the smallest useful choice]

## 已核验证据
[Facts and their evidence]

## AI 假设
[Unverified possibilities, clearly labeled]

## 需要人决定
[Only decisions that genuinely require the user]

## 产出
[Rewritten brief, prototypes, specification, implementation, notes, or quiz]

## 下一步
[Smallest concrete next action]
```

Do not manufacture empty sections. If no human decision is required, say so briefly and continue.

## Preserve safety and review boundaries

- A blind spot pass produces candidates for verification, not facts.
- Prototypes reveal possible preferences; they are not user research or validation.
- A reference does not grant permission to copy its code, design, assets, or branding.
- Implementation notes document deviations; they do not expand the Agent's authority.
- A reverse quiz does not replace code review, automated tests, security review, domain experts, or real users.

## Attribute the method correctly

The English methods `blind spot pass`, `brainstorms and prototypes`, `interviews`, `references`, `implementation notes`, and `quiz me` come from Thariq Shihipar's talk *Field Guide to Fable*.

The Chinese method cards, exact output structures, additional permission and safety rules, and the combined before/during/after routing were editorially developed for AI Builders 解读 01 by Elisedai在创造. Treat portability across Agent products as an editorial generalization, not as an official Anthropic workflow.
