# adr-threat-review

A GitHub Action workflow that asks Adam Shostack's four questions about every architecture decision record (ADR) in a pull request, and comments with feedback.

It is a reviewer, not a gate: it drafts, people decide.

## Setup
1. Add `ANTHROPIC_API_KEY` to the repo secrets.
2. Copy `.github/` and `docs/adr/0000-template.md` into your repo.
3. Protect `main`, and turn on "Require review from Code Owners" so nobody (including an agent) can change the checks without a human.

## Safety defaults
- Runs on `pull_request`, never `pull_request_target`, and skips fork PRs.
- Token is read-only except for PR comments. No other secrets.
- The prompt tells the model to treat ADR text as data, and limits it to `gh pr diff` and `gh pr comment`.
- Actions are pinned to a commit SHA.
- The LLM output is non-deterministic and costs tokens on every ADR PR.

The example ADRs describe [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/), a web shop that is vulnerable on purpose.
