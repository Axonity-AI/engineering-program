# Phase 1a — The Taste Test

Six exercises. One full day each. About a week and a half.

## Why this exists

You've had real exposure to maybe two of the areas in
[CANDIDATES.md](CANDIDATES.md). For the rest, any preference you have right now
is based on descriptions, job titles and what sounds impressive — none of which
predict whether you'll enjoy the work.

Committing 8+ weeks to a field you've never touched, based on a paragraph, is a
bad bet. A week spent finding out is cheap insurance, and the exercises are
useful practice regardless of what you pick.

**A full day each, not half.** Half a day gets you through setup and a working
example, which tells you nothing — everything is pleasant when it works. The
signal is what happens in the hour *after* it stops working. That's the hour
you're actually sampling, because that hour is most of the job.

---

## The rules that make this worth doing

Read these before exercise 1. They're the difference between a real experiment
and a week and a half of going through the motions.

### 1. Predict before you start

Before each exercise, write one line: **do you expect to enjoy this, and why?**
Commit it before you begin.

At the end you'll compare predictions against reality. Where they diverge is the
most useful output of the whole week — it tells you how much your sense of your
own interests is worth, which is worth knowing well beyond this project.

### 2. Write your reaction before discussing it

Finish the exercise, write the reaction, *then* talk to your mentor about it. Not the
other way around.

This one is not bureaucracy. Once you've heard someone else's opinion — 
especially someone whose judgement you rate — your own recollection quietly
reshapes itself to match. Writing first is the only reliable defence.

### 3. Answer behavioural questions, not "did you like it?"

"Did you enjoy it" gets you a politeness reflex. These get you evidence:

- Did you look anything up **beyond what the exercise required**? What?
- When it broke, did you want to understand *why*, or just get past it?
- What did you want to try next when the day ended?
- At what point did you first want to stop?
- Would you spend a Saturday on this, unpaid, out of curiosity?
- Did you explain any of it to someone unprompted?

The last two are the strongest signals. Voluntary time and unprompted
explanation are hard to fake and hard to talk yourself into.

### 4. Rank on the work, not the label

At the end you'll rank all six. Every justification must be **about the work
itself** — what you were doing, hour to hour, and how it felt.

Reasoning from career labels is explicitly disallowed. "ML engineers earn more,"
"computer vision is what's hot," "this is what my mentor does" — these are not
reasons, and if they're doing the work then this whole week was wasted. There's
no wrong answer here. Landing on RF signal processing or graph analytics is a
completely fine outcome, and the project will adapt.

### 5. Your mentor stays quiet

They'll write their own observations independently and won't share any preference
until all six are done and your ranking is written. Then you compare notes. If
they steer you mid-week, the experiment is contaminated and we've learned nothing.

---

## Exercise 1 — 3D and geometry

**Maps to:** SceneWeaver

**Setup:** Install COLMAP and `gsplat` (Nerfstudio). Note: use `gsplat`, not the
Inria reference implementation — see the licensing note in CANDIDATES.md.

**Do this:**
1. Shoot a short video of an object on a desk with your phone. Walk around it.
2. Reconstruct it. Look at the result.
3. Now shoot a video of something that will *fail*: a blank wall, a shiny or
   transparent object, or move the camera fast enough to motion-blur.
4. Work out why it failed. Not "it didn't work" — the actual mechanism.

**The point:** step 4. Understanding *why* geometry fails requires understanding
how feature matching works. This is the part that can't be prompted out of a
model, and it's what the whole project would be made of.

---

## Exercise 2 — Systems and measurement

**Maps to:** EdgeSmith, NeuroTrace

**Setup:** Any pretrained vision model from `timm` or `torchvision`.

**Do this:**
1. Measure inference latency. Properly — warmup runs, many iterations, report
   the median and the p95, not one `time.time()` call.
2. Profile it. Find where the time actually goes. It will surprise you; it's
   frequently not the part you'd guess.
3. Make it 2x faster with one change.
4. Prove the output didn't change meaningfully.

**The point:** steps 1 and 4. Most people's benchmarking is wrong in ways that
flatter their results. Learning to distrust your own measurements is a
genuinely valuable and quite rare skill.

---

## Exercise 3 — Reinforcement learning

**Maps to:** GripForge

**Setup:** Stable-Baselines3 with a standard control environment.

**Do this:**
1. Train PPO on CartPole or similar until it solves the task.
2. Now **modify the reward function** to something slightly wrong but
   superficially reasonable. Reward staying near the centre, say, or reward
   survival time in a way that lets the agent stall.
3. Retrain and watch what the agent does with your mistake.
4. Sit and watch a training curve for a while. Genuinely — this is the job.

