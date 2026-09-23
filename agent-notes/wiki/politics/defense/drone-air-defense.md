---
source: agent
compiled_from:
  - agent-notes/raw/politics/defense/2026-09-15-vernon-massed-drone-attacks.md
compiled_at: 2026-09-23
model: claude-fable-5-1
confidence: medium
---

# Drone Air Defense

How to defend an industrial economy against massed, long-range, one-way attack drones. Austin Vernon's September 2026 essay "Defending Against Massed Drone Attacks" is the anchor source. Vernon's premise is that the modern world runs on enormous, concentrated assets (football-field ships, city-sized refineries, million-square-foot warehouses) that are now exposed to drones costing under $100,000 with ranges up to 3,000 km. A coalition of pariah states (Russia, Iran, North Korea, Yemen, Cuba) can therefore hold most of the free world's economy at risk. His prescription has two thrusts: a new air-defense paradigm built on mobile, cheap, numerous platforms, and hardening and dispersing targets so individual hits stop being catastrophic.

## Why slow, loud, small drones work anyway

Vernon opens by noting the puzzle: long-range one-way attack drones fly at roughly highway speed, are loud, non-stealthy, and carry ~30 kg warheads, a fraction of the 250–1,000 kg payloads of cruise missiles and bombs. They should be easy prey. He also dismisses the popular "too cheap to shoot down" cost-exchange argument as dated: APKWS laser-guided rockets, attack-helicopter guns, point-defense anti-aircraft artillery, and Ukrainian interceptor drones all cost less than the attacker. Yet interception rates top out around 90% and are often much worse. The real difficulties are structural:

1. **Waves demand peak capacity.** A barrage is a burst-load problem, not an average-load one. Defense sized for steady state saturates.
2. **Routing avoids known defenses.** Flight paths and altitudes are planned around the defender's fixed assets.
3. **Cheap interceptors are short-ranged or immobile.** They cannot be tasked to every inbound track.
4. **Many targets are close to the launch point.** Long range does not mean long warning; the engagement window is often short.
5. **Targets carry their own fuel.** Refineries, flammable warehouse roofs, and ship engine rooms turn a 30 kg warhead into a total loss.

The two defensive thrusts follow directly: defenses must be mobile and numerous to meet waves, and critical targets must not offer a catastrophic outcome to a small warhead.

## The coverage-geometry problem

The existing air-defense paradigm was designed against expensive threats. Exoatmospheric interceptors cover whole regions from a few acres; lower-tier batteries reach hundreds of kilometers; fighters have 500–1,000 km combat radii plus missile reach; radars see hundreds of kilometers out. Vernon calls it "absurdly efficient, as long as the enemy targets remain expensive." He notes the paradigm was already fraying against accurate short- and medium-range ballistic missiles in the hands of middling powers.

The reason planners chose it is area coverage. Coverage scales with the square of effective radius, so replacing one 400 km asset with 10 km assets takes (400/10)² = 1,600 units. That is the load-bearing number in the essay: a cheap-interceptor paradigm needs roughly three orders of magnitude more units, and therefore the binding constraint is not unit cost but logistics footprint per unit. Every requirement in Vernon's gun-fighter design (VTOL, fuel-sipping cruise, disposability, no airfield, no maintenance) is a consequence of that arithmetic, not a nice-to-have.

## The VTOL drone gun fighter

Vernon's central proposal is a guns-only, vertical-takeoff drone fighter, explicitly modeled on John Boyd's Energy-Maneuverability theory and the original F-16 concept as told in Robert Coram's *Boyd*. Boyd wanted a lightweight, extremely agile dogfighter with less emphasis on top speed, payload, or sensors, and fought every added kilogram because weight snowballs: more mass needs more structure, which needs more thrust, which needs more fuel. Vernon's framing is that a pilotless drone can be a purer version of Boyd's aircraft than the Pentagon ever allowed the F-16 to be.

**Requirements:** extreme agility, high thrust-to-weight, low cost, minimal logistics footprint, long endurance, a gun and only a gun, VTOL. Vernon argues missile platforms (F-22, F-35, F-15) and gun fighters have conflicting requirements, so a cheap gun fighter complements the missile fleet without competing for its budget.

**Trade-off choices:** subsonic only (most gun fights are subsonic and supersonic capability taxes everything else); high thrust-to-weight anyway (turn recovery and VTOL); a camera-only automotive-grade vision stack; no radar stealth; sheet-metal structure over composites; disposable rather than repairable.

