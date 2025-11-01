# Tasty Chips GR-Mega

Documentation for controlling the Tasty Chips GR-Mega granular synthesizer with the Sequentix Cirklon.

## Overview

The GR-Mega is a polyphonic granular synthesizer offering up to 20 simultaneous voices and 4 independent layers. It combines an advanced granular synthesis engine with a complete system of filters, envelopes, LFOs, modulation matrix, and effects.

### MIDI Configuration

- **MIDI Channel**: Configurable (1-16, default = 1)
- **Polyphony**: 1-20 voices (configurable via CC 23)
- **Layers**: 4 layers with independent MIDI channels
- **MIDI Port**: Configurable
- **NRPN Support**: 14-bit high-precision control available

## Cirklon Instrument File

### `gr_mega.cki` - P3 Polyphonic Mode
**P3 Pattern** with 117 control slots

#### Usage Mode
- **1 Cirklon track** to control one GR-Mega layer
- **Polyphony**: up to 20 simultaneous voices
- **Notes**: C0 to G8 (full range)
- Ideal for **melodic synthesis** and **granular sound design**

#### Control Sections:
- **Layer Configuration** (slots 3-5): ModWheel, Pitchbend Range, Focus & Enable Layer
- **Sub-Oscillator** (slots 6-7): Sub Pitch, Sub Amp
- **Granular Engine** (slots 8-18): Layer Vol, Position, Rate, Pan, Grain Size, Spray, Direction, Scan, Tune, M-S, Patch Volume
- **Synchronization** (slots 19-27): Grain/Scan Clock & Key Sync, Polyphony, Glide, Grain ARP Mode
- **Sample** (slots 28-33): Start/Stop/Loop Positions, Scan Mode
- **Sequencer** (slots 34-38): BPM, Rate, Position, Length, Mode
- **Audio** (slots 39-43): Recording Trigger, Record Sample, Dry/Wet Volumes
- **Grain Windowing** (slots 44-49): Sides, Tilt, Curve, AM, Type, Granular Mode
- **Filters** (slots 50-53): LPF/HPF Cutoff & Resonance
- **Envelopes** (slots 54-75): Pitch, Filter, Amp, Aux (complete ADSR)
- **Modulation Matrix** (slots 76-87): Row, Enable, Source, Curve, Amount, Polarity, Destination, CV1/CV2
- **LFO 1-4** (slots 88-106): Sync, Frequency, Wave, Amount, Destination (4 complete LFOs)
- **Effects** (slots 107-117): Focus, Type, Dry/Wet, FX1/FX2 Knobs & Values, Panic/Reset

#### Required GR-Mega Configuration
```
SETTINGS → MIDI
- Layer 1 MIDI Channel: 1 (or chosen channel)
- Receive Program Change: ON (optional)
- Receive MIDI Clock: ON (for sync)
```

---

## Main GR-Mega Sections

### Granular Engine

The heart of the GR-Mega is its granular synthesis engine that slices audio into micro-segments called "grains":

- **Position (CC 8)**: Playback position in the sample
- **Grain Size (CC 12)**: Grain size (0.1ms to 5s)
- **Rate/Density (CC 9)**: Grain rate or density depending on mode
- **Spray (CC 13)**: Position randomization
- **Scan (CC 15)**: Automatic scanning through the sample
- **Direction (CC 14)**: Forward/reverse playback probability

### Granular Modes (CC 49)

```
0: Free         - Free control of all parameters
1: DensitySize  - Density controls grain size
2: DensityRate  - Density controls rate
3: ScanRate     - Scan controls rate
4: ScanOverlap  - Scan controls overlap
```

### Grain Windowing

Two window types available (CC 48):

**RaisedCosine** (Type 0):
- **AM (CC 47)**: Amplitude modulation frequency

**PowAR** (Type 1):
- **Sides (CC 44)**: Side shape (square → triangle)
- **Tilt (CC 45)**: Tilt (left → center → right)
- **Curve (CC 46)**: Curvature (hollow → linear → bulging)

