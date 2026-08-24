# Roland TR-1000 Rhythm Creator

Documentation for controlling the Roland TR-1000 with the Sequentix Cirklon.

## Overview

The TR-1000 is a 10-instrument hybrid rhythm machine (analog + ACB + sample) in the
classic TR lineage. Each voice is triggered by a **note**, and a fixed set of
**66 Control Changes** is the machine's entire MIDI surface.

### MIDI Configuration

- **Reference**: TR-1000 MIDI Implementation Chart v1.20 (Apr. 14, 2026)
- **MIDI Port**: OUT 1 (default — adjust to your routing)
- **Velocity**: Note On `9nH` (v=80 default), Note Off `8nH v=00`
- **Program Change**: 0-127 (kit recall), on the Kit Channel
- **Clock / Start / Stop / Continue / Song Position**: supported
- **Aftertouch, Pitch Bend, SysEx**: not supported (`x` in the chart)
- **NRPN**: not documented

### The two MIDI Modes

Firmware 1.20 added `MENU > SYSTEM > MIDI > MIDI Mode`, which changes how the machine
handles incoming **notes**:

| Mode | Behaviour | Cirklon files |
|------|-----------|---------------|
| `Single Ch.` | One channel for everything (Pattern Ch., default 10). The **note** selects the voice. | `single_ch/` |
| `Each Track Ch.` | Each track gets its own channel, 1 to 15. The **channel** selects the voice. Required to sequence individual slices. | `each_track_ch/` |

Pick the mode on the machine first, then load the matching set. The two sets are not
interchangeable.

> The Reference Manual describes `MIDI Mode` as changing how the TR-1000 "handles
> external MIDI **notes**". Roland does not document whether CCs also follow the
> per-track channel in `Each Track Ch.` mode — see the caveat in that section below.

---

## `single_ch/` — one channel, note-addressed

12 definitions on channel 10 (the default Pattern Channel). One CK file for live
drumming, 11 P3 files for per-voice CC control. They are not exclusive — load both.

### CK Pattern Mode — `tr1000.cki`

One CK track covering the whole machine: 25 note rows (10 voices + TRG, plus hidden
Layer A / Layer B alternate notes) and all **66 CCs as track values** (68 slots =
2 track controls + 66 CCs, 12 rows of six).

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

> **Note convention**: the Cirklon names MIDI note 0 as C0, Roland names it C-1. The
> same note therefore reads **C 3** on the Cirklon and **C2** in the Roland chart. The
> tables here use Cirklon names. These note numbers are configurable on the machine
> (`MENU > SYSTEM > MIDI > Inst Note`) — adjust the rows if you remap them.

### P3 Multi-Instrument Mode

11 P3 instruments: one per voice plus a global FX track. **Each P3 exposes only its own
CCs**, so a voice fits in one or two rows of the track values page.

| File | Note | Track values (after `quant%` / `leng%`) | Slots | Rows |
|------|------|------------------------------------------|-------|------|
| `TR-BD.cki` | C 3  | 22 Tune, 23 Decay, 24 Mix, 25-27 Ctrl 1-3, 28 Level | 9 | 2 |
| `TR-SD.cki` | D 3  | 29 Tune, 30 Decay, 31 Mix, 46-48 Ctrl 1-3, 49 Level | 9 | 2 |
| `TR-LT.cki` | G 3  | 50 Tune, 51 Decay, 52 Mix, 53-55 Ctrl 1-3, 56 Level | 9 | 2 |
| `TR-HT.cki` | D 4  | 57 Tune, 58 Decay, 59 Mix, 60-62 Ctrl 1-3, 63 Level | 9 | 2 |
| `TR-RS.cki` | C#3  | 80 Tune, 81 Decay, 82 Ctrl, 83 Level | 6 | 1 |
| `TR-HC.cki` | D#3  | 84 Tune, 85 Decay, 86 Ctrl, 87 Level | 6 | 1 |
| `TR-CH.cki` | F#3  | 102 Tune, 103 Decay, 104 Ctrl, 105 Level | 6 | 1 |
| `TR-OH.cki` | A#3  | 106 Tune, 107 Decay, 108 Ctrl, 109 Level | 6 | 1 |
| `TR-CC.cki` | C#4  | 110 Tune, 111 Decay, 112 Ctrl, 113 Level | 6 | 1 |
| `TR-RC.cki` | D#4  | 114 Tune, 115 Decay, 116 Ctrl, 117 Level | 6 | 1 |
| `TR-FX.cki` | C 0  | the 14 global CCs | 16 | 3 |

