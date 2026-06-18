---
name: spec-verify-optimize
description: "Use this skill when the user wants a reusable AI collaboration mode for project planning or execution: clarify the true goal before work, define a measurable objective function, split work into small checkpointed buckets, write a Spec and Verifier for each bucket, and choose the next bucket using an optimization/experimental approach inspired by Hua Luogeng's optimization method. Trigger on requests mentioning SVO, Spec-Verify-Optimize, 优选小桶, 优选法, checkpoints, project buckets, goal-first collaboration, or do not start coding/docs before clarifying goals."
---

# Spec Verify Optimize

## Overview

Use Spec-Verify-Optimize, or SVO, to turn vague project work into a sequence of small, verifiable experiments. The agent must optimize learning and decision quality before output volume.

## Purpose

Use SVO to solve a specific collaboration problem: AI agents often produce plausible work before the human and agent have agreed on the real goal, success criteria, key assumptions, and validation method.

SVO makes the agent pause long enough to answer:

- What are we actually trying to improve?
- What must be true for this work to matter?
- Which uncertainty should be reduced first?
- What evidence will prove the output is good enough?
- When should we stop, pivot, or ask the user?

## Problems Solved

SVO helps prevent:

- **Premature execution**: coding, writing, or designing before the real goal is clear.
- **Prompt-only collaboration**: relying on one large prompt instead of a reusable process.
- **Confident wrongness**: accepting AI output without an external verifier.
- **Overbuilding**: expanding scope to look complete instead of testing the next important assumption.
- **Decision drift**: losing track of what has been confirmed, rejected, or left uncertain.
- **Context reset**: forcing the user to re-explain the same goals and decisions across sessions, computers, or AI tools.

## Not For

Do not use SVO as:

- A replacement for domain expertise, user research, tests, or real-world evidence.
- A heavy planning ceremony for trivial tasks.
- A way to make the agent ask endless questions.
- A guarantee that the chosen goal is correct.
- A project management system for tracking every task.

Core idea:

```text
Goal Function -> Key Variables -> Best Next Bucket -> Spec -> Verifier -> Execute -> Checkpoint -> Narrow the Search Space
```

## Core Principles

### 1. Split by Hypothesis, Not by Task

Buckets should test assumptions, not merely divide work into modules. A bucket named "build login page" is weak. A bucket named "test whether users must experience core value before registration" is stronger.

Always ask:

```text
What hypothesis does this bucket test?
What would make the hypothesis true or false?
What decision becomes easier after this bucket?
```

### 2. Define Anti-Goals

Every meaningful objective needs anti-goals: things the project must not optimize for or accidentally sacrifice.

Examples:

- Optimize launch speed, but do not create a demo that cannot evolve.
- Optimize conversion, but do not use misleading copy.
- Optimize scope control, but do not remove the core user value.
- Optimize visual quality, but do not hide missing product logic behind decoration.

Anti-goals protect against local optima and over-optimization.

### 3. Rank Evidence Quality

Verifier evidence is not equal. Prefer higher-quality evidence:

```text
Level 1: Real users, real usage data, production/staging behavior, real task completion
Level 2: Automated tests, builds, screenshots, reproducible scripts, benchmark runs
Level 3: Structured manual review, checklists, sample comparisons, expert review
Level 4: AI self-review or reasoning-only evaluation
```

AI self-review can support a checkpoint, but must not be the only verifier for important decisions.

### 4. Shrink the Search Space

A checkpoint is useful only if it changes the decision space. It should not merely say "done".

Each checkpoint must identify:

```text
Confirmed assumptions:
Rejected assumptions:
Options ruled out:
Variables now less important:
Variables still uncertain:
Whether to refine, pivot, stop, or choose the next bucket:
```

### 5. Stop Optimizing When Good Enough

SVO is not endless improvement. Stop or switch modes when:

- The acceptance criteria are met.
- The objective function threshold is reached.
- Further optimization has lower expected value than its cost.
- The core hypothesis is rejected and the project needs a goal or strategy reset.
- The user chooses delivery over more exploration.

## Operating Rules

1. Do not start coding, writing docs, designing, or building until the current bucket has a clear Spec and Verifier, unless the user explicitly asks to skip planning.
2. Ask only the minimum clarifying questions needed to avoid pursuing the wrong objective. Prefer proposing a concrete draft when enough context exists.
3. Treat every bucket as an experiment that should confirm, reject, or narrow one important assumption.
4. Optimize bucket order with this heuristic:

```text
Priority = Impact x Uncertainty x Verifiability / Cost
```

5. Prefer the bucket that most reduces uncertainty for the least effort.
6. Keep each bucket focused on one primary variable. Avoid mixing product positioning, UI design, architecture, content, and implementation decisions in the same bucket unless they are inseparable.
7. Stop at checkpoints. Present the result and ask for confirmation before moving to the next bucket when the user requested checkpointed collaboration.
8. Make understanding explicit: the user may outsource thinking, but must not be asked to outsource understanding. Explain key tradeoffs plainly before asking for decisions.

## Mode Selection

Use the lightest version that protects decision quality:

