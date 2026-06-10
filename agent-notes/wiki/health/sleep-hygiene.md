---
source: agent
compiled_from:
  - agent-notes/raw/health/2024-10-16-bryan-johnson-six-sleep-habits.md
compiled_at: 2026-06-10
model: claude-opus-4-7
confidence: medium
---

# Sleep hygiene

Sleep hygiene is the bundle of behavioral and environmental controls that govern sleep quality — meal timing, pre-bed cognitive load, stimulant clearance, evening light, bedroom temperature, and ambient noise. The mechanisms are well-established in chronobiology and sleep medicine; the contested questions are around the magnitude of each lever and the practical thresholds at which they bind. This article currently reflects Bryan Johnson's self-experimentation framing, which is N-of-1 and optimization-maxxed; treat the specific numbers as Johnson's measured optima rather than population recommendations.

## The six levers (Johnson's framing)

Johnson — the Blueprint protocol founder — frames sleep degradation as the cumulative effect of six modifiable habits. He arrived at his settings by running "a few hundred experiments" with resting heart rate (RHR) as the proxy for sleep quality.

### 1. Late eating

Eating close to bedtime triggers a digestive metabolic load, a blood glucose spike followed by reactive drop, and a disruption of the evening melatonin rise. Johnson's claim is that his RHR at sleep onset is the best single predictor of sleep quality: 46–50 bpm "almost guarantees" a high-quality night; 55–57 bpm guarantees ~30% lower quality. His personal optimum is a final meal at 11:00–11:30 a.m. for an 8:30 p.m. bedtime — roughly a 9-hour fast before sleep. He recommends others not copy the time but progressively walk back from current habits in 1-hour steps (2 → 3 → 4 hours before bed).

The RHR-as-sleep-quality-proxy is consistent with the broader use of HRV and resting HR as recovery markers in the [[health-stack]] preventive-medicine framework. The directional claim — earlier last meal → better sleep — is well-supported; the specific "11 a.m." threshold is Johnson-specific.

### 2. No wind-down (cognitive arousal)

Working until lights-out keeps the sympathetic nervous system active when it should be ceding to parasympathetic dominance. Johnson's protocol is a hard role switch 60 minutes before bed: "nighttime Brian is now in charge" and incoming work thoughts are externalized ("thank you work Brian — we have all day tomorrow"). Parasympathetic-activating activities he recommends: reading a physical book (his favorite), journaling, meditation, a bath, a walk. Things to avoid: arguments, hard exercise, and "anything really stimulating."

The framing is consistent with standard cognitive behavioral therapy for insomnia (CBT-I) protocols — externalization of intrusive thoughts ("worry time") and stimulus-control rules.

### 3. Late stimulants

Caffeine has a ~6-hour half-life, so a 4 p.m. cup is pharmacologically equivalent to half a cup at 10 p.m. Genetic variation in CYP1A2 produces wide differences in caffeine metabolism — fast metabolizers tolerate evening doses, slow metabolizers don't. Johnson stopped both caffeine and alcohol entirely; he attributes mood stabilization to alcohol elimination specifically (alcohol fragments REM sleep even when it reduces sleep latency).

### 4. Evening light

Morning sun (15–30 min in the first hour after waking) anchors the circadian rhythm and lifts mood. In the evening, the inverse: 2 hours before bed, dim to warm-spectrum lighting (2700–3500 K), eliminate blue light. Mechanisms: blue light suppresses melatonin production via melanopsin-expressing intrinsically photosensitive retinal ganglion cells (ipRGCs). Practical interventions:
- `f.lux` (or system Night Shift) to wash blue out of screens
- Blue-light-blocking glasses
- Best: no screens at all in the last hour before bed (Johnson's house rule)

### 5. Bedroom temperature

Core body temperature drops to initiate sleep and dips further into deep sleep. A hot bedroom blocks this thermoregulatory ramp. Johnson uses an Eight Sleep temperature-controlled mattress with a stage-aware temperature profile:
- 73°F at sleep onset
- 69°F in deep sleep
- 71–72°F during REM
- 73°F on waking

Eight Sleep's "autopilot" mode automates these transitions. Johnson notes a downside: once you're acclimated to a controlled mattress, travel becomes harder — hotel rooms typically only cool to ~64°F, and you lose the dynamic profile.

Lower-cost interventions before splurging on an Eight Sleep: open windows for cross-ventilation, blackout blinds to reduce daytime heat soak.

### 6. Noise

Even sub-arousal noise (dogs, traffic, neighbors) produces sleep micro-arousals that fragment sleep architecture without waking you fully. Johnson's first-resort fix is social: ask neighbors directly, offer a good-faith gesture in exchange. Second resort: a brown/white/pink noise machine to mask intermittent disruptions. ("Good evidence" that masking works — uncited.)

## Mechanistic substrate

Five of the six levers operate via the autonomic nervous system or circadian system:

| Lever | Mechanism |
|---|---|
| Late eating | Sympathetic activation from digestion + glucose volatility + melatonin disruption |
| Cognitive arousal | Sympathetic activation; failure to downshift to parasympathetic |
| Late stimulants | Caffeine adenosine-receptor antagonism; alcohol REM disruption |
| Evening light | Melanopsin/ipRGC → suppressed melatonin via the suprachiasmatic nucleus |
| Temperature | Disrupted thermoregulatory descent that gates sleep onset and deep sleep |
| Noise | Auditory cortex micro-arousals fragmenting sleep architecture |

The "RHR as sleep proxy" claim works because RHR at sleep onset reflects autonomic balance — high sympathetic tone keeps RHR elevated and predicts poor recovery.

## Implications and how to use this

- **The levers are independently modifiable.** You don't have to adopt Johnson's full protocol; the smallest-effort wins are usually evening light and meal timing.
- **Johnson's specific numbers are N-of-1.** The 11 a.m. last meal, 8:30 p.m. bedtime, 46–50 bpm RHR target, and 69–73°F profile are his measured optima after hundreds of experiments. Use them as a search-space prior, not a prescription. The protocol Johnson is selling — the [[health-stack|Blueprint stack]] — is itself an aggressive optimization regimen, so the recommendations are framed for someone willing to upend their schedule.
- **The cultural framing matters.** Johnson closes by arguing that sleep-deprivation bravado is a status signal that should be inverted: getting 8 hours is the hero move. This is a deliberate counter-positioning against hustle culture.
- **The hard part is the wind-down, not the inputs.** Buying an Eight Sleep, flux, and blackout blinds is one weekend. Externalizing work thoughts at 7:30 p.m. every night is the practice that actually compounds.

## Sources

- Bryan Johnson (2024-10-16). "Why You're Always Tired." <https://www.youtube.com/watch?v=3kAiPSEnrHI> — [[2024-10-16-bryan-johnson-six-sleep-habits|local copy]]
