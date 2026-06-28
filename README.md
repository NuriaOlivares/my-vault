# My Knowledge Vault

A personal AI memory system. Plain Markdown files, tracked in Git.
One vault. Multiple agents. Knowledge compounds over time.

---

## What this is

Instead of explaining context to Claude every single session,
I keep everything here. Any agent reads this vault before working.
Over time the vault gets smarter, and every agent that reads it gets better.

---

## Who uses this vault

| Agent | Trigger | What it does |
|-------|---------|-------------|
| claude-agent | PR opened on GitHub | Reviews code against project conventions |
| claude-agent | PR merged on GitHub | Updates the relevant project file |
| meeting-agent | Every morning at 8am | Generates cheatsheet for today's meetings |
| meeting-agent | Transcript lands in inbox | Summarises meeting, updates client file |

---

## Folder structure

```
my-vault/
  CLAUDE.md              ← the rules. every agent reads this first.
  README.md              ← this file. for humans.
  00_index/
    index.md             ← table of contents + routing table
  10_inbox/
    transcripts/         ← raw meeting transcripts land here
    cheatsheets/         ← generated cheatsheets saved here
  20_knowledge/          ← reusable patterns, not project-specific
  30_projects/           ← one file per code project
  30_clients/            ← one file per client or company
  90_memory/
    lessons.md           ← mistakes and corrections
```

---

## Daily workflow

### Starting any session

1. Open the relevant file (project or client).
2. Paste CLAUDE.md + that file into Claude.
3. Work. Claude has full context.

### Ending any session

Paste this into Claude at the end:

> "Update the relevant vault files based on our session.
> Add decisions made, problems solved, open items, and anything new.
> If you made a mistake I corrected, add it to lessons.md."

Review the changes. Commit.

```bash
cd ~/my-vault
git add .
git commit -m "session: [what you worked on]"
git push
```

---

## Adding a new code project

1. Create `30_projects/your-project-name.md` using this template:

```markdown
# Project: [Name]

> Summary: one line.

## What this does
## Stack
## Conventions
## Decisions made
## Problems solved
## Open items
```

2. Add a row to `00_index/index.md` under Projects.

---

## Adding a new client

1. Create `30_clients/client-name.md` using this template:

```markdown
# Client: [Name]

> Summary: one line.

## Key people
## What they care about
## Decisions made (do not re-open these)
## Open items
## Meeting history
| Date | Key outcome |
|------|------------|
## Notes
```

2. Add a row to `00_index/index.md` under Clients.

---

## Git setup (one time)

```bash
cd ~
mkdir my-vault
cd my-vault
git init
git add .
git commit -m "init: vault structure"

# Push to GitHub private repo
git remote add origin git@github.com:yourusername/my-vault.git
git branch -M main
git push -u origin main
```