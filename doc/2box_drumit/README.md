# 2Box DrumIt

Documentation for controlling the 2Box DrumIt electronic drum module with the Sequentix Cirklon.

## Overview

The 2Box DrumIt is an electronic drum module that responds to MIDI notes for triggering drum sounds. It supports multiple articulations per instrument (bow, edge, bell for cymbals; rim shots for toms and snare).

### MIDI Configuration

- **MIDI Channel**: 10 (GM Percussion standard)
- **MIDI Port**: OUT 4
- **Pattern Type**: CK (drum key mapping)

## Cirklon Instrument File

### `2box_drumit.cki` - CK Pattern Mode
**CK Pattern** on Channel 10 — 24 row definitions

#### Usage Mode
- **1 Cirklon track** controls the entire DrumIt module
- Note-triggered drum sounds with multiple articulations
- Notes C3 to G6 range
- Ideal for **drum sequencing** with articulation control

#### Track Values (4 CCs)

| Slot | CC | Label | Description |
|------|-----|-------|-------------|
| 1 | — | quant% | Quantization |
| 2 | — | leng% | Note length |
| 3 | CC 1 | HH Ped | Hi-Hat pedal position |
| 4 | CC 7 | Volume | Master volume |
| 5 | CC 10 | Pan | Stereo panning |
| 6 | CC 11 | Expr | Expression |

#### Key Mapping

| Note | Label | Instrument | Always Show |
|------|-------|-----------|-------------|
| C3 | Kick | Kick Drum | Yes |
| F3 | Snr | Snare | Yes |
| F#3 | SRim | Snare Rim | No |
| A3 | HHBw | Hi-Hat Bow | Yes |
| A#3 | HHEd | Hi-Hat Edge | No |
| B3 | HHFt | Hi-Hat Foot | No |
| D4 | Tom1 | Tom 1 | Yes |
| D#4 | T1Rm | Tom 1 Rim | No |
| F4 | Tom2 | Tom 2 | Yes |
| F#4 | T2Rm | Tom 2 Rim | No |
| A4 | Tom3 | Tom 3 | Yes |
| A#4 | T3Rm | Tom 3 Rim | No |
| C5 | Tom4 | Tom 4 | Yes |
| C#5 | T4Rm | Tom 4 Rim | No |
| E5 | C1Bl | Cymbal 1 Bell | Yes |
| F5 | C1Bw | Cymbal 1 Bow | No |
| F#5 | C1Ed | Cymbal 1 Edge | No |
| G5 | C1Ch | Cymbal 1 Choke | No |
| B5 | C2Bl | Cymbal 2 Bell | Yes |
| C6 | C2Bw | Cymbal 2 Bow | No |
| C#6 | C2Ed | Cymbal 2 Edge | No |
| D6 | C2Ch | Cymbal 2 Choke | No |
| E6 | C3Bl | Cymbal 3 Bell | Yes |
| F6 | C3Bw | Cymbal 3 Bow | No |
| F#6 | C3Ed | Cymbal 3 Edge | No |
| G6 | C3Ch | Cymbal 3 Choke | No |

**Primary rows** (always visible): Kick, Snare, HH Bow, Tom 1-4, Cymbal 1-3 Bell
**Secondary rows** (shown when needed): Rim shots, Edge/Foot/Choke articulations

---

## Instruments Detail

### Kick (C3)
Single articulation.

### Snare (F3-F#3)
- **F3**: Snare center hit
- **F#3**: Snare rim shot

### Hi-Hat (A3-B3)
- **A3**: Hi-Hat bow (standard hit)
- **A#3**: Hi-Hat edge
- **B3**: Hi-Hat foot close
- **CC 1 (HH Ped)**: Pedal position for open/closed control

### Toms 1-4 (D4-C#5)
Each tom has 2 articulations:
- Main hit (center)
- Rim shot

### Cymbals 1-3 (E5-G6)
Each cymbal has 4 articulations:
- **Bell**: Bell hit (primary)
- **Bow**: Bow hit (body)
- **Edge**: Edge hit
- **Choke**: Cymbal choke/mute

---

## Using with Cirklon

### Setup

1. **Load instrument**:
   - Copy `2box_drumit.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Assign to track**:
   - Create or select a track
   - Assign instrument `2BOXDRM`
   - MIDI channel: 10

3. **2Box Configuration**:
   - Ensure MIDI receive is enabled
   - MIDI channel: 10
   - Note mapping: GM standard

4. **Sequencing**:
   - Use the 10 primary rows for standard drum patterns
   - Add articulation rows as needed for detail
   - CC 1 for hi-hat pedal automation

### Workflow Tips

- Start with the `always_show` rows for basic patterns
- Add rim and edge articulations for more expressive beats
- Use **CC 1 (HH Ped)** to automate hi-hat open/close transitions
- Cymbal choke notes (C1Ch, C2Ch, C3Ch) are useful for tight arrangements

---

## Resources

### Official Documentation
- [2Box Drums Official Website](https://www.2box-drums.com/) - 2Box Official
- DrumIt Three/Five User Manual — included with device

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2025)
