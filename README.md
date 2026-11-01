# The Verdant Shell

An incremental healing game about coaxing an Ancient Turtle out of mud and thorns and into a full verdant bloom.

## Stack

- **React 19** + **TypeScript** (strict)
- **Vite 8** for the dev server and production build
- **Tailwind CSS v4** (via `@tailwindcss/vite`) with a stage-driven atmosphere theme
- **lucide-react** for iconography
- Hand-authored inline SVG artwork — no external art assets

## Getting started

```bash
npm install
npm run dev       # http://localhost:5173
npm run build     # typecheck (tsc -b) + production build
npm run preview   # preview the production build
npm run typecheck # TypeScript only
```

## Gameplay

- **Follow the Warden's quest.** A fresh run (or "Begin anew") opens with a
  three-beat MMORPG-style quest banner at the bottom of the screen. The Warden
  explains the wounded turtle, points the player at the shell with a pulsing
  spotlight, then opens the shop dock and asks for restoration allies. Advance
  with **Next** (or Space / Enter), or skip the quest entirely; the banner stays
  clear of the stage so the turtle can be healed while it is being read.
- **Touch the shell** to restore vitality and earn essence. Every touch spawns a
  floating healing number, a shockwave ring and a burst of leaves and spores.
- **Recruit allies** to heal passively. Passive healing also trickles essence at
  25% of the healing rate, so the loop keeps running while you idle. Allies
  appear in the **Shop** overlay.
- **Each ally is a hand-drawn character that lives where its magic makes
  sense.** The Dewdrop Sprout and the Ancient Root stand rooted at the turtle's
  flanks, twice their old size, lifting healing beams and ground ripples out of
  the soil. The Moss Beetle paces back and forth across the shell plates,
  leaving a trail of green spores. Only the Mist Wisp and the Bloom Moth fly,
  drifting through gentle orbits above the shell, trailing fog and scattering
  pollen on every wing beat.
- **Deepen Verdant Focus** in the **Spells** overlay to strengthen each touch.
- **Restore the turtle** through four chapters, driven by vitality percentage:

  | Stage | Chapter             | Threshold |
  | ----- | ------------------- | --------- |
  | 1     | Mud & Thorns        | 0%        |
  | 2     | Moss & Roots        | 25%       |
  | 3     | Emerald Canopy      | 50%       |
  | 4     | Full Verdant Bloom  | 80%       |

  The palette, ambient glow, stage badge, shell artwork and vitality bar all
  change with the current stage, and a bloom flash washes the canvas whenever a
  new chapter begins. The backdrop itself is continuous: a cold, drained forest
  twilight in **Stage 1** warms into dawn, brightens into emerald daylight and
  finally opens into a sunlit clearing with crystal glints, while the HUD, shop,
  spellbook and quest banner move from weathered vellum with dark wood grain to
  bright, golden-trimmed forest glass. In **Stage 1** the turtle is visibly
  dying: its eyes are heavy-lidded, its mouth pulls into a weary frown, deep
  fissures branch across the scutes, mud cakes the seams and flippers, and dark
  thorny vines cinch its shell and limbs while a cold vignette presses in from
  the edges. Every one of those marks recedes as vitality returns, so the first
  green shoots land as a genuine rescue.

The interface is a fullscreen game canvas: a slim HUD with Essence, Vitality and
HPS, plus Shop, Spells and Settings triggers that open compact overlays. Ambient
leaves and spores drift upward across the scene, and passive healing adds rising
green mist around the shell.

### Corruption waves (Ascension 1+)

- **Unlocked at Prestige 1 and ~2 % vitality.** Once the reborn shell has healed
  past 2 % of its cap, corruption starts testing it.
- **Warning, then a march.** A pulsing banner with an alarm ring and triangle
  indicator gives five seconds of warning, then shadow beasts and blight
  parasites climb out of the treeline at staggered intervals and crawl toward
  the shell. A corner chip counts down to the next wave, and a live counter
  tracks the beasts felled in the current one.
- **Strike before they reach the shell.** Click or tap each beast: parasites
  fall in one hit, shadow beasts take two. Every beast that reaches the shell
  drains 1 % of max vitality (capped at 12 % of current life, never below one
  spark) and briefly stains the canvas with corruption.