### Filter Architecture

- **LPF**: Low-pass filter with Cutoff (CC 50) and Resonance (CC 51)
- **HPF**: High-pass filter with Cutoff (CC 52) and Resonance (CC 53)
- **Routing (NRPN 293)**: LPF only / LPF+HPF / HPF
- **Bypass (NRPN 289)**: 0 = active, 1 = bypassed

### 4 ADSR Envelopes

Each envelope features:
- **Amount**: Modulation amount
- **Attack**: Attack time (0-45s)
- **Decay**: Decay time (0-45s)
- **Sustain**: Sustain level
- **Release**: Release time (0-45s)

**Destinations**:
1. **Pitch Envelope** (CC 54-58): Pitch modulation
2. **Filter Envelope** (CC 59-63): Filter modulation
3. **Amp Envelope** (CC 65-69): Amplitude modulation
4. **Aux Envelope** (CC 70-75): Assignable auxiliary envelope

### 4 Independent LFOs

Each LFO includes:
- **Clock Sync**: Free / MIDI / Sequencer
- **Frequency**: 0 Hz (stopped) to 50 Hz
- **Wave**: Sine, Triangle, Saw, -Saw, Square, Random
- **Amount**: Modulation amount
- **Destination**: Target parameter (see table)

### Modulation Matrix

50 programmable modulation slots:
- **Row (CC 76)**: Slot selection (0-49)
- **Enable (CC 77)**: Activation 0/1
- **Source (CC 78)**: 19 available sources
- **Curve (CC 79)**: Curve shape (flatline → linear → saturating)
- **Amount (CC 80)**: Intensity
- **Polarity (CC 81)**: +uni / -uni / +bi / -bi
- **Destination (CC 82)**: 91 possible destinations

### Effects

4 effects slots in chain:
- **Compressor**
- **Delay** / **Ping Pong Delay**
- **Distortion**
- **Reverb** / **Large Reverb**
- **Reducer** (bit reduction & sample rate reduction)

**Controls**:
- **Focus (CC 113)**: FX slot selection (0-3)
- **Type (CC 114)**: Effect type
- **Dry/Wet (CC 115/116)**: Effect balance
- **Knobs (CC 117/119)**: Assignable parameters

---

## 14-bit NRPN Control

The GR-Mega supports NRPN for maximum precision (16384 values instead of 128).

### Notable NRPN Parameters

| NRPN | Parameter | Range | Description |
|------|-----------|-------|-------------|
| 128 | Sequencer Record | 0/1 | Sequencer recording |
| 188-191 | LFO Phase | 0-16383 | Initial phase for LFOs 1-4 |
| 192-195 | LFO Amp Quantization | 0-16383 | LFO amplitude quantization |
| 196-199 | LFO Polarity | 0-3 | LFO polarity (+uni/-uni/+bi/-bi) |
| 210 | Anti-alias | 0/1 | Anti-aliasing on/off |
| 211 | Tape Slew | 0-16383 | Tape slew simulation |
| 249-280 | Effects | 0-16383 | High-precision FX parameters |
| 289 | Bypass Filter | 0/1 | Complete filter bypass |
| 291 | Rate Mode | 0-... | Grain rate mode |
| 293 | Filter Routing | 0-2 | LPF only / LPF+HPF / HPF |
| 294 | Input Level | 0-16383 | Audio input level |

### NRPN Format

To send an NRPN (example: Position with 14-bit precision):

```
CC 99 = NRPN MSB (upper 7 bits of CC number)
CC 98 = NRPN LSB (lower 7 bits of CC number)
CC 6  = Data MSB (high 7 bits of value)
CC 38 = Data LSB (low 7 bits of value)
```

Example for CC 8 (Position) = value 16181:
```
CC 99, 0    (8 >> 7 = 0)
CC 98, 8    (8 & 127 = 8)
CC 6, 126   (16181 / 128 = 126)
CC 38, 53   (16181 % 128 = 53)
```

---

## Using with Cirklon

