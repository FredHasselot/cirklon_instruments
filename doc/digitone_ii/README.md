# Elektron Digitone II

Documentation for controlling the Elektron Digitone II with the Sequentix Cirklon.

## Overview

The Digitone II is an 8-voice FM synthesizer with 4 synth tracks (or 8 drum tracks), featuring multiple FM algorithms, wavetable synthesis, analog multi-mode filters, and powerful effects.

### MIDI Configuration

- **Synth Track Channels**: 1-4
- **Drum Track Channels**: 1-8
- **FX Channel**: 9
- **MIDI Port**: 1

### Limitation

**The Digitone II does NOT support drum mode on a single MIDI channel** (unlike Machinedrum or Analog Rytm). Each track requires its own MIDI channel. For 8 drums, you need 8 Cirklon tracks.

## Cirklon Instrument Files

Three configuration modes are provided:

### 1. `multi_p3_mode/digitone_ii_multi.cki` - Synth P3 Mode
**P3 Pattern** with full CC control per track

#### Usage Mode
- **4 Cirklon tracks** for 4 synth voices
- All CC parameters including LFOs
- Ideal for **melodic sequencing** and sound design

#### Control Sections (per track):
- **Synth Pages 1-4**: All 32 synth parameters (CC 40-77)
- **Filter**: Complete filter section (CC 16-28)
- **Amp**: Full amp envelope and output (CC 84-92)
- **LFO 1**: Speed, Multiplier, Fade, Destination, Waveform, Phase, Trig Mode, Depth (CC 102-109)
- **LFO 2**: Speed, Multiplier, Fade, Destination, Waveform, Phase, Trig Mode, Depth (CC 111-118)
- **Track FX**: Bit Reduction, SRR, Overdrive, Sends (CC 29-31, 78-82)
- **Trig Controls**: Note, Velocity, Length, Portamento (CC 3-14, 65)
- **Track Level/Mute** (CC 94-95)

#### Digitone II Configuration
```
SETTINGS → MIDI CONFIG → CHANNELS
- Track 1-4 Channel: 1-4
```

---

### 2. `drum_p3_mode/digitone_ii_drum_p3.cki` - FM Drum P3 Mode
**P3 Pattern** with FM drum synthesis parameters

#### Usage Mode
- **8 Cirklon tracks** for 8 drum voices
- One instrument, select channel 1-8 when assigning
- Complete FM drum synthesis control
- Ideal for **drum programming** with deep sound design

#### Control Sections:
- **FM Drum 1** (CC 40-47): Tune, Sweep Time/Depth, Algorithm, Waveforms, Feedback, Wave Fold
- **FM Drum 2** (CC 48-55): Ratio A/B, Decay A/B, End A/B, Mod A/B
- **FM Drum 3** (CC 56-63): Body Hold/Decay, Phase, Level, Noise Reset/Ring
- **FM Drum 4** (CC 70-77): Noise Hold/Decay, Transient, Noise Base/Width/Grain/Level
- **Filter** (CC 16-24): Frequency, Resonance, Type, ADSR, Depth
- **Amp** (CC 84-90): Attack, Hold, Decay, Sustain, Release, Pan, Volume
- **Sends** (CC 29-31): Chorus, Delay, Reverb
- **Track Level/Mute** (CC 94-95)

#### Digitone II Configuration
```
SETTINGS → MIDI CONFIG → CHANNELS
- Track 1-8 Channel: 1-8
```

---

### 3. `fx_p3_mode/digitone_ii_fx.cki` - Global FX P3 Mode
**P3 Pattern** for global effects control

#### Usage Mode
- **1 Cirklon track** controls all global FX
- Channel 9
- Ideal for **effect automation** and mixing

#### Control Sections:
- **Chorus** (CC 9, 12-14, 16, 70-72): Speed, Depth, HPF, Width, Sends, Mix
- **Delay** (CC 21-28): Time, Pingpong, Width, Feedback, HPF, LPF, Reverb Send, Mix
- **Reverb** (CC 29-31, 89-92): Predelay, Decay, Frequency, Gain, HPF, LPF, Mix
- **Master FX** (CC 78-82): Bit Reduction, SRR, Overdrive

---

## Mode Comparison

| Criteria | Multi P3 | Drum P3 | FX P3 |
|----------|----------|---------|-------|
| **Cirklon Tracks** | 4 | 8 | 1 |
| **MIDI Channels** | 1-4 | 1-8 | 9 |
| **Use Case** | Melodic/Sound Design | FM Drums | Mixing |
| **LFO Control** | Yes | No | No |
| **Complexity** | Advanced | Medium | Simple |

---

## Using with Cirklon

### Synth Setup (Multi P3)

1. **Load instrument**:
   - Copy `multi_p3_mode/digitone_ii_multi.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Create 4 Cirklon tracks**:
   - Assign `DN2-T1` to track 1 (MIDI Ch 1)
   - Assign `DN2-T2` to track 2 (MIDI Ch 2)
   - Assign `DN2-T3` to track 3 (MIDI Ch 3)
   - Assign `DN2-T4` to track 4 (MIDI Ch 4)

### Drum Setup (Drum P3)

1. **Load instrument**:
   - Copy `drum_p3_mode/digitone_ii_drum_p3.cki` to SD card

2. **Create 8 Cirklon tracks**:
   - Assign `DN2-DRM` to each track
   - Set MIDI channel 1-8 for each track

3. **Digitone II Configuration**:
   - Configure channels 1-8 for tracks 1-8

### FX Automation Setup

1. **Load instrument**:
   - Copy `fx_p3_mode/digitone_ii_fx.cki` to SD card

2. **Assign to track**:
   - Create a P3 track, assign `DN2-FX`
   - MIDI channel 9

---

## Recommended Workflows

### Studio Production
- **Tracks 1-4**: Multi P3 for synth voices with full LFO control
- **Tracks 5-12**: Drum P3 for 8 FM drum tracks
- **Track 13**: FX P3 for effect automation

### Live Performance
- **Tracks 1-4**: Synth sequences
- **Tracks 5-8**: Key drum sounds (4 drums max to save tracks)
- **Track 9**: FX automation

---

## Technical Notes

### FM Drum Synthesis
The Digitone II's FM drum engine provides 4 pages of parameters specifically designed for percussive sounds. Each drum track can be completely different - from kicks to cymbals - using FM synthesis.

### Effects Routing
- Track FX (Bit Reduction, SRR, Overdrive) are per-track
- Global FX (Chorus, Delay, Reverb) are controlled via sends (CC 29-31)
- FX track (channel 9) controls global effect parameters

### Limitation vs Other Elektron Machines
Unlike the Machinedrum or Analog Rytm, the Digitone II cannot receive multiple drum sounds on a single MIDI channel using different note numbers. Each track requires its own dedicated MIDI channel, making it less efficient for drum machine use with external sequencers.

---

## Resources

### Official Documentation
- [Elektron Support](https://www.elektron.se/support-downloads/)

### MIDI Implementation
- [MIDI CC Database - midi.guide](https://midi.guide/d/elektron/digitone-ii/)

### Community
- [Elektronauts Forum - Digitone](https://www.elektronauts.com/c/digitone/50)

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2025)
