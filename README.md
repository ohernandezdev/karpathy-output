# karpathy-output

Agent skill that turns a large language-model dump into something a human can check.

Based on [Andrej Karpathy's note](https://x.com/karpathy/status/2105819303471976479) (2 Oct 2026): ASD-STE100 prose, diagrams, interactive HTML, and 3Blue1Brown-style explainer videos. The STE limits come from the sheet attached to that post, not from the full ASD-STE100 specification.

This is not an official Karpathy or ASD project.

## What the agent does

It picks the cheapest rung that makes the claim checkable:

1. STE prose at about 80% of ASD-STE100 (20/25 word caps, approved verb forms, dictionary swaps).
2. One Mermaid diagram. Nodes only from the source.
3. One self-contained interactive HTML file.
4. A shot list for an explainer video. It does not pretend a video was rendered.

The artifact is a view, not evidence. The agent must list claims that still need the original source.

## Install

Any agent that loads a folder with `SKILL.md` can use this. Clone, copy the folder, tell the agent to read `SKILL.md`.

```bash
git clone https://github.com/ohernandezdev/karpathy-output.git
```

Project-local (Codex, Claude Code, and other agents that scan the repo):

```bash
mkdir -p .agents/skills
cp -R karpathy-output .agents/skills/karpathy-output
```

Claude Code, user-wide:

```bash
mkdir -p ~/.claude/skills
cp -R karpathy-output ~/.claude/skills/karpathy-output
```

Claude Code, this repo only:

```bash
mkdir -p .claude/skills
cp -R karpathy-output .claude/skills/karpathy-output
```

Paste this to the agent if it does not auto-load skills:

```text
Install the skill at https://github.com/ohernandezdev/karpathy-output.
Read SKILL.md. When I give you a model dump, follow that skill instead of writing another long summary.
```

## Layout

```text
SKILL.md                 trigger + workflow
references/ste100.md     sentence limits and dictionary swaps
references/prompts.md    copy-paste prompts
evals/                   trigger and behavior checks
```

## License

MIT. ASD-STE100 itself is a specification from ASD (asd-ste100.org). This repo only records the public limits shown on Karpathy's sheet.
