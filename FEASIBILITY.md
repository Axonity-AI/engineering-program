# Phase 1b — Feasibility Spikes

Two candidates. Two days each. Four days total, then you decide.

## Why not just pick after the taste test?

The taste test tells you what kind of work you enjoy. It doesn't tell you whether
a specific project is *doable* — and that's a separate question with a habit of
answering itself late and expensively.

Things that only show up when you touch the real thing:

- The dataset needs an application, or a licence agreement, or is 400GB
- The reference implementation doesn't build, or hasn't been touched since 2023
- A "quick baseline" is a two-day CUDA dependency fight
- Training that was going to take an hour takes eleven
- The paper's numbers turn out to rely on something not in the released code

Every one of those is cheap to discover on day two and brutal on week five.

**The rule: reproduce a baseline before committing.** Not read about it. Run it,
on the real data, on your actual hardware.

---

## The two days

**Day 1 — get something running.**
Install the tooling. Get the real dataset (not a toy sample). Run the simplest
baseline that produces a number or an image. Capture evidence — a screenshot, a
metric, a log.

If day 1 ends with nothing running, that is not a failed spike. That's a
successful spike returning a clear result, and it should weigh heavily.

**Day 2 — find the edges.**
Now push on it. What's the hardest unknown? Can you see a path through it, or is
it a wall? How long did that training run actually take, and what does that imply
for an experiment you'd need to run fifty times? What would V1 have to exclude?

Then write the note.

---

## The feasibility note

One page. Not two. If you can't say it in a page, you don't understand it yet.

```markdown
# Feasibility: <project>

## The question
What this project answers, in one sentence.

## Baseline I actually ran
What I ran, on what data, on what hardware, and what came out.
<Evidence: metric, screenshot or log. This section is void without it.>

## Data
Source, size, how I got it, licence, and any access friction.

## Compute reality
How long the baseline took. What a full experiment would take. What that
implies for how many experiments fit in six weeks.

## Three decisions I'd own
The judgement calls that would be mine — the things an interviewer would ask
about. If you can't name three, the project may be integration rather than
engineering.

## Hardest unknown
The thing most likely to eat a week. Do I have a route through it?

## V1 "done" definition
What exists at the end. Specific enough to be checkable.

## What I will explicitly NOT build
The scope guardrail. Be aggressive here — this is the line that saves the
project, and everyone writes it too generously.

## Do I still want this?
After actually touching it. Honest answer.
```

That last section carries real weight. Enthusiasm surviving contact with the
real tooling is a meaningful signal; enthusiasm evaporating on contact is a
*more* meaningful one, and it's much cheaper to act on now than in week six.

---

## Using AI tools during a spike

Use them freely to install things, fight dependencies and get a baseline running.
That's exactly what they're good for.

**But the note must be written from your own understanding.** If you can't
explain what the baseline is doing and why it produces the number it produces,
that candidate isn't ready to commit to — the spike has told you that you'd be
supervising a system you don't understand for eight weeks.

---

## Deciding

Both notes on the table, then choose. Weigh in roughly this order:

1. **Did the baseline run?** A project that resisted a spike will resist a build.
2. **Do you still want it after touching it?** This outranks any ranking made
   before you'd run anything.
3. **Are the three decisions real?** If they're all "which library," it's
   integration work and it won't generate interview material.
4. **Does compute fit?** If one experiment takes six hours, you get very few of
   them, and a project needing fifty ablations is already out of scope.
5. **Is the V1 genuinely cuttable?** Every project here can expand infinitely.
   The ones that survive are the ones with an honest floor.

**Not on the list: which sounds more impressive.** Everything here is impressive
if it's finished and well-explained. Nothing here is impressive if it's abandoned
at 70%.

Write the decision down with reasoning, as an ADR in the project repo. It's the
first one, and the reasoning is worth having on record when someone asks in an
interview why you chose it.
