# Cursor Skills

A collection of practical skills for improving AI-assisted software development with [Cursor](https://cursor.com/).

The goal is simple: use AI coding tools more effectively by giving them better context, clearer instructions, and repeatable workflows.

## Skills

| Skill                             | Description                                                                                                                                               |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Chat Handover](./chat-handover/) | Creates a concise handover when moving a long implementation from one Cursor chat to a new one without losing important context, decisions, or direction. |

## Why this repository?

AI coding tools are powerful, but long development sessions can become difficult to manage.

A large feature may take many small implementation steps. As the conversation grows, the AI has to process more context, and eventually it can become useful to start a fresh chat.

The problem is that a new chat does not automatically know everything that was established in the previous one.

These skills are intended to solve practical problems like this with simple, reusable workflows.

## Using a skill

Each skill lives in its own folder and contains:

* `SKILL.md` — the actual skill instructions
* `README.md` — explanation, use case, and usage instructions

Browse into the skill's folder to see how to use it.

## Skills in this repository

### Chat Handover

When a Cursor conversation becomes long, use the Chat Handover skill to create a compact context package for the next chat.

It preserves the important parts of the work, including:

* Original goal
* Current context
* Implementation plan
* Completed work
* Remaining work
* Important decisions
* Requirements and constraints
* Important discoveries
* Current implementation state
* Open issues
* Relevant files
* Next step

The goal is not to summarize every message.

The goal is to make a new Cursor chat feel like a continuation of the previous engineering session.

→ [View Chat Handover](./chat-handover/)

---

## Contributing

More skills will be added over time.

If you have a useful workflow for working with AI coding tools, feel free to adapt the ideas in this repository for your own projects.

## License

This repository is intended to be freely usable and adaptable. Add an explicit license here if you decide to publish the repository under a specific open-source license.
