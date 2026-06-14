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
- **Clear a level, then EVOLVE.** Early cities advance on outbreak momentum, while later districts demand shelter breaches, boss kills, and tighter horde control.
- **Draft one mutation.** Each cleared level offers four build options. Pick one card, or spend biomass to reroll. Boss rewards are where the strongest strain-defining powers appear.
- **Named city districts.** Malls, hospitals, Civic Hall, police stations, and subway hubs now create local objectives: overrun them for bonuses, shut down decon pressure, drop heat, or stop civilians from escaping.
- **Five breakable shelters.** The mall, hospital, Civic Hall, police station, and subway are the only buildings. Their inner circles are blocked to the horde until breached, while panicked civilians can enter and smarter humans barricade them stronger over time.
- **Solid city blocks.** Patient Zero and the horde have to move around buildings; only civilians can duck inside shelters.
- **Responder guards.** Once the later cities heat up, soldiers deploy around shelters and try to hold the horde off long enough for civilians to survive or escape.
- **Mutation evolutions.** Certain draft combinations become named strain upgrades like **Feral Pack**, **Plague Bomb**, **Juggernaut Strain**, **Contamination Zone**, and **Alpha Bite**.
- **Patient Zero builds.** Cards inspired by Fangs, Muscle, Adrenal, Carapace, Regeneration, Venom, Predatory Leap, and Viral Scream let the player zombie become faster, tougher, more lethal, or better at breaking defenses.
- **Horde builds.** Pack Mind, Swarm Speed, Thick Dead, Brood Seed, Siege Instinct, Special Strains, Death Drum, and Meat Wave push the army toward better target sharing, building pressure, special infected, and swarm surges.
- **Zombie strains.** Victims rise as **shamblers** (slow), **walkers**, **runners** (fast — they catch fleers), **brutes** (tanky), or **bloaters** (burst into an infection cloud when shot, so enemy gunfire backfires).
- **GTA wanted system.** More infection = higher heat (CALM → ALERTED → POLICE → MILITARY → MARTIAL LAW). Lie low and it cools. Soldiers now show up earlier, while **hunter-killer teams**, **telegraphed airstrikes**, and **assault waves** escalate as the outbreak spreads.
- **Incremental boss ladder.** Medium bosses appear on levels 5, 15, 25, 35, and 45; hard bosses appear on 10, 20, 30, 40, and 50. After level 50, the roster loops with higher tiers, more health, faster pressure, and stronger support.
- **Boss families.** Brute Captains, Hazmat Purifiers, Riot Wardens, Evac Commanders, and Rival Alphas teach different counters before the harder Behemoth, Blacksite Purifier, Fortress Core, Apex Hunter, and Omega Response checks.
- **Anti-stall pressure with recovery windows.** Scent trails, nearby starter prey, and bite assist keep early outbreaks from fizzing, while adaptive heat and shelter pressure keep later levels tense without making every boss a hard wall.
- **The public stays calm** until ~10% of the city is infected, giving you room to build a starter horde before panic spreads.

## 🛠️ Tech

A single `index.html`: vanilla JavaScript + Canvas 2D for rendering and the Web Audio API for all sound. No libraries. `sw.js` makes the GitHub Pages version installable and keeps the HTML fresh with a network-first cache path.

Built and balanced with the help of automated playtests, including repeated early-game samples and boss-path checks to tune the difficulty curve.

---

**Recent improvements** draw from infection strategy games, horde survival games, and repeated local playtests: clearer early prey, bigger readable buildings, breakable/rebuildable barriers, smarter shelter pressure, a smoother endless boss ladder, and more build-defining mutation choices.

Prioritized next slices: true shareable strain codes, deeper mutation synergies, more city layouts, daily challenge seeds, Android packaging, or multiplayer stubs.

---

*Made for fun. Infect responsibly.* 🧟‍♂️
