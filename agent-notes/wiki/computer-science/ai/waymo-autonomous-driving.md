---
source: agent
compiled_from:
  - agent-notes/raw/computer-science/ai/2026-03-24-waymo-dolgov-stripe-interview.md
compiled_at: 2026-04-15
model: claude-opus-4-6
confidence: high
---

# Waymo Autonomous Driving

Waymo, Alphabet's autonomous vehicle subsidiary, operates fully driverless ride-hailing across US cities. Co-CEO Dmitri Dolgov — who joined the Google self-driving car project in 2009 as one of its first engineers — has described the system architecture, scaling trajectory, and why full autonomy is a qualitatively different problem from driver assistance.

## Architecture: foundation model → teachers → distilled students

The Waymo Driver is built from a single large **foundation model** that understands physical-world dynamics — how objects relate, how agents behave socially, what constitutes good driving. This foundation is specialized into three off-board "teacher" models:

1. **The Driver** — the primary driving model, which becomes the backbone running on-car after distillation.
2. **The Simulator** — powers a synthetic generative environment for closed-loop training and evaluation. Shares the foundation model's understanding of multi-agent interaction, but generates probabilistic future worlds rather than choosing actions.
3. **The Critic** — evaluates behavior quality, providing reward signals. Identifies interesting events and judges what constitutes good vs. bad driving.

Each teacher trains a smaller **distilled student** model optimized for its deployment context (on-car inference, cloud simulation, evaluation). This architecture means improvements to the foundation model cascade through all three downstream systems.

All real-time driving inference runs locally on the vehicle — nothing safety-critical goes to the cloud. Cloud models handle non-driving tasks like detecting left items or flagging cars for cleaning.

## Sensor fusion: cameras, LiDAR, radar

Waymo uses three complementary sensing modalities, all with 360-degree coverage:

- **Cameras** — high-resolution visual data; degrades in darkness, glare, and fog
- **LiDAR** — millions of laser pulses per second sampling 3D structure; unaffected by lighting conditions but can degrade in heavy particulates
- **Radar** — lower resolution but resilient to adverse weather (fog, rain, snow); can detect vehicles invisible to cameras

Each modality has a dedicated encoder. Rather than estimating the world separately through each sensor and comparing, the encoders jointly feed a fused representation. Dolgov describes this as the system learning to weight each modality based on conditions — on bright days cameras contribute more; in fog, radar dominates — without explicit switching logic.

A striking example of emergent sensor fusion: a Waymo detected a pedestrian hidden behind a bus by picking up noisy LiDAR reflections of foot movement bouncing *under* the bus. The AI models were confident enough in this minimal signal to classify a pedestrian and predict their trajectory. Dolgov notes this would be nearly impossible for a pure pixels-to-actions system since the pedestrian doesn't exist in pixel space — it requires an intermediate world representation.

## End-to-end vs. augmented end-to-end

Dolgov frames the end-to-end debate with nuance: Waymo's system *is* end-to-end in the sense that gradients propagate through all layers (no narrow information bottleneck between encoder and decoder). However, pure "pixels in, trajectories out" is augmented with structured intermediate representations — objects, roads, signs, speed limits.

These intermediate representations serve three purposes:

1. **Simulation efficiency** — you can simulate at the representation level rather than regenerating full pixel scenes
2. **Safety validation** — additional real-time verification layers
3. **Reward specification** — more precise critic/evaluation signals

