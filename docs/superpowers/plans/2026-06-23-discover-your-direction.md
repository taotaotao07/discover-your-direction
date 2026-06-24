# Discover Your Direction Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build, validate, and publish a Chinese-first Codex Skill that helps experienced users select a falsifiable direction experiment without presenting AI inference as destiny.

**Architecture:** Keep orchestration and hard boundaries in `SKILL.md`. Load three focused references only when handling evidence, interviewing, or designing an experiment. Validate with the official checker, deterministic contract searches, and fresh-context forward tests.

**Tech Stack:** Markdown, YAML, official Python Skill utilities, Git, GitHub CLI.

---

## File map

- `discover-your-direction/SKILL.md`: trigger description, stages, transitions, and boundaries.
- `discover-your-direction/agents/openai.yaml`: user-facing Skill metadata.
- `discover-your-direction/references/evidence-mirror.md`: consent, provenance, evidence hierarchy, contradictions.
- `discover-your-direction/references/interview-guide.md`: six evidence dimensions, adaptive follow-ups, framing check.
- `discover-your-direction/references/direction-experiment.md`: direction cards, selection, experiment, review.
- `README.md`: public purpose, installation, usage, privacy, limitations.
- `LICENSE`: MIT license.

### Task 1: Scaffold the Skill

**Files:**
- Create: `discover-your-direction/SKILL.md`
- Create: `discover-your-direction/agents/openai.yaml`
- Create: `discover-your-direction/references/`

- [ ] **Step 1: Run the official initializer**

```powershell
python "$HOME\.codex\skills\.system\skill-creator\scripts\init_skill.py" discover-your-direction --path . --resources references --interface 'display_name=发现你的方向' --interface 'short_description=从真实经历与本地资料中提炼方向，并设计可证伪的七天实验' --interface 'default_prompt=Use $discover-your-direction to help me choose a direction experiment from my real experience.'
```

Expected: the Skill folder contains `SKILL.md`, `agents/openai.yaml`, and `references/`.

- [ ] **Step 2: Verify generated metadata**

```powershell
Get-Content -Raw discover-your-direction\agents\openai.yaml
rg -n 'T[O]DO|\[T[O]DO' discover-your-direction\SKILL.md
```

Expected: metadata uses the three interface values above; the placeholder search fails the pre-implementation check by finding scaffold markers.

### Task 2: Implement the evidence mirror

**Files:**
- Create: `discover-your-direction/references/evidence-mirror.md`

- [ ] **Step 1: Write the consent and scope contract**

Include these imperative rules:

```markdown
# Evidence Mirror

## Consent gate
- Offer direct interview or user-selected file analysis.
- Never scan the workspace implicitly.
- Resolve exact files, restate the complete list, state that access is read-only, and require affirmative confirmation before reading.
- Do not follow links, transclusions, attachments, symlinks, or references outside the confirmed list without fresh consent.
- Pause and explain why for secrets or credentials, system files, executables or binaries, unexpectedly broad directories, or unrelated personal data; ask the user to narrow broad, suspicious, sensitive, or oversized selections.
- List the files actually used. Say the agent used them only for reading and did not modify them; never claim protection against other processes.

## Evidence extraction
Extract repeated actions, difficult outcomes, recurring requests, actual time, money, reputation, or other commitment others invested, transferable skills, energy changes, returns after setbacks, judgment under uncertainty, contradictions, and counterexamples. Prefer concrete episodes over topic frequency.

## Canonical evidence records
Make this file canonical. Apply provenance, evidence kind, and `claim status=source observation/paraphrase` only to source observations. Each source-observation record has an ID, observation, quoted/paraphrased flag, provenance, evidence kind, and source reference: file path + precise locator for files; `current conversation` + turn/message locator for a live interview; or transcript file + speaker/message locator for stored chats.

Keep current AI inference as a separate, non-evidence record with `claim status=current AI inference`, linked source-observation IDs, interpretation, alternative interpretation, strongest contradiction, missing evidence, and confidence (`strong`, `mixed`, `weak`). It must have no provenance, evidence-kind, or source-reference fields. Base confidence on the linked observations' specificity, quality, independent repetition, and contradictions. Never calculate a composite score.

## Evidence ledger
Maintain linked source-observation and current-AI-inference collections. Never merge their fields.

## Mirror output
Share at most five tentative patterns with linked source-observation IDs and source references. Include the strongest known contradiction or counterexample whenever one exists and the key missing evidence separately. Invite correction; user corrections override the AI interpretation.
```

