# Project: My Knowledge Vault

> Summary: A personal AI memory system. One shared vault of Markdown files 
> used by multiple agents across coding, meetings, and learning.

---

## What this is

A Git-tracked folder of Markdown files that acts as persistent memory 
for any AI agent I build or use.

The goal: any agent reads this vault before working, so context is never 
lost between sessions and never has to be re-explained.

---

## Design principles (from the source slides)

- One shared vault — not one vault per topic or project
- Plain Markdown files in Git — no lock-in, always readable by AI
- Index first — agents navigate, they do not scan every file
- Humans validate — agents suggest, humans approve
- Scripts for sorting, AI for judgment

---

## Folder structure

```
my-vault/
  CLAUDE.md                  ← rules for any agent reading this vault
  00_index/
    index.md                 ← master index and routing table
  10_inbox/
    transcripts/             ← raw meeting transcripts
    cheatsheets/             ← generated meeting prep sheets
  20_knowledge/              ← reusable patterns and concepts
  30_projects/               ← one file per code project
  30_clients/                ← one file per client (for meeting agent)
  90_memory/
    lessons.md               ← mistakes and corrections across all work
```

---

## Agents that use this vault

| Agent | What it does | Reads from | Writes to |
|-------|-------------|------------|-----------|
| claude-agent | Reviews PRs, updates vault after merges | 30_projects/, 20_knowledge/ | 30_projects/ |
| meeting-agent | Preps cheatsheets, summarises meetings | 30_clients/, 10_inbox/ | 30_clients/, 10_inbox/cheatsheets/ |

---

## Decisions made

- One vault for everything — coding, meetings, learning, clients
- Separate 30_clients/ from 30_projects/ — different structure, different agents
- Git for version control — AI edits are permanent, Git gives rollback
- CLAUDE.md covers all agents — one contract, not one per agent
- Raw transcripts stay in inbox only — summaries go into client files

---

## Current workflow (manual loop)

1. Start a session — paste CLAUDE.md and the relevant file into Claude
2. Do the work
3. End of session — ask Claude to update the relevant files
4. Review the changes like a PR diff
5. Commit to Git

---

## Next steps

- [ ] Push vault to GitHub private repo
- [ ] Add first real client file to 30_clients/
- [ ] Build claude-agent (PR reviewer)
- [ ] Build meeting-agent (cheatsheet + summary)
- [ ] Automate the write-back step so agents update the vault themselves

---

## Open questions

- How often to commit? After every session feels right for now.
- Should lessons.md be split by topic eventually, or stay as one file?