Dolgov notes that a vanilla VLM fine-tuned to output trajectories (as in Waymo's published EMMA paper) actually drives well in nominal cases — "like a talking horse, it's impressive that it's talking" — but is "orders of magnitude" from the safety level required for full autonomy. The gap is bridged by closed-loop training via RLFT (Reinforcement Learning-based Fine-Tuning) in simulation, which requires the simulator and critic subsystems that pure end-to-end makes impractical at scale.

This connects to [[the-bitter-lesson]] — general methods leveraging computation dominate — but with a twist: Dolgov argues that for safety-critical physical-world AI, you need structured intermediate representations alongside the learned ones, not as a crutch but because they unlock the simulator and critic infrastructure necessary for the required "number of nines."

## The ADAS vs. L4 discontinuity

Dolgov is explicit that driver-assist systems (ADAS, L2/L3) and full autonomy (L4/L5) are **fundamentally different problems**, not points on a spectrum. Product convergence (ride-hailing today, personal cars eventually) and hardware convergence (cheaper, more integrated sensors) will happen, but the core technology challenges are qualitatively different.

The hardest parts of building a fully autonomous rider-only system "are very different from what you do for a driver-assist system." Work in the ADAS space helps, but reaching full autonomy requires a "qualitative jump." This is a direct counter to the incremental-improvement thesis (e.g., Tesla's approach of scaling up from Autopilot).

## Hardware generations and cost trajectory

Waymo is on its sixth hardware generation:

| Generation | Vehicle | Key characteristic |
|---|---|---|
| Gen 4 | Chrysler Pacifica | First commercial deployment (Chandler, AZ, 2020). Many small ML models. |
| Gen 5 | Jaguar I-PACE | Unified AI backbone. Massive operating-domain expansion. Currently in fleet. |
| Gen 6 | Ojai (custom) + Hyundai Ioniq | Simpler, more capable, "fraction of the cost." Comparable to a high-end ADAS system. Same software as Gen 5. |

The Gen 5 → Gen 6 transition is notable: the software barely changes, but the sensor hardware is dramatically simplified and cheaper. LiDAR, radar, and camera costs are all following well-known manufacturing cost curves. Gen 6's Ojai vehicle is purpose-built for passengers (flat floor, sliding doors, living-room feel) rather than retrofitted from a driver-centric car.

## Scaling metrics (as of March 2026)

- ~3,000 cars on roads
- ~500,000 rides per week (~25M annualized)
- ~4M+ fully autonomous miles per week
- 11 US cities (10 with public riders; Nashville testing-only)
- Launched 4 new cities in a single day (vs. 8 years from first autonomous operation to first 4 cities)
- London and Tokyo launches planned for 2026

## Generalization and remaining challenges

The core technology generalizes well across cities, vehicle platforms, and sensor configurations. VLM integration provides strong zero-shot/few-shot transfer to new geographies. Waymo frames expansion not by city but by **operating domain** (freeways, weather conditions, density, etc.) — a city either falls within the current domain or requires domain extension.

What generalizes least well: **cold weather** affects the entire stack (hardware needs heating/cleaning; motion control on slippery surfaces is a distinct engineering problem). Drop-off/pickup behavior remains a nuanced UX challenge.

## Second-order effects of autonomous traffic

Dolgov highlights two major downstream effects:

1. **Traffic flow** — autonomous vehicles drive smoothly and predictably, which should dramatically reduce standing-wave traffic jams caused by abrupt human reactions
2. **Urban land use** — cars sit idle ~90% of the time; autonomous fleets could eliminate most parking infrastructure, freeing vast urban land for other uses (echoing arguments about parking minimums reshaping cities)

Personally-owned Waymo vehicles may eventually serve low-density areas where fleet ride-hailing doesn't make economic sense.

## On Google's role

Dolgov credits Alphabet's culture — "big vision and stamina to go the distance" — for sustaining a 20-year investment through periods where self-driving seemed perennially two years away. The problem's complexity required iterative learning through multiple technology waves (ImageNet, transformers, VLMs), none of which were silver bullets. Each "drastically reshaped the early part of the curve" but couldn't shortcut the full safety engineering. The standard rule of thumb applies: every additional nine of reliability costs 10x more effort.

## Sources

- Stripe (2026). "The 20-year journey to fully autonomous cars with Dmitri Dolgov of Waymo." <https://www.youtube.com/watch?v=PCCtWDbTDX4> — [[2026-03-24-waymo-dolgov-stripe-interview|local copy]]
