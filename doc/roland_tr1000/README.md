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

**Every one of the 12 definitions exposes all 66 CCs of the chart** as track values
(68 slots = 2 track controls + 66 CCs, spread over 12 rows of six). All CCs are
machine-wide on channel 10, so any track can address any parameter — you never have
to switch track to reach a CC. Each file only differs in its default note and in the
ordering of its track values.

### CK Pattern Mode — `tr1000.cki`

A single CK pattern on channel 10 with one row per instrument, plus hidden
alternate-note rows for the TR-1000's Layer A / Layer B note assignments. It also
carries the full set of 66 CCs as track values, so the live mode gives access to
every parameter without loading a P3.

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

10 P3 instruments (one per voice) plus a global FX P3, all on channel 10. Each P3
exposes the 66 CCs of the chart, with its own voice placed first for quick access.

| File | Inst Name | Note | Slots 3+ (own voice first) |
|------|-----------|------|-----------------------------|
| `TR-BD.cki` | TR-BD | C 3  | 22-28, then FX, then the 9 other voices |
| `TR-SD.cki` | TR-SD | D 3  | 29-31 / 46-49, then FX, then the 9 other voices |
| `TR-LT.cki` | TR-LT | G 3  | 50-56, then FX, then the 9 other voices |
| `TR-HT.cki` | TR-HT | D 4  | 57-63, then FX, then the 9 other voices |
| `TR-RS.cki` | TR-RS | C#3  | 80-83, then FX, then the 9 other voices |
| `TR-HC.cki` | TR-HC | D#3  | 84-87, then FX, then the 9 other voices |
| `TR-CH.cki` | TR-CH | F#3  | 102-105, then FX, then the 9 other voices |
| `TR-OH.cki` | TR-OH | A#3  | 106-109, then FX, then the 9 other voices |
| `TR-CC.cki` | TR-CC | C#4  | 110-113, then FX, then the 9 other voices |
| `TR-RC.cki` | TR-RC | D#4  | 114-117, then FX, then the 9 other voices |
| `TR-FX.cki` | TR-FX | C 0  | 9 / 12-21 / 89-91, then the 10 voices |

The FX block always follows the same order: 9, 12, 13, 14, 15, 16, 17, 18, 19, 20,
21, 89, 90, 91. The voice blocks always follow BD, SD, LT, HT, RS, HC, CH, OH, CC,
RC. No CC appears twice in a definition.

> The four "drum" voices (BD, SD, LT, HT) expose **3 Ctrl** parameters each;
> the percussion/cymbal voices (RS, HC, CH, OH, CC, RC) expose a **single Ctrl**.
> This mirrors the chart exactly.

> **Track value labels** are prefixed with the voice (`BD Tune`, `SD Dcay`,
> `RC Lvl`) and kept to seven characters so they fit the Cirklon display. The
> global FX CCs keep their unprefixed names (`Ext In`, `Dly Lvl`, `Rev Lvl`).

> **Why TR-FX uses note C 0.** Every voice lives on channel 10, so any note sent
> from the FX track would hit a voice — C 3 is note 36, the bass drum. C 0 (note 0)
> is assigned to nothing on the TR-1000, the lowest note in the chart being 35.
> The FX track can therefore carry steps without triggering a sound.

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

### What Mix and Ctrl actually do

Two entries in the table above are easy to misread.

**Mix** is not an effect send. The Reference Manual describes the `[MIX]` knob as
*"Adjusts the mix balance for layers A/B"* — it doses the balance between the two
layers of the voice. It has nothing to do with reverb or delay.

**Ctrl 1/2/3 are not fixed parameters.** The manual describes the `[CTRL 1-3]` knobs
as *"Controls what is set with the [KNOB ASSIGN] button"*. Nothing is wired to them
out of the factory, which is why they can appear to do nothing. See the next section.

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
| 11 | `TR-FX` | C 0 | Global Delay / Reverb / Master FX / Filter / Drive / Morph |

