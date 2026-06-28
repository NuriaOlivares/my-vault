# Master Index

This is the first file any agent or human should read.
It maps everything in the vault so you never have to open every folder.

Last updated: June 2026

---

## Projects (30_projects/)
Code projects and technical work.

| File | What it is | Status |
|------|-----------|--------|
| claude-agent.md | Python agent that reviews PRs and updates the vault | Active |
| my-vault.md | The knowledge vault project itself — this system | Active |

---

## Clients (30_clients/)
One file per client or company. Used by the meeting agent.

| File | Who | Status |
|------|-----|--------|
| *(empty — add my first client when ready)* | | |

---

## Knowledge (20_knowledge/)
Reusable patterns and concepts. Not project-specific.

| File | What it covers |
|------|---------------|
| api-patterns.md | REST API conventions and response structures |
| typescript-patterns.md | TypeScript patterns used regularly |
| python-notes.md | Python syntax and patterns — learning reference |

---

## Memory (90_memory/)

| File | What it covers |
|------|---------------|
| lessons.md | Mistakes, corrections, and things to remember across all work |

---

## Inbox (10_inbox/)
Temporary landing zone. Processed and moved elsewhere.

| Folder | What lands here |
|--------|----------------|
| transcripts/ | Raw meeting transcripts — processed then summarised into 30_clients/ |
| cheatsheets/ | Generated meeting cheatsheets — named [date]-[client].md |

---

## Routing table
When new information comes in, where does it go?

| Type of information | Where it goes |
|--------------------|---------------|
| Decision made in a code project | 30_projects/[project].md → Decisions made |
| Decision made with a client | 30_clients/[client].md → Decisions made |
| Reusable code pattern | 20_knowledge/[topic].md |
| Bug solved in a specific way | 30_projects/[project].md → Problems solved |
| Python concept learned | 20_knowledge/python-notes.md |
| AI/ML concept learned | 20_knowledge/ai-ml-notes.md |
| Mistake Claude made | 90_memory/lessons.md |
| Meeting happened | 30_clients/[client].md → Meeting history |
| New file created | This index → add a row |
| New preference or rule | CLAUDE.md |