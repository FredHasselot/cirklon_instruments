# Buchla Easel Command (208C)

Documentation for controlling the Buchla Easel Command (208C with 208MIDI) with the Sequentix Cirklon.

## Overview

The Buchla Easel Command is a self-contained version of the Music Easel built around the **208C** sound generator card with the **208MIDI** card pre-installed. It is a monophonic, semi-modular West Coast-style synthesizer featuring a Complex Oscillator, Modulation Oscillator, Low-Pass Gate, Envelope Generator, Pulser, Sequencer, and Random source.

Unlike a typical multi-timbral synth, the 208MIDI implementation is built around **MIDI channel routing**: different MIDI channels address different parts of the instrument (keyboard, oscillators, internal modulation triggers) rather than different patches. This collection provides one P3/CK pattern per documented MIDI channel.

### MIDI Configuration

- **Reference**: 208MIDI Implementation v31.0 (August 2023)
- **Channels used**: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
- **MIDI Port**: OUT 1 (default — adjust to your routing)
- **Polyphony**: monophonic (each channel controls a single voice/source)
- **NRPN / Sysex**: none documented
- **Aftertouch**: Channel pressure supported (poly aftertouch is **not** supported — falls back to CC 14)

## Cirklon Instrument Files

10 `.cki` files are provided, one per documented MIDI channel:

| File | Inst Name | Channel | Pattern | Role |
|------|-----------|---------|---------|------|
| `EC-KBD.cki`  | EC-KBD  | 1  | P3 | Keyboard pitch + all CCs (timbre, mod, pressure, velocity) |
| `EC-COSC.cki` | EC-COSC | 2  | P3 | Complex Oscillator pitch + timbre + mod + pressure |
| `EC-MOSC.cki` | EC-MOSC | 3  | P3 | Modulation Oscillator pitch + pressure (no timbre/mod) |
| `EC-BUSC.cki` | EC-BUSC | 4  | P3 | Internal Bus C (AuxCard / 200e) — Note On + Velocity only |
| `EC-TRIG.cki` | EC-TRIG | 5  | CK | Triggers only (Seq/Rnd/EG/Pulser, octave-repeated) |
| `EC-COS2.cki` | EC-COS2 | 6  | P3 | C.Osc + timbre + mod + velocity + EG trigger |
| `EC-MOS2.cki` | EC-MOS2 | 7  | P3 | M.Osc + pressure + Pulser trigger |
| `EC-COS3.cki` | EC-COS3 | 8  | P3 | C.Osc + timbre + mod + pressure + Pulser |
| `EC-MOS3.cki` | EC-MOS3 | 9  | P3 | M.Osc + velocity + EG trigger |
| `EC-BUC2.cki` | EC-BUC2 | 10 | P3 | Bus C (AuxCard) + pressure + Pulser |

### Channel Map (208MIDI v31.0)

```
Ch 1  : Keyboard + all CCs (timbre, mod, pressure, velocity from card)
Ch 2  : C.Osc pitch + timbre + mod + pressure
Ch 3  : M.Osc pitch + pressure (no timbre/mod)
Ch 4  : Internal bus C (AuxCard / 200e modules)
Ch 5  : Triggers only (lowest range, repeated in higher octaves)
Ch 6  : C.Osc + timbre/mod + velocity + EG trigger
Ch 7  : M.Osc + pressure + Pulser trigger
Ch 8  : C.Osc + timbre/mod + pressure + Pulser
Ch 9  : M.Osc + velocity + EG trigger
Ch 10 : Bus C + pressure + Pulser
```

> **Hint from Buchla**: *Odd = Mod*. The Modulation Oscillator is always on the odd channels (3, 7, 9).

---

## CC Reference (208MIDI)

The 208MIDI implementation uses a small, deliberate set of MIDI CCs:

