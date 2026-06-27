# Faction Wars — Design Notes & Roadmap

Living notes for **Faction Wars** (`index.html`), the State.io-style 4-faction conquest RTS.
This is a planning doc — **nothing here is implemented yet.** Numbers are starting points to tune.

Current state: 4 factions (Zombies / Werewolves / Humans / Vampires), one random map layout,
greedy single-base AI, passive faction modifiers only, variable send amount (25/50/75/100%),
guaranteed resolution (150s territory backstop). The old action game is archived at `classic.html`.

---

## 0. Top priorities (do these first)

1. **Smarter AI — the "swarm" / multi-base assault** (player explicitly asked).
2. **Active faction abilities** (an energy meter + 1 signature power per faction).
3. **Game feel pass** (screenshake, hit-stop, node squash, threat arrows).
4. **Real adjacency** (sends legal along the lines we already draw) — biggest *strategic* depth gain.
5. **Run meta-progression** (pick 1 of 3 upgrades between battles).

---

## 1. AI improvement — the SWARM (coordinated multi-base attacks)

**Problem:** `aiThink()` only ever sends from its single fullest base. So once the AI owns 5 bases,
it still pokes with one base at a time and can't crack a defended target — it should **combine all its
nearby bases and dogpile one spot**, exactly like the player can (multi-select → send), and like
Galcon / Phage Wars / State.io bots do.

