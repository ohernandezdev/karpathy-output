# Prompt bank

Use these as the transformation instruction. Fill the brackets. Keep the user's language in the output request.

## STE prose (80%)

Read `references/ste100.md` first. Then use:

```
Rewrite the source at about 80% of ASD-STE100.
Limits:
- Procedural sentence: max 20 words. Descriptive sentence: max 25 words.
- Max 6 sentences per paragraph. One topic per paragraph.
- Noun cluster: max 3 words. One instruction per sentence.
- Active voice. Keep the, a, this.
- Approved verb forms only: imperative, simple present, simple past, simple future, infinitive.
- Do not use progressive, perfect, or passive in a procedure.
- Swaps: commence→START, ensure→MAKE SURE, utilize→USE, prior to→BEFORE, replenish→FILL, approximately→ABOUT, in order to→TO.
- Same word for the same thing. Do not add facts.
- End with claims the source does not support.
Source:
[PASTE]
```

## Diagram

```
Do not write an essay. Make one Mermaid diagram of [architecture | call chain | causality | dependencies].
- Nodes only from the source.
- Edge labels are verbs: calls, writes, blocks, causes.
- Mark missing links as "?".
- After the diagram, list 5 claims to verify in the source.
Source:
[PASTE]
```

## Interactive page

```
Build one self-contained HTML file. No external network.
Show this claim: [CLAIM]
Controls: [PARAMETERS]
Live output must change when a control changes.
Add a guess step: hide the result until the user picks a direction or value.
Add a note: what this page does not prove.
Do not invent numbers that are not in the source. If a number is missing, show "unknown".
Source:
[PASTE]
```

## Video plan

```
Write a 3Blue1Brown-style shot list for [TOPIC]. Do not render video.
8 to 14 shots. Each shot: seconds, visual motion, one narration sentence (max 20 words), on-screen label.
Narration path: ElevenLabs if the user supplies a key, otherwise a local free alternative. Do not generate audio here.
One idea per shot. No bullet slides.
End with claims the video would assert that still need a source check.
Source:
[PASTE]
```

## Escalate

If the user already has STE text and still cannot check the result, move one rung up. Do not stack all four formats unless the user asks.
