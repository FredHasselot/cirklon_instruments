# Elektron Digitone II

Documentation for controlling the Elektron Digitone II with the Sequentix Cirklon.

## Overview

The Digitone II is an 8-voice FM synthesizer with 4 synth tracks, featuring multiple FM algorithms, wavetable synthesis, analog multi-mode filters, and powerful effects. Each track has its own synthesis engine with 4 synth pages, filter, amp, and 2 LFOs.

### MIDI Configuration

- **Track Channels**: 1-4 (one per synth track)
- **FX Channel**: 9 (global effects)
- **MIDI Port**: OUT 1

## Cirklon Instrument Files

Four configuration modes are provided:

### 1. `quad_ck_mode/digitone_ii.cki` - 4-Track CK Pattern Mode
**CK Pattern** with 64 control slots per track

#### Usage Mode
- **4 Cirklon tracks** for 4 synth voices
- Each track controls one DN2 synth track
- Ideal for **melodic/polyphonic** sequencing

#### Control Sections (per track):
- **Track Control** (slots 1-4): Quant%, Length%, Track Level, Track Mute
- **Trig Parameters** (slots 5-11): Note, Velocity, Length, Filter Trig, LFO Trig, Portamento Time/Enable
- **Synth Page 1** (slots 12-19): Parameters A-H (Algorithm, Ratios, etc.)
- **Synth Page 2** (slots 20-27): Parameters A-H
- **Synth Page 3** (slots 28-35): Parameters A-H
- **Synth Page 4** (slots 36-43): Parameters A-H
- **Filter** (slots 44-56): Frequency, Resonance, Type, Delay, ADSR, Depth, Reset, Key Track, Base, Width
- **Amp** (slots 57-64): Attack, Hold, Decay, Sustain, Release, Pan, Volume, Mode

#### Required DN2 Configuration
```
SETTINGS → MIDI CONFIG → CHANNELS
- Track 1 Channel: 1
- Track 2 Channel: 2
- Track 3 Channel: 3
- Track 4 Channel: 4
```

---

### 2. `drum_ck_mode/digitone_ii_drum.cki` - Drum Kit CK Pattern Mode
**CK Pattern** with 16 drum sounds on one track

#### Usage Mode
- **1 Cirklon track** controls a pseudo drum kit
- 16 aux notes mapped to drum sounds
- DN2 must be configured in **Multi Map** mode
- Ideal for **drum programming** with FM percussion

#### Drum Mapping:
```
C2  : Kick1    C#2 : Kick2    D2  : Snare1   D#2 : Snare2
E2  : Clap     F2  : Rim      F#2 : Tom1     G2  : Tom2
G#2 : CHH      A2  : OHH      A#2 : Cymbal1  B2  : Cymbal2
C3  : Perc1    C#3 : Perc2    D3  : Perc3    D#3 : Perc4
```

#### Required DN2 Configuration
```
SETTINGS → MIDI CONFIG → MULTI MAP
- Enable Multi Map mode
- Configure note ranges per track:
  - Track 1: C2-E2 (Kicks, Snares, Clap)
  - Track 2: F2-G2 (Rim, Toms)
  - Track 3: G#2-B2 (Hats, Cymbals)
  - Track 4: C3-D#3 (Percs)
```

---

### 3. `multi_p3_mode/digitone_ii_multi.cki` - P3 Multi-Timbral Mode
**P3 Pattern** with full CC control per track

#### Usage Mode
- **4 Cirklon tracks** for complete control
- All CC parameters available including LFOs
- Ideal for **studio/composition** and sound design

#### Control Sections (per track):
- **Synth Pages 1-4**: All 32 synth parameters (CC 40-77)
- **Filter**: Complete filter section with all parameters (CC 16-28)
- **Amp**: Full amp envelope and output (CC 84-92)
- **LFO 1**: Speed, Multiplier, Fade, Destination, Waveform, Phase, Trig Mode, Depth (CC 102-109)
- **LFO 2**: Speed, Multiplier, Fade, Destination, Waveform, Phase, Trig Mode, Depth (CC 111-118)
- **Track FX**: Bit Reduction, SRR, Overdrive, Sends (CC 29-31, 78-82)
- **Trig Controls**: Note, Velocity, Length, Portamento, Trigs (CC 3-14, 65)
- **Track Level/Mute** (CC 94-95)

---

### 4. `fx_p3_mode/digitone_ii_fx.cki` - Global FX P3 Mode
**P3 Pattern** for global effects control

#### Usage Mode
- **1 Cirklon track** controls all global FX
- Single instrument with all FX parameters
- Ideal for **effect automation** and mixing

#### Control Sections:
- **Chorus** (CC 9, 12-16, 70-72): Speed, Depth, HPF, Feedback, Width, Sends, Mix
- **Delay** (CC 21-28): Time, Pingpong, Width, Feedback, HPF, LPF, Reverb Send, Mix
- **Reverb** (CC 29-31, 89-92): Predelay, Decay, Frequency, Gain, HPF, LPF, Mix
- **Compressor** (CC 111-119): Threshold, Attack, Release, Makeup, Ratio, Sidechain Source/Filter, Mix, Pattern Volume