In this mode every CC is machine-wide on channel 10 — a CC sent from any track does the
same thing. The split is a workflow convenience, not a MIDI scope. When you need a CC
that is not on the current P3, use the CK track, which carries all 66.

> **Why `TR-FX` uses note C 0.** Every voice lives on channel 10, so any note sent from
> the FX track would trigger a voice. C 0 (note 0) is assigned to nothing in this mode —
> the lowest note in the chart is 35 — so the FX track can carry steps silently.

---

## `each_track_ch/` — one channel per track

16 definitions for `MIDI Mode = Each Track Ch.`. The channel selects the voice, so the
note numbers become uniform: **40** for the voice, **89** for its alternate layer, and
low note ranges for slices.

| File | Ch | Note 40 | Note 89 | Slices 0-15 | Slices 16-31 | CCs |
|------|----|---------|---------|-------------|--------------|-----|
| `TR-BD-A.cki` | 1  | BD (Layer A+B) | Layer A only | Layer A | — | 22-28 |
| `TR-BD-B.cki` | 2  | — | Layer B only | Layer B | Layer A+B | — |
| `TR-SD-A.cki` | 3  | SD (Layer A+B) | Layer A only | Layer A | — | 29-31, 46-49 |
| `TR-SD-B.cki` | 4  | — | Layer B only | Layer B | Layer A+B | — |
| `TR-LT-A.cki` | 5  | LT (Layer A+B) | Layer A only | Layer A | — | 50-56 |
| `TR-LT-B.cki` | 6  | — | Layer B only | Layer B | Layer A+B | — |
| `TR-HT-A.cki` | 7  | HT (Layer A+B) | Layer A only | Layer A | — | 57-63 |
| `TR-HT-B.cki` | 8  | — | Layer B only | Layer B | Layer A+B | — |
| `TR-RS.cki`  | 9  | RS | Layer B / Alt | Layer A+B | — | 80-83 |
| `TR-HC.cki`  | 10 | HC | Layer B / Alt | Layer A+B | — | 84-87 |
| `TR-CH.cki`  | 11 | CH | Layer B / Alt | Layer A+B | — | 102-105 |
| `TR-OH.cki`  | 12 | OH | Layer B / Alt | Layer A+B | — | 106-109 |
| `TR-CC.cki`  | 13 | CC | Layer B / Alt | Layer A+B | — | 110-113 |
| `TR-RC.cki`  | 14 | RC | Layer B / Alt | Layer A+B | — | 114-117 |
| `TR-TRG.cki` | 15 | TRIGGER OUT | — | — | — | — |
| `TR-FX.cki`  | 10 | — | — | — | — | the 14 global CCs |

In Cirklon names: note 40 is **E 3**, note 89 is **F 7**, slices 0-15 run **C 0** to
**D#1**, slices 16-31 run **E 1** to **G 2**. Slice rows are declared with
`always_show: false` — reveal them on the Cirklon when you need them.

Three points worth knowing before wiring this up:

- **The voice CCs sit on the odd (Layer A) channel** of the dual-layer voices. A voice
  has one set of CCs, not one per layer, so `TR-BD-B` carries notes only.
- **`TR-FX` sits on channel 10**, the default Pattern Channel, because the global
  effects belong to no track. Channel 10 is also HC's note channel in this mode; that
  is not a conflict (notes and CCs are different messages), but it means `TR-FX` needs a
  note that triggers nothing. It uses **E 8** (note 100) — on channel 10 only notes
  0-15, 40 and 89 are assigned.
- **Untested against hardware, and partly undocumented.** Roland documents `MIDI Mode`
  as affecting notes. Whether the voice CCs are received on the track channel or stay on
  the Pattern Channel is not stated anywhere in the chart or the Reference Manual. These
  files assume the track channel. If a CC does not respond, send it on the Pattern
  Channel instead — the `single_ch/` definitions do exactly that.