### Basic Setup

1. **Load instrument**:
   - Copy `gr_mega.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Assign to track**:
   - Create or select a track
   - Assign instrument `GR-MEGA`
   - Configure MIDI channel (e.g., 1)

3. **GR-Mega Configuration**:
   - SETTINGS → MIDI
   - Layer MIDI Channel: 1 (or chosen channel)
   - MIDI Clock: ON (for sync)

4. **Sequencing**:
   - Melodic notes across full range C0-G8
   - Parameter automation via slots
   - Polyphony up to 20 voices (CC 23)

### Studio Workflow

#### Granular Sound Design
```
1. Load a sample into GR-Mega
2. Adjust Position (CC 8) and Grain Size (CC 12)
3. Set Spray (CC 13) for texture
4. Automate Scan (CC 15) for movement
5. Shape with Filter Envelope (CC 59-63)
6. Add LFO to Grain Size or Position
```

#### Polyphonic Synthesis
```
1. Configure Polyphony (CC 23): 3-8 voices
2. Set Glide (CC 24) for portamento
3. Use Pitch Envelope (CC 54-58)
4. Program melodic sequence
5. Automate filters in real-time
```

#### Evolving Textures
```
1. Granular Mode: ScanRate (CC 49 = 3)
2. LFO1 → Scan Speed (slow, ~0.1 Hz)
3. LFO2 → Filter Cutoff (medium, ~1 Hz)
4. Filter Envelope → Amount (for attack)
5. Large Reverb for space
```

### Live Workflow

#### Expressive Control
- **ModWheel (CC 1)**: Assignable in modulation matrix
- **Pitchbend**: Configurable range (CC 2, 0-48 semitones)
- **Aftertouch**: Channel & Poly supported
- **Glide (CC 24)**: For expressive transitions

#### Real-Time Automation
- **Slots 1-2**: Quant% and Leng% (rhythmic control)
- **Position + Spray**: Live texture variation
- **Filter Cutoff**: Classic tonal control
- **FX Wet/Dry**: Dynamic effect balance

#### Preset Changes
- **Program Change**: 128 presets (organized in banks)
  - PGM 0-7: Preset 1-8, Sub-bank 1, Bank 1
  - PGM 8-15: Preset 1-8, Sub-bank 2, Bank 1
  - ...

---

## Multi-Layer Architecture

The GR-Mega offers 4 independent layers on separate MIDI channels.

### Multi-Layer Configuration (NRPN)

```
NRPN 158: Layer 1 MIDI Channel (0-15 = channel 1-16)
NRPN 159: Layer 2 MIDI Channel
NRPN 160: Layer 3 MIDI Channel
NRPN 161: Layer 4 MIDI Channel