- **Clearing pays a burst.** Each felled beast is worth 45 seconds of passive
  essence plus twelve touches (floor of 150 essence), and a flawless wave
  doubles that subtotal. Grasp of Abundance adds another +50 %, and Essence
  Bloom multiplies the payout as it does every essence source.
- **Aegis of the Canopy** (grove tier 3) auto-strikes each beast 0.9 s after it
  appears, so idle healing is never interrupted. Lifetime waves repelled and
  corruption slain are tracked in Settings.

### Ascension (prestige) and the legacy tree

- **Victory at full bloom.** Reaching 100% vitality in Stage 4 opens the victory
  prompt and rewards 1 legendary **Essence of Primal Nature** (*Essenz der
  Urnatur*). "Ascend" performs the prestige; "Not yet" dismisses the prompt for
  the rest of the run, and the glowing **Ascend** trigger in the HUD brings it
  back.
- **Every Ascension multiplies the requirement by five.** Prestige 0 needs
  100,000 HP, Prestige 1 needs 500,000, Prestige 2 needs 2,500,000, and so on.
  Because chapter thresholds are percentages of max vitality, Stages 1-4 all
  scale together.
- **A hard run reset, a permanent legacy.** Ascending clears vitality, essence,
  allies, Verdant Focus and the spell cooldown, then starts the next run at 1
  vitality under the new cap. Ascension level, awakened perks and the lifetime
  Essence of Primal Nature ledger are kept (and validated back out of the save).
- **Four mutually exclusive tiers.** The **Legacy** trigger opens the skill
  tree. Each Ascension tier forks into *Path of the Warden* and *Path of the
  Grove*. Choosing one node awakens its effect permanently and seals the sibling
  node forever.

  | Tier | Warden branch                            | Grove branch                              |
  | ---- | ---------------------------------------- | ----------------------------------------- |
  | 1    | Touch of the Warden · +100% click        | Verdant Harmony · +50% ally HPS           |
  | 2    | Storm Surge · −30% spell cooldown        | Essence Bloom · +25% all essence          |
  | 3    | Grasp of Abundance · +50% wave pay       | Aegis of the Canopy · auto-defend         |
  | 4    | Golden Touch · +100% manual click essence | Automatic Pulse · 5 automatic touches/s  |

- **Golden Touch** (warden tier 4) doubles the essence of every deliberate press
  of the shell. **Automatic Pulse** (grove tier 4) instead performs five whole
  touches per second on its own: each beat heals for the full click power,
  grants click essence, increments the touch count, and plays the same floating
  number, ring and leaf burst as a manual touch. The two nodes share one tier,
  so the legacy can only ever hold one of them.

### Titan forms

The Ascension level decides the base Titan form; from Prestige 9 the run also
stores which stance is worn and which stances have been attuned.

| Prestige | Titan                      | Signature                                                             |
| -------- | -------------------------- | --------------------------------------------------------------------- |
| 0        | Verdant Moss Ancient       | +35% healing; baseline touch and Essence                              |
| 1        | Prismatic Crystal Titan    | +10% healing, +25% touch, +20% Essence, prism aura                    |
| 2        | Volcanic Obsidian Behemoth | −5% healing, +45% touch, +15% Essence, magma aura                     |
| 3        | Cosmic Astral Titan        | +15% healing, +50% touch, +35% Essence; Supernova (5% max, 30s)       |
| 4        | Temporal Chrono Titan      | +20% healing, +35% touch, +25% Essence; Shift + Rewind                |
| 5        | Tidal Leviathan            | +15% healing, +10% touch, +45% Essence; sluice valves and coral beds  |
| 6        | Mycelium Titan             | +28% healing, +15% touch, +20% Essence; spore network and chains      |
| 7        | Storm Tempest Titan        | +20% healing, +40% touch, +25% Essence; charge and energy conductors  |
| 8        | Sandsmith Titan            | +18% healing, +18% touch, +55% Essence; sand drifts and relic blessings |
| 9+       | Paragon Nexus Titan        | Shift between all nine earlier stances mid-run                        |

- **Astral constellation.** Five stars sit over the shell while the Astral Titan
  is worn. Link all five inside the 6 s chain window to detonate a Supernova.
  The Spells dock shows the cooldown and can also fire it directly.