- **Light SVO**: Use for small, reversible tasks. Produce a one-paragraph goal, a short Spec, a short Verifier, then execute.
- **Standard SVO**: Use for normal project work. Clarify the goal, rank 3-7 buckets, recommend one, and stop for checkpoint confirmation.
- **Full SVO**: Use for ambiguous, high-cost, strategic, or multi-session work. Add scoring, decision records, explicit out-of-scope items, and a project-level SVO state file when useful.

Do not use SVO when the user asks for a trivial direct answer, a simple command output, or an urgent mechanical edit with clear acceptance criteria. In those cases, answer or execute directly.

## Workflow

### 1. Clarify the Real Goal

Identify what the project should actually drive, not just what artifact should be produced.

Capture:

```text
Project:
First users:
Real desired result:
Primary objective function:
Anti-goals:
Hard constraints:
Out of scope:
Stop-and-ask conditions:
```

Good objective functions include conversion rate, launch speed, user task completion time, reliability, cost, content quality, maintainability, learning progress, or validation of a market/product hypothesis.

If the objective is still vague, propose 2-3 likely objective functions and ask the user to choose.

### 2. Identify Key Variables

List the variables that most affect the objective function.

Common variables:

- User segment
- Core use case
- MVP scope
- Interaction model
- Data/source quality
- Technical route
- Quality bar
- Distribution channel
- Time/cost constraints
- Verification method

For each variable, estimate:

```text
Impact: Low / Medium / High
Uncertainty: Low / Medium / High
Verification speed: Slow / Medium / Fast
Cost: Low / Medium / High
```

For Standard or Full SVO, map the estimates to numbers when ranking matters:

```text
Low = 1
Medium = 2
High = 3

Priority = Impact x Uncertainty x Verifiability / Cost
```

Use judgment when ties occur. Prefer buckets that reduce irreversible decisions, unblock later work, or create reusable evidence.

### 3. Split Buckets by Decision Value

Create small buckets that each test one main assumption or produce one inspectable artifact.

Use this format:

```text
Bucket:
Main assumption:
Anti-goal protected:
Why this bucket now:
Expected output:
Verifier:
Checkpoint question:
```

Prefer 3-7 candidate buckets. Mark only one as the recommended next bucket.

### 4. Write the Current Bucket Spec

Before execution, write a concise Spec:

```text
Current Bucket Spec

Goal:
Key assumption:
Anti-goals:
Inputs:
Output:
Scope:
Out of scope:
Constraints:
Acceptance criteria:
Stop condition:
Checkpoint:
```

If the task is implementation work, include affected files/modules and commands to verify when known. If the task is product/design/doc work, include the review criteria and required sections/states/examples.

### 5. Define the Verifier

Define how correctness or usefulness will be checked before work starts.

Verifier examples:

- Code: tests, typecheck, lint, build, screenshot, manual flow, failing-then-passing reproduction.
- Document: structure check, audience fit, decision coverage, actionability, contradiction check.
- Product: user journey, edge cases, conversion path, must-not-do list, decision log.
- Design: key screens, states, responsive behavior, accessibility, visual consistency.
- Research: source quality, decision enabled, confidence level, open questions.

The Verifier must say what evidence level and evidence artifact will be shown at the checkpoint.

### 6. Execute One Bucket

Execute only the approved current bucket. Keep edits and artifacts scoped to the bucket.

If new information changes the bucket's premise, pause and state:

```text
What changed:
Why it matters:
Recommended adjustment:
Decision needed:
```

### 7. Checkpoint and Optimize

At the end of each bucket, report:

```text
Output:
Verifier evidence:
Evidence level:
Confirmed:
Rejected or ruled out:
Remaining uncertainty:
Search space change:
Recommended next bucket:
Why this next:
Decision for user:
```

The checkpoint's purpose is not just status reporting. It must narrow the search space and improve the next decision.

### 8. Persist State When Useful

For multi-session or cross-AI projects, keep or propose a project-level `SVO.md` file. Update it only with durable context:

```text
Current goal:
Objective function:
Active constraints:
Validated decisions:
Ruled-out options:
Current bucket:
Verifier evidence:
Next recommended bucket:
Open questions:
```

Do not turn the state file into a verbose diary. It should let another AI or another computer resume with minimal re-explanation.

## Portable Protocol

When the user wants to use this mode outside Codex or on another computer, provide or adapt `references/SVO.md`. Keep it as plain Markdown so it can be pasted into Claude, Gemini, Cursor, ChatGPT, Codex, or a project rule file such as `AGENTS.md`, `CLAUDE.md`, or `GEMINI.md`.

## Examples and Anti-Patterns

When the agent or user needs a concrete example of how SVO should behave, read `references/examples.md`. Use it to avoid common drift:

- Turning buckets into ordinary task lists.
- Accepting AI self-review as strong verification.
- Continuing after a checkpoint without a decision.
- Expanding scope because the answer looks more complete.
- Optimizing a metric while silently violating an anti-goal.

## Tone

Be collaborative and decisive. Use simple Chinese by default when the user uses Chinese. Avoid over-planning: the goal is short, high-signal checkpoints that make the next action obvious.