---

## Mode Comparison

| Criteria | Quad CK | Drum CK | Multi P3 | FX P3 |
|----------|---------|---------|----------|-------|
| **Cirklon Tracks** | 4 | 1 | 4 | 1 |
| **MIDI Channels** | 1-4 | 1 | 1-4 | 9 |
| **Use Case** | Melodic | Drums | Sound Design | Mixing |
| **LFO Control** | No | No | Yes | No |
| **FX Control** | No | No | Sends only | Full |
| **Complexity** | Medium | Simple | Advanced | Simple |

---

## Notable Parameters

### Synth Pages (CC 40-77)
The Digitone II has multiple synthesis engines. The 4 synth pages control different parameters depending on the selected engine:

**FM Tone**: Algorithm, Ratios, Harmonics, Detune, Feedback, Mix, Envelopes
**FM Drum**: Tune, Sweep, Algorithm, Waveforms, Feedback, Noise
**Wavetone**: Oscillators, Waveforms, Phase Distortion, Levels, Wavetables
**Swarmer**: Tune, Swarm parameters, Main oscillator, Animation

### Filter Types (CC 18)
Multiple filter architectures available:
- Multi-Mode (LP/HP/BP)
- Lowpass 4-pole
- Legacy LP/HP
- Comb+/Comb-
- Equalizer

### LFO Destinations (CC 105/114)
LFOs can be assigned to any parameter. Common destinations:
- Filter Frequency
- Amp Level
- Synth parameters
- Pan

---

## Using with Cirklon

### Basic Setup - Quad CK Mode

1. **Load instrument**:
   - Copy `quad_ck_mode/digitone_ii.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Create 4 Cirklon tracks**:
   - Assign `DN2-T1` to track 1 (MIDI Ch 1)
   - Assign `DN2-T2` to track 2 (MIDI Ch 2)
   - Assign `DN2-T3` to track 3 (MIDI Ch 3)
   - Assign `DN2-T4` to track 4 (MIDI Ch 4)

3. **Digitone II Configuration**:
   - SETTINGS → MIDI CONFIG → CHANNELS
   - Track 1-4 Channels: 1-4

### Drum Kit Setup

1. **Load instrument**:
   - Copy `drum_ck_mode/digitone_ii_drum.cki` to SD card
   - DISK → LOAD → INSTR

2. **Assign to track**:
   - Create a track, assign `DN2-DRM`
   - MIDI channel 1

3. **Digitone II Configuration**:
   - Enable Multi Map mode
   - Configure note ranges for each track
   - Create FM drum sounds on each track

4. **Sequencing**:
   - Use aux notes (C2-D#3) to trigger different drum sounds
   - All sounds on one CK pattern

### FX Automation Setup

1. **Load instrument**:
   - Copy `fx_p3_mode/digitone_ii_fx.cki` to SD card

2. **Assign to track**:
   - Create a P3 track, assign `DN2-FX`
   - MIDI channel 9

3. **Automate**:
   - Use P3 lanes to automate Delay, Reverb, Chorus, Compressor

---

## Recommended Workflows

### Live Performance (Quad CK + FX)
- **Tracks 1-4**: Synth sequences in CK mode
- **Track 5**: FX automation in P3 mode
- Real-time filter sweeps and effect manipulation

### Studio Production (Multi P3)
- **4 Cirklon tracks**: Full parameter control
- Detailed LFO and envelope automation
- Complex sound design with P3 lanes

### Drum Programming (Drum CK)
- **1 track**: Complete drum kit
- Quick FM percussion programming
- Easy pattern creation with aux notes

### Hybrid Workflow
Combine modes:
- **Tracks 1-4**: Multi P3 for synth voices
- **Track 5**: Drum CK for percussion
- **Track 6**: FX P3 for effects

---

## Resources

### Official Manuals
- [Digitone II User Manual](https://www.elektron.se/support-downloads/) - Check Elektron Support

### MIDI Implementation
- [MIDI CC/NRPN Database - midi.guide](https://midi.guide/d/elektron/digitone-ii/)

### Support & Community
- [Elektron Support - Digitone II](https://www.elektron.se/support-downloads/)
- [Elektronauts Forum - Digitone](https://www.elektronauts.com/c/digitone/50)

---

## Technical Notes

### Multi Map Mode
The Digitone II can be configured so each track responds to a specific range of MIDI notes. This allows using it as a pseudo drum machine where different notes trigger different tracks/sounds.

### FM Synthesis Control
The 4 synth pages (32 parameters) control the FM engine. Parameter meanings change based on the selected synthesis type (FM Tone, FM Drum, Wavetone, Swarmer).

### Effects Routing
- Track FX (Bit Reduction, SRR, Overdrive) are per-track
- Global FX (Chorus, Delay, Reverb) are controlled via sends (CC 29-31)
- Compressor affects the master output

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2025)