| CC  | Label    | Slot Name | Description |
|-----|----------|-----------|-------------|
| 1   | Timbre   | `Timbre`  | Mod wheel — timbre control (CH 1, 2, 6, 8) |
| 2   | Mod Amt  | `Mod Amt` | Breath — modulation amount (CH 1, 2, 6, 8) |
| 3   | PrsSlew  | `PrsSlew` | Slew rate of the pressure CV (CH 1, 2, 3, 6, 8) |
| 5   | Porta    | `Porta`   | Portamento rate (all pitch-bearing channels) |
| 9   | PB Dpth  | `PB Dpth` | Pitchbend depth, ±1-12 semitones (global, value 0-127 = 10/step on the 218eV3) |
| 14  | PressCV  | `PressCV` | Pressure CV (alternative to channel pressure / aftertouch) |
| 120 | Pul Off  | `Pul Off` | Turn off Pulser |
| 121 | Reset    | `Reset`   | Reset pressure and oscillator control to 0v |
| 123 | EG Off   | `EG Off`  | Turn off Envelope Generator |

> **No 14-bit (MSB/LSB) controllers, no NRPNs, no SysEx are documented.**

---

## Note Map — Triggers in Octave -1

The 208MIDI repurposes the lowest MIDI octave (notes 0-11) to fire the internal modulation/timing sources directly. This applies to channels 1, 2, 3, 4, 5 (and is repeated on CH 5 in higher octaves for limited sequencers/keyboards that cannot transpose to MIDI octave -1):

| MIDI Note | Note Name | Trigger | Channels |
|-----------|-----------|---------|----------|
| 0-2       | C0 - D0   | **Sequencer** trigger | 1, 2, 3, 4, 5 |
| 3-5       | D#0 - F0  | **Random** trigger    | 1, 2, 3, 4, 5 |
| 6-8       | F#0 - G#0 | **Envelope Generator** trigger | 1, 2, 3, 4, 5 |
| 9-11      | A0 - B0   | **Pulser** trigger    | 1, 2, 3, 4, 5 |

### Channels 6-9 — Paired Trigger Pairings

Buchla added "non-conflicting" CV control pairings on CH 6-9:

| Channel | C.Osc/M.Osc | EG | Pulser | Timbre/Mod | Velocity | Pressure |
|---------|-------------|----|--------|------------|----------|----------|
| 6 | C.Osc | Note On | — | yes | yes | — |
| 7 | M.Osc | — | Note On | — | — | yes |
| 8 | C.Osc | — | Note On | yes | — | yes |
| 9 | M.Osc | Note On | — | — | yes | — |

### Oscillator Pitch Range

The 208C oscillators start at **MIDI note 24 (C1, ~32.7Hz)** — that is the `default_note` used in the P3 patterns of this collection. To get the full range starting from C1, the **Frequency** and **Pitch** front-panel faders must be at their **lowest** position and fine-tuned as needed.

---

## Pattern Modes Used

### P3 Patterns (CH 1-4, 6-10)

Each P3 pattern exposes the relevant subset of CCs as track values, plus the keyboard/oscillator note in `row_defs`. Trigger rows (Seq/Rnd/EG/Pul) are added as `always_show` rows when the channel can fire them.

### CK Pattern — `EC-TRIG` (CH 5)

Channel 5 is dedicated to triggering the four internal sources. It is mapped as a CK drum-style pattern with 12 rows covering the lowest octave plus optional repetitions (Seq/Seq2/Seq3, Rnd/Rnd2/Rnd3, EG/EG2/EG3, Pul/Pul2/Pul3) so any of the documented octave repetitions in the 208MIDI spec can be programmed.

---

## Using with Cirklon

### Basic Setup — Single Channel (live)

For a simple workflow where you only want to play notes and use a few CCs:

1. **Load instrument**:
   - Copy `EC-KBD.cki` to your Cirklon SD card
   - `DISK → LOAD → INSTR`

2. **Assign to track**:
   - Create a track
   - Assign instrument `EC-KBD`
   - MIDI channel: 1

3. **Easel Configuration**:
   - Connect the Easel Command MIDI IN to your Cirklon MIDI OUT
   - Set the front-panel Frequency and Pitch faders to their lowest position
   - Default note `C 1` matches the lowest oscillator pitch

### Advanced Setup — Multi-Channel (studio)

For full exploitation of the 208MIDI per-channel routing:

