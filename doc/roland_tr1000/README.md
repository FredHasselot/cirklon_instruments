# Roland TR-1000 Rhythm Performer

Documentation for controlling the Roland TR-1000 with the Sequentix Cirklon.

## Overview

The Roland TR-1000 is a 10-instrument hybrid rhythm machine (analog + ACB/sample
engines) in the classic TR lineage. Over MIDI it behaves like a GM-style drum
machine: a **single MIDI channel** addresses the whole instrument, each of the 10
drum voices is triggered by a **note**, and every synthesis parameter is exposed
as a **Control Change (CC)**.

There is no aftertouch, no pitch bend, no NRPN and no SysEx in the documented
implementation — a deliberately simple, readable MIDI surface.

### MIDI Configuration

- **Reference**: TR-1000 MIDI Implementation Chart v1.11 (Oct. 1, 2025)
- **Channel**: Pattern Channel — default **10**, changeable 1-16 (`MENU > SYSTEM > MIDI`)
- **MIDI Port**: OUT 1 (default — adjust to your routing)
- **Polyphony**: drum-style — one note per voice
- **Velocity**: Note On `9nH` (v=80 default), Note Off `8nH v=00`
- **Aftertouch / Pitch Bend**: not supported
- **NRPN / SysEx**: none documented
- **Program Change**: 0-127 (Kit / Pattern recall)
- **Clock / Start / Stop / Continue / Song Position**: supported

## Cirklon Instrument Files

Two complementary modes are provided. They are not exclusive — load the CK file
for live drumming and the P3 files for per-instrument CC automation.

### CK Pattern Mode — `tr1000.cki`

A single CK pattern on channel 10 with one row per instrument, plus hidden
alternate-note rows for the TR-1000's Layer A / Layer B note assignments.

| Row | Label | MIDI Note | Cirklon | Visible |
|-----|-------|-----------|---------|---------|
| BD  | `BD ` | 36 | C 3  | yes |
| BD Layer A | `BD-A` | 35 | B 2  | hidden |
| BD Layer B | `BD-B` | 99 | D#8  | hidden |
| RS  | `RS ` | 37 | C#3  | yes |
| RS Layer B | `RS-B` | 56 | G#4  | hidden |
| SD  | `SD ` | 38 | D 3  | yes |
| SD Layer A | `SD-A` | 40 | E 3  | hidden |
| SD Layer B | `SD-B` | 104 | G#8 | hidden |
| HC  | `HC ` | 39 | D#3  | yes |
| HC Layer B | `HC-B` | 54 | F#4  | hidden |
| CH  | `CH ` | 42 | F#3  | yes |
| CH Layer B | `CH-B` | 44 | G#3  | hidden |
| LT  | `LT ` | 43 | G 3  | yes |
| LT Layer A | `LT-A` | 41 | F 3  | hidden |
| LT Layer B | `LT-B` | 105 | A 8 | hidden |
| OH  | `OH ` | 46 | A#3  | yes |
| OH Layer B | `OH-B` | 58 | A#4  | hidden |
| CC  | `CC ` | 49 | C#4  | yes |
| CC Layer B | `CC-B` | 61 | C#5  | hidden |
| HT  | `HT ` | 50 | D 4  | yes |
| HT Layer A | `HT-A` | 48 | C 4  | hidden |
| HT Layer B | `HT-B` | 112 | E 9 | hidden |
| RC  | `RC ` | 51 | D#4  | yes |
| RC Layer B | `RC-B` | 63 | D#5  | hidden |
| TRG | `TRG` | 84 | C 7  | yes |

> **Note convention**: the Cirklon uses C0 = MIDI note 0, so MIDI note 36 displays
> as **C 3** (not C1). All rows above use the Cirklon names. The TR-1000's own
> note numbers are configurable on `MENU > SYSTEM > MIDI > Inst Note`; if you
> remap them on the machine, adjust the rows to match.

### P3 Multi-Instrument Mode