- **Chrono-Shift and Time Rewind.** Chrono-Shift accelerates passive healing,
  passive Essence and automatic pulses by 3× for 12 s. While the Chrono Titan is
  worn, every breach banks its lost vitality; Time Rewind spends the bank to
  restore it immediately, on a 45 s cooldown.
- **Prism refraction.** Four rings of prisms sit on the shell; the sunlight beam
  must leave each aligned prism before the chain fires a laser surge.
- **Core Heat.** The Obsidian Behemoth's crater runs through snuffed, cold, glut,
  hot and overheat states. Touches stoke it, and the Glut Zone triples ally
  damage in wave combat.
- **Sluice valves and coral beds.** The Leviathan's four valves spill water into
  the coral beds beneath them; balancing pressure keeps the whole reef fed.
- **Spore network.** Plant spores in the mycelial nodes, let them mature, then
  link three mature mushrooms to detonate a chain reaction that enlarges the web.
- **Storm charge.** Static gathers on the Tempest shell every second and faster
  with each touch. Discharge the reservoir into one of three energy conductors
  for a burst heal of up to 30% of max vitality; the conductor then cools for
  10 s, and below 20% charge a strike only fizzles.
- **Sand drifts.** Six drifts bury relics on the Sandsmith shell. Brush a drift
  clear to uncover its relic and start a 22 s blessing: Oasis (+30% healing),
  Sunstone (+50% Essence) or Mirage (+120% touch). The wind slowly rebuilds the
  sand and buries the relic again.
- **Paragon stances.** From Prestige 9 the Nexus can swap to any earlier form
  every 8 s. Each distinct form attuned during the run adds +5% healing, touch
  and Essence (max +45%), and the active stance supplies its own aura, allies,
  economy modifiers and signature power. Ascending resets the stance ledger.

- **Verdant Cascade** is the active spell in the Spells dock: it restores 12% of
  max vitality on a 90 s cooldown (63 s with Storm Surge). Cooldowns keep ticking
  while idle, and the card shows a live progress bar.

Progress autosaves to `localStorage` every five seconds and on page hide. On
return, up to 24 hours of passive healing and Essence are presented in "The
Verdant Shell" offline popup and credited the moment you press **Collect &
Continue**. "Begin anew" clears the save, including the Ascension legacy;
Ascending is the way to reset a run while keeping your tree.

## Architecture

```
src/
├─ types/game.ts              # Domain types only (state, actions, config shapes)
├─ config/gameConfig.ts       # Balance knobs, stage palettes, helpers, formulas
├─ config/atmosphere.ts       # Stage atmosphere palettes, blending, CSS variables
├─ context/GameContext.tsx    # Reducer, 100 ms game loop, autosave, useGame()
├─ lib/format.ts              # Compact number / rate / duration formatting
├─ lib/storage.ts             # Versioned, validated localStorage persistence
├─ components/
│  ├─ Hud.tsx                 # Slim stat HUD + panel triggers
│  ├─ TurtleView.tsx          # Fullscreen stage, click FX, passive mist, vitality
│  ├─ EnemyWaveOverlay.tsx    # Corruption waves, marching beasts, strikes, payouts
│  ├─ TurtleArt.tsx           # Stage-reactive inline SVG turtle
│  ├─ AllyOrbit.tsx           # Ally orbits, tethers and per-species heal FX
│  ├─ AllySprite.tsx          # Hand-drawn SVG character for every ally
│  ├─ VitalityBar.tsx         # Slim vitality bar with chapter notches
│  ├─ StageBadge.tsx          # Chapter pill + shared stage icon map
│  ├─ NatureParticles.tsx     # Ambient drifting leaves, spores and mist
│  ├─ Atmosphere.tsx          # Stage-driven sky, sunlight, haze and glints
│  ├─ GameModal.tsx           # Accessible overlay shell (Escape, focus, scroll lock)
│  ├─ ShopPanel.tsx           # Compact ally cards
│  ├─ SpellsPanel.tsx         # Verdant Cascade + Verdant Focus cards
│  ├─ SkillTreeModal.tsx      # Four-tier branching legacy tree, perk locking
│  ├─ PrestigeModal.tsx       # Victory prompt, legendary reward, Ascend
│  ├─ SettingsPanel.tsx       # Run statistics and reset
│  └─ TutorialModal.tsx       # Onboarding quest banner (portrait + steps)
├─ App.tsx                    # Fullscreen game shell with overlay routing
├─ index.css                  # Tailwind theme, keyframes, base styles
└─ main.tsx                   # React root with <GameProvider>
```

