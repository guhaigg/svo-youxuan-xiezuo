# SVO Examples and Anti-Patterns

Use these examples when the user or agent needs a concrete model of SVO behavior. Keep examples short and decision-oriented.

## Example 1: Product MVP

Weak task split:

```text
Bucket 1: Build landing page
Bucket 2: Build login
Bucket 3: Build dashboard
```

Better hypothesis split:

```text
Objective function: Validate whether first users understand the product value within 30 seconds.
Anti-goal: Do not build fake product depth just to make the page look complete.

Bucket 1:
Hypothesis: The target user can recognize the core value from one concrete use case.
Output: One-page value proposition with one primary workflow mock.
Verifier: Level 3 structured review against user, pain, promise, proof, next action.
Checkpoint: Is the value proposition specific enough to justify a prototype?

Bucket 2:
Hypothesis: Users need to see a realistic output before they will sign up.
Output: Two onboarding flow variants: see-output-first vs sign-up-first.
Verifier: Level 1 if tested with users, otherwise Level 3 scenario walkthrough.
Checkpoint: Which onboarding path should the MVP use?
```

## Example 2: Code Implementation

Weak task split:

```text
Bucket 1: Refactor auth
Bucket 2: Add tests
Bucket 3: Fix bugs
```

Better hypothesis split:

```text
Objective function: Reduce login failure ambiguity without changing the auth contract.
Anti-goal: Do not rewrite authentication architecture.

Bucket 1:
Hypothesis: The observed failures come from unclear error mapping, not token validation.
Output: Reproduce one failing login case and map current error path.
Verifier: Level 2 failing reproduction or trace from existing tests/logs.
Checkpoint: Is the failure source localized enough for a small fix?

Bucket 2:
Hypothesis: A narrow error-mapping change fixes the reproduced case without affecting valid login.
Output: Minimal code change plus targeted regression test.
Verifier: Level 2 failing-then-passing test and existing auth tests.
Checkpoint: Is the fix safe to merge, or does it reveal a deeper contract issue?
```

## Example 3: Learning Project

Weak task split:

```text
Bucket 1: Learn basics
Bucket 2: Build demo
Bucket 3: Read docs
```

Better hypothesis split:

```text
Objective function: Become able to build and explain one working end-to-end flow.
Anti-goal: Do not confuse passive reading with usable understanding.

Bucket 1:
Hypothesis: The learner can explain the core model after building one tiny example.
Output: Minimal working example plus a 5-sentence explanation.
Verifier: Level 3 self-explanation checked against official docs; Level 2 if code runs.
Checkpoint: Which concept is still blocking independent use?

Bucket 2:
Hypothesis: The learner can transfer the concept to a slightly different case.
Output: Modified example solving a new input or scenario.
Verifier: Level 2 run result plus Level 3 explanation of what changed.
Checkpoint: Is more reading needed, or should the next bucket be another transfer task?
```

## Anti-Patterns

### Mistaking Tasks for Hypotheses

Bad:

```text
Next bucket: Create settings page.
```

Better:

```text
Next bucket: Test whether users need settings before the first successful core workflow.
```

### Weak Verifier

Bad:

```text
Verifier: AI says the design is good.
```

Better:

```text
Verifier: Screenshot at desktop and mobile sizes, checklist for key states, and one manual flow through the primary task.
```

### Missing Anti-Goal

Bad:

```text
Goal: Increase conversion.
```

Better:

```text
Goal: Increase conversion.
Anti-goal: Do not use misleading urgency, hide pricing, or collect unnecessary user data.
```

### No Search-Space Change

Bad:

```text
Checkpoint: Done. Continue?
```

Better:

```text
Checkpoint: We confirmed users understand the core value, ruled out sign-up-first onboarding for MVP, and the remaining uncertainty is whether the generated output is credible enough.
```

### Endless Optimization

Bad:

```text
Let's improve the copy again.
```

Better:

```text
Acceptance criteria are met. Further copy polishing is lower value than testing the workflow with one real user, so stop optimizing copy and move to user validation.
```