- [ ] **Step 2: Verify the hard boundaries**

```powershell
rg -n 'Never scan|read-only|files actually used|affirmative confirmation|fresh consent|secrets or credentials|Canonical evidence records|Source-observation record|Current-AI-inference record|source reference|current conversation|linked source-observation IDs|Do not add.*provenance|composite score|override|only for reading' discover-your-direction\references\evidence-mirror.md
```

Expected: every boundary is found.

### Task 3: Implement the interview guide

**Files:**
- Create: `discover-your-direction/references/interview-guide.md`

- [ ] **Step 1: Write the interview contract and questions**

Include:

```markdown
# Interview Guide

## Contract
Treat fifteen minutes as an experience target, not a countdown. Ask one question at a time. Cover six evidence dimensions, but summarize and confirm dimensions already supported by files. Use at most three adaptive follow-ups for vague claims, contradictions, missing outcomes, or unusually revealing events. Permit "I don't know" and skipping.

## Six evidence dimensions
1. Critical incident: situation → surprise → action → adjustment → feedback.
2. Real demand, relevance, or uptake: who sought help, engaged, used, or reused the work; the exact problem or practice; prior attempts; and actual cost or commitment.
3. Career capital: difficult outcomes, transferable skills, hard-to-copy combinations, compounding ability.
4. Self-directed return: unpaid curiosity, energy after action, and return after setbacks.
5. Reversed advice: advice that caused a cost and the event that changed the judgment.
6. People and avoided truth: concrete group, recurring problem, avoided truth, first-hand basis.

## Follow-up selector
Ask only one: a recent example; the surprise and adjustment; who acted and what they spent; what actions prove without interpretation; or a counterexample.

## Framing check
Offer two plausible interpretations of the richest event. Ask which is closer, what is distorted, and what tacit contribution is missing. Update the evidence ledger.

## Weak input
Return once to a recent event. Preserve conflicting interpretations. Label weak evidence and design observation; never invent a coherent identity.
```

- [ ] **Step 2: Check interaction safeguards**

```powershell
rg -n 'one question at a time|at most three|two plausible interpretations|never invent' discover-your-direction\references\interview-guide.md
```

Expected: all safeguards are found.

### Task 4: Implement direction experiments

**Files:**
- Create: `discover-your-direction/references/direction-experiment.md`

- [ ] **Step 1: Write synthesis, experiment, and review rules**

Include:

