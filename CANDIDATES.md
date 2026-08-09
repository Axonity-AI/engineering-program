# Candidate Projects

Ten options, narrowed from a longer research list. They're deliberately spread
across **different kinds of engineering**, not ten variations on one theme —
because the point of Phase 1 is to find out which kind you actually like doing.

Don't pick from this document. Read it, do the [taste-test](TASTE_TEST.md), then
pick. Descriptions are a bad predictor of what's enjoyable to debug at week five.

---

## How to read these

Each entry has:

- **The question** — the thing the project answers. If a project has no question,
  it's a demo, not a project.
- **What you'd own** — the decisions that are yours. This is what an interviewer
  will actually ask about.
- **Data + licence** — verified, not assumed. See the licensing note below.
- **Compute** — against a local NVIDIA GPU plus a cloud budget.
- **Hardest unknown** — the thing most likely to eat a week.

### A note on licensing, because it matters more than it sounds

Several of the obvious "default" datasets for these projects are
**non-commercial research-use only** (CC BY-NC-SA). That's fine for a portfolio
piece and a public repo. It is *not* fine if Axonity ever wants to put the
result in front of a client. Where the obvious dataset is restricted, a
commercially-usable alternative is named. **Decide which track you're on in week
one** — retrofitting a different dataset in week six is miserable.

---

## 1. Sim2Inspect — industrial defect inspection

**The question:** does synthetic training data actually improve real-world defect
detection, and by how much?

Detect manufacturing defects in product images. The interesting part isn't the
detector — it's the controlled experiment: generate synthetic defects, train
with and without them, and measure whether it helped. **The answer might be no.**
A rigorously measured negative result is a better interview story than a demo
that works for unclear reasons.

**What you'd own:** anomaly detection vs. supervised segmentation vs.
embedding-kNN as the formulation; how realistic synthetic defects need to be
before they help; what metric to use when false positives are expensive (AUROC
alone is not enough); how thresholds shift across product types and lighting.

**Data + licence:** **VisA** — CC BY 4.0, commercial use permitted.
⚠️ **Avoid MVTec AD** as your primary dataset: it's CC BY-NC-SA 4.0,
non-commercial only. Fine to cite as a research comparison, not as the spine.

**Compute:** Low-medium. Frozen pretrained features + kNN needs almost no
training, which means fast iteration.

**Hardest unknown:** whether your synthetic defects are realistic enough to
transfer at all.

---

## 2. SceneWeaver — video to explorable 3D scene

**The question:** how do you fuse 2D semantic understanding into a 3D
reconstruction consistently, and how do you know when the reconstruction is bad?

Turn a phone video of a room into a 3D scene you can fly through, then layer
learned semantic understanding on top so objects are identifiable and
searchable.

**What you'd own:** classical structure-from-motion vs. learned pose/depth, and
where each fails; how 2D masks fuse into 3D without contradicting each other
across views; how view count, blur and camera baseline affect quality; whether
V1 is a splat, a point cloud or a mesh.

**Data + licence:** you generate your own captures, so no dataset restriction.
⚠️ **Tooling licence is the trap here:** the reference 3D Gaussian Splatting
implementation from Inria is **research/non-commercial only**. Use **`gsplat` /
Nerfstudio (Apache 2.0)** instead. COLMAP is BSD — fine.

**Compute:** Medium-high. This is the most GPU-hungry option.

**Hardest unknown:** reconstruction quality on real handheld video, which is
much worse than the paper figures suggest.

---

## 3. EdgeSmith — deployment optimizer

**The question:** for a given model and target hardware, what's the actual
accuracy/latency/memory frontier, and which optimisations are safe?

Feed it a trained model and a deployment target; it finds the best configuration
across precision, quantisation and runtime, and produces a Pareto report.

**What you'd own:** which optimisations are safe for a given architecture; how to
benchmark fairly (warmup, batching, thread count, variance); where the
acceptable accuracy-loss boundary sits; when quantisation calibration data is
misleading.

**Data + licence:** standard vision models and validation sets — permissive.

**Compute:** Low. Mostly inference.

**Hardest unknown:** measurement noise. Benchmarking honestly is much harder than
it looks, and this project lives or dies on it.

**Note:** this is the option that most directly attacks testing, Docker and
deployment — the three you rated yourself lowest on. It's also the least
"read a paper" of the ten, which cuts against what you said motivates you.

---

## 4. GripForge — robot arm learns to pick things up

**The question:** what does the reward function actually incentivise, as opposed
to what you intended it to incentivise?

Train a simulated arm to pick and place, then explain why the learned policy
succeeds or fails. Compare a scripted baseline, imitation learning and RL
side-by-side.

**What you'd own:** reward design; state vs. vision observations and the cost of
partial observability; when imitation should bootstrap RL; how much domain
randomisation helps before training destabilises.

**Data + licence:** MuJoCo (Apache 2.0) or Isaac Lab (BSD-3). Clean.

**Compute:** Medium, but long wall-clock — RL training runs are measured in hours.

**Hardest unknown:** RL debugging has genuinely unbounded time variance. When it
doesn't learn, the cause could be the reward, the observation space, the
hyperparameters or a bug, and telling those apart is the skill.

---

## 5. PitchIQ — soccer footage to tactical data

**The question:** how do you track identities reliably through occlusion, and how
do you measure that honestly rather than by picking nice clips?

Broadcast video in, player tracks and a top-down tactical map out.

**What you'd own:** detector/tracker association trade-offs during occlusion; how
to estimate camera homography robustly from broadcast video; which tactical
metrics are stable enough to actually claim; how to evaluate identity switches
instead of cherry-picking.

**Data + licence:** **SoccerNet** — free for research and education with
attribution. ⚠️ Commercial use requires prior written permission. Fine for a
portfolio piece; would need a conversation before any client use.

