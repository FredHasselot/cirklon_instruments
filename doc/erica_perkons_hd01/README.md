# Erica Synths Pērkons HD-01

Documentation for controlling the Erica Synths Pērkons HD-01 with the Sequentix Cirklon.

## Overview

The Pērkons HD-01 is a four-voice hybrid drum synthesizer. Each voice has **8 knobs and
3 switches**, and all 11 controls of each voice are reachable by MIDI CC. That is the
machine's whole MIDI surface: nothing else has a CC.

### MIDI Configuration

- **Reference**: Pērkons HD-01 manual rev. 10/26 (firmware 1.3), MIDI Implementation p. 35-36
- **Firmware**: 1.3.0 (`perkons_v1.3.0-0-force.img`, Oct. 20, 2026)
- **MIDI Port**: OUT 1 (default, adjust to your routing)
- **Notes**: trigger the voices (Single mode) or play them chromatically (Multi mode)
- **Velocity**: recorded and applied when `MIDI VELOCITY` is ON in the configuration menu
- **Clock**: received (select MIDI as clock source in the configuration menu)
- **No CC**: BBD delay (Time, Feedback), tempo, master level, pattern/kit selection
- **NRPN, SysEx**: not documented

### Configuration menu (SHIFT + MOD)

All settings are made with the step buttons:

| Setting | Where | Value for the Cirklon |
|---------|-------|-----------------------|
| Clock source | 1st row, step 2 | MIDI |
| MIDI mode | 3rd row, step 1 (Single) / step 2 (Multi) | the mode of the set you load |
| MIDI velocity | 3rd row, step 8 | ON to use Cirklon velocity |
| **MIDI CC filter** (1.3) | 3rd row, step 9 | **OFF**, otherwise every CC is ignored |
| Voice quantiser (1.3) | 2nd row, step 13 | ON to snap Tune to semitones |
| Multi channel config | 1st row, sub-menu | Voice 1-4 = CH 1-4 |
| Single channel config | 1st row, sub-menu | the channel of `perkons.cki` (1) |

The two MIDI modes are exclusive: pick one on the machine, then load the matching set.

---

## CC reference

From the manual, p. 35:

| Parameter | Voice 1 | Voice 2 | Voice 3 | Voice 4 |
|-----------|---------|---------|---------|---------|
| Tune          | 70 | 81 | 92  | 103 |
| Decay         | 71 | 82 | 93  | 104 |
| Param 1       | 72 | 83 | 94  | 105 |
| Param 2       | 73 | 84 | 95  | 106 |
| Cutoff        | 74 | 85 | 96  | 107 |
| Drive         | 75 | 86 | 97  | 108 |
| FX Send       | 76 | 87 | 98  | 109 |
| Level         | 77 | 88 | 99  | 110 |
| Algo switch   | 78 | 89 | 100 | 111 |
| Mode switch   | 79 | 90 | 101 | 112 |
| Filter switch | 80 | 91 | 102 | 113 |

In **Multi** mode every voice uses the Voice 1 column (70-80) on its own channel.

The CC numbers can be remapped in `SYSTEM/single-midi-cc.json` on the SD card. The
files here assume the factory mapping.

---

## `multi_ch/` — one channel per voice (recommended)

### `PK-VOICE.cki` — P3

One instrument for the four voices. Assign it to four Cirklon tracks and set the MIDI
channel of each track to 1, 2, 3 and 4.

- Notes are **chromatic** (firmware 1.1): the note sets the pitch of the voice, so
  transpose and fine-tune stay enabled (`no_xpose: false`, `no_fts: false`)
- 13 track values: `quant%`, `leng%` and the 11 CCs 70-80

| Slot | CC | Label |
|------|----|-------|
| 3  | 70 | Tune |
| 4  | 71 | Decay |
| 5  | 72 | Param 1 |
| 6  | 73 | Param 2 |
| 7  | 74 | Cutoff |
| 8  | 75 | Drive |
| 9  | 76 | FX Send |
| 10 | 77 | Level |
| 11 | 78 | Algo |
| 12 | 79 | Mode |
| 13 | 80 | Filter |

---

## `single_ch/` — one channel for the whole machine

### `perkons.cki` — CK

One CK track for live drumming on channel 1.

| Row | MIDI Note | Cirklon | Voice |
|-----|-----------|---------|-------|
| `V1` | 36 | C 3  | Voice 1 |
| `V2` | 37 | C#3  | Voice 2 |
| `V3` | 38 | D 3  | Voice 3 |
| `V4` | 39 | D#3  | Voice 4 |

46 track values: `quant%`, `leng%` and the 44 CCs 70-113, labelled `V1 Tune` to
`V4 Filt` (`Dcy` Decay, `Pr1`/`Pr2` Param 1/2, `Cut` Cutoff, `Drv` Drive, `FX` FX Send,
`Lvl` Level, `Alg` Algo, `Mode`, `Filt` Filter).

> **Note convention**: the Cirklon names MIDI note 0 as C0. Note 36 therefore reads
> **C 3** on the Cirklon.

---

## Not verified against hardware

These files have not been tested on a Pērkons. The manual leaves three points open:

1. **Octave of the Single-mode notes.** The manual only says "Voice 1 – C, Voice 2 – C#,
   Voice 3 – D, Voice 4 – D#", with no octave. The rows use 36-39. If nothing plays,
   move the rows to another octave.
2. **Reference pitch in Multi mode.** The manual does not say which note plays the voice
   at its knob pitch. `PK-VOICE` defaults to C 3 (note 36). Adjust after listening.
3. **Switch values.** The Algo, Mode and Filter switches have three positions. The manual
   does not give the CC value ranges for each position.

## Sources

- [Pērkons HD-01 manual rev. 10/26 (PDF)](https://erp.ericasynths.lv/media/PERKONS_manual_10_26.pdf) - Erica Synths Official
- [Pērkons configuration settings 1.3 (PDF)](https://erp.ericasynths.lv/media/PERKONS_Configuration_settings.pdf) - Erica Synths Official
- [Pērkons HD-01 Update 1.3 changelog](https://www.ericasynths.lv/news/post/perkons1-3) - Erica Synths Official
- [Pērkons 1.1 update changelog](https://www.ericasynths.lv/news/perkons-11-update/) - Erica Synths Official