```markdown
# Direction Experiments

## Three possible selves
Generate three materially different roles. At least one may be a low-evidence new identity worth a cheap rehearsal. Each card contains only five short bullets: role, beneficiary/stakeholder/peer/practice community or consequential context, and problem; sourced observations for ability; demand, relevance, or uptake; and energy, separated from AI interpretation; biggest unknown; observable falsifier; smallest identity rehearsal. Defer to the canonical record schema in `evidence-mirror.md`; do not duplicate it. A falsifier lowers confidence in the tested component, not the whole possible self. Use `strong`, `mixed`, or `weak`. Do not use a total score or declare a winner. Offer the full ledger on request.

## Choose one experiment
Compare willingness to do the real work, speed and cost of decisive bad news, engagement with a real beneficiary, stakeholder, peer, practice community, or consequential work context, and potential to build scarce or compounding ability. The user selects one; retain the others in the conversation without rejecting them, and persist them only on explicit request.

## Safety and outreach gate
The user performs all outreach and delivery. The agent only drafts. In this workflow, the agent never contacts, sends, publishes, recruits, or delivers; the user always performs those actions. Require voluntary participation, stated purpose, minimized/de-identified data, consent before retaining quotes or identifying details, respect for decline or no response, and no more than one polite unsolicited follow-up. Keep work small, bounded, reversible, and within competence. In medical, legal, financial, therapeutic, safeguarding, or vulnerable-person contexts, prohibit unqualified advice/service and use public-source study, informational interviews with qualified practitioners, or qualified supervision. Observation involving a regulated setting or vulnerable people must be public, or both appropriately consented and institutionally/professionally approved; non-sensitive alone is insufficient.

## Seven-day experiment
After selection, plan two respectful outreach attempts to adjacent practitioners; completed conversations are stronger but not required. When outreach is unsafe, inappropriate, or impractical, one relevant public talk, published case study, or supervised observation substitutes for one attempt; record the substitution and reason, and allow two substitutions when the reason applies to both attempts. Attempt to help one real target only when safe, consensual, and within competence; otherwise perform consequential work in a faithful context. Choose the medium closest to the work: content, interview, consulting, service, small tool, workshop, or another practice.

Preregister the tested hypothesis component, biggest unknown, action, target/context, observation window, valid-test conditions (target fit, exposure count/denominator, medium, delivery fidelity), evidence, disconfirming observation/falsifier, and outcome updates for demand, relevance, or uptake; ability; energy; or role fit. Freeze interpretation rules during the run and log deviations separately.

## Signal and commitment record
Use role-calibrated signals rather than a universal ladder. Record every material behavior, its time/money/reputation/privacy/effort cost, target fit, friend/stranger/context, count, and exposure denominator. Payment is optional and role-specific; do not report only the highest signal.

A commercial Commitment ladder—polite response or like < detailed question or story < submitted material or referral < booking, trial, or collaboration time < payment or repeat use—is only a non-universal example. Praise and future promises are not commitments.

## Internal learning
Track willingness to return, autonomy, skill growth, visible progress, and reframing surprise. Sustained energy loss may justify adjustment; persistence is not moralized.

## Generate the minimum artifact
Generate a content draft only for a content test. Otherwise generate the appropriate interview guide, service offer and delivery checklist, tool scope, workshop outline, or one-person help protocol. Do not default to content.

## Review
Ask what ran faithfully, what role-calibrated signals appeared, what contradicted the hypothesis, what changed internally, what skill/learning emerged, and whether to continue, adjust, or stop. Integrate external response, faithful execution, internal experience, and skill/learning. For returned results without preregistration, separate source observations from post-hoc interpretation, do not retrofit a falsifier or pretend valid-test conditions were fixed, and limit conclusions. Such observations may inform a tentative next hypothesis or practical decision, but they are not an update from a preregistered test and cannot be described as falsifying or confirming one. No feedback is missing data when valid exposure was not met; when adequate preregistered exposure was met, silence is weak negative evidence only for the tested response, demand, relevance, or uptake component. One seven-day test updates only that component, never a whole identity. Reserve 30–90 day projects for delivery and career-capital validation.
```

- [ ] **Step 2: Verify falsifiability and non-content paths**

```powershell
rg -ni 'Falsifier.*tested hypothesis component|total score|decisive new information|two respectful outreach attempts|substitutes for one outreach attempt|persist them only|Signal and commitment record|Do not default to content|No feedback is missing data|canonical.*evidence-mirror|exposure denominator' discover-your-direction\references\direction-experiment.md
```

Expected: each contract appears.

### Task 5: Implement the Skill orchestrator

**Files:**
- Modify: `discover-your-direction/SKILL.md`

- [ ] **Step 1: Replace the scaffold frontmatter**

```yaml
---
name: discover-your-direction
description: Use when an experienced person wants to identify or test a personal next direction grounded in accumulated work, interests, projects, or life experience—for example a transferable advantage, life's work, or a content or business direction derived from that experience. Do not use for tactical content calendars, ordinary business validation, generic strengths lists, or unrelated small experiments.
---
```

- [ ] **Step 2: Write the complete stage router**

Implement these exact stages in imperative prose:

