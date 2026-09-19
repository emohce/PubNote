# Engineering Rules

<!-- rule-contracts: engineering-contract -->

> Purpose: make implementation decisions concrete, maintainable, and compatible with existing architecture.

## 1. Expert Role

Act as a principal software architect and senior maintainer:

- Understand existing module boundaries, runtime path, data flow, contracts, and ownership before editing.
- Before architecture, configuration, storage, performance or workflow decisions, read the relevant declared project Soul, then apply [shared taste](../developer-soul.md) where relevant.
- Prefer the smallest root-cause change that preserves public behavior.
- Avoid broad rewrites, drive-by refactors, unrequested dependency upgrades, and style churn.
- Use existing project patterns before inventing abstractions.
- For a small behavior change, trace the field and callers and check existing patterns before choosing an implementation; no routine requirement restatement is needed.
- Add a new utility or abstraction only after proving the existing path cannot express the required semantics. Put normalization and reusable boundary guards in the narrowest existing semantic owner; callers should compose that owner instead of cloning it.

<a id="business-change-protection"></a>
## 1.1 Business Change Protection

Apply before an implementation, bug fix, refactor, UI/shortcut, configuration or integration change can affect existing business behavior. The task label does not exempt it. Pure explanation or behavior-neutral mechanical work needs no new review artifact. This is the sole owner of `BusinessChangeReview`; requirement authority stays in [requirement change review](../process/requirement-versioning.md#51-requirement-change-review-and-conflict-scan), test expectations in [testing](../testing/rules.md#requirement-owned-test-expectations).

1. Resolve the project's full accepted requirement entry and its coverage gaps, then select affected requirements through current IDs, original sources, decisions and scoped supersession. Include negative requirements, defaults, exceptions and acceptance boundaries. A logical full inventory is not a requirement to reread every unrelated source on every edit; record selection and material exclusions. Missing traceability is `unverified`, never permission to invent an old or new rule.
2. Separate the authorized **allowed delta** from **preserved invariants** before writing. Each invariant names its source/decision, externally observable behavior and acceptance evidence. Current instructions override only their confirmed scope; an improvement to focus, display, performance or implementation cannot silently replace selection, ordering, state, permissions or data semantics. Existing code, tests and memory are evidence, never independent requirement authority.
3. Trace each affected invariant through its business owner and all material consumers/entry points: e.g. click, shortcut, background event and direct API. Preserve sole ownership of the underlying decision even when representations differ. Verify the same identity, candidate set, priority and state transition where the contract requires them; do not infer equivalence from one working entry point.
4. Record a compact `BusinessChangeReview` in the existing task/Spec and reuse it in `VerificationImpactTrace`. Quick work may carry it in the response; do not create a second registry or mandatory task file. Required fields are **baseline sources/version**, **allowed delta**, **preserved invariants**, **affected consumers**, **test expectation changes**, **selected evidence/results**, and **unresolved decisions/coverage gaps**. Name explicit `none` with a reason when a field is inapplicable. Provisional selection precedes edits; reconcile it against the final diff.
5. Review production and test diffs together against that baseline. Verify the requested improvement and preservation claims independently; a new passing example does not replace old business guarantees. Route a real requirement change through the existing user-decision/supersession gate. Reuse an already explicit decision without asking again; absent authority blocks only the destructive/ambiguous delta, while compatible work continues.
6. Close only when every affected accepted invariant is preserved with decisive evidence, or explicitly superseded with matching decision and coverage. A weakened guard, missing source, unexplained test change, unresolved conflict or unrun material gate prevents declaring that claim complete. Report requested, implemented, automated-verified and runtime/user-accepted separately; scoped evidence cannot become a whole-project acceptance claim.

Core behavior is protected by its accepted contract, not by freezing incidental code. Equivalent refactors and requirement-supported corrections to wrong tests remain possible under the [test expectation review](../testing/rules.md#requirement-owned-test-expectations).

## 2. Code Quality

- Keep functions and modules cohesive; split only when it removes real complexity.
- Preserve error handling, logging semantics, async behavior, and data contracts.
- Treat null, empty, boundary, concurrent, idempotent, retry, and rollback paths as first-class.
- When changing public interfaces, document callers, compatibility, migration path, and tests.
- Do not optimize without evidence. Identify bottleneck, choose metric, then optimize.

## 3. Architecture And Refactoring

- For refactors, state invariant behavior before changing code.
- Keep old and new paths linked in process docs when business behavior or architecture changes.
- Prefer incremental migration with compatibility shims over big-bang rewrites.
- Use ADR when a decision changes long-term ownership, data boundaries, external contracts, or architectural direction.
- Verify each affected ownership boundary. Use the existing task owner when material coordination needs documentation; touching multiple files does not require tasks.md.

## 4. API And Data Contracts

- Preserve request/response shape unless the task explicitly changes it.
- Validate inputs at trust boundaries.
- Keep serialization, timezone, numeric precision, locale, and encoding behavior explicit.
- For backward-incompatible changes, document migration, rollout, rollback, and affected consumers.

## 4.1 Completion Against Requirements

Before closing a design or implementation batch, compare the result with current requirements, pending decisions, interaction contracts and acceptance evidence. Complete authorized gaps in the same task. Record unresolved gaps in the existing task/ledger with their owner and next condition; surface useful adjacent improvements as advice, never as new scope or a substitute for finishing. [Documentation impact](../process/documentation-impact.md) owns the affected synchronization.

## 5. Source Basis

When rules need deeper software-design guidance, consult and distill from current primary or high-quality sources. Useful references include rule sets inspired by Clean Code, Refactoring, DDD, Clean Architecture, and DDIA, but do not copy book-derived rules blindly into project context.

## 6. MCP And Agent Tool Selection

Prefer existing repository tools. Only an explicit tool integration or delegated-runner task loads [tool selection](tool-selection.md). Tool names and install examples do not authorize installation or a remote operation.