10 P3 instruments (one per voice) plus a global FX P3, all on channel 10. Each
P3 exposes only the CCs that actually exist for that voice in the chart.

| File | Inst Name | Note | CCs | Parameters |
|------|-----------|------|-----|------------|
| `TR-BD.cki` | TR-BD | C 3  | 22-28 | Tune, Decay, Mix, Ctrl 1/2/3, Level |
| `TR-SD.cki` | TR-SD | D 3  | 29-31, 46-49 | Tune, Decay, Mix, Ctrl 1/2/3, Level |
| `TR-LT.cki` | TR-LT | G 3  | 50-56 | Tune, Decay, Mix, Ctrl 1/2/3, Level |
| `TR-HT.cki` | TR-HT | D 4  | 57-63 | Tune, Decay, Mix, Ctrl 1/2/3, Level |
| `TR-RS.cki` | TR-RS | C#3  | 80-83 | Tune, Decay, Ctrl, Level |
| `TR-HC.cki` | TR-HC | D#3  | 84-87 | Tune, Decay, Ctrl, Level |
| `TR-CH.cki` | TR-CH | F#3  | 102-105 | Tune, Decay, Ctrl, Level |
| `TR-OH.cki` | TR-OH | A#3  | 106-109 | Tune, Decay, Ctrl, Level |
| `TR-CC.cki` | TR-CC | C#4  | 110-113 | Tune, Decay, Ctrl, Level |
| `TR-RC.cki` | TR-RC | D#4  | 114-117 | Tune, Decay, Ctrl, Level |
| `TR-FX.cki` | TR-FX | C 3  | 9, 12-21, 89-91 | Ext In, Delay, Master FX, Analog FX, Filter, Drive, Morph, Reverb |

> The four "drum" voices (BD, SD, LT, HT) expose **3 Ctrl** parameters each
> (deeper synthesis); the percussion/cymbal voices (RS, HC, CH, OH, CC, RC)
> expose a **single Ctrl**. This mirrors the chart exactly.

---

## CC Reference (TR-1000 MIDI Implementation v1.11)

### Global / FX

| CC  | Label    | Description |
|-----|----------|-------------|
| 9   | Ext In   | External input level |
| 12  | Dly Lvl  | Delay level |
| 13  | Dly Tim  | Delay time |
| 14  | Dly Fbk  | Delay feedback |
| 15  | MFX On   | Master FX on |
| 16  | MFX Ct1  | Master FX control 1 |
| 17  | MFX Ct2  | Master FX control 2 |
| 18  | MFX Ct3  | Master FX control 3 |
| 19  | AnFX On  | Analog FX on |
| 20  | Filter   | Filter |
| 21  | Drive    | Drive |
| 89  | Morph    | Morph |
| 90  | Rev Tim  | Reverb time |
| 91  | Rev Lvl  | Reverb level |

### Per-Instrument

| Voice | Tune | Decay | Mix | Ctrl 1 | Ctrl 2 | Ctrl 3 | Level |
|-------|------|-------|-----|--------|--------|--------|-------|
| BD | 22 | 23 | 24 | 25 | 26 | 27 | 28 |
| SD | 29 | 30 | 31 | 46 | 47 | 48 | 49 |
| LT | 50 | 51 | 52 | 53 | 54 | 55 | 56 |
| HT | 57 | 58 | 59 | 60 | 61 | 62 | 63 |

| Voice | Tune | Decay | Ctrl | Level |
|-------|------|-------|------|-------|
| RS | 80  | 81  | 82  | 83  |
| HC | 84  | 85  | 86  | 87  |
| CH | 102 | 103 | 104 | 105 |
| OH | 106 | 107 | 108 | 109 |
| CC | 110 | 111 | 112 | 113 |
| RC | 114 | 115 | 116 | 117 |

> **No NRPN, no SysEx, no aftertouch, no pitch bend are documented.**

---

## Note Map (TR-1000 MIDI Implementation v1.11)

