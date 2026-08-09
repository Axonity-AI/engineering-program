# Axonity Engineering Program

The plan for Suhaas's project with Axonity: how we pick it, how we build it, and
what you walk away with.

---

## What this is for

The goal is that at the end of this you can show an employer a system you
designed, built, measured, deployed and can defend in detail — and that you got
there by working the way a real engineering team works, not the way a solo
side-project works.

Two things make that different from another portfolio repo:

1. **You'll choose the project by trying things, not by reading about them.**
   Most of the candidate areas below are ones you haven't touched. Reading a
   paragraph about reinforcement learning tells you nothing about whether you
   like doing it. A day of actually doing it tells you a lot.
2. **Everything goes through a real engineering process** — reviewed pull
   requests, blocking CI, written decision records. Almost nobody comes out of
   undergrad having worked this way, and it's a large part of what you'll be
   able to claim afterwards.

Read **[ONBOARDING.md](https://github.com/Axonity-AI/project-template/blob/main/ONBOARDING.md)**
in the template repo before Phase 0. It's the mechanics — branches, PRs, CI,
commit format, ADRs — written assuming you've never done any of it.

---

## Commitment

- **20-25 hours/week.**
- **8-week core.** Extendable to ~6 months depending on how your job search goes.
- Phases are designed to be independently valuable, so if we stop after any one
  of them, you still have something coherent to show.

---

## Phases

| Phase | Weeks | What you do | What exists at the end |
|---|---|---|---|
| **0 — Onboard** | 1 | Build the repo auditor ([WEEK0_WARMUP.md](WEEK0_WARMUP.md)) | A merged PR, a CI run you broke and fixed, one ADR |
| **1 — Discover** | 2 – 3.5 | 5 taste-test exercises ([TASTE_TEST.md](TASTE_TEST.md)), then 2 feasibility spikes ([FEASIBILITY.md](FEASIBILITY.md)) | Written reactions, 2 feasibility notes, a decision |
| **2 — Build V1** | 3.5 – 8 | The project ([CANDIDATES.md](CANDIDATES.md)) | Working system, benchmark, ablations, ADRs |
| **3 — Productionize** *(if extended)* | 9+ | Tests, cloud deploy, monitoring, load testing | Deployed service, real coverage, technical report, demo video, postmortem |

Phase 0 is deliberately low-stakes. Its purpose is to get the workflow into
muscle memory on something with no research risk attached, so that when Phase 2
gets hard you're only fighting one thing at a time.

Phase 3 is where testing, Docker and cloud deployment actually get exercised.
Those are the areas you rated yourself lowest in and said you wanted to improve,
and they're the half of the work most portfolio projects never do — which is
exactly why having done it is worth something.

---

## What "finished" means

The project is not done when the code works. It's done when someone else can
understand what you did and why. Concretely, all of these are deliverables, not
afterthoughts:

- **README with results at the top.** A reader gives it 40 seconds. Lead with
  what it does and what the numbers are, not with installation instructions.
- **A benchmark table.** What you compared, on what data, measured how.
- **A 2-3 minute demo video.** Most people will never run your code.
- **A technical report.** The reasoning: what you tried, what failed, what you
  changed, what you'd do next.
- **ADRs** for the real decisions, written as you go rather than reconstructed
  at the end.

The report and the ADRs are the part that separates this from a repo with a nice
screenshot. A negative result you measured properly is worth more in an
interview than a demo that works for reasons you can't explain.

---

## Working agreement

- **Weekly demo.** Show what runs. Broken-with-an-explanation is fine and normal.
- **Weekly written update:** did / learned / blocked / next. Short.
- **PRs reviewed within one working day.** If yours is sitting longer, ping.
- **Stuck for about an hour → ask.** Say what you tried and what you expected.
  Being stuck is normal and expected; sitting on it silently for three days is
  the only version that's a problem.

Since we're working across timezones, default to written and asynchronous. If
something needs a call, say so and we'll schedule it — but don't block on one.

---

## Open questions

- **Repo and IP arrangement** — decided once you've picked a project, since it
  depends on what the project turns out to be. It'll be written down explicitly
  before Phase 2 starts rather than left informal.
