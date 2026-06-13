# 🧟 ZZombiegame — *Patient Zero*

**You are the outbreak.** A top-down zombie survival game played from the *infector's* side: bite humans to turn them, build an autonomous horde that hunts on its own, and consume an entire city while an escalating, GTA-style military tries to put you down.

> Single self-contained HTML file. No build step, no dependencies, no assets — every sound is synthesized live in the browser. Works offline.

## ▶️ Play now

**[👉 Play in your browser](https://cajub311.github.io/ZZombiegame/)**

Or open **`index.html`** locally in any modern browser — that's it. Works on desktop and mobile.

## 📱 Install on Android (as an app)

This is an installable **PWA** — it adds to your home screen as a real full-screen, offline app:

1. Open **https://cajub311.github.io/ZZombiegame/** in **Chrome** on your phone.
2. Tap the **⋮ menu → "Install app"** (or "Add to Home screen").
3. Launch it from your home screen — own icon, full-screen, plays offline.

Controls on phone: **left half of the screen = move, right half = aim & bite.**

## 🎮 Controls

| Input | Action |
|---|---|
| **WASD / Arrows** | Move |
| **Mouse** | Aim your lunge |
| **Space / Click** | **Bite** — lunge forward and infect/maul what's in front |
| **Q E R F** | Earned mutations (Spit, Pandemic, Frenzy, Regenerate) |
| **M** | Mute / unmute sound |

## 🦠 How it works

- **Bite to infect.** Turned humans join your horde and autonomously hunt the rest of the city — you're steering a chain reaction, not racking up kills.
- **Clear a level, then EVOLVE.** Early cities still advance on outbreak momentum, but the streets are more crowded and responders arrive earlier. From level 5 onward, shelter defenses and assault pressure start pushing back.
- **Choose upgrade or mutation.** Each cleared level offers a real fork: spend the reward on a permanent Speed, Health, Strength, or Horde Control bar, or skip the stat point and take one mutation card.
- **Named city districts.** Malls, hospitals, Civic Hall, police stations, and subway hubs now create local objectives: overrun them for bonuses, shut down decon pressure, drop heat, or stop civilians from escaping.
- **Five breakable shelters.** The mall, hospital, Civic Hall, police station, and subway are the only buildings. Their inner circles are blocked to the horde until breached, while panicked civilians can enter and smarter humans barricade them stronger over time.
- **Solid city blocks.** Patient Zero and the horde have to move around buildings; only civilians can duck inside shelters.
- **Responder guards.** Once the later cities heat up, soldiers deploy around shelters and try to hold the horde off long enough for civilians to survive or escape.
- **Mutation evolutions.** Certain draft combinations become named strain upgrades like **Feral Pack**, **Plague Bomb**, **Juggernaut Strain**, **Contamination Zone**, and **Alpha Bite**.
- **Smarter horde upgrades.** Draft powers like **Pack Mind**, **Siege Claws**, and **Jumper Strain** make the horde coordinate with your attacks, crack shelters faster, and leap into prey.
- **More mutation skills.** New draft picks like **Corrosive Bite**, **Bone Plating**, **Brood Seed**, and **Hunting Scream** open up harder-hitting, tougher, faster-starting, or better-commanded builds.
- **Zombie strains.** Victims rise as **shamblers** (slow), **walkers**, **runners** (fast — they catch fleers), **brutes** (tanky), or **bloaters** (burst into an infection cloud when shot, so enemy gunfire backfires).
- **GTA wanted system.** More infection = higher heat (CALM → ALERTED → POLICE → MILITARY → MARTIAL LAW). Lie low and it cools. Soldiers now show up earlier, while **hunter-killer teams**, **telegraphed airstrikes**, and **assault waves** escalate as the outbreak spreads.
- **Bosses every 5th level.** A hulking **Behemoth** with a telegraphed shockwave stomp and cannon fire, getting stronger each tier. The level 5 boss is still the first major test, but it is no longer a free pass.
- **The public stays calm** until ~10% of the city is infected, giving you room to build a starter horde before panic spreads.

## 🆕 Shareable Strain Codes (New)

After any run the end screen now shows a **YOUR STRAIN CODE** (compact base64 encoding of your mutations/powers + key stats).

- Click **COPY** to grab it.
- Load the exact same build on any play by appending `?strain=THECODE` (or `#THECODE`) to the URL before starting.
- The game auto-applies the powers using the existing mutation system (non-breaking, reuses your POWERUPS/ABILITIES/applyPower logic).

Perfect for sharing killer builds with friends, competing on identical strains, saving favorites, or experimenting. Inspired by Plague Inc gene codes and roguelite share culture.

## 🛠️ Tech

A single `index.html`: vanilla JavaScript + Canvas 2D for rendering and the Web Audio API for all sound. No libraries.

Built and balanced with the help of an automated playtest bot that ran several hundred simulated games to tune the difficulty curve.

---

**Recent improvements** draw from deep analysis of Plague Inc (evolution trees, Patient Zero origin, cure pressure, DNA economy, asymmetry across pathogen types, 700M+ plays from tension + replay via genes/scenarios/dailies), infection tag & multiplayer Patient Zero experiences (asymmetric lobbies, proximity spread, social deduction, containment vs outbreak), and horde/survivor design (Vampire Survivors-style drafting/autonomy/juice + meta progression). See the session plan for the full categorized roadmap (gameplay, multiplayer, content, UX, tech, retention).

Prioritized next slices (per approved plan): mutation synergies, heat/lie-low expansions, more strains or city variety, meta/dailies, or multiplayer stubs. Tell the agent what to tackle next!

---

*Made for fun. Infect responsibly.* 🧟‍♂️