```markdown
# Discover Your Direction

Help the user choose the next direction experiment. Never claim to discover a fixed identity, perfect niche, or lifelong mission.

## Core contract
Treat direction as a hypothesis; prefer actions, outcomes, and real commitments; separate inference from evidence; ask one question at a time; accept correction. In this workflow, the agent only drafts: the user always contacts, sends, publishes, recruits, and delivers. Modify files only with a separate explicit request.

## Route from the user's current state
Before branching, enforce two route-independent invariants. Whenever any stage involves user files—including returned results or an existing draft stored in files—read `references/evidence-mirror.md` completely, resolve and restate the exact read-only scope, and require affirmative confirmation before reading. Whenever reviewing results, load and apply the canonical evidence-record schema before classifying observations, even with no files.

Do not force Stage 0. If results already exist, apply the review invariant and, when applicable, the file invariant before entering review; without preregistration, do not retrofit a falsifier or overclaim evidence. If a direction or experiment is already selected, apply the file invariant when applicable, summarize known state, confirm once, and enter Stage 3 with safety and preregistration applied before remaining external action; completed actions remain post-hoc because preregistration is never retroactive. Otherwise offer direct interview or user-selected files and apply the file invariant before reading. Never infer workspace-wide permission.

## Stage 1: Evidence interview
Read `references/interview-guide.md` completely and use the canonical records in `references/evidence-mirror.md`. Use Chinese unless the user uses another language. Do not synthesize before the framing check or before naming unknown dimensions.

## Stage 2: Possible directions
Read the synthesis section of `references/direction-experiment.md`. Present three concise cards using canonical evidence records, uncertainty, and component-level falsifiers. Include an exploratory identity when justified. Help the user choose one by real-role willingness and information value. Stop and ask whether to design the seven-day experiment.

## Stage 3: Experiment and review
When the user opts in or confirms an existing selection, follow the remaining experiment reference. Match the artifact to the work; content is optional. At review, separate role-calibrated external signals, execution fidelity, internal experience, skill growth, and reframing; update only the preregistered hypothesis component. Without preregistration, label post-hoc interpretation and limit conclusions.

## Failure behavior
Narrow excessive material; skip suspicious files; ground abstractions in a recent event; preserve contradictions; mark weak evidence; diagnose a feedback-free test; refuse false certainty.

The agent analyzes, interviews, designs, and reviews. The user authorizes sources, corrects interpretation, chooses and runs the role, returns feedback, and decides.
```

- [ ] **Step 3: Run official validation and placeholder scan**

```powershell
python "$HOME\.codex\skills\.system\skill-creator\scripts\quick_validate.py" discover-your-direction
if (rg -n 'T[O]DO|T[B]D|\[T[O]DO|PLACEH[O]LDER' discover-your-direction) { exit 1 } else { 'No placeholders.' }
```

Expected: official validation succeeds and no placeholders remain.

- [ ] **Step 4: Commit the Skill**

```powershell
git add discover-your-direction
git commit -m "feat: add direction discovery skill"
```

### Task 6: Add GitHub documentation

**Files:**
- Create: `README.md`
- Create: `LICENSE`

- [ ] **Step 1: Write `README.md`**

Include: Chinese summary; “not a personality test or mission guarantee”; capabilities; installation by copying the Skill folder or installing from GitHub; invocation example; optional file analysis and privacy boundary; experiment methodology; MIT license.

Use this invocation example:

```text
$discover-your-direction 帮我从过去的经历里找到值得验证的下一步方向。
```

- [ ] **Step 2: Add the standard MIT license**

Use the unmodified MIT grant and warranty text with:

```text
Copyright (c) 2026 taotaotao07
```

- [ ] **Step 3: Verify claims and commit**

```powershell
rg -n '十五分钟|七天|明确指定|AI 推测|MIT' README.md
git diff --check
git add README.md LICENSE
git commit -m "docs: add usage and privacy guide"
```

Expected: all claims appear, the diff is clean, and documentation is committed.

### Task 7: Run deterministic validation

**Files:**
- Modify only if a check exposes a defect.

- [ ] **Step 1: Run the official validator**

```powershell
python "$HOME\.codex\skills\.system\skill-creator\scripts\quick_validate.py" discover-your-direction
```

