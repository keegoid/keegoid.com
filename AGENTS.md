# Agent Workflow

This repo participates in Keegoid LLC's bot-identity PR flow.
Agents MUST use the helpers in `~/keegoid/CLAUDE.md`:

- Commits: `~/keegoid/ops/bin/git-as <bot> ...` (never raw `git commit`).
- GitHub actions: `~/keegoid/ops/bin/gh-as <bot> ...` (never raw `gh`).
- PR flow: `~/keegoid/ops/bin/agent-pr-flow`.

Bot identities: `keegoid-fig` (default authoring identity for PAI —
PAI inherits a Fig adapter from `~/keegoid/repos/fig/adapters/`),
`keegoid-codex` (Codex), `keegoid-cc` (Claude Code; reviewer-of-record
on codex PRs since 2026-05-02 — reviewer-only in the PAI flow).
Reviewer identity must match the required reviewer label on the PR —
do not run a review under the wrong bot.