---

## CC Reference (MIDI Implementation Chart v1.20)

Identical to v1.11: no CC was added, removed or renamed between the two revisions.

### Global / FX

| CC | Label | Parameter |
|----|-------|-----------|
| 9  | Ext In  | EXT IN |
| 12 | Dly Lvl | DELAY LEVEL |
| 13 | Dly Tim | DELAY TIME |
| 14 | Dly Fbk | DELAY FEEDBACK |
| 15 | MFX On  | MASTER FX ON |
| 16 | MFX Ct1 | MASTER FX CTRL1 |
| 17 | MFX Ct2 | MASTER FX CTRL2 |
| 18 | MFX Ct3 | MASTER FX CTRL3 |
| 19 | AnFX On | ANALOG FX ON |
| 20 | Filter  | FILTER (analog FX section) |
| 21 | Drive   | DRIVE (analog FX section) |
| 89 | Morph   | MORPH |
| 90 | Rev Tim | REVERB TIME |
| 91 | Rev Lvl | REVERB LEVEL |

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

52 voice CCs + 14 global CCs = 66. That is the whole list.

---

## What the TR-1000 does not expose over MIDI

Most of the machine has **no CC at all**. Parameter names below are taken from the
Reference Manual v1.20 parameter list.

| Section | Page | Reachable by CC | Not reachable |
|---------|------|-----------------|---------------|
| GEN (engine) | 60-64 | `TUNE`, `DECAY` | `PHASE`, `DELAY`, `TONE`, `SNAPPY`, `SNPY DCY`, `COLOR`, `CLP SIZE`, `TAIL LVL`, `MUTE ATK`, `MUTE TRG`, `DETUNE`, `PITCH`, `ATTACK`, `COARSE`, `BODY DEP`, `BODY DCY`, `REFORMER`, `RFM TYP`, `RFM DEP`, `EXCITE`, `OSC DCY`, `OSC MIX`, `MODEL` |
| FILTER (per instrument) | 65 | nothing | `MODEL`, `CUTOFF`, `RESO`, `TYPE`, `SW`, `ATTACK`, `HOLD`, `HLD STEP`, `HLD MODE`, `DECAY`, `CURVE`, `AMOUNT`, and the EQ `LOW F/G`, `HIGH F/G`, `MID1 F/Q/G`, `MID2 F/Q/G`, `BALANCE` |
| AMP, CMP | 66 | nothing | all |
| IFX (instrument FX) | 67-71 | nothing | all |
| MOD (LFO) | 72 | nothing | `WAVE`, `TIME`, `STEP`, `NOTE`, `PHASE`, `DEST`, `TARGET`, `AMOUNT`, `MODE` |
| MIXER | 72 | nothing | `PAN`, `RVB SEND`, `DLY SEND`, `FX ROUTE`, `SC DEPTH`, `TRK GAIN`, `INDV OUT` |
| DELAY | 55 | `LEVEL` (12), `TIME` (13), `FEEDBACK` (14) | `SYNC`, `SYNC TIME`, `TYPE`, `MODE`, `LOW DAMP`, `PAN S/M/L`, `BASS`, `TREBLE`, `SC DEPTH`, `RVB SEND`, `FX ROUTE` |
| REVERB | 54 | `TIME` (90), `LEVEL` (91) | `PRE DLY`, `LOW CUT`, `HIGH CUT`, `DENSITY`, `MOD`, `TYPE`, `SC DEPTH`, `FX ROUTE` |
| AFX (analog FX) | 59 | `ON` (19), cutoff via `FILTER` (20), `DRIVE` (21) | `ROUTING`, `RESO`, `FLT TYPE`, `FLT IN G`, `OFFSET`, `DRV IN G`, `OUT GAIN` |
| MFX (master FX) | 56-58 | `ON` (15) + three generic `CTRL` (16-18) | the type-specific parameters |

Watch the naming trap: **CC 20 `FILTER` is the global analog-FX filter**, not the filter
of a voice. The per-instrument filter has no CC at all.