NRPN 175: Layer 1 Preset (0-127 = preset 1-128)
NRPN 176: Layer 2 Preset
NRPN 177: Layer 3 Preset
NRPN 178: Layer 4 Preset
```

### Multi-Layer Workflow with Cirklon

**Option A: 4 Cirklon tracks = 4 layers**
```
Track 1 → Channel 1 → Layer 1 (lead)
Track 2 → Channel 2 → Layer 2 (pad)
Track 3 → Channel 3 → Layer 3 (bass)
Track 4 → Channel 4 → Layer 4 (texture)
```

**Option B: Sequential control**
```
CC 3 (Focus Layer): 0=disable, 1=enable, 2=enable & focus
Switch between layers on a single Cirklon track
```

---

## Internal Sequencer

The GR-Mega integrates a 64-step sequencer with sync capabilities.

### Sequencer Parameters

| CC | Parameter | Range | Description |
|----|-----------|-------|-------------|
| 34 | BPM | 0-127 | Tempo (better in 14-bit NRPN) |
| 35 | Rate | 0-21 | Rhythmic division (see table) |
| 36 | Position | 0-63 | Current position (step 1-64) |
| 37 | Length | 0-63 | Sequence length (1-64) |
| 39 | Mode | 0-3 | Forward/Reverse/Pingpong/Random |

**NRPN 128**: Sequencer Record (0/1) - Recording

### Synchronization

**Grain Clock Sync (CC 19)**:
- 0: Free running
- ≥1: Synced

**Scan Clock Sync (CC 20)**:
- 0: Free
- ≥1: Synced

**LFO Sync (CC 88, 93, 102, 108)**:
- 0: Free
- 1: MIDI Clock
- 2: Sequencer

### MIDI Clock

GR-Mega receives MIDI Clock at 24 PPQN:
- **0xFA**: Start (position 0)
- **0xFB**: Continue
- **0xFC**: Stop
- **0xF8**: Clock pulse (24 per quarter note)

---

## Advanced Use Cases

### 1. Spectral Synthesis
```
Mode: Spectral (configure in GR-Mega)
Spray: Controls FFT block size
Position: Spectral scanning
Filter: Frequency sculpting
```

### 2. Granular Percussion
```
Grain Size: Very short (0.1-10ms)
Rate: High (dense)
Amp Envelope: Fast attack, short decay
Direction: Forward 100%
Mono mode (CC 23 = 0)
```

### 3. Ambient/Pad
```
Grain Size: Medium-long (100-500ms)
Spray: Moderate (texture)
Scan: Slow (movement)
LFO → Filter Cutoff
Large Reverb + long decay
Polyphony: 8-12 voices
```

### 4. Expressive Monophonic Lead
```
Polyphony: 0 (mono)
Glide: 50-100 (portamento)
Pitch Envelope: +1 octave, fast decay
Filter: LPF + Envelope
LFO → Vibrato (pitch, ~5Hz, low amount)
```

### 5. Granular Arpeggios
```
Grain ARP Mode (CC 27): Up/Down/Random
Grain Key Sync (CC 21): ON
Scan Key Sync (CC 22): Legato
Complex pattern via Cirklon sequencer
```

---

## Tips and Tricks

### CPU Optimization
- Reduce polyphony if CPU is high
- Bypass filters when not in use (NRPN 289)
- Disable anti-aliasing if needed (NRPN 210)

### Precise Control
- Use 14-bit NRPN for Position, Scan, Filter Cutoff
- Envelopes support custom curves (NRPN 156-173)
- Tape Slew (NRPN 211) adds analog inertia

### Complex Modulation
- Combine multiple LFOs on one destination
- Use Aux Envelope as modulation source
- CV1/CV2 for external inputs (Eurorack)

### Emergency
- **CC 120 (All Sound Off)**: MIDI panic (kills everything)
- **CC 121 (Reset CC)**: Reset received CCs
- **CC 123 (All Notes Off)**: Cuts notes (envelopes continue)

---

## Resources

### Official Manuals
- [GR-Mega User Manual](https://tastychips.nl/product/gr-mega/) - Official Tasty Chips site
- GR-Mega Manual 1.4 - MIDI Implementation (included with device)

### MIDI Support
- MIDI Command Table (see `midi_cc_reference.md`)
- Complete NRPN Implementation
- No SysEx currently (MTS planned)

### Community
- [Tasty Chips Support](https://tastychips.nl/support/)
- Granular synthesis forums
- GR-1/GR-Mega user groups

---

## Technical Notes

### MIDI vs Audio Precision
- **7-bit CC**: 128 values (sufficient for most uses)
- **14-bit NRPN**: 16384 values (near-audio precision)
- **Critical 14-bit parameters**: Position, Scan, Filter Cutoff

### MIDI Latency
GR-Mega has very low MIDI latency. For tight timing:
- Prefer MIDI Clock sync
- Use Key Sync for grains (CC 21)

### MPE Compatibility
GR-Mega supports MPE (MIDI Polyphonic Expression):
- **CC 74**: MPE Timbre MSB
- **CC 106**: MPE Timbre LSB
- Channel & Poly Aftertouch
- Per-note Pitchbend

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2025)

Based on GR-Mega Manual 1.4 by Tasty Chips Electronics