1. **Load all 10 instruments** to your SD card.

2. **Create dedicated Cirklon tracks** (one per channel you actually use):

| Track | Instrument | Channel | Use |
|-------|-----------|---------|-----|
| 1 | `EC-KBD`  | 1  | Keyboard line + global CCs |
| 2 | `EC-COSC` | 2  | Complex Oscillator pitch line |
| 3 | `EC-MOSC` | 3  | Modulation Oscillator pitch line |
| 4 | `EC-BUSC` | 4  | Bus C → AuxCard (if present) |
| 5 | `EC-TRIG` | 5  | Drum-style trigger sequencing of internal sources |
| 6 | `EC-COS2` | 6  | C.Osc with EG trigger pairing |
| 7 | `EC-MOS2` | 7  | M.Osc with Pulser pairing + pressure |
| 8 | `EC-COS3` | 8  | C.Osc with Pulser pairing + pressure |
| 9 | `EC-MOS3` | 9  | M.Osc with EG pairing + velocity |
| 10 | `EC-BUC2` | 10 | Bus C with pressure + Pulser |

3. **Sequencing**:
   - Independent pitch lines on the keyboard, Complex Osc, and Modulation Osc.
   - Use `EC-TRIG` (CH 5) as a "drum machine" track to fire Seq/Random/EG/Pulser at any rhythm.
   - Combine CH 6/7/8/9 to drive C.Osc and M.Osc with their dedicated EG/Pulser pairings without conflicting CC routing.

---

## Notable Behaviour & Caveats

### EG and Pulser Mode Switches (Note 8 from spec)

The front-panel **EG** and **Pulser** mode selection switches (Sustained / Transient) only affect the **keyboard "trigger source"** on Channel 1. Direct triggers fired through MIDI Notes 6-8 (EG) and 9-11 (Pulser) — or through CH 5/6/7/8/9 trigger pairings — always behave as if in **Sustained** mode.

> **Tip**: To emulate Transient mode on direct-trigger channels, use **very short MIDI note lengths**. The Pulser does not output its trigger signal until it reaches the **end** of its duration, never at its start.

### Pitchbend Depth (CC 9, Note 9 from spec)

Pitchbend depth is a **global, memorized** setting. In firmware ≥ v30.5 the response is linearly aligned with the 218eV3: CC 9 values 10, 20, 30 ... 110, 120 = ±1 to ±12 semitones.

### Pressure Routing (Notes 1 & 2 from spec)

- The 208C does **not** support polyphonic aftertouch.
- For controllers/DAWs that emit poly AT or prefer CC routing, use **CC 14** as a direct alternative to channel pressure.
- **CC 3** sets the slew rate of the pressure CV — useful to smooth out aftertouch from controllers that produce stepped values.

### AuxCard / 200e — Bus C (Notes 3, 4, 5)

Channels 4 and 10 send Note data on **internal bus C**. This is only routed to:
- The **Music Easel AuxCard** (sold separately) when its oscillator range switch is in the middle position.
- The **259e, 261e, 281e, 292e** modules with module ID set to `C` and `remote` enabled.

The 208C must also be in **Remote** or **Both** mode for bus C to be sent.

---

## Resources

### Official Documentation

- [208MIDI Implementation v8 (firmware v31.2, Aug 2023)](https://buchla.com/guides/208C_%20208MIDI_MIDI_Implementation_v8_for_v31.2.pdf) — primary reference for this collection
- [208MIDI Implementation (pre-2024)](https://buchla.com/guides/208C_208MIDI_Implementation.pdf) — legacy version
- [Buchla Downloads](https://buchla.com/download/)
- [Easel Command product page](https://buchla.com/product/buchla-easel-command/)
- [Easel Command and 208C overview](https://buchla.com/easel-command-and-208c/)

### Community

- [Buchla Easel Command MIDI thread — MOD WIGGLER](https://www.modwiggler.com/forum/viewtopic.php?t=231066)
- [Music Easel MIDI Implementation — MOD WIGGLER](https://www.modwiggler.com/forum/viewtopic.php?t=150534)

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2026).
