# Brownify

Brownify packages GitHub pull request lifecycle skills for Claude Code and
Codex. Invoke skills with their `brownify:` namespace to avoid collisions.

## Latest release

Version `0.1.0` publishes nine pull request lifecycle skills for Claude Code
and Codex. Plugin installs use the `brownify:` namespace. Direct `npx skills`
installs use unscoped skill names.

## Skills

| Skill | Say | What it does |
|---|---|---|
| `full-send` | "full send" | Takes a change to a merged PR with nobody watching: proves it, reviews it, files it, babysits it, merges it. |
| `full-stop` | "full stop" | Same as `full-send`, but stops when the PR is ready for you to merge. |
| `council` | "council" | Gets review from three models from different providers, and loops until they agree. |
| `sol-loop` | "sol loop" | Reviews a change with GPT Sol in a loop until both agents agree. |
| `file-pr` | "file a PR" | Files a short PR that leads with the problem, not an inventory of changes. |
| `takeover` | "take over" | Finishes someone else's PR, branch, or agent thread, and keeps their credit. |
| `babysit-pr` | "babysit" | Watches a PR through CI and review bots, and fixes the real findings. |
| `modernize` | "modernize" | Rebases an old PR and decides if it should still exist. |
| `leaving-pr-comments` | (automatic) | Formats comments that an agent posts on your behalf. |

Some skills call others. Install the ones they need too:

- `full-send` uses `sol-loop`, `file-pr`, and `babysit-pr`.
- `full-stop` uses `sol-loop`, `file-pr`, and `babysit-pr`.
- `takeover` uses `modernize`, `file-pr`, `babysit-pr`, and `leaving-pr-comments`.
- `file-pr`, `babysit-pr`, and `modernize` use `leaving-pr-comments`.

## Install

Install plugin to keep skill names scoped under `brownify`.

### Claude Code

```bash
claude plugin marketplace add borg0ai/as-brownify
claude plugin install brownify@brownify-marketplace
```

Invoke a skill as `/brownify:full-send`.

### Codex

```bash
codex plugin marketplace add borg0ai/as-brownify
codex plugin add brownify@brownify-marketplace
```

Invoke a skill as `$brownify:full-send`.

Direct skill installation remains available through `npx skills`, but it
installs skills without the `brownify:` namespace.

## Requirements

- An authenticated [GitHub CLI](https://cli.github.com) (`gh`).
- `python3` for `babysit-pr`'s `pr-wait` script.
- `council` and `sol-loop` need subagents on other providers' models. T3 Code
  does this with `delegate_task`. Otherwise you need a harness that can run
  those models.

## Make them yours

These are starting points. Edit them. Put personal settings, like which models
sit on your council, in your `CLAUDE.md` or `AGENTS.md`, so you can update the
skills without losing them.

## License

[MIT](LICENSE)
