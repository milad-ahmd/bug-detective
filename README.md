> [!NOTE]
> **This skill lives in the main collection: [milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills/tree/main/skills/bug-detective)**. Please ⭐ star it there; that's where updates land first.
> Docs: **https://milad-ahmd.github.io/agent-skills/skills/bug-detective/** · Claude Code: `/plugin install all-skills --marketplace milad-ahmd/agent-skills`

<div align="center">

# 🕵️ bug-detective

**Debug by reproducing first, logging hypotheses and auto-bisecting the commit that broke it. An Agent Skill for Claude Code, Cline, Cursor, Codex and other AI coding agents.**

[![License: MIT](https://img.shields.io/github/license/milad-ahmd/bug-detective)](LICENSE)
[![Stars](https://img.shields.io/github/stars/milad-ahmd/bug-detective?style=social)](https://github.com/milad-ahmd/bug-detective)
![Category](https://img.shields.io/badge/category-Testing%20&%20Quality-blue)
![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cline%20%7C%20Cursor%20%7C%20Codex-8A2BE2)

[Install](#-install) · [Usage](#-usage) · [How it works](skills/bug-detective/SKILL.md) · [All skills](https://github.com/milad-ahmd/agent-skills)

</div>

> Part of **[agent-skills](https://github.com/milad-ahmd/agent-skills)**, a growing collection of practical skills for AI coding agents.

## 📦 Install

**One command (installs the whole collection):**

```bash
curl -fsSL https://raw.githubusercontent.com/milad-ahmd/agent-skills/main/install.sh | bash -s -- bug-detective
```

**Manually (Claude Code):**

```bash
git clone https://github.com/milad-ahmd/bug-detective /tmp/bug-detective
mkdir -p ~/.claude/skills && cp -r /tmp/bug-detective/skills/bug-detective ~/.claude/skills/
```

**Per project:** copy `skills/bug-detective` into `<project>/.claude/skills/`.
**Any other agent:** paste [`SKILL.md`](skills/bug-detective/SKILL.md) into your rules or system prompt.

## 💬 Usage

Just ask your agent:

```text
This test passed last week and fails now, find the commit that broke it
The cart total is sometimes wrong, help me find out why
```

The full workflow, rules and output format are in [`SKILL.md`](skills/bug-detective/SKILL.md).

## 🔎 Sample output

`bisect_run.py` is plain Python 3 with no dependencies. Real output on a small repo where a cart total broke somewhere in 8 commits:

```text
$ python3 bisect_run.py --good v1.0 -- python3 test_cart.py

Checking the repro at both ends first:
  good  3a78346285  good
  bad   f496d7eb41  bad
Bisecting:
  1673fed043  good  (exit 0, run 1/1)
  bd6e296b35  bad   (exit 1, run 1/1)
  69c5a05d10  bad   (exit 1, run 1/1)

First bad commit: 69c5a05d10b22e1977410534bec22e99aa0208a5
  cart: apply discount per line
  Author: Dana Lee <dana@example.com>
  Date:   2026-10-15 10:00:00 +0000
  Steps:  3 (plus the check at --good and --bad)

 cart.py  | 4 ++--
 notes.md | 1 +
 2 files changed, 3 insertions(+), 2 deletions(-)

Read it with: git show 69c5a05
```

It refuses to start on a dirty tree, checks that `--good` passes and `--bad` fails before bisecting, and always restores your HEAD, Ctrl-C included. `--repeat N` handles flaky bugs.

## 🧩 More skills

See the full collection: **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 🤝 Contributing

This repo is a read-only mirror. Please open issues and PRs in **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 📄 License

[MIT](LICENSE) © Milad Ahmadi

<div align="center">

**If this skill saved you time, a ⭐ helps others find it.**

</div>
