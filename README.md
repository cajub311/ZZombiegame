# 🧟 ZZombiegame — *Patient Zero*

**You are the outbreak.** A top-down zombie survival game played from the *infector's* side: bite humans to turn them, build an autonomous horde that hunts on its own, and consume an entire city while an escalating, GTA-style military tries to put you down.

> Single self-contained HTML file. No build step, no dependencies, no assets — every sound is synthesized live in the browser. Works offline.

## ▶️ Play now

**[👉 Play in your browser](https://cajub311.github.io/ZZombiegame/)**

Or open **`index.html`** locally in any modern browser — that's it. Works on desktop and mobile.

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
- **Clear a level, then EVOLVE.** Each cleared city lets you draft one of three **mutations** (unlock new powers or stack passives like Sharper Fangs, Pack Hunger, Thick Hide, Viral Vigor). Every level the city grows and the military hits harder — it's endless.
- **Zombie strains.** Victims rise as **shamblers** (slow), **walkers**, **runners** (fast — they catch fleers), **brutes** (tanky), or **bloaters** (burst into an infection cloud when shot, so enemy gunfire backfires).
- **GTA wanted system.** More infection = higher heat (CALM → ALERTED → POLICE → MILITARY → MARTIAL LAW). Lie low and it cools. At max heat, **hunter-killer teams** track *you* specifically, **telegraphed airstrikes** rain down, and the army rolls in as **assault waves** — walls of soldiers that advance and shove your horde back.
- **Bosses every 5th level.** A hulking **Behemoth** with a telegraphed shockwave stomp and cannon fire, getting stronger each tier. Boss levels have only a few civilians to rebuild your horde from — you'll need your skills to bring it down.
- **The public stays calm** until ~10% of the city is infected, giving you room to build a starter horde before panic spreads.

## 🛠️ Tech

A single `index.html`: vanilla JavaScript + Canvas 2D for rendering and the Web Audio API for all sound. No libraries.

Built and balanced with the help of an automated playtest bot that ran several hundred simulated games to tune the difficulty curve.

---

*Made for fun. Infect responsibly.* 🧟‍♂️