**The idea (player's words):** "when it has taken over multiple areas it can use swarm — use multiple
bases at once, all 5 buildings, drag and shoot all those areas into one spot."

**How to build it:**
- In `aiThink(fid)`, after picking a target node, gather **all** my bases within striking range whose
  *combined* units would win: `sum(myBases.units * combat) > target.def * 1.15`.
- If a single base can't take it but the **coalition** can, fire a synchronized multi-base send
  (this is just calling `sendFrom(coalitionBases, target)` — the function already loops sources).
- Prefer a coalition when the target is a **fortress** (high units + homeDef) or the **leader's** base.
- Keep 1–2 reserve bases stocked for defense (don't empty the whole empire).
- Add a short "muster" delay so the waves arrive together (stagger sends by distance so streams land
  at the same time = an actual coordinated strike, not a trickle).

**Also for the AI:**
- **Defend**: if an enemy stream is inbound (`scan streams` where `s.node.owner===fid`), reinforce that
  base from a neighbor before it falls.
- **Personalities** (cheap, big flavor): weight the shared scorer per faction —
  Werewolf AI = aggressive/blitz, Human AI = turtle + counter-punch, Vampire AI = grab adjacency to
  drain, Zombie AI = relentless expansion. A few multipliers in the scoring block.
- **Difficulty curve**: scale coalition aggressiveness + reaction speed with `state.battle`.

---

## 2. Active ability system (the core missing layer)

Today factions differ only by passive stat tweaks. Give each an **active power** the player triggers
(and the AI can use too).

**Resource — "Energy" meter (0–100), fills faster the more you own:**
`regen = 4 + ownedBases * 1.3 per second`. A signature ability costs a **full 100**; a minor one **40**.
This reinforces snowball *and* comeback tension and gives the AI a natural pacing knob.
Store `state.energy` for the player and `ai[fid].energy` for each AI; timed buffs live on
`state.frenzy/shield/eclipse` so player + AI read the same fields (same pattern the global Blood Moon
already uses).

**Data-driven:** add an `ability` (and optional `minor`) object to each `FACTIONS` entry, with
`{ id, name, icon, cost, target }` where `target ∈ none | own | enemy | any`. One `castAbility()`
dispatcher (a `switch` on `id`) does the work.

**Hooks reuse what exists:**
- Timed buffs → a countdown read inside `cmult`/`smult`/`resolve` (like Blood Moon).
- Node effects (plague, wall) → a field on the node processed in the production loop (the vampire
  `drain` code is the template).
- Instant economy → one loop over owned bases.

**UI:** a bottom-right energy button (mirror the existing `#ratios` bar), vertical fill = charge,
greyed out until affordable. Targeted abilities: tap button → tap a node. Desktop hotkey = Space/Q.

---

## 3. Faction kits (upgrades) — passive + active per faction

Designed as a rough 4-way cycle: **Zombies → Humans → Werewolves → Vampires → Zombies.**
Each faction's active sits in a *different mechanical category* so they never feel samey.

### 🧟 Zombies — Attrition / Snowball  (beats Humans)
- **Passive:** `convert 0.55` (captures turn a share of the dead into your units). New: the horde can
  **overfill past cap** by ~15% from conversions (visible bloat).
- **Signature — OUTBREAK** (enemy target, 100): plant a plague — target loses **4 units/sec for 6s,
  ignoring homeDef**, and **50% of the drained respawn as a zombie stream** toward it. Hard counter to
  turtling Humans; chews stacks a frontal assault can't crack.
- **Minor — RISE** (own, 40): instantly raise +25% of a base's cap in fresh units.

### 🐺 Werewolves — Burst Timing  (beats Vampires)
- **Passive:** `speed 1.4`, `combat 1.3` (1.75 in Blood Moon). New: a capturing stream **keeps 35%
  momentum** as a chained mini-blitz.
- **Signature — HOWL / FRENZY** (none, 100): a personal 5s Blood Moon — `combat 1.75`, `speed 1.95`,
  even outside the global moon; **stacks** with the real moon for a terrifying window. Caps the vampire
  before their slow economy matures.
- **Minor — POUNCE** (enemy, 40): next send to that node travels 3× speed.

### 🛡️ Humans — Fortress / Production  (beats Werewolves)
- **Passive:** `prod 1.18`, `cap 1.25`, `homeDef 1.2`. New: **+15% production while no enemy stream is
  inbound** (peacetime industry).
- **Signature — MOBILIZE** (none, 100): instantly add **20% of each base's cap** to every base, and set
  **homeDef 1.7 for 4s**. Cast reactively when you see a raid inbound — the burst breaks on the wall.
- **Minor — RAMPART** (own, 40): one base gets homeDef 2.2 for 6s.

### 🦇 Vampires — Economic Denial / Long Night  (beats Zombies)
- **Passive:** `combat 1.1`, `lifesteal 0.22`, `drain 0.6` (siphon from adjacent enemy bases). New:
  drain range 250→280 and draw a faint tether line to drained bases.
- **Signature — ECLIPSE / ETERNAL NIGHT** (none, 100): for 6s **all enemy production is halved**, your
  **drain ×2.5**, **lifesteal → 0.45**; deep-purple screen wash. Starves the horde that out-grinds you.
- **Minor — SIPHON** (enemy, 40): instantly steal 35% of a target's units as a stream to your nearest base.

**Distinctness check:** DoT/conversion vs self-buff vs instant-economy/defense vs global enemy-debuff. ✅

### Future factions (add later — fill empty niches)
- **❄️ Frost / Lich — crowd control** (no faction does denial yet). *FREEZE*: a target base can't produce
  or send for 4s. Passive: immune to plague/eclipse debuffs but `speed 0.8`. **Add this one first** — CC
  is a brand-new verb and makes great rock-paper-scissors.
- **🦗 Swarm / Locusts — economic explosion.** Cheap, fast, weak (`prod 1.4`, `combat 0.85`). *BLOOM*:
  +250% production on one base for 5s, or *MIGRATION*: teleport a whole garrison across the map.

---

## 4. "Make it cooler" — ranked by impact-to-effort

1. **Juice: screenshake + hit-stop + node squash.** Short decaying shake on captures/casts; nodes
   squash-and-spring on capture and production ticks. ~25 lines, enormous feel upgrade. (We already have
   `burst`/`ring`; add a `state.fx.shake` read by `render`'s world transform.)
2. **Real adjacency (lane-gated sends).** We already compute & draw `links` (nearest-neighbor edges) but
   sends ignore them. Make sends legal only along links (or 1.5× slower off-link) → chokepoints,
   frontlines, positioning. Biggest *strategic* gain for the least code. (Auralux / Galcon / Risk DNA.)
3. **Run meta-progression (Slay-the-Spire boons).** After each battle win, pick **1 of 3** run-long
   upgrades: +12% production, abilities −20% cost, start with +1 base, longer Blood Moons, etc. Cheapest
   path to long-session retention. Store `state.boons`, apply as a multiplier layer.
4. **Map variety + mutators.** Add handcrafted/symmetric layouts (ring, cross, central fortress,
   two-continents-with-a-bridge) chosen by battle #, plus per-battle mutators: permanent Blood Moon, fog
   (enemy counts hidden until adjacent), a neutral **boss mega-node** (r≈50, 120 units) worth a bonus.
5. **Threat & readability cues.** Red pulsing ring / inbound-arrow on a base when an enemy stream targets
   it; a thin arc on every node showing fill-toward-cap; white pulse on each production tick.
6. **Dynamic audio.** Pitch send/capture sounds to a pentatonic scale so play coalesces into music;
   low drone during Blood Moon / Eclipse. (Auralux's signature.)
7. **Visible doom timer.** Surface the existing 150s escalation/backstop as a thin top bar that reddens
   near the end, so players *feel* the pressure to close out.
8. **Alt modes** (reuse the whole loop, branch `genMap` + win check): King of the Hill (hold a central
   node for global production), Last Stand (1 base vs 3, survive 90s), Speed Conquest (timed scoring).

---

## 5. Similar games studied — what to borrow

- **State.io** (the template): bases produce to a cap; drag from base(s) to send; outnumber to capture;
  conquer all to win. *Borrow:* the clean core (have it), multi-base drag-select dogpiles (→ AI swarm),
  level packs with rising AI counts.
- **Galcon / Galcon 2**: the original "send % of a planet's ships to another planet" RTS. *Borrow:*
  send-percentage (have it via 25/50/75/100), fast 2–5 min matches, simple but vicious bot AI that
  masses fleets — the multi-base swarm behaviour.
- **Phage Wars / Tentacle Wars**: cells connected by tubes; you can only attack connected cells.
  *Borrow:* **adjacency/lanes** (#2 above) — turns a positioning-free map into one with frontlines.
- **Auralux**: minimalist, meditative; the universe pulses to generative music; positioning > reflex.
  *Borrow:* musical/dynamic audio, calm-but-deep readability, symmetric map layouts.
- **Eufloria**: grow seedlings, colonize asteroids, organic snowball + a little base-building.
  *Borrow:* gentle progression feel; the idea of upgrading a base (bigger cap / faster prod) as a sink.
- **Risk / Dice Wars**: territory control with adjacency + reinforcement phases. *Borrow:* adjacency,
  "reinforce the border" AI behaviour, the tension of overextending.
- **Plague Inc**: evolve traits, race a global cure timer. *Borrow:* a **cure / doom timer** as a tension
  mechanic; faction "evolution" upgrade tree (ties into meta-progression and faction upgrades).
- **Tooth and Tail / Bad North**: tiny, readable, faction-flavored RTS with strong identity & juice.
  *Borrow:* readability + character on a small board, satisfying feedback, faction personality.
- **Slay the Spire / roguelites**: between-fight choices that compound over a run. *Borrow:* the
  1-of-3 boon meta-progression (#3) and per-run build identity.
- **agar.io / .io vibe**: instant-play, escalating dominance, "one more game" loop. *Borrow:* zero-friction
  start, short matches, snowball-with-comeback tension.

---

## 6. Open questions / decisions to make
- Active abilities: **energy meter** (scales with territory — recommended) vs simple cooldowns?
- Adjacency: hard lanes (Phage Wars) vs soft (off-link allowed but slower)? Soft is friendlier.
- Meta-progression: persistent across runs, or reset each run (roguelite)? Roguelite first.
- Map: keep procedural + add templates, or go full handcrafted level pack?
- Which 5th faction first? (Recommendation: **Frost/Lich** for the new CC verb.)
