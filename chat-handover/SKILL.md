# Cursor Chat Handover

## Purpose

When the current Cursor conversation becomes long enough that continuing in the same chat may reduce context quality, generate a concise **handover summary** that can be pasted into a new Cursor chat.

The purpose is to transfer the important context from the current conversation so the new chat can continue the work without losing the original goal, reasoning, decisions, constraints, or implementation direction.

This is a **continuation handover**, not a generic conversation summary.

---

## When to use

Generate the handover when:

* The conversation has become long or complex.
* The work has already gone through several implementation steps.
* The current task is part of a larger multi-step implementation.
* A new Cursor chat will be opened to continue the work.
* The current chat recommends starting a new chat because context is becoming large.

If the user explicitly asks for a handover/context summary, generate it immediately.

---

## What to preserve

Extract the information that is necessary for another developer/AI to continue the work correctly.

Prioritize:

### 1. Original Goal

What are we ultimately trying to accomplish?

State the end goal in a few sentences.

Do not describe only the latest subtask. Preserve the larger purpose behind the work.

### 2. Current Context

Briefly explain:

* What part of the product/system this concerns.
* Relevant architecture or flow.
* Important existing behavior.
* Important files, modules, tables, APIs, functions, or components when they matter.

Only include information relevant to continuing this task.

### 3. Implementation Plan

Preserve the larger implementation plan.

If the original task was broken into multiple parts, show:

* What has been completed.
* What is currently being worked on.
* What remains.
* The intended order of the remaining work.

Do not lose the relationship between the smaller tasks and the larger goal.

### 4. Decisions Already Made

Preserve important decisions made during the conversation.

For each decision, capture:

* What was decided.
* Why it was decided, when the reasoning is important.

The next chat must NOT casually revisit or reverse an established decision unless new evidence requires it.

### 5. Constraints and Requirements

Preserve important constraints such as:

* Existing architecture that should be followed.
* Technologies or patterns that must be used.
* Things that must NOT be changed.
* Business rules.
* Validation requirements.
* Security or permission requirements.
* Backward-compatibility requirements.
* Naming or implementation conventions.

### 6. Important Discoveries

Include important findings discovered during investigation.

For example:

* Existing behavior that affects the implementation.
* Existing bugs or gaps.
* Important dependencies.
* Unexpected relationships between components.
* Relevant edge cases.
* Things that initially appeared one way but were discovered to work differently.

### 7. Completed Work

Clearly state what has already been implemented.

Include relevant:

* Files changed.
* Functions/components added or modified.
* Database changes.
* APIs/Edge Functions changed.
* Tests added.
* Configuration changes.

Do not make the next chat repeat completed work.

### 8. Current State

Describe exactly where the work stands now.

For example:

> Part 7 of 15 is complete. The backend changes are finished. The frontend integration remains.

The new chat should immediately understand what it is inheriting.

### 9. Remaining Work

List the next concrete pieces of work.

Keep them aligned with the original plan.

### 10. Open Questions / Unresolved Issues

Include only questions that genuinely remain unresolved.

Do not turn already-decided questions into open questions.

### 11. Important Files

Include a short list of the most relevant files and why they matter.

Example:

```text
src/features/billing/checkout.ts
→ Main checkout flow.

supabase/functions/create-checkout/index.ts
→ Creates the Stripe checkout session.

supabase/functions/stripe-webhook/index.ts
→ Handles subscription updates.
```

Do not dump the entire repository structure.

---

## Important behavior

The handover must preserve **intent**, not just facts.

The next Cursor chat should understand:

> What are we building?

> Why are we building it?

> What approach did we choose?

> What decisions have already been made?

> What has already been completed?

> What remains?

> What should I avoid changing?

> What should I do next?

The summary should make these answers obvious.

---

## Do not do this

Do NOT:

* Summarize every message chronologically.
* Include irrelevant conversation.
* Include repeated explanations.
* Include every command or tool call.
* Include generic information about the codebase.
* Repeat code unnecessarily.
* Include reasoning that no longer affects the implementation.
* Invent missing information.
* Assume that an implementation is complete when the conversation did not confirm it.
* Re-open decisions that were already settled.
* Replace specific decisions with vague statements such as "we discussed the architecture."

Avoid producing a huge transcript-like summary.

---

## Handover format

Use this structure:

# HANDOVER — [Short Task Name]

## 1. Goal

[The overall objective and why we are doing it.]

## 2. Context

[Only the relevant product/architecture context needed to understand the task.]

## 3. Implementation Plan

### Completed

* [Part]
* [Part]

### Current

* [Current part and exact state]

### Remaining

* [Next part]
* [Next part]
* [Next part]

## 4. Key Decisions

* **Decision:** ...
  **Reason:** ...

* **Decision:** ...
  **Reason:** ...

## 5. Important Requirements / Constraints

* ...
* ...
* ...

## 6. Important Discoveries

* ...
* ...
* ...

## 7. Current Implementation State

[Concise description of what exists now and what is working.]

## 8. Open Issues / Questions

* ...
* ...

## 9. Important Files

* `path/to/file`
  → Why it matters.

* `path/to/file`
  → Why it matters.

## 10. Next Step

[Give the next Cursor chat a clear starting point.]

---

## Final instruction

Write the handover so that a **fresh Cursor chat with no knowledge of this conversation** can understand the task and continue correctly after reading it.

The handover should be **concise but complete**.

Prefer high-information bullet points over long paragraphs.

Preserve important technical and business context even if it makes the summary slightly longer.

Do not optimize for minimum length at the cost of losing important decisions, constraints, intent, or implementation direction.

The goal is:

**New chat should feel like it is continuing the same engineering session, not starting the task from scratch.**
