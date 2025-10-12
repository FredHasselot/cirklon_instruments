# Elektron Analog Rytm MKII

Documentation for controlling the Elektron Analog Rytm MKII with the Sequentix Cirklon.

## Overview

The Analog Rytm MKII is an 8-voice analog drum machine with integrated sampler, offering 12 controllable tracks via MIDI. Each voice features an analog synthesis engine, sample playback, analog multi-mode filter, envelopes, and an assignable LFO.

### MIDI Configuration

- **Auto Channel**: Configurable channel (default = 10)
- **Track Channels**: Channels 1-12 (one channel per track)
- **MIDI Port**: OUT 1

## Cirklon Instrument Files

Two `.cki` files are provided to adapt to your workflow:

### 1. `analog_rytm_mk2.cki` - CK Pattern Mode
**CK Pattern** with 67 control slots

#### Usage Mode
- **1 Cirklon track** controls the entire Analog Rytm
- Notes **C0 to B0** (MIDI 36-47) trigger tracks 1-12
- All CCs affect the **active/selected track** in the AR
- Ideal for **live performance** and quick sequencing

#### Control Sections:
- **Track Control** (slots 3-7): Track Level, Mute, Solo, Machine Type, Scene
- **Trig Parameters** (slots 8-13): Velocity, Length, Synth/Sample Levels, Envelope/LFO Amounts
- **Sample Player** (slots 14-21): Tune, Fine, Bit Reduction, Slot, Start, End, Loop, Level
- **Filter** (slots 22-29): ADSR Envelope, Frequency, Resonance, Type, Envelope Depth
- **Amp** (slots 30-34): Volume, AHD Envelope, Overdrive
- **LFO** (slots 35-39): Speed, Multiplier, Fade, Destination, Depth (14-bit LSB)
- **FX - Compressor** (slots 40-44): Threshold, Ratio, Attack, Release, Makeup
- **FX - Delay** (slots 45-47): Time, Feedback, Level
- **FX - Reverb** (slots 48-51): Pre-Delay, Decay, Frequency, Level
- **Performance** (slots 52-63): 12 Performance Knobs (assignable)
- **Synth** (slots 64-67): 4 generic machine parameters

#### Required AR Configuration
```
SETTINGS → MIDI CONFIG → CHANNELS
- Auto Channel: 10 (or chosen channel)
- Track 1-12 Channels: Can remain on 1-12
- OUTPUT CH: Auto Channel
```

---

### 2. `analog_rytm_mk2_multi.cki` - P3 Multi-Timbral Mode
**P3 Pattern** with 55 control slots per track

#### Usage Mode
- **12 Cirklon tracks** for independent control
- Each track controls **one specific track** of the AR
- Simultaneous control of all tracks
- Independent automation per track
- Ideal for **studio/composition** and total control

#### Control Sections (per track):
- **Trig Controls** (slots 3-9): Note, Velocity, Length, Synth/Sample Levels, Envelope/LFO Amounts
- **Sample** (slots 10-17): Tune, Fine, Bit Reduction, Slot, Start, End, Loop, Level
- **Filter** (slots 18-25): ADSR Envelope, Frequency, Resonance, Type, Envelope Depth
- **Amp** (slots 26-30): Volume, AHD Envelope, Overdrive
- **LFO** (slots 31-35): Speed, Multiplier, Fade, Destination, Depth (14-bit)
- **Synth Machine** (slots 36-40): Machine Type, 4 specific parameters
- **Track Level** (slots 41-43): Track Level, Mute, Solo
- **Performance** (slots 44-55): 12 Performance Knobs

#### Required AR Configuration
```
SETTINGS → MIDI CONFIG → CHANNELS
- Track 1 Channel: 1
- Track 2 Channel: 2
- ...
- Track 12 Channel: 12
- OUTPUT CH: Track Channel
```

#### Cirklon Configuration
- Create 12 tracks in the Cirklon
- Assign the `AR-Multi` instrument to each track
- Configure the MIDI channel of each track (1-12)
- Each Cirklon track = 1 Analog Rytm track

---

## Mode Comparison

| Criteria | CK Pattern | P3 Multi-Timbral |
|---------|-----------|------------------|
| **Cirklon Tracks** | 1 | 12 |
| **MIDI Channels** | 1 (Auto Channel) | 12 (Track Channels) |
| **Simultaneous Control** | No (active track) | Yes (all tracks) |
| **Live Performance** | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| **Studio/Composition** | ⭐⭐⭐ | ⭐⭐⭐⭐⭐ |
| **Complexity** | Simple | Advanced |
| **Slots** | 67 | 55 × 12 = 660 |

---

## Notable Parameters

