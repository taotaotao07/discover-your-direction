# Evidence Mirror

Build a consented, traceable mirror of evidence. Treat every pattern as tentative and falsifiable.

## Consent gate

- Offer two routes: a direct interview or files the user selects explicitly.
- Never scan the workspace implicitly.
- Resolve the exact files first. Restate the complete path list, say the access is read-only, and require affirmative confirmation before reading.
- Do not follow links, transclusions, attachments, symlinks, or references outside the confirmed list without fresh consent.
- Pause on secrets or credentials, system files, executables or binaries, unexpectedly broad directories, and unrelated personal data. Explain the reason: security risk, unsafe or irrelevant format, excessive scope, or privacy exposure.
- Ask the user to narrow any broad, suspicious, sensitive, or oversized selection before proceeding.
- List the files actually used in the final response.
- Never modify, rename, move, or annotate a source file.

## Evidence extraction

Extract concrete episodes that show:

- repeated actions;
- difficult outcomes achieved;
- recurring requests from other people;
- actual time, money, reputation, or other commitment that others invested;
- transferable skills;
- energy gains or drains;
- returns after setbacks;
- judgment under uncertainty;
- contradictions and counterexamples.

Prefer specific behavior, decisions, consequences, and context over topic frequency. Ask what happened, what the user did, what made it difficult, and what changed.

## Canonical evidence records

Use this file as the canonical schema. Keep source observations and current AI inferences as separate record types. The three-axis classification applies **only** to source observations.

### Source-observation record

Record:

- `source observation ID`
- `claim status`: `source observation/paraphrase`
- `observation`: the quoted or faithfully paraphrased source content
- `quoted or paraphrased`
- `provenance`: `direct artifact/record`, `user self-report`, `AI transcript user turn`, or `AI transcript model turn`
- `evidence kind`: `first-hand behavior/outcome`, `relational commitment`, `interest/energy self-report`, or `contextual clue`
- `source reference`, in exactly one applicable form:
  - selected file: file path + precise heading, line, message, or timestamp locator;
  - live interview: `current conversation` + turn or message locator;
  - stored chat: transcript file + speaker and message or timestamp locator.

A user-described action remains `user self-report` unless a separate source corroborates it. Treat model turns only as AI-conversation (AI-chat) clues: model-generated identity stories can echo across conversations. Seek behavior, contradiction, or independent confirmation. Prefer concrete, repeated episodes over frequency or category alone.

### Current-AI-inference record

Never call a current AI inference evidence. Record it separately with:

- `inference ID`
- `claim status`: `current AI inference`
- `linked source-observation IDs`
- `interpretation`
- `alternative interpretation`
- `strongest known contradiction`
- `missing evidence`
- `confidence`: `strong`, `mixed`, or `weak`

Do not add `provenance`, `evidence kind`, or a source reference to an inference record. Set confidence from the specificity and quality of linked observations, independent repetition, and contradictions—not from provenance or evidence kind alone. Use `strong` for specific, high-quality support with independent repetition and no material unresolved contradiction; `mixed` for meaningful support with limited repetition or a material contradiction; and `weak` for vague, low-quality, uncorroborated, or substantially contradicted interpretations. Record counterexamples instead of smoothing them away. Do not calculate a composite score.

## Evidence ledger

Maintain the two linked record collections above. Never merge observation fields into an inference record or attach inference fields to a source observation.

## Mirror output

- Present no more than five tentative patterns.
- For each pattern, cite the linked source-observation IDs and their source references.
- State the strongest known contradiction or counterexample whenever one exists.
- State the key missing evidence separately from the contradiction.
- Mark uncertainty plainly and invite correction.
- State that user correction overrides AI interpretation.
- End with the files actually used. Say that the agent used them only for reading and did not modify them; do not claim protection against changes by other processes.