**Compute:** Medium.

**Hardest unknown:** homography estimation from moving broadcast cameras.

---

## 6. ThreatGraph — lateral movement detection

**The question:** how do you rank suspicious activity when labels are almost
nonexistent, without leaking future information into the model?

Turn authentication logs into a graph and surface suspicious lateral-movement
paths with supporting evidence.

**What you'd own:** how to build the graph without temporal leakage (this is the
central trap and it's subtle); which baseline catches real anomalies without
drowning an analyst in alerts; how to rank with sparse labels; what counts as
evidence versus post-hoc storytelling.

**Data + licence:** **LANL authentication dataset** — released under a public
domain waiver. Cleanest licensing of the ten, and it includes labelled red-team
activity, so you have ground truth.

**Compute:** Low. This is CPU-friendly.

**Hardest unknown:** temporal leakage. It's easy to build a model that looks
excellent and is silently cheating.

**Scope guardrail:** defensive detection only. No exploit or attack tooling.

---

## 7. SpectraGuard — RF signal classification

**The question:** how does a signal classifier degrade as signal-to-noise
worsens, and can it recognise a signal type it was never trained on?

Classify radio signals from raw IQ data, and show exactly where the model
collapses.

**What you'd own:** raw IQ vs. spectrogram representation; how to stop synthetic
channel artifacts becoming shortcuts the model exploits; how to randomise SNR,
frequency offset and fading; how to detect unknown signals rather than forcing
everything into a known class.

**Data + licence:** ⚠️ **RadioML is CC BY-NC-SA — non-commercial.** Generate your
own with **GNU Radio** instead; data you generate is yours, and generating it is
itself a good chunk of the learning.

**Compute:** Low.

**Hardest unknown:** making synthetic channel effects realistic enough that the
model learns signal structure rather than your simulator's fingerprints.

**Scope guardrail:** classification and anomaly awareness only. No jamming or
operational RF tooling.

---

## 8. GeoSentinel — satellite change detection

**The question:** how do you distinguish real change from misregistration,
seasonal variation and sensor differences?

Compare before/after satellite imagery and produce an evidence-backed damage or
change map.

**What you'd own:** pixel differencing vs. learned semantic change detection; how
to align imagery across sensors and dates before comparing; handling severe
class imbalance and noisy labels; communicating uncertainty without implying a
map is certain.

**Data + licence:** **SpaceNet** (CC BY-SA 4.0, commercial use permitted with
share-alike) or **Sentinel-2** via Copernicus (open). ⚠️ **Avoid xBD** as the
spine — CC BY-NC-SA, non-commercial.

**Compute:** Medium. Data volume is the real cost, not training.

**Hardest unknown:** registration. Two images of the same place are never quite
the same place.

---

## 9. SoundScape — silent video to spatial audio

**The question:** what visual motion cues predict sound timing, and how do you
evaluate audio-visual synchronisation objectively?

Watch a silent clip, identify what's making noise, and construct spatially
plausible stereo audio.

**What you'd own:** generate audio vs. retrieve from a licensed library; which
motion cues predict onset timing; how to map 2D position and a depth proxy into
stereo space; how to evaluate synchronisation without relying purely on "sounds
right to me."

**Data + licence:** ⚠️ **Needs checking during the spike.** Audio-visual datasets
are frequently YouTube-derived, which brings redistribution restrictions. Verify
before committing — this is the least-settled licensing position of the ten.

**Compute:** Medium.

**Hardest unknown:** evaluation. "Does this sound right" is hard to turn into a
number.

---

## 10. FlowTwin — physics surrogate model

**The question:** where does a fast learned approximation of a slow physics
solver stop being trustworthy?

Replace a slow simulation with a neural surrogate, then quantify precisely where
the surrogate breaks down.

**What you'd own:** operator model vs. convolutional surrogate vs.
physics-informed network; what normalisation preserves physical meaning; how to
split the parameter space so your test set is genuinely out-of-distribution; how
to communicate uncertainty where the surrogate is unsafe to trust.

**Data + licence:** you generate it from an open solver (OpenFOAM, SU2). No
dataset restrictions; note the solvers themselves are GPL/LGPL, which affects
distribution of modified solver code but not your generated data.

**Compute:** Medium, plus meaningful CPU time generating training data.

**Hardest unknown:** the physics ramp-up. This is the biggest domain-knowledge
investment of the ten.

---

## Wildcard: NeuroTrace

A path tracer where a neural network predicts where to spend compute. It's the
most technically differentiated thing on the original list — very few new grads
can write a renderer *and* train a model — and it's genuinely rare in a
portfolio.

It's held back rather than dropped because it's C++-heavy and has the largest
scope. **If the systems exercise in the taste-test is the one you enjoy most,
ask about this** and we'll look at whether a scoped V1 fits the timeline.

---

## What was cut, and why

Transparency on the curation, so you can push back if something looks wrong:

| Cut | Reason |
|---|---|
| ScanTrust (MRI reconstruction) | Your capstone already covers medical imaging + CV. Re-proving it adds little. |
| DriveWorld, TrafficMind, GridPilot, SiliconPilot, ArenaMind | All reinforcement learning. GripForge represents the category; five variants would waste slots. |
| AgroScout | Overlaps GeoSentinel — both aerial imagery segmentation. |
| WeatherScale, MatForge | Overlap FlowTwin — all scientific ML with uncertainty. |
| Anything LLM/RAG/agent-centred | Erseno already demonstrates this, and it's the most saturated category in the market. |
| Frontend-led work | Your portfolio site already covers it. |

The redundancy cuts are the important ones. You already have real evidence of CV
model training and of RAG/agent systems. The marginal value of a third project
in either area is low; the marginal value of something genuinely different is
high.
