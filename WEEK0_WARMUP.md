# Phase 0 — Warm-up: the repo auditor

**Time:** 2-4 days
**Deliverable:** a working CLI, merged via a reviewed PR with green CI

---

## Why this task

Two reasons, and it's worth being straight about both.

**For you:** it runs you through the entire Axonity workflow — branch, PR, CI
failing, CI fixed, review, ADR, merge — on something with **no research risk**.
When Phase 2 gets hard, you'll be fighting the research problem only, not the
research problem *and* an unfamiliar process at the same time. It's also a
project where **testing is the product** — usually the weakest skill coming out of
undergrad, and hard to avoid practising in a tool whose entire job is checking
things.

**For Axonity:** it's genuinely useful, though it's worth being honest about the
scale. See "what it's actually for" below.

---

## What it does

A CLI that audits a repository against the Axonity engineering standard and
reports pass/fail per item.

```bash
axonity-audit /path/to/repo
```

The checks come from the summary table in
[ENGINEERING_STANDARDS.md](https://github.com/Axonity-AI/project-template/blob/main/ENGINEERING_STANDARDS.md).
Each row there already names a mechanism that's mechanically checkable:

| Check | How you'd verify it |
|---|---|
| CODEOWNERS | File exists and is non-empty |
| Dependabot | `.github/dependabot.yml` exists, has ≥1 ecosystem |
| CI exists | A workflow file exists and has jobs |
| Secret scanning in CI | A CI job runs gitleaks |
| Lint gate | A CI job runs ruff (or equivalent) |
| Type-check gate | A CI job runs mypy (or `tsc` for JS) |
| Test gate | A CI job runs pytest (or equivalent) |
| Checks actually gate | **No `continue-on-error: true` on a job that's meant to block** |
| Pre-commit | `.pre-commit-config.yaml` exists and includes gitleaks |
| Conventional Commits | A `commit-msg` hook is configured |
| ADRs | `docs/adr/` exists |
| Licence | A `LICENSE` file exists |
| Security policy | `SECURITY.md` exists |

That last mechanical one — `continue-on-error` on a gating job — is worth
calling out. `visual_search_ranking` has exactly that today on its
`code-quality` job. The check runs, reports, and blocks nothing. It looks like a
gate and isn't one. That class of silent decay is the most valuable thing this
tool can catch.

---

## What it's actually for — honestly

You asked good questions get asked about internal tools, so here's the real
answer including the unflattering part.

**Three genuine uses:**

1. **Bootstrap verification.** When a new repo is created from
   `project-template`, run this to confirm the setup actually completed —
   placeholders resolved, every file and CI job present. Today that's a manual
   checklist at the end of `REFACTOR_GUIDE.md`, and manual checklists at the end
   of long processes are the ones that get skipped.

2. **Drift detection — the one with real ongoing value.** Standards decay
   silently. Someone deletes a `dependabot.yml` during a merge conflict, or
   adds `continue-on-error` to unblock a release and never removes it. Run
   weekly on a schedule across all repos and you catch it in week two rather
   than a year later.

3. **Client-facing audits.** Axonity does client work. "We'll audit your repo
   against a production-readiness standard and hand you a report" is a small,
   real, sellable engagement — and this tool is its engine.

**The honest part:** with four repos, use (1) fires a handful of times a year and
the day-to-day productivity gain is modest. The real value is (2) accumulating
over time and (3) as a service offering. It's a good tool, not a transformative
one, and it would be strange to pretend otherwise.

---

## Decisions you own

Not implementation details — the actual design questions. Each deserves a line
in your PR description, and at least one deserves an ADR.

1. **What counts as a pass when a check is partially satisfied?** A CI file with
   a `test` job that only runs on one of three Python versions — pass, fail, or
   a third state? If a third state, what does it mean and how does it affect the
   exit code?

2. **Exit code semantics.** Non-zero on any failure? Only on some severity? This
   determines whether the tool can be used in CI at all, and whether a warning
   can break someone's pipeline.

3. **Handling non-Python repos.** `axonity_chatbot` has a React frontend; the
   `mypy` check is meaningless there but `tsc` is the equivalent. Does the tool
   detect stack, take a flag, or report "not applicable"? What's the difference
   between "not applicable" and "pass" in the output, and does it matter?

4. **How checks are defined.** Hard-coded in Python, or declared in a config
   file? Hard-coded is faster to write; config-driven means the standard can
   change without a code change. There's a real trade-off and either answer is
   defensible — say which you picked and why.

5. **Output format.** Human-readable terminal output and machine-readable JSON
   are different consumers. Both? One with a flag?

**Don't ask an AI assistant to decide these for you.** Ask it to implement your
decision once you've made it. These five questions are the entire point of the
exercise.

---

## Definition of done

- [ ] Runs against all four Axonity repos and produces sensible output
- [ ] Tests cover each check, including the failure path — a check that never
      fails in tests is not a tested check
- [ ] Handles a repo missing the files entirely without crashing
- [ ] `README.md` explaining usage and what each check means
- [ ] Green CI: secrets, lint, typecheck, test
- [ ] One ADR covering whichever of the five decisions above was hardest
- [ ] Merged via a reviewed PR

---

## Suggested approach

Not prescriptive — if you have a better structure, propose it in the PR.

1. Scaffold from `Axonity-AI/project-template` ("Use this template"), then work
   through `REFACTOR_GUIDE.md` to resolve the placeholders.
2. Read `ONBOARDING.md` first if you haven't. The workflow matters as much as
   the code here.
3. Start with **three** checks, end to end, with tests. Get that merged before
   adding the rest — a small first PR that goes all the way through is worth
   more than a large one that stalls.
4. Add the remaining checks incrementally.

**Break CI on purpose at some point.** Push something that fails lint, watch the
merge button disable, fix it. Knowing what that looks and feels like before it
happens for real is genuinely part of the exercise.