### Machine Types (CC 15)
Each track can load a different machine type from 11 analog machines:
- **BD** (Bass Drum) - Hard/Classic
- **SD** (Snare Drum) - Hard/Classic/FM
- **RS** (Rim Shot) - Hard/Classic
- **CP** (Clap) - Classic
- **BT/LT/MT/HT** (Toms) - Hard/Classic
- **CH/OH** (Hi-Hats) - Classic
- **CY** (Cymbal) - Classic/Ride
- **CB** (Cowbell) - Classic

### Filter Types (CC 76)
```
0-15   : LP2 (Low Pass 2-pole)
16-31  : LP1 (Low Pass 1-pole)
32-47  : BP (Band Pass)
48-63  : HP1 (High Pass 1-pole)
64-79  : HP2 (High Pass 2-pole)
80-95  : BS (Band Stop/Notch)
96-127 : Peak
```

### Active Scenes (CC 92)
```
0-31   : Scene A
32-63  : Scene B
64-95  : Scene C
96-127 : Scene D
```

### 14-bit Control
The **LFO Depth** parameter uses 14-bit control for maximum precision:
- **CC 105**: MSB (Most Significant Byte)
- **CC 118**: LSB (Least Significant Byte)

---

## Using with Cirklon

### Basic Setup - CK Pattern Mode

1. **Load instrument**:
   - Copy `analog_rytm_mk2.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Assign to track**:
   - Create or select a track
   - Assign instrument `AR-MK2`
   - Configure MIDI channel (e.g., 10)

3. **Analog Rytm Configuration**:
   - SETTINGS → MIDI CONFIG → CHANNELS
   - Auto Channel: 10
   - OUTPUT CH: Auto Channel

4. **Sequencing**:
   - Notes C0-B0 trigger tracks 1-12
   - Parameter automation via slots

### Advanced Setup - P3 Multi Mode

1. **Load instrument**:
   - Copy `analog_rytm_mk2_multi.cki` to SD card
   - DISK → LOAD → INSTR

2. **Create 12 Cirklon tracks**:
   - Assign `AR-Multi` to each track
   - Track 1 → MIDI Channel 1
   - Track 2 → MIDI Channel 2
   - ...
   - Track 12 → MIDI Channel 12

3. **Analog Rytm Configuration**:
   - Track 1 Channel: 1
   - Track 2 Channel: 2
   - ...
   - Track 12 Channel: 12
   - OUTPUT CH: Track Channel

4. **Sequencing**:
   - Each Cirklon track controls one AR track
   - Independent automation per track

---

## Recommended Workflows

### Live Performance Workflow (CK Pattern)
- **Cirklon Track 1**: Complete drum sequence
- Real-time FX automation (Delay, Reverb)
- Scene changes (A/B/C/D) for variations
- Filter and LFO tweaking during sets

### Studio Workflow (P3 Multi)
- **12 Cirklon tracks**: Total control
- Precise automation per track
- Complex pattern recording
- Independent LFO modulation per voice
- Different effects and filters per track

### Hybrid Workflow
Combine both approaches:
- **Tracks 1-8**: Multi mode for 8 main voices
- **Track 9**: CK mode for global FX and scenes
- Best of both worlds!

---

## Resources

### Official Manuals
- [Analog Rytm MKII User Manual (PDF)](https://elektron-software.s3.eu-west-1.amazonaws.com/firmware/Analog+Rytm+MKII+User+Manual_ENG_OS1.70_231122.pdf) - OS 1.70
- [Quick Guide (PDF)](https://www.elektron.se/wp-content/uploads/2024/09/AnalogRytmMKIIQuickGuide_ENG_231122.pdf)

### MIDI Implementation
- [MIDI CC/NRPN Database - midi.guide](https://midi.guide/d/elektron/analog-rytm-mkii/)
- [Complete MIDI CC Reference](midi_cc_reference.md)

### Support & Community
- [Elektron Support - Analog Rytm MKII](https://www.elektron.se/support-downloads/analog-rytm-mkii)
- [Elektronauts Forum - Analog Rytm](https://www.elektronauts.com/c/analog-rytm/52)

---

## Technical Notes

### Auto Channel vs Track Channels
The Analog Rytm offers two distinct MIDI modes:

**Auto Channel**: All MIDI messages are received on a single channel. Notes C0-B0 trigger tracks 1-12. CCs affect the currently selected/active track in the AR.

**Track Channels**: Each track listens on its own MIDI channel. Allows simultaneous and independent control of all tracks.

### Performance Knobs (CC 35-47)
The 12 Performance Knobs are assignable in the Analog Rytm to any parameter of any track. They offer quick, customizable control during performances.

### Synth Parameters (CC 106-109)
These 4 CCs correspond to specific parameters of each synthesis machine. The exact mapping depends on the selected machine type (BD, SD, RS, etc.). Refer to the AR manual for complete details per machine.

---

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2025)
