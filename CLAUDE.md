# CLAUDE.md — My Personal Assistant Rules

This file is the contract between me and any agent that reads this vault.
Read this before doing anything. Every session. No exceptions.

---

## Who I am

Full-stack engineer working mostly with JavaScript/TypeScript and Java.
Re-learning Python — explain Python things more carefully.
Learning AI and ML — still early, explain concepts before using them.
I use Mac. My editors are VSCode and IntelliJ.
I am a native Spanish and Catalan speaker, professional English speaker — keep explanations clear, avoid unnecessary jargon.

---

## How to talk to me

- Explain things clearly, like I am smart but new to this specific topic.
- When you introduce a concept I may not know, define it briefly before using it.
- Prefer concrete examples over abstract descriptions.
- Do not over-explain things I already know: JavaScript, TypeScript, REST APIs, Git, SQL basics.
- When I ask a Python question, assume I know the concept but not the Python syntax.
- When I ask about AI/ML, assume I know software engineering but not the AI-specific parts.

---

## Code style preferences

### JavaScript / TypeScript
- Use TypeScript by default when writing new code.
- Use const by default, let only when needed, never var.
- Use arrow functions for callbacks.
- Prefer functional approaches (map, filter, reduce) over loops when it reads clearly.
- Always handle errors explicitly — no silent catches.

### Java
- Prefer Java over Kotlin — I have not worked with Kotlin yet.
- Use clear, explicit types — avoid over-engineering with generics unless necessary.
- Follow standard Java naming conventions (camelCase methods, PascalCase classes).

### Python
- Use type hints always: def my_func(name: str) -> int.
- Follow PEP 8.
- Explain any Python-specific patterns you use — I may not recognise them initially.
- Prefer simple and explicit over clever and compact.

### General (all languages)
- Write comments only when the WHY is not obvious from the code.
- Keep functions small and single-purpose.
- If writing a test, use the same framework already in the project.
- Never use a library or dependency not already in the project without asking first.

---

## Meeting and client context

- Client files live in 30_clients/. Read the relevant one before anything client-related.
- Meeting transcripts land in 10_inbox/transcripts/. Process them after meetings.
- Cheatsheets go in 10_inbox/cheatsheets/ and are named [date]-[client].md.
- When summarising a meeting, extract: decisions made, open items, next steps, anything that changed.
- When generating a cheatsheet, include: who is attending, what they care about, open items, decisions that are final.

---

## What to always do

- Before any task, read 00_index/index.md to understand what exists in the vault.
- Find and read the most relevant file for the current task before starting:
  - Coding task → read the relevant file in 30_projects/
  - Client or meeting task → read the relevant file in 30_clients/
  - General pattern or concept → check 20_knowledge/ first
- Check 90_memory/lessons.md for lessons learned before making suggestions.
- If a decision is already recorded anywhere in the vault, respect it — do not re-suggest alternatives.
- If you are unsure about something, say so. Do not guess silently.

---

## What to never do

- Never push to main or suggest force pushes.
- Never delete files without explicit confirmation.
- Never make changes outside the scope of the current task.
- Never ignore existing conventions in a project just because you have a preference.
- Never use a library or dependency I have not already approved without asking first.
- Never store raw meeting recordings or transcripts long-term — store derived summaries only.

---

## How to update the vault

After any useful session:

| What happened | Where it goes |
|--------------|---------------|
| Technical decision in a project | 30_projects/[project].md → Decisions made |
| Client decision or preference discovered | 30_clients/[client].md → Decisions made |
| Reusable pattern or concept | 20_knowledge/[topic].md |
| Meeting summary | 30_clients/[client].md → Meeting history |
| Mistake Claude made or correction given | 90_memory/lessons.md |
| New file created anywhere | 00_index/index.md → add a row |

---

## If you are starting a new session

1. Read this file fully.
2. Read 00_index/index.md to understand what exists in the vault.
3. Ask me what we are working on today.
4. Read the most relevant file for that task before touching anything.