| INST | Default | Layer A | Layer B / Alt |
|------|---------|---------|---------------|
| BD   | 36 | 35 | 99  |
| SD   | 38 | 40 | 104 |
| LT   | 43 | 41 | 105 |
| HT   | 50 | 48 | 112 |
| RS   | 37 | —  | 56  |
| HC   | 39 | —  | 54  |
| CH   | 42 | —  | 44  |
| OH   | 46 | —  | 58  |
| CC   | 49 | —  | 61  |
| RC   | 51 | —  | 63  |
| TRG  | 84 | —  | —   |

> These note numbers are configurable on `MENU > SYSTEM > MIDI > Inst Note`.

---

## Using with Cirklon

### Basic Setup — CK (live)

1. **Load instrument**:
   - Copy `tr1000.cki` to your Cirklon SD card
   - `DISK → LOAD → INSTR`

2. **Assign to track**:
   - Create a track, assign instrument `TR-1000`
   - MIDI channel: 10 (match the TR-1000 Pattern Channel)

3. **TR-1000 configuration**:
   - Connect TR-1000 MIDI IN to your Cirklon MIDI OUT
   - Confirm `MENU > SYSTEM > MIDI` Pattern Channel = 10
   - Sequence the 10 instruments on their rows; reveal Layer A/B rows only if you
     use the alternate note assignments.

### Advanced Setup — P3 (studio)

1. **Load all 11 P3 instruments** to your SD card.

2. **Create dedicated Cirklon tracks** (one per voice you want to automate):

| Track | Instrument | Note | Use |
|-------|-----------|------|-----|
| 1  | `TR-BD` | C 3 | Bass drum + Tune/Decay/Mix/Ctrl1-3/Level |
| 2  | `TR-SD` | D 3 | Snare |
| 3  | `TR-LT` | G 3 | Low tom |
| 4  | `TR-HT` | D 4 | High tom |
| 5  | `TR-RS` | C#3 | Rim shot |
| 6  | `TR-HC` | D#3 | Hand clap |
| 7  | `TR-CH` | F#3 | Closed hi-hat |
| 8  | `TR-OH` | A#3 | Open hi-hat |
| 9  | `TR-CC` | C#4 | Crash cymbal |
| 10 | `TR-RC` | D#4 | Ride cymbal |
| 11 | `TR-FX` | C 3 | Global Delay / Reverb / Master FX / Filter / Drive / Morph |

3. **Sequencing**:
   - Trigger each voice on its own track and automate its CCs per step.
   - All P3 instruments share channel 10 — the note determines which voice plays.
   - Use `TR-FX` to ride the global Delay/Reverb/Master FX from the sequencer.

---

## Notable Behaviour & Caveats

### Single Channel, Note-Addressed Voices

Unlike multi-timbral synths, the TR-1000 puts all voices on one channel. The
**note number** selects the voice — the P3 instruments here differ only by their
default note and CC set, all on channel 10.

### Layer A / Layer B Notes

Each main voice can be addressed through up to three note numbers (Default,
Layer A, Layer B/Alt) to hit different sound layers without changing kit. The CK
pattern exposes these as hidden rows; reveal them on the Cirklon if you use them.

### Velocity

Note On is sent at v=80 by default. Use Cirklon velocity per step to vary
dynamics; the TR-1000 maps incoming velocity to its accent/level behaviour.

---

## Resources

### Official Documentation

- [TR-1000 MIDI Implementation Chart v1.11 (Roland PDF)](https://static.roland.com/assets/media/pdf/TR-1000_MIDI_ImpleChart_eng01_W.pdf) — primary reference for this collection
- [Roland Support — TR-1000 Owner's Manuals](https://www.roland.com/global/support/by_product/tr-1000/owners_manuals/)
- [Roland TR-1000 product page](https://www.roland.com/global/products/tr-1000/)

### Community

- [Roland TR-1000 MIDI CCs and NRPNs (midi.guide)](https://midi.guide/d/roland/tr-1000/)

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2026).
