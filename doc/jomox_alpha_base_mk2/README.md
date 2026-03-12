# Jomox Alpha Base MK2

Documentation for controlling the Jomox Alpha Base MK2 with the Sequentix Cirklon.

## Overview

The Alpha Base MK2 is an analog/digital hybrid drum machine featuring 11 instruments: analog kick, dual-membrane snare, 6 sample-based instruments with analog filters, 2 sample-only channels, and an FM synthesizer. All instruments are controllable via MIDI on independent channels.

### MIDI Configuration

- **Global Channel**: 16 (CK mode, key mapping for all instruments)
- **Individual Channels**: 1-11 (one per instrument)
- **MIDI Port**: OUT 1

## Cirklon Instrument Files

13 `.cki` files are provided:

### 1. `alpha_base_mk2.cki` - CK Pattern Mode
**CK Pattern** on Channel 16 — 44 row definitions

#### Usage Mode
- **1 Cirklon track** controls all 11 instruments
- Key mapping with **4 pitch variants** per instrument (+0, +6, +12, +18 semitones)
- Notes C1 to G4 (44 rows)
- Ideal for **live performance** and quick drumming

#### Instruments & Key Mapping

| Note Range | Instrument | Label |
|-----------|-----------|-------|
| C1 - D#1 | Kick Drum | KD, KD+6, KD12, KD18 |
| E1 - G1 | MBrane/Snare | MB, MB+6, MB12, MB18 |
| G#1 - B1 | Closed HiHat | CHH, CH+6, CH12, CH18 |
| C2 - D#2 | Open HiHat | OHH, OH+6, OH12, OH18 |
| E2 - G2 | Clap | CLP, CL+6, CL12, CL18 |
| G#2 - B2 | Rim Shot | RIM, RM+6, RM12, RM18 |
| C3 - D#3 | Crash | CRH, CR+6, CR12, CR18 |
| E3 - G3 | Ride | RID, RD+6, RD12, RD18 |
| G#3 - B3 | X1 Sample | X1, X1+6, X112, X118 |
| C4 - D#4 | X2 Sample | X2, X2+6, X212, X218 |
| E4 - G4 | FM Synth | FM, FM+6, FM12, FM18 |

---

### 2. P3 Multi-Channel Mode — 11 Individual Instruments

Each instrument has its own `.cki` file on its own MIDI channel with full CC automation:

| File | Instrument | Channel | CCs | Key Parameters |
|------|-----------|---------|-----|----------------|
| `AB-KD.cki` | Kick Drum | 1 | 19 | Tune, Pitch, Decay, Harmonics, Pulse, Noise, EQ, Comp, LFO |
| `AB-MB.cki` | MBrane/Snare | 2 | 25 | Dual membrane, Coupling, 2 LFOs |
| `AB-CHH.cki` | Closed HiHat | 3 | 28 | Sample engine, Filter (ADSR), VCA (ADSR), LFO |
| `AB-OHH.cki` | Open HiHat | 4 | 28 | Sample engine, Filter (ADSR), VCA (ADSR), LFO |
| `AB-CLP.cki` | Clap | 5 | 27 | Sample engine, Filter, VCA, LFO |
| `AB-RIM.cki` | Rim Shot | 6 | 27 | Sample engine, Filter, VCA, LFO |
| `AB-CRH.cki` | Crash | 7 | 27 | Sample engine, Filter, VCA, LFO |
| `AB-RID.cki` | Ride | 8 | 27 | Sample engine, Filter, VCA, LFO |
| `AB-X1.cki` | X1 Sample | 9 | 27 | Sample engine, Filter, VCA, LFO |
| `AB-X2.cki` | X2 Sample | 10 | 27 | Sample engine, Filter, VCA, LFO |
| `AB-FM.cki` | FM Synth | 11 | 35 | 4 operators, full FM matrix, polyphonic |

#### Common Parameters (Sample Instruments: CHH, OHH, CLP, RIM, CRH, RID, X1, X2)

- **Sample Engine**: Tune, Content, Start, Stop, Select, Loop
- **VCA Envelope**: Attack, Decay, Sustain, Release
- **Filter Envelope**: Attack, Decay, Sustain, Release
- **Filter**: Cutoff, Resonance, HP, Env Amount, Mod
- **Metallic Noise**: Level
- **LFO**: Waveform, Rate, Tune, VCA, Filter, Sync

#### Kick Drum (AB-KD) — Specific Parameters

- **Synthesis**: Tune, Pitch, Decay, Harmonics, Pulse, Noise
- **Shaping**: Attack, EQ, Compression, Gate
- **Noise**: Metallic Noise, Envelope Amount
- **LFO**: Waveform, Intensity, Rate

#### MBrane/Snare (AB-MB) — Specific Parameters

