# Elektron Digitone II

Documentation for controlling the Elektron Digitone II with the Sequentix Cirklon.

## Overview

The Digitone II is a 16-voice FM synthesizer with 16 tracks, featuring multiple FM algorithms, wavetable synthesis, analog multi-mode filters, and powerful effects.

### MIDI Configuration

- **Synth Track Channels**: 1-16
- **FX Channel**: configurable
- **MIDI Port**: 1

### Limitation

**The Digitone II does NOT support drum mode on a single MIDI channel** (unlike Machinedrum or Analog Rytm). Each track requires its own MIDI channel.

## Cirklon Instrument Files

Two configuration modes are provided:

### 1. `multi_p3_mode/digitone_ii_multi.cki` - Synth P3 Mode
**P3 Pattern** with full CC control per track

#### Usage Mode
- **1 instrument (DN2-SYN)**, select channel 1-16 when assigning
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
- Track 1-16 Channel: 1-16
```

---

### 2. `fx_p3_mode/digitone_ii_fx.cki` - Global FX P3 Mode
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

| Criteria | Synth P3 | FX P3 |
|----------|----------|-------|
| **Cirklon Tracks** | 1-16 | 1 |
| **MIDI Channels** | 1-16 | configurable |
| **Use Case** | Melodic/Sound Design | Mixing |
| **LFO Control** | Yes | No |
| **Complexity** | Advanced | Simple |

---

## Using with Cirklon

### Synth Setup (Multi P3)

1. **Load instrument**:
   - Copy `multi_p3_mode/digitone_ii_multi.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Create Cirklon tracks**:
   - Assign `DN2-SYN` to each track
   - Set MIDI channel 1-16 for each track

### FX Automation Setup

1. **Load instrument**:
   - Copy `fx_p3_mode/digitone_ii_fx.cki` to SD card

2. **Assign to track**:
   - Create a P3 track, assign `DN2-FX`
   - MIDI channel 9

---

## Recommended Workflows

### Studio Production
- **Tracks 1-16**: DN2-SYN for synth voices with full LFO control
- **Track 17**: FX P3 for effect automation

### Live Performance
- **Tracks 1-8**: Synth sequences
- **Track 9**: FX automation

---

## Technical Notes

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
