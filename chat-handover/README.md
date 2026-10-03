# Cursor Chat Handover

A Cursor skill for continuing large implementation tasks across multiple AI chat sessions without losing important context.

## The problem

Large development tasks rarely finish in a single conversation.

A feature might look like:

```text
Large Feature
    ↓
Implementation Plan
    ↓
Part 1
    ↓
Part 2
    ↓
Part 3
    ↓
...
    ↓
Part 15
```

To keep the work manageable, it can be useful to start a new Cursor chat after several implementation steps.

But a new chat does not have the full context of the previous conversation.

It may not know:

* What the original goal was
* Why the feature is being built
* What decisions were already made
* Which approaches were rejected
* What has already been implemented
* What remains
* What constraints must be respected
* What important discoveries were made
* What the next step should be

Simply telling the new chat:

> "Continue the feature from here."

is not enough.

## The solution

The **Chat Handover** skill creates a concise handover before moving to a new Cursor chat.

The handover acts as a bridge:

```text
Chat 1
  ↓
Implementation
  ↓
Handover
  ↓
New Chat
  ↓
Continue implementation
```

Instead of transferring the entire conversation, it transfers the information that matters for continuing the work.

## What it preserves

The skill captures the important context from the current conversation:

* **Original Goal** — what we are ultimately trying to accomplish
* **Context** — relevant product and architecture information
* **Implementation Plan** — the larger plan and its progress
* **Key Decisions** — decisions that should not be casually changed
* **Requirements / Constraints** — rules the implementation must follow
* **Important Discoveries** — findings that affect the implementation
* **Completed Work** — what has already been implemented
* **Current State** — exactly where the work stands
* **Remaining Work** — what still needs to be done
* **Open Issues** — unresolved questions
* **Important Files** — files the next chat should know about
* **Next Step** — where the new chat should start

## What makes it different from a normal summary?

A normal summary often focuses on:

> "What happened in this conversation?"

A handover focuses on:

> "What does the next developer/AI need to know to continue this work correctly?"

That distinction is important.

The skill preserves **intent and direction**, not just conversation history.

## How to use it

Add the `SKILL.md` instructions to your Cursor skills/rules setup.

When your implementation chat becomes long or you are ready to move to a new chat, ask Cursor to generate a handover using the skill.

For example:

```text
Generate a handover for this implementation so I can continue in a new Cursor chat.
```

Copy the generated handover into the new Cursor chat.

Then continue the implementation from the stated current state and next step.

## Recommended workflow

For a large feature:

```text
1. Define the overall goal
          ↓
2. Ask Cursor to investigate the codebase
          ↓
3. Create a large implementation plan
          ↓
4. Break the plan into smaller parts
          ↓
5. Implement several parts in one chat
          ↓
6. Generate a handover
          ↓
7. Start a new Cursor chat
          ↓
8. Paste the handover
          ↓
9. Continue from the current state
          ↓
10. Repeat when needed
```

This allows large tasks to be split across multiple focused conversations without repeatedly explaining the entire feature from scratch.

## Example

Suppose you are implementing a billing feature that involves:

```text
Frontend
    ↓
Edge Function
    ↓
Stripe
    ↓
Webhook
    ↓
Database
```

After several implementation steps, the first Cursor chat may have already established:

* how billing currently works
* which Stripe objects are used
* why a particular architecture was selected
* which database changes are required
* which edge cases must be handled
* which files have already been changed
* which implementation steps remain

The handover transfers that context to the next chat.

The new chat can then start from:

> "Here is where we are and why we got here."

instead of:

> "Please figure out the entire project again."

## Design principle

The handover should be:

**Concise enough to paste into a new chat.**

but:

**Complete enough that important context is not lost.**

It should not become a transcript of the previous conversation.

The goal is to preserve the **engineering context required for continuity**.

---

## Files

* [`SKILL.md`](./SKILL.md) — the actual Cursor skill
* `README.md` — this documentation

## Repository

This skill is part of the [Cursor Skills](../) collection.