- **Dual Membrane**: Envelope 1 (Att/Dec/Amt/Damp), Envelope 2 (Att/Dec/Amt/Damp)
- **Coupling**: Membrane 1→2, Membrane 2→1
- **Pitch**: Independent pitch per membrane
- **2 LFOs**: Waveform, Intensity, Rate each

#### FM Synth (AB-FM) — Specific Parameters

- **4 Operators**: Tune, Envelope Attack, Envelope Decay, VCA, FM Amount (per operator)
- **FM Matrix**: Full 4×4 routing (12 cross-modulation paths: 1>2, 1>3, 1>4, 2>1, 2>3, 2>4, 3>1, 3>2, 3>4, 4>1, 4>2, 4>3)
- **Polyphonic**: Voices control (CC 30)
- **Note**: Responds to pitch (no `no_xpose`)

---

### 3. `AB-FX.cki` - Effects Global P3
**P3 Pattern** on Channel 16 — 40 parameters

#### Control Sections:

- **Reverb** (15 CCs):
  - Room, Low-Pass, Hi-Pass, Level (global)
  - Per-instrument sends: KD, MB, CH, OH, CLP, RIM, CRH, RID, X1, X2, FM

- **Delay** (15 CCs):
  - Time, Feedback, Spatial, Level (global)
  - Per-instrument sends: KD, MB, CH, OH, CLP, RIM, CRH, RID, X1, X2, FM

- **Pan** (10 CCs):
  - Per-instrument pan: MB, CH, OH, CLP, RIM, CRH, RID, X1, X2, FM

---

## Mode Comparison

| Criteria | CK Pattern | P3 Multi-Channel |
|---------|-----------|------------------|
| **Cirklon Tracks** | 1 | 11 (+1 FX) |
| **MIDI Channels** | 1 (CH16) | 11 (CH1-CH11) + CH16 FX |
| **CC Automation** | No | Yes (full per instrument) |
| **Pitch Variants** | 4 per instrument | Fixed note |
| **Live Performance** | Ideal | Advanced |
| **Studio/Composition** | Basic | Ideal |
| **Total Parameters** | 0 CC (note-only) | ~300+ CCs |

---

## Using with Cirklon

### Basic Setup — CK Pattern Mode

1. **Load instrument**:
   - Copy `alpha_base_mk2.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Assign to track**:
   - Create or select a track
   - Assign instrument `AB-MK2`
   - MIDI channel: 16

3. **Alpha Base Configuration**:
   - Global MIDI Channel: 16
   - Individual channels: 1-11

4. **Sequencing**:
   - Notes C1-G4 trigger instruments with pitch variants
   - `always_show` rows: KD, MB, CHH, OHH, CLP, RIM, CRH, RID, X1, X2, FM

### Advanced Setup — P3 Multi Mode

1. **Load all instruments**:
   - Copy all 13 `.cki` files to SD card
   - DISK → LOAD → INSTR

2. **Create 12 Cirklon tracks**:
   - Track 1 → `AB-KD` → Channel 1
   - Track 2 → `AB-MB` → Channel 2
   - Track 3 → `AB-CHH` → Channel 3
   - Track 4 → `AB-OHH` → Channel 4
   - Track 5 → `AB-CLP` → Channel 5
   - Track 6 → `AB-RIM` → Channel 6
   - Track 7 → `AB-CRH` → Channel 7
   - Track 8 → `AB-RID` → Channel 8
   - Track 9 → `AB-X1` → Channel 9
   - Track 10 → `AB-X2` → Channel 10
   - Track 11 → `AB-FM` → Channel 11
   - Track 12 → `AB-FX` → Channel 16

3. **Sequencing**:
   - Independent automation per instrument
   - Full CC control on each track
   - FX sends and panning on the FX track

---

## Notable Parameters

### Select Instrument (CC 64)
All P3 instruments include a `SelInst` parameter (CC 64) to select the active instrument on the Alpha Base front panel.

### FM Matrix Routing
The FM synth provides complete cross-modulation between all 4 operators:
```
OP1 → OP2 (CC 104)    OP2 → OP1 (CC 107)    OP3 → OP1 (CC 110)    OP4 → OP1 (CC 113)
OP1 → OP3 (CC 105)    OP2 → OP3 (CC 108)    OP3 → OP2 (CC 111)    OP4 → OP2 (CC 114)
OP1 → OP4 (CC 106)    OP2 → OP4 (CC 109)    OP3 → OP4 (CC 112)    OP4 → OP3 (CC 115)
```

### Reverb & Delay Sends
The FX instrument (AB-FX) provides per-instrument send levels for both Reverb and Delay, allowing independent effect routing for each of the 11 instruments.

---

## Resources

### Official Documentation
- [Jomox Alpha Base MK2 Product Page](https://www.jomox.de/alpha-base/) - Jomox Official
- Alpha Base MK2 MIDI Implementation — included with device

### Support & Community
- [Jomox Official Website](https://www.jomox.de/)
- [Jomox Support](https://www.jomox.de/support/)

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2025)
