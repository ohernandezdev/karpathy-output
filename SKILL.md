---
name: karpathy-output
description: "Turn large LLM dumps into forms a human can actually check: ASD-STE100 prose, diagrams, interactive HTML, or an explainer-video plan. Use when the user has too much model text, code, research, or a plan to read, or asks for Karpathy output formats, STE100, diagrams, interactive pages, or explainer videos instead of more writing."
type: workflow
lifecycle: active
---

# Karpathy Output — Understand the model, don't read the dump

Use this when model output outruns human reading speed. The job is oversight: turn the dump into a discardable artifact the user can scan, poke, or watch, then check claims against the source.

Do not summarize by writing another long essay. Pick the cheapest format that makes the structure checkable.

## Ladder

Escalate only when the current rung still hides the thing the user must judge.

| Rung | Use when | Do not use when |
|---|---|---|
| 1. STE prose | The issue is wording: long sentences, synonyms, vague claims | The issue is structure, time, or parameters |
| 2. Diagram | Relations matter: architecture, call chain, causality, dependencies | The user must change a parameter and see the result |
| 3. Interactive HTML | State, parameters, or counterfactuals matter | Motion over time is the actual subject |
| 4. Explainer video plan | Sequence, algorithm steps, or physical change is the subject | A static check is enough |

Default: start at the lowest rung that fits. Offer the next rung only if verification is still hard.

## Workflow

1. Name the decision the user must make (accept the code, trust the claim, see the bug, learn the mechanism).
2. Quote or keep the source dump available. The new artifact is a view, not evidence.
3. Pick a rung from the table. Say which rung and why in one line.
4. Produce the artifact in the user's language. Keep identifiers, APIs, and quotes in the original language.
5. Attach a check list of 3–7 claims the artifact asserts. Each claim must point back to a part of the source.
6. Flag what the artifact cannot show (missing data, untested branches, model guesses).

## Rung rules

### 1. STE prose

Ask for about 80% of ASD-STE100, not the full spec. Full STE is too rigid for explanations. Karpathy softens it the same way.

Enforce the limits in `references/ste100.md`. Short form:

- Procedural sentence ≤ 20 words. Descriptive sentence ≤ 25 words.
- ≤ 6 sentences per paragraph. One topic per paragraph.
- Noun cluster ≤ 3 words. One instruction per sentence.
- Approved forms: imperative, simple present/past/future, infinitive, participle as adjective.
- Not approved: progressive, perfect, passive in a procedure.
- Swap commence/ensure/utilize/prior to/replenish/approximately/in order to for START, MAKE SURE, USE, BEFORE, FILL, ABOUT, TO.
- Keep articles (the, a, this). Same word for the same thing.

Read `references/ste100.md` before writing STE prose. See `references/prompts.md` for the prompt.

### 2. Diagram

Produce a diagram the user can read in one pass. Prefer Mermaid in a fenced block unless the user asked for an image.

Pick one diagram type:

- flowchart for control and decisions
- sequence for calls over time
- graph for dependencies
- state for modes

Label edges with the actual relation (calls, writes, blocks), not "related to". Mark unknown edges as `?`. Do not invent nodes that are not in the source.

### 3. Interactive HTML

Build one self-contained HTML file. No build step. No external CDN unless the user asks.

Must include:

- the claim being tested, in one sentence
- controls for the parameters that change the result
- a visible before/after or live output
- a short "what this does not prove" note

Hide the answer behind a guess when the point is intuition: user picks up/down or a range, then reveals the model result.

### 4. Explainer video plan

Do not claim a rendered video unless a video tool actually ran. Default deliverable is a shot list a video tool can execute.

Each shot: duration, visual, narration (one STE sentence, ≤ 20 words), on-screen label. Style target: 3Blue1Brown — one idea, continuous motion, no slide walls. Karpathy's narration path is an ElevenLabs API key, or a free local alternative. Say which one the shot list assumes. Do not invent audio.

## Evidence rule

Diagrams, pages, and videos compress errors as well as signal. After the artifact, list claims that still need a look at the original source. Never tell the user the artifact replaces the source.

## Prompt bank

Read `references/prompts.md` when writing the transformation prompt or when the user wants reusable prompts rather than the artifact itself. Read `references/ste100.md` before any STE rewrite.
