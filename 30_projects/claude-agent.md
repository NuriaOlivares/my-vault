# Project: Claude Coding Agent

> Summary: A Python agent that reviews PRs against vault conventions 
> and updates the vault after merges. Runs on GitHub Actions.

---

## What this does

1. When a PR is opened → reads the PR diff + vault project file → 
   posts a code review comment on GitHub
2. When a PR is merged → reads what changed → updates the relevant 
   vault file automatically

---

## Stack

- Language: Python 3.11+
- Automation: GitHub Actions
- AI: Claude API (claude-sonnet-4-6)
- External APIs: GitHub REST API
- Package manager: pip
- Virtual environment: venv

---

## Repo structure (planned)

claude-agent/
  .github/
    workflows/
      pr-review.yml       ← triggers on PR open
      vault-update.yml    ← triggers on PR merge
  agent/
    review.py             ← reads PR diff + vault, calls Claude, posts comment
    vault_update.py       ← reads merged PR, updates vault file
    github_client.py      ← wrapper for GitHub API calls
    claude_client.py      ← wrapper for Claude API calls
  tests/
    test_review.py
  requirements.txt
  README.md

---

## Conventions

- Use type hints on every function.
- Every function has one job. If it does two things, split it.
- No silent error handling. If something fails, raise or log loudly.
- Environment variables for all secrets. Never hardcode API keys.
- Keep functions under 30 lines. If longer, it needs to be split.

---

## Decisions made

- Using claude-sonnet-4-6 not opus: cheaper, fast enough for PR reviews.
- GitHub Actions over a server: free, no infrastructure to maintain.
- Separate workflows for review and vault-update: cleaner, easier to debug.
- venv for isolation: standard Python practice, no extra tools needed.

---

## Open items

- [ ] Set up the repo and venv (Week 1)
- [ ] Write claude_client.py and test it locally (Week 1)
- [ ] Write github_client.py (Week 2)
- [ ] Write review.py and connect everything (Week 2)
- [ ] Write the GitHub Actions workflow (Week 2)
- [ ] Write vault_update.py (Week 3)
- [ ] Test on a real PR (Week 3)

---

## Problems solved

## Problems solved

- GitHub Actions 403 error when posting comments — fixed by adding
  `permissions: pull-requests: write` to the workflow YAML file.
  GitHub Actions tokens have read-only permissions by default.

- github_client.py created on wrong branch — was on test/first-pr
  instead of main. Fixed by using `git checkout main -- agent/github_client.py`
  to copy the file across branches.

- Vault not accessible on GitHub Actions — the Linux machine GitHub
  spins up has no access to local Mac files. Fixed by adding a second
  checkout step in the workflow that downloads the vault repo onto
  the GitHub machine before running the agent.

---

## Lessons learned

*(empty — will fill as we go)*