### Reaching the rest: KNOB ASSIGN

With no SysEx and no NRPN, the **only** way in is `KNOB ASSIGN`. Reference Manual p. 36:

> *You can assign parameters to each knob in the Instrument controlling section to
> control the pattern while it plays back. You can assign up to four parameters to a
> knob, and set the minimum and maximum values per parameter.*

The `Ctrl` CCs are the sequencer's handle on those knobs. To drive the bass drum's
reverb send from the Cirklon:

1. On the TR-1000, press `[KNOB ASSIGN]`
2. Turn the BD `CTRL 1` knob to select it for editing
3. Assign `RVB SEND` and set its minimum and maximum
4. **CC 25** now drives the bass drum's reverb send

Four parameters per knob means BD, SD, LT and HT can each reach twelve arbitrary
parameters over MIDI; RS, HC, CH, OH, CC and RC have a single `Ctrl`, so four.

---

## Using with Cirklon

### `Single Ch.` — CK, live

1. Copy `single_ch/tr1000.cki` to the SD card, then `DISK → LOAD → INSTR`
2. Create a track, assign instrument `TR-1000`, MIDI channel 10
3. On the machine, set `MIDI Mode` to `Single Ch.` and Pattern Ch. to 10
4. Sequence the voices on their rows; reveal the Layer A/B rows only if you use the
   alternate note assignments

### `Single Ch.` — P3, studio

1. Load the `single_ch/TR-*` instruments you need
2. One Cirklon track per voice, all on channel 10 — the note selects the voice
3. `TR-FX` carries the machine-wide effects

### `Each Track Ch.`

1. On the machine, set `MIDI Mode` to `Each Track Ch.`
2. Load the `each_track_ch/` instruments and give each one its own Cirklon track
3. Channels 1-15 are all used; check no other gear on the same port claims them

The CCs declared in these files land in the Cirklon's **track values** — live encoders on
the TRACK page, stored per SONG or SCENE. They are not per-step automation: that is the
P3 pattern's four aux rows, each assignable to any CC. See
[`doc/track_values_limitations.md`](../track_values_limitations.md).

---

## Caveats

- **`Rx Edit Data` must be ON** (`MENU > SYSTEM > MIDI`, Reference Manual p. 47):
  *"Specifies whether CC messages are received (ON) or are not"*. This one switch
  silences every CC at once — check it first if nothing responds.
- **`Ctrl 1-3` do nothing out of the factory**: *"Controls what is set with the
  [KNOB ASSIGN] button"*. Assign them first (see above).
- **`Mix` is not an effect send**: *"Adjusts the mix balance for layers A/B"*. It is
  inaudible on an INST with no layer B loaded.
- **Turn `MOTION [ON]` off while testing**: recorded knob motions replay continuously
  and overwrite incoming CC values.
- **Check `FX ROUTE` before blaming a CC**: a voice set to `THROUGH` bypasses the master
  and analog effects entirely.
- **Channels**: CCs travel on the Pattern Channel (default 10). `Kit Ch.` (default 1) is
  only for the program changes that switch kits.

---

## Resources

- [TR-1000 MIDI Implementation Chart v1.20 (Roland PDF)](https://static.roland.com/assets/media/pdf/TR-1000_MIDIImpleChart_eng02_W.pdf) — primary reference for this collection
- [TR-1000 Reference Manual v1.20 (Roland PDF)](https://static.roland.com/assets/media/pdf/TR-1000_reference_eng03_W.pdf) — KNOB ASSIGN (p. 36), `Rx Edit Data` and `MIDI Mode` (p. 47), parameter list (p. 54-72)
- [Roland Support — TR-1000 Owner's Manuals](https://www.roland.com/global/support/by_product/tr-1000/owners_manuals/)
- [Cirklon Operation Manual v1.22 (Sequentix PDF)](https://cdn.shopify.com/s/files/1/0757/8429/0571/files/cirklon_operation_manual_1.22.pdf) — track values (ch. 9), aux rows and gate flags (ch. 3)
- [Roland TR-1000 MIDI CCs (midi.guide)](https://midi.guide/d/roland/tr-1000/)

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2026).