**The point:** step 3, watching your agent exploit a loophole you didn't know you
wrote, is the entire character of RL work. Some people find this delightful.
Others find it maddening. Both reactions are informative and neither is wrong.

---

## Exercise 4 — Pick one: signals *or* graphs

**Maps to:** SpectraGuard, ThreatGraph, MolForge — and Option B is also the core
skill in QuantRisk, where leaking future information is the single most common way
financial models look brilliant and are worthless.

Choose whichever sounds *less* appealing. You'll learn more from it.

### Option A — Signals

1. Generate a clean signal. Add noise, or throw away 75% of the samples.
2. Reconstruct it with something simple.
3. Push the corruption until reconstruction fails.
4. **Look closely at what the model invents** when it doesn't have the
   information. It won't output "I don't know" — it'll output something
   confident and wrong. Find where.

### Option B — Graphs

1. Take any log file with timestamps and entities. Build a graph from it.
2. Score nodes for anomalousness with something simple.
3. Now check: **does your scoring use information from the future?** If you
   built the graph from all the data and then scored events in the middle, it
   does.
4. Fix it so it doesn't, and see how much worse the results get.

**The point:** both land on the same lesson from opposite directions — models
producing confident output that is silently invalid. Step 3/4 is the payload.

---

## Exercise 5 — Experimental rigor

**Maps to:** Sim2Inspect, GeoSentinel, PitchIQ — and honestly, all nineteen

**Setup:** Any trained classifier. Reuse one of yours if it's easiest.

**Do this:**
1. Get its overall accuracy. Write it down.
2. Now **break that number apart.** Accuracy per class, per image size, per
   brightness, per any property you can slice by. Find the slice where it's
   worst.
3. Form a hypothesis about *why* that slice is bad.
4. **Design the experiment that would confirm or refute it.** Write it out:
   what you'd change, what you'd hold fixed, what result would prove you wrong.
5. If time permits, run it.

**The point:** step 4 is the single most transferable skill on this list, and
it's the thing your existing portfolio has no evidence of. This exercise is in
the area you're most comfortable in — but it's testing a skill, not a domain.
Being good at training models and being good at *evaluating* them are different
abilities, and the second one is rarer.

---

## Exercise 6 — LLM engineering, with rigor

**Maps to:** EvalForge, AgentProof, CompliAgent, InsightBoard, ClinicalScribe

**Setup:** Any LLM API and about 30 examples of a task with a right-ish answer —
summarisation, extraction, classification, whatever you like.

**Do this:**
1. Run the task. Collect the outputs.
2. Write an **LLM-as-judge** prompt that scores each output. Run it. You now have
   a quality number.
3. Now **hand-label the same 30 yourself.** Properly. It's tedious; that's the point.
4. **Measure the agreement** between your labels and the judge's. Not "do they
   look similar" — compute it.
5. Look hard at every case where you and the judge disagreed. Who was right?

**The point:** step 4 is where it lands. The judge will not agree with you as much
as you assumed, and the disagreements will not be random — judges tend to have
systematic biases, like preferring longer, more confident-sounding answers.

The moment you see your quality metric is itself unreliable is the moment LLM
engineering stops being prompt-writing and becomes engineering. Roughly 95% of
enterprise LLM projects fail, and this is the thing they mostly failed to do.

**Note:** this is the one exercise where an AI assistant can do the whole task
badly and you'd never notice. Step 3 in particular has to be your own labour. If
you outsource the hand-labelling, the exercise measures nothing.

---

## The write-up

Per exercise, a short markdown file in **`taste-test/` in this repository**
(`Axonity-AI/engineering-program`) — committed via a PR like anything else, so
the write-ups are reviewable and the habit stays consistent:

```markdown
# Exercise N — <area>

## Prediction (written before starting)
<one line>

## What I did
<a paragraph; what actually happened, including what broke>

## Behavioural answers
- Looked up beyond requirements:
- When it broke, I wanted to:
- Wanted to try next:
- First wanted to stop:
- Would spend a Saturday on it:
- Explained it to someone unprompted:

## Reaction
<a paragraph. Honest. "I found this tedious" is a completely valid and useful
answer — arguably more useful than enthusiasm.>
```

Then a final `taste-test/RANKING.md`: all six ranked, each with a justification
**about the work**, plus an explicit note on where your predictions were wrong.

That last section is the one to spend real time on.

---

## What happens next

You name **two** candidates. Not one — two, so the feasibility spikes
([FEASIBILITY.md](FEASIBILITY.md)) have something to compare against. Then we
spend two days each actually touching the real data and tooling, and decide on
evidence.
