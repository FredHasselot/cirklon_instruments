# Cyclone Analogic TT-303 Bass Bot

Documentation for controlling the Cyclone Analogic TT-303 Bass Bot with the Sequentix Cirklon.

## Overview

The TT-303 Bass Bot is a monophonic analog bass synthesizer — a faithful
recreation of the Roland TB-303, with VCO, low-pass filter (Cutoff, Resonance),
filter envelope (Env Mod, Decay) and Accent. Compared to a drum machine it is a
deliberately **simple** MIDI target: a single melodic voice on one channel, with
just two Control Changes and accent driven by note velocity.

This is why only **one P3 instrument file** is provided — there is no per-voice
split, no CK pattern and no FX channel to model.

### MIDI Configuration

- **Reference**: InstaDJ 2.0 MIDI Implementation Chart (The Bass Bot manual v2.0)
- **Channel**: 1-10, set on the machine in MIDI Mode (`[FUNC] + [UP]/[DOWN]`)
- **MIDI Port**: OUT 1 (default — adjust to your routing)
- **Mode**: Mode 4 (Omni Off, Mono) — monophonic
- **Notes received**: MIDI 12-43 (C 1 - G 3, Cirklon convention) — MIDI Mode only
- **Velocity**: `1-111` = normal note, `112-127` = **accent**
- **Aftertouch / Pitch Bend / Program Change**: not supported
- **SysEx**: pattern backup and firmware updates only
- **Clock / Start / Stop / Continue**: supported

> The TT-303 must be in **MIDI mode** (Mode switch) to receive note data.

## Cirklon Instrument File

| File | Inst Name | Channel | Pattern | Role |
|------|-----------|---------|---------|------|
| `TT-303.cki` | TT-303 | 1 | P3 | Bassline note + Slide + Sustain |

### Track Values (P3)

| Slot | Control | Description |
|------|---------|-------------|
| 1 | `quant%` | Cirklon quantize |
| 2 | `leng%`  | Cirklon note length |
| 3 | CC 65 — `Slide` | Portamento / Slide between notes |
| 4 | CC 64 — `Sustain` | Sustain pedal |

> **No CC for the panel knobs.** Tuning, Cutoff, Resonance, Env Mod, Decay and
> Accent are **not** MIDI-controllable on the TT-303 — the chart documents only
> CC 64 (Sustain) and CC 65 (Slide). These knobs are tweaked by hand on the unit.

---

## Playing & Accent

### Notes

Play the bassline as a normal melodic P3 track. The TT-303 receives MIDI notes
12-43 in MIDI Mode; a default note of **C 2** sits comfortably in that range.
The instrument is **monophonic** — one note at a time.

### Accent via Velocity

The TT-303 maps incoming velocity to its Accent behaviour:

| Velocity | Result |
|----------|--------|
| 1-111   | Normal note |
| 112-127 | **Accented** note (louder, filter envelope boosted) |

To accent a step in the Cirklon, set that step's velocity to **112 or higher**.

### Slide

Use **CC 65 (Slide)** to engage portamento between notes — the characteristic
303 glide. On the TT-303 itself slide is also a per-step (DUAS) modifier; over
MIDI it is exposed as CC 65.

---

## Using with Cirklon

1. **Load instrument**:
   - Copy `TT-303.cki` to your Cirklon SD card
   - `DISK → LOAD → INSTR`

2. **Assign to track**:
   - Create a track, assign instrument `TT-303`
   - Set the MIDI channel to match the TT-303's MIDI IN channel (1-10)

3. **TT-303 configuration**:
   - Set the Mode switch to **MIDI** mode (required to receive notes)
   - Connect TT-303 MIDI IN to your Cirklon MIDI OUT
   - Set the MIDI IN channel with `[FUNC] + [UP]/[DOWN]`

4. **Sequencing**:
   - Program a bassline on the track; accent steps with velocity ≥ 112
   - Ride CC 65 (Slide) for glides; tweak the filter/envelope knobs by hand

---

## Notable Behaviour & Caveats

### MIDI Mode Required

Note data is only received when the Mode switch is set to MIDI. In the other
modes the unit plays its internal sequencer instead.

### Panel Knobs Are Not Automatable

The five sound knobs (Tuning, Cutoff, Resonance, Env Mod, Decay) and Accent are
hardware-only. There is no CC, NRPN or SysEx parameter for them, so they cannot
be automated from the Cirklon — only Slide (CC 65) and Sustain (CC 64) are.

### Auto-Tuning Cannot Be Triggered Over MIDI

The Bass Bot's automatic tuning (`[FUNCTION] + [C#]`) is a front-panel-only
operation; it cannot be requested via MIDI.

---

## Resources

### Official Documentation

- [The Bass Bot User Manual v2.0 (Cyclone Analogic PDF)](https://www.cyclone-analogic.fr/img/cms/The-Bass-Bot-English-2.0.pdf) — primary reference, includes the InstaDJ 2.0 MIDI Implementation Chart
- [Cyclone Analogic — Downloads](https://www.cyclone-analogic.fr/en/content/10-download)

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2026).