3. **Sequencing**:
   - All P3 instruments share channel 10 — the note determines which voice plays.
   - The CCs declared in these files are Cirklon **track values**: real-time knobs on
     the TRACK page, not per-step automation. See "Track values are not step
     automation" below.
   - `TR-FX` carries the machine-wide effects. It is a convenience grouping, not a
     separate MIDI destination — the same CC sent from `TR-BD` does exactly the same
     thing.

---

## Controlling the FX

### The global effects are machine-wide

CC 9, 12-21 and 89-91 act on the whole TR-1000. There is no MIDI channel, note or
track that scopes them to one voice. Which voices feed the delay is decided **on the
machine**, not over MIDI.

Two of these CCs are switches, not amounts:

- **CC 15 `MASTER FX ON`** — while the master effect is off, `MFX Ct1/2/3` (CC 16-18)
  produce nothing. Those three are generic controls whose function depends on the
  master effect type selected on the machine.
- **CC 19 `ANALOG FX ON`** — the `[ON]` button of the analog effect section, which also
  holds `[FILTER]` (CC 20) and `[DRIVE]` (CC 21).

### Per-instrument sends do exist — but have no dedicated CC

Each instrument carries its own MIXER parameters:

| Parameter | Range | Reference Manual wording |
|-----------|-------|--------------------------|
| `RVB SEND` | 0-100 % | *Adjusts the level of audio sent to the reverb effect* |
| `DLY SEND` | 0-100 % | *Adjusts the level of audio sent to the delay effect* |
| `FX ROUTE` | THROUGH / MASTER / … | *THROUGH: The signal bypasses master and analog effects* |
| `PAN`      | L100-CENTER-R100 | stereo position |

None of them appears in the MIDI chart. On the machine they are reached by holding a
track select button `[BD]`-`[RC]` and turning the `REVERB [LEVEL]` or `DELAY [LEVEL]`
knob.

> **If the effects seem dead on one voice, check `FX ROUTE` first.** A voice set to
> `THROUGH` bypasses the master and analog effects entirely, whatever CC you send.

### Reaching them over MIDI: KNOB ASSIGN

The `Ctrl` CCs are the way in. The Reference Manual:

> *You can assign parameters to each knob in the Instrument controlling section to
> control the pattern while it plays back. You can assign up to four parameters to a
> knob, and set the minimum and maximum values per parameter.*

To drive the bass drum's reverb send from the sequencer:

1. On the TR-1000, press `[KNOB ASSIGN]`
2. Turn the BD `CTRL 1` knob to select it for editing
3. Assign `RVB SEND`, and set its minimum and maximum
4. From the Cirklon, **CC 25** (`BD CTRL1`) now drives the bass drum's reverb send

Up to four parameters per knob means BD, SD, LT and HT expose as many as twelve
assignable parameters each over MIDI; RS, HC, CH, OH, CC and RC have a single `Ctrl`,
so four.

### Track values are not step automation

The CCs declared in these `.cki` files land in the Cirklon's **track values** — the
sub-page reached by pressing `TRACK` while already on the TRACK page. Six slots per
row, up to 30 rows browsed with the ROW encoder, edited live with the six encoders.
They can be stored per SONG or SCENE and are re-sent when a song is recalled. Placing
steps in a pattern does **not** move them.

Per-step automation is a different mechanism: the P3 pattern's **aux rows**, four per
pattern (aux A to D), each assignable to any CC by holding the ROW encoder and turning
it one step. So four CCs can be automated per step, per pattern — not fourteen.

A step's aux flag is independent from its gate flag:

| Flag | Cirklon manual wording |
|------|------------------------|
| `gate` | *Trigger the note* |
| `aux A-D status` | *Trigger the associated CC or event* |

A CC can therefore be sent on a step whose gate is off — select the aux row before
pressing the step keys, and no note is emitted.

---

## Troubleshooting — CCs do nothing

Work through this list in order. Every point is sourced from the manuals.

### 1. `Rx Edit Data` must be ON

