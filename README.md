# Axonity Engineering Program

Onboarding and project selection for engineers joining Axonity: how you pick a
project, how you build it, and what you walk away with.

---

## Start here

Two stages. **Stage 1 is reading and thinking — a few hours, do it before your first
working session.** Stage 2 is hands-on and begins once that session is scheduled.

### Stage 1 — orientation (start here, a few hours)

**1. Check your access.**
You should have write access to this repository. If you're reading this, you're in.
Everything else you need is public.

**2. Read [ONBOARDING.md](https://github.com/Axonity-AI/project-template/blob/main/ONBOARDING.md)** — about 15 minutes.
The day-to-day mechanics: branches, pull requests, CI, commit format, ADRs. Written
assuming you've never worked this way before. **Don't skip it** — everything later
assumes you've read it.

**3. Read the rest of this README** — about 10 minutes.
The phases, what "finished" means, and the working agreement. This is the shape of
the next two months.

**4. Read [CANDIDATES.md](CANDIDATES.md) — about 30 minutes. Don't choose anything yet.**
Nineteen projects grouped by industry. Start with the overview diagram and summary
table, then read properly under two or three industries that catch your eye.

You will *want* to pick a favourite. Resist it — you'll choose in Phase 1 after
actually trying things, and a preference formed from reading is mostly a preference
about job titles. What's useful now is **reactions**: which ones you don't
understand, which sound tedious, which you'd want to ask about.

**Done with stage 1 when** you can describe in one sentence what the next two months
look like, and you have real questions about at least three projects. Bring those to
the first session — questions, not a decision.

### Stage 2 — hands-on (once your first session is scheduled)

**5. Set up your machine.** Git configured, Python 3.11, the
[GitHub CLI](https://cli.github.com/) (`gh auth login`).

**6. Start Phase 0: [WEEK0_WARMUP.md](WEEK0_WARMUP.md).** A repo gets set up for you
at the start of this stage; then you scaffold it and get one check working. Low
stakes on purpose.

### Done with week one when

- [ ] A pull request has been reviewed and merged
- [ ] You broke CI at least once and fixed it
- [ ] One ADR is written
- [ ] The warm-up tool does something useful

---

## Reading order

Six documents across two repositories. This is the order that makes sense — don't
read them all up front.

| # | Document | Time | Read it when |
|---|---|---|---|
| 1 | [ONBOARDING.md](https://github.com/Axonity-AI/project-template/blob/main/ONBOARDING.md) | 15 min | **Stage 1** — before anything else |
| 2 | This README | 10 min | **Stage 1** |
| 3 | [CANDIDATES.md](CANDIDATES.md) | 30 min | **Stage 1** — read, don't choose |
| 4 | [WEEK0_WARMUP.md](WEEK0_WARMUP.md) | 10 min | Stage 2, then work from it all week |
| 5 | [TASTE_TEST.md](TASTE_TEST.md) | 15 min | Start of Phase 1 |
| 6 | [FEASIBILITY.md](FEASIBILITY.md) | 10 min | After the taste test |
| — | [ENGINEERING_STANDARDS.md](https://github.com/Axonity-AI/project-template/blob/main/ENGINEERING_STANDARDS.md) | 30 min | Whenever you want the *why* behind the process |

---

## What this is for

The goal is that at the end of this you can show an employer a system you designed,
built, measured, deployed and can defend in detail — and that you got there working
the way a real engineering team works, not the way a solo side-project works.

Two things make that different from another portfolio repo:

1. **You choose the project by trying things, not by reading about them.** Most of
   the candidate areas are ones you haven't touched. Reading a paragraph about
   reinforcement learning tells you nothing about whether you like doing it. A day
   of actually doing it tells you a lot.
2. **Everything goes through a real engineering process** — reviewed pull requests,
   blocking CI, written decision records. Almost nobody comes out of undergrad
   having worked this way, and it's a large part of what you'll be able to claim
   afterwards.

---

## Commitment

- **20-25 hours/week.**
- **8-week core**, extendable to around 6 months depending on how your job search goes.
- Phases are independently valuable, so if things stop after any one of them, you
  still have something coherent to show.

---

## Phases

| Phase | Weeks | What you do | What exists at the end |
|---|---|---|---|
| **0 — Onboard** | 1 | Build the repo auditor ([WEEK0_WARMUP.md](WEEK0_WARMUP.md)) | A merged PR, a CI run you broke and fixed, one ADR |
| **1 — Discover** | 2 – 4 | 6 taste-test exercises ([TASTE_TEST.md](TASTE_TEST.md)), then 2 feasibility spikes ([FEASIBILITY.md](FEASIBILITY.md)) | Written reactions, 2 feasibility notes, a decision |
| **2 — Build V1** | 4 – 8 | The project ([CANDIDATES.md](CANDIDATES.md)) | Working system, benchmark, ablations, ADRs |
| **3 — Productionize** *(if extended)* | 9+ | Tests, cloud deploy, monitoring, load testing | Deployed service, real coverage, technical report, demo video, postmortem |

Phase 0 is deliberately low-stakes. Its purpose is to get the workflow into muscle
memory on something with no research risk attached, so that when Phase 2 gets hard
you're only fighting one thing at a time.

Phase 3 is where testing, Docker and cloud deployment actually get exercised — the
half of the work most portfolio projects never do, which is exactly why having done
it is worth something.

---

## What "finished" means

The project is not done when the code works. It's done when someone else can
understand what you did and why. All of these are deliverables, not afterthoughts:

- **README with results at the top.** A reader gives it 40 seconds. Lead with what
  it does and what the numbers are, not with installation instructions.
- **A benchmark table.** What you compared, on what data, measured how.
- **A 2-3 minute demo video.** Most people will never run your code.
- **A technical report.** What you tried, what failed, what you changed, what you'd
  do next.
- **ADRs** for the real decisions, written as you go rather than reconstructed at
  the end.
- **An operational dashboard** — an at-a-glance view of what you built: current
  metrics, recent runs, where it's failing. Every project ships one. It's the
  fastest way to make work legible to someone who won't read your code, and it
  doubles as the demo surface.
- **A one-page decision brief** per major result, written for a non-technical
  reader: what was measured, what it means, what you recommend. Not the benchmark
  table — the *decision*.

The report and the ADRs are what separate this from a repo with a nice screenshot. A
negative result you measured properly is worth more in an interview than a demo that
works for reasons you can't explain.

---

## On explaining your work

As routine technical tasks automate, the bottleneck in most engineering
organisations moves to communication — and the valuable version of that is
translating a technical result into a decision someone can act on. It's practised
deliberately here rather than left to chance:

- The **decision brief** above, for every significant result.
- The **weekly demo presented to a non-expert.** Your mentor will sometimes play the
  client or the executive rather than the engineer — assume no context.
- **At least one result per phase gets challenged.** Someone will push back on a
  conclusion and you either defend it with evidence or revise it. That's the real
  version of this interaction, rehearsed somewhere safe.

**What this can't give you, honestly:** emotional intelligence and leading
interdisciplinary teams are real skills, and you can't get them from a solo project
— there's no team. Those come from working with actual colleagues. Worth knowing
that's a gap this doesn't close, rather than assuming it does.

---

## Working agreement

- **Weekly demo.** Show what runs. Broken-with-an-explanation is fine and normal.
- **Weekly written update:** did / learned / blocked / next. Short.
- **PRs reviewed within one working day.** If yours is sitting longer, ping.
- **Stuck for about an hour → ask.** Say what you tried and what you expected. Being
  stuck is normal and expected; sitting on it silently for three days is the only
  version that's a problem.

Working across timezones, default to written and asynchronous. If something needs a
call, say so and it'll get scheduled — but don't block on one.

---

## Open questions

- **Repo and IP arrangement** — decided once you've picked a project, since it
  depends on what the project turns out to be. It'll be written down explicitly
  before Phase 2 starts rather than left informal.