### State flow

All gameplay rules live in `gameReducer`:

- `tick` — applies `healingPerSecond × dt` and `essencePerSecond × dt`, and
  counts the active spell cooldown down
- `heal` — applies click power, grants essence, records stats
- `castSpell` — when off cooldown, restores 12 % of max vitality and starts the
  cooldown (90 s, or 63 s with Storm Surge)
- `buyHelper` / `upgradeFocus` — validated against current essence
- `selectPerk` — awakens one legacy node if its Ascension tier is reached and
  undecided; the sibling node stays sealed forever
- `prestige` — only legal after victory: increments the Ascension level, awards
  one Essence of Primal Nature, applies the ×5 vitality cap and clears the run
- `waveDamage` — a shadow beast reached the shell: drains the capped breach
  slice, never dropping the turtle below its last spark
- `waveReward` — pays a finished wave's essence burst from the live economy and
  perks, and records repelled waves / corruption slain
- `advanceTutorial` / `skipTutorial` — walk the onboarding quest (1 → 2 → 3 →
  0) or dismiss it; `0` marks it finished
- `reset` — returns a fresh run (including the legacy), which restarts the quest
  at step 1

The quest step lives in `GameState`, so a first-time player is onboarded
automatically, a returning save (written before the quest existed) is treated as
finished, and "Begin anew" brings the tutorial back.

`withDerivedState` is the single source of truth for HPS, passive essence, stage
resolution and the full-vitality victory flag. It applies the perk multipliers
(Verdant Harmony, Essence Bloom) every time, so saved base numbers can never
drift from the balance rules.

`loadGame` re-derives the vitality cap from the Ascension level, drops unknown or
duplicate perk ids (one node per tier), and clamps the remaining spell cooldown,
so a tampered save cannot break the x5 scaling or hold both sides of a tier.

The loop reads real elapsed time from `performance.now()` and dispatches every
100 ms; a single delta is capped at 60 s so tab throttling cannot fast-forward
progress. Automatic Pulse accumulates fractional beats in `autoClickProgress`
and applies only whole touches, so exactly five pulses land per second at any
tick cadence and the remainder survives a save. Autosave and the game loop are
independent effects, and the reducer re-validates every purchase as a last line
of defence.

### Tuning

Economy values (starting vitality, click power, essence conversion, focus costs,
offline cap, prestige multiplier) are in `GAME_CONFIG`. Helpers and stage
palettes/thresholds are in `HELPERS` and `STAGES` in the same file. Prestige
balance lives in `PERK_EFFECTS`, `ACTIVE_SPELL`, `PRESTIGE_BRANCHES` and
`PRESTIGE_PERKS`; `getPrestigeMaxVitality` is the only place the ×5 cap is
computed. Wave timing, damage, wave sizes and payout maths live in
`WAVE_CONFIG`, `areWavesUnlocked`, `getWaveBreachDamage` and
`getWaveEssenceReward`.

### Atmosphere

`getAtmosphere(vitalityFraction)` blends four atmospheric anchors plus a final
full-bloom palette, easing across each chapter so the scene changes continuously
rather than snapping at 25 %, 50 % and 80 %. `atmosphereCssVariables` turns that
blend into:

- `--world-*` variables for the sky, sunlight, canopy gap, moss glow,
  undergrowth, hearth light, haze, vignette, sun shafts, sparkle opacity and
  ambient particle tints, consumed by `Atmosphere.tsx` and `index.css`; and
- stage-specific overrides for the Tailwind design tokens
  (`--color-parchment-*`, `--color-bark-*`, `--color-amber-*`,
  `--color-canopy-*`, `--color-emerald-*`, `--color-teal-*`) plus `--panel-*`
  variables for grain, blur, inner glow and drop shadow.

Because every panel already paints with those tokens, the HUD, shop dock, spells,
settings modal and quest banner re-theme automatically. Retuning a chapter's look
means editing its palette in `src/config/atmosphere.ts`; no component changes are
required.#   t i t a n s h e l l s  
 