Expected: validation succeeds.

- [ ] **Step 2: Verify cross-file contracts**

```powershell
$required = @('one question at a time','Never scan','Do not use a total score','falsifier','Do not default to content','No feedback is missing data')
$all = (Get-Content -Raw discover-your-direction\SKILL.md) + (Get-Content -Raw discover-your-direction\references\*.md)
$missing = $required | Where-Object { $all -notmatch [regex]::Escape($_) }
if ($missing) { $missing; exit 1 }
'All contracts found.'
```

Expected: `All contracts found.`

- [ ] **Step 3: Confirm repository scope**

```powershell
git status --short
git ls-files
```

Expected: a clean worktree containing only intentional design, plan, Skill, README, and license files.

### Task 8: Forward-test fresh conversations

**Files:**
- Create temporarily, then remove: `tmp-evals/`
- Modify: Skill files only when a failure is reproduced.

- [ ] **Step 1: Test no-material and sparse-answer paths**

Fresh prompt A:

```text
Use $discover-your-direction at ./discover-your-direction. I worked in operations for eight years and people call me reliable, but I do not know what direction suits me. Start without files. Ask one question at a time.
```

Fresh prompt B:

```text
Use $discover-your-direction at ./discover-your-direction. I say I love writing but avoided publishing for three years; colleagues repeatedly ask me to repair messy delivery processes. I often answer “不知道.” Do not force a neat identity.
```

Accept only if the agent grounds labels in events, preserves contradictions, performs the framing check, gives sourced cards and falsifiers, and stops after primary selection.

Record core-dialogue duration, evidence dimensions skipped, and whether the cards remain concrete. Treat repeated overruns or generic cards as a time-pressure failure.

- [ ] **Step 2: Test evidence-source bias**

Create temporary fixtures containing an AI-generated identity narrative, a contradictory first-hand project record, and an energy-loss note. Run the same request with no files, AI chat only, and all sources.

Accept only if AI chat is labeled a clue, first-hand evidence changes confidence for an explicit reason, energy affects internal-fit uncertainty, actual files are listed, and nothing outside the selected fixture is read.

- [ ] **Step 3: Test a non-content direction**

```text
Use $discover-your-direction at ./discover-your-direction. The chosen direction is helping independent cafés reduce closing-shift mistakes. I dislike public content and want the cheapest honest test.
```

Accept only if the user—not the agent—runs a safe, consensual experiment with real café staff, creates a service checklist/interview/tool rather than an article, preregisters valid exposure, and records all role-calibrated signals and their costs rather than assuming payment is universal.

- [ ] **Step 4: Patch only reproduced failures and rerun**

Remove `tmp-evals/`. For each failure, make the smallest instruction change, rerun the failing prompt in a fresh context, and rerun official validation.

- [ ] **Step 5: Commit tested improvements when needed**

```powershell
git add discover-your-direction
git diff --cached --check
git commit -m "fix: harden direction experiment workflow"
```

Skip the commit if no files changed.

### Task 9: Verify and publish to GitHub

**Files:**
- No content changes expected.

- [ ] **Step 1: Run final verification**

```powershell
python "$HOME\.codex\skills\.system\skill-creator\scripts\quick_validate.py" discover-your-direction
git diff --check
git status --short
git log --oneline -5
```

Expected: validator success, no diff errors, clean worktree, intentional commits only.

- [ ] **Step 2: Ensure the target does not already exist**

```powershell
gh repo view taotaotao07/discover-your-direction
```

Expected for a new publication: repository not found. If it exists, stop and inspect instead of overwriting.

- [ ] **Step 3: Create the public repository and push**

```powershell
git branch -M main
gh repo create taotaotao07/discover-your-direction --public --source . --remote origin --push
```

Expected: public repository created; `origin/main` tracks local `main`.

- [ ] **Step 4: Verify publication**

```powershell
gh repo view taotaotao07/discover-your-direction --json nameWithOwner,url,visibility,defaultBranchRef
git remote -v
git status -sb
```

Expected: correct repository, public visibility, default `main`, clean tracked branch.