**Mass budget** (Vernon's estimates):

| Subsystem | Mass | Notes |
|---|---|---|
| Gun and ammo | 25–30 kg | Stripped .50 cal ~15 kg; 100–150 rounds at ~0.1 kg each. Multiple 5.56 mm guns also possible |
| Propulsion | 26–40 kg | Baseline two Kratos TDI-J85 turbojets (26 kg); ducted-fan, hybrid-electric, or adaptive-engine variants under 40 kg |
| Structure | ~50 kg | Laser-cut, laser-welded sheet metal including control surfaces and fuel lines |
| Sensors and comms | ~6 kg | Automotive cameras and compute (~5 kg, a few hundred watts) plus Link-16, Anduril Lattice, or StarShield |
| Hardware total | 107–120 kg | |
| Fuel | 30–43 kg | Fills the remainder of a ~150 kg airframe |

**Propulsion tiers.** A ducted-fan or hybrid-electric version (small battery for takeoff and landing, fuel engine for base load) tops out at 200–300 mph. Vernon argues that is enough: anything faster with real range and payload is expensive enough to justify a conventional fighter and an AIM-9. A twin-turbojet version reaches true fighter performance but loiters only a few hours because turbojets throttle down inefficiently. An adaptive engine with an electric compressor (the Astro Mechanica concept) would be "almost perfect": efficient cruise as low as 1 kg/hr, high-subsonic sprint, and VTOL from one powerplant.

**Sensors.** Vernon's bet is Tesla-style unfiltered cameras feeding an end-to-end neural net. Unfiltered CMOS sensors see near infrared, giving cheap night capability; stereo pairs estimate range; the same computer flies the aircraft and runs tactics. He asserts drone autonomy is "an order of magnitude or two easier" than self-driving cars. The drone gets its wider picture from a sensor net (scout drones, radars, human supervisors), which Vernon treats as another weight-saving measure.

**Sustainment.** Never repair. Vernon cites the WWII Pacific practice of pushing lightly damaged aircraft off carrier decks when new ones were arriving faster than repairs could be done, and argues the same logic holds when there might be 1,000 drones per F-35. Fuel and ammunition reload are the only ground operations. Early on, drones would be teleoperated to generate training data, keeping the human-pilot peak in the thousands rather than the hundreds of thousands global coverage would otherwise demand.

**Cost.** Under $100,000 marginal cost for the fan version, a few hundred thousand for the adaptive-engine version. Vernon's sanity check: even at F-35 cost per kilogram the airframe would come in under $400,000.

**Tactics.** Hundreds or thousands patrol coastlines, borders, and naval formations as a "wall of coverage" against drones and cruise missiles. Later they act as skirmishers alongside crewed fighters, constraining enemy formations during missile exchanges. Vernon's line: an F-35 pilot would rather have hundreds of subsonic gun fighters than two subsonic Collaborative Combat Aircraft missile carriers.

### Manufacturing and design evolution

Tooling and factory costs can be half an aircraft program's development cost. Vernon argues laser-cut sheet metal, laser welding, and 3D-printed tooling collapse that, and that a pilotless, cheap airframe does not need to be right the first time. The consequence is a different evolution model: rather than a fixed airframe with incremental modifications, redesign the whole aircraft around each new requirement (a stealthier variant, a different gun, APKWS rockets). He points to Ukraine, where dozens of drone models coexist and turn over continuously. End-to-end neural nets eliminate most low-level flight code, and LLM-assisted CAD shortens conceptual and detailed design.

## Ballistic missiles

Vernon treats ballistic missiles as a known problem with expensive answers. Long-range missiles cost orders of magnitude more than long-range drones, so the cost-exchange pressure is gentler. Endoatmospheric interceptors like PAC-3 are already about a quarter the cost of exoatmospheric SM-3 and THAAD, and the limit case is a cheap battery sitting at the aim point taking the easy head-on shot in the last few thousand meters. For launcher hunting, long-loiter Reapers performed well over Iran but are too expensive and too few relative to losses; Vernon wants a Ukraine-style loitering hunter at roughly 1/100th the cost, built by a company other than General Atomics.

## Hardening targets

The principle is "don't allow easy wins."

- **Ships.** Small drones rarely sink large vessels but easily achieve mission kills on the bridge and engine room, with insurance costs as a knock-on. Vernon wants those critical nodes armored (his naval-shipbuilding post covers cheap, repairable options) and expects ships to get smaller under air threat so each loss matters less. Small specialized vessels would run the Strait of Hormuz and transfer cargo to ordinary ships or nearby ports outside the danger zone.
- **Warehouses and factories.** Too large to be meaningfully damaged by one drone, unless a flammable roof lets one hit burn down a million square feet. Roof fire ratings become a defense measure.
- **Refineries.** The hardest target. They need more air defense, spare equipment, and standing repair crews. The most vulnerable and slowest-to-repair units are the conversion units that turn heavy fractions into gasoline and diesel, which is why Vernon calls electrifying ground transport "a strong substitute" for refinery defense. He notes it already takes monthly or faster strikes to dent Russian refinery output, and that simpler teapot refineries might need weekly hits.
- **Military bases.** "Disperse and dig." Bury what is near the front or too expensive to lose (bombers); spread everything else too thin to target.

## Implications for US power projection

Vernon's closing argument is that the US military is optimized for a narrow mission: two armies facing off. Enemies who hide, dig in, or simply do not care were previously ignorable. Cheap precision changes that, because lesser powers can now take pot shots at economically important targets. That collides with the US model of ultra-powerful formations concentrated in a few large bases, which become liabilities once precision is cheap. He also argues the offensive orientation the US has held since the 1940s has frayed: low domestic appetite for war, most of the world already aligned with the US bloc, nearly all outliers nuclear-armed, and those outliers able to disperse and dig themselves.

His prescription is low-end, long-loiter air and sea power to complement the high-end offensive force: loitering hunters that wait for launchers to emerge, gun-fighter drones and patrol boats against drones and small surface combatants, all with footprints small enough to harden and disperse. "Large bases anywhere close to hostile actors are now obsolete in their current form." Richer, more capable allies should operate much of this with minimal US advisory presence. Vernon expects the Gulf states to find the transition unpleasant and expects constant iteration for decades, "similar to the early 20th century."

He is optimistic about the US because the constraint is not manufacturing. A month of combined Russian and Ukrainian FPV production (about a million units, a few hundred tons) fits in a few dozen semi-trucks, and a 30% US cost premium over Asia does not matter at that scale. The hard parts are intelligence, systems integration, and control of low Earth orbit: putting useful autonomy into a 1 kg or 100 kg airframe at an acceptable price, since remote piloting every drone is the current bottleneck. Terminal Autonomy's Hornet is his example of the US staying on that frontier. The essay ends: "The American umbrella is dead, long live the American umbrella!"

## Synthesis

- **The square law is the whole argument.** Vernon's essay reads as an aircraft-design post, but the decisive claim is the (R₁/R₂)² coverage relation. Once the threat is cheap, the defender's cost function shifts from interceptor price to per-unit logistics, and every design choice follows from minimizing that. The same reasoning explains why point defenses and interceptor drones, though cheap per shot, have not solved the problem on their own: they are cheap but not mobile or numerous enough.
- **A Boyd-style weight diet is a delete-the-part philosophy.** The design method is the same one catalogued in [[elon-operating-philosophy]]: strip requirements until the remaining ones are load-bearing, and accept that a kilogram of payload costs several kilograms of aircraft. The gun-only constraint is doing the same work as Boyd's refusal of the pilot ladder.
- **Disposability as a logistics decision, not a values one.** Vernon's "never repair" rule is a direct counterpoint to the repair ethic in [[maintenance]]. The resolution is fleet ratio: when the unit is cheap and the fleet is a thousand per crewed fighter, the maintenance organization itself becomes the expensive, targetable asset. Brand's argument still applies to the sensor net, bases, and manufacturing base that the drones depend on.
- **The vision-only bet is the least argued part.** Vernon asserts camera-only autonomy is one to two orders of magnitude easier than driving. The airspace is emptier than a street, but [[waymo-autonomous-driving]] shows the fusion camp's case rests on fog, glare, and darkness, all of which a coastal patrol drone will meet. Stereo cameras at a few hundred watts against a 200 mph target with a 100-round magazine is a tight engagement problem the essay does not work through.
- **Numbers to treat as sketches.** A 50 kg sheet-metal structure rated for 9g+ turns, 100–150 rounds (a few seconds of fire), and unitemized battery mass in the hybrid variant are back-of-envelope. Vernon says as much. The design's contribution is the requirement set and the cost target, not the specific mass budget.
- **Grand-strategy reading.** Cheap long-range drones erode the moat that makes maritime powers secure in [[continental-vs-maritime-powers]]: the sea lanes and chokepoints (Hormuz, Red Sea) that a navy once protected can now be contested from land by a middling power for the price of a few semi-trucks of drones. Vernon's "distributed umbrella" operated by allies is a redesign of the freedom-of-navigation public good discussed in [[liberal-international-order]]. And Paine's warning in [[why-russia-lost-the-cold-war]] against symmetric strategies applies in reverse: answering $100,000 drones with million-dollar interceptors is the symmetric trap, and the gun fighter is the asymmetric answer.
- **Where this sits in time.** Written in September 2026 against the backdrop of the Russia–Ukraine drone war, Ukrainian deep strikes on Russian refineries, and the 2025–26 Iran conflict (Reapers hunting launchers, Hormuz shipping risk). Vernon flags a forthcoming series and a 2026 Progress Conference talk on drone form factors; those are the natural next sources to integrate here.

## Sources

- Vernon, A. (2026). "Defending Against Massed Drone Attacks." <https://www.austinvernon.site/blog/gunfighter.html> — [[2026-09-15-vernon-massed-drone-attacks|local copy]]