`MENU > SYSTEM > MIDI` (Reference Manual p. 47):

> *Rx Edit Data — OFF, ON — Specifies whether CC messages are received (ON) or are not.*

This single switch silences **every** CC at once. It is the first thing to check when
nothing responds at all. Its companion `Tx Edit Data` governs transmission, and
`Rx Program Change` governs kit recall — neither affects CC reception.

### 2. Half the CCs do nothing by design

These CCs are wired to knobs that control nothing out of the factory, or that need a
specific kit to be audible:

| CCs | Why they appear dead |
|-----|----------------------|
| 25, 26, 27 (BD Ctrl 1-3) | `[CTRL 1-3]`: *"Controls what is set with the [KNOB ASSIGN] button"* — nothing assigned by default |
| 46, 47, 48 (SD Ctrl 1-3) | same |
| 53, 54, 55 (LT Ctrl 1-3) | same |
| 60, 61, 62 (HT Ctrl 1-3) | same |
| 82, 86, 104, 108, 112, 116 (RS/HC/CH/OH/CC/RC Ctrl) | same |
| 24, 31, 52, 59 (BD/SD/LT/HT Mix) | `[MIX]`: *"Adjusts the mix balance for layers A/B"* — inaudible if the INST has no layer B loaded |

That is 4 out of 7 CCs on BD/SD/LT/HT and 1 out of 4 on the percussion voices.
`Tune`, `Decay` and `Level` are the ones that always respond. Assign the Ctrl knobs
via `[KNOB ASSIGN]` (see "Reaching them over MIDI" above) to bring the rest to life.

### 3. Turn MOTION off while testing

`MOTION [ON]`: *"If this is ON, knob operation data (MOTION) is played back"*. Recorded
knob motions replay continuously and overwrite incoming CC values. Switch it off before
concluding that a CC is dead.

### 4. Track values only send when you turn the encoder

Cirklon manual, ch. 9. A track value emits a CC when its encoder is turned, when the
value is re-sent (double-press the encoder), or when a SONG/SCENE that stored it is
recalled. Placing steps in a pattern never moves a track value — see "Track values are
not step automation" above.

### 5. Aux rows are not wired to these CCs

Cirklon manual 3-20:

> *In a new P3 pattern, the aux rows are assigned to some commonly used MIDI CC numbers.*

The CCs declared in these `.cki` files do **not** populate the aux rows. A fresh P3
pattern sends whatever CCs the Cirklon defaults to, which the TR-1000 ignores. Reassign
each aux row by holding the ROW encoder and turning it one step, then picking the CC.

### 6. Channel and port

The CCs travel on the Pattern Channel — `Pattern Ch.` in `MENU > SYSTEM > MIDI`,
*"the MIDI transmit/receive channel of the pattern sequencer"*, default 10. `Kit Ch.`
(default 1) is only *"the channel for program change messages that switch kits"* and
plays no part in CC reception. The `.cki` files use `midi_port: 1` — change it if the
TR-1000 hangs off another Cirklon output.

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
- [TR-1000 Reference Manual (Roland PDF)](https://static.roland.com/assets/media/pdf/TR-1000_reference_eng02_W.pdf) — source for KNOB ASSIGN, the MIXER parameters (RVB/DLY SEND, FX ROUTE) and the Mix / Ctrl knob descriptions
- [Roland Support — TR-1000 Owner's Manuals](https://www.roland.com/global/support/by_product/tr-1000/owners_manuals/)
- [Roland TR-1000 product page](https://www.roland.com/global/products/tr-1000/)
- [Cirklon Operation Manual v1.22 (Sequentix PDF)](https://cdn.shopify.com/s/files/1/0757/8429/0571/files/cirklon_operation_manual_1.22.pdf) — source for track values (ch. 9) and the aux row / gate flag distinction (ch. 3)

### Community

- [Roland TR-1000 MIDI CCs and NRPNs (midi.guide)](https://midi.guide/d/roland/tr-1000/)

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2026).
