# PokéStat Matcher

A browser-based tool that finds the closest Pokémon to any set of base stats using Euclidean distance similarity matching. Built as part of a larger project reverse-engineering the methodology behind a viral NBA × Pokémon stat comparison series.

---

## What it does

Enter any combination of the six Pokémon base stats (HP, Attack, Defense, Sp. Atk, Sp. Def, Speed) and the tool returns the five closest matching Pokémon from a database of 1,092 unique stat spreads, ranked by similarity percentage.

Results show each match's full stat profile, the difference from your input on every stat, and a similarity score calculated from Euclidean distance across all six dimensions.

---

## Background

This tool was built as the front-end component of a larger data project that mapped real NBA player performance statistics onto the Pokémon base stat framework — assigning each player an HP, Attack, Defense, Sp. Atk, Sp. Def, and Speed based on their 2025–26 season box score data.

The matcher was needed to identify the most statistically similar Pokémon to each generated player spread, which became the signature element of the dataset. It grew into a standalone tool usable for any input.

---

## Features

- **Instant matching** — all 1,092 Pokémon spreads embedded directly in the file; no server, no API calls, no loading time after the first open
- **Dual input** — sliders for quick adjustment, number fields for precise entry; both stay in sync
- **Live BST** — Base Stat Total updates in real time as you adjust stats
- **Similarity scoring** — percentage based on normalised Euclidean distance, accounting for the practical stat range across the full database rather than an arbitrary scale
- **Visual diff** — each result card shows exactly how the Pokémon's stats compare to your input, highlighted per stat
- **Fully offline** — works by opening the HTML file locally; no hosting required

---

## How similarity is calculated

Distance between the input spread and each Pokémon is measured as standard Euclidean distance across all six stats. This is converted to a percentage using:

```
similarity = 100 × (1 − distance / k)
```

where `k = √6 × span`, and `span` is the 2nd–98th percentile stat range across the database. This anchors the scale to the real distribution of Pokémon stats rather than a hand-picked constant, so scores are meaningful and consistent regardless of BST tier.

---

## Dataset

- **1,092 unique stat spreads** drawn from the full Pokédex
- Includes base forms and regional variants (Alolan, Galarian, Hisuian, Paldean)
- Excludes Mega Evolutions, Gigantamax forms, and other temporary battle transformations
- Duplicate stat lines (forms sharing an identical spread) are collapsed to a single entry

---

## Tech

Single self-contained HTML file. No frameworks, no dependencies, no build step. Data pre-processed from PokéAPI's open dataset using Python and embedded at build time.

---

## Part of a larger project

The NBA × Pokémon stat mapping project involved:

- Designing a six-stat formula translating real basketball metrics (per-36 rates, usage percentage, true shooting, defensive rebounding, physical profile) into Pokémon-style base stats
- Running the model across all 30 NBA teams — 180 players — for the 2025–26 regular season
- Using this matcher to assign each player their closest Pokémon as a signature identifier

---

*Data sourced from Basketball-Reference and PokéAPI. Built for a personal analytics project.*
