# Elektron Analog Heat +FX

Documentation for controlling the Elektron Analog Heat +FX with the Sequentix Cirklon.

## Overview

The Analog Heat +FX is an analog effects processor with distortion, filters, modulation and digital effects (reverb, delay, chorus, etc.). It features over 100 parameters controllable via MIDI CC.

### MIDI Configuration

- **MIDI CH MAIN**: Channel 1 (default)
- **MIDI CH FX**: Channel 2 (default)
- **MIDI Port**: OUT 1

## Cirklon Instrument Files

Two `.cki` files are provided for complete control:

### 1. `analog_heat_fx.cki` - Main Controls (Channel 1)
**P3 Pattern** with 77 control slots

#### Sections:
- **Heat Character** (slots 3-9): Circuit, Drive, Level, Mix (14-bit)
- **Heat EQ** (slots 10-13): Low, High (14-bit)
- **Heat Filter** (slots 14-25): Mode, Frequency, Pan, Resonance, Dirt, Envelope, LFO1 (14-bit)
- **Envelope** (slots 26-37): Mode, Attack, Release, Trig Level, Base, Width, Destinations, Depths
- **LFO 1** (slots 38-46): Speed, Multiplier, Waveform, Phase, Destinations, Depths
- **LFO 2** (slots 47-55): Speed, Multiplier, Waveform, Phase, Destinations, Depths
- **LFO 3** (slots 56-64): Speed, Multiplier, Waveform, Phase, Destinations, Depths
- **CV/Expression** (slots 65-72): CV A/B and Expression A/B (Destinations and Depths)
- **Gate** (slots 73-76): Threshold, Hold, Release, Range
- **Volume** (slot 77): Preset Volume

### 2. `analog_heat_fx_effects.cki` - Effects (Channel 2)
**P3 Pattern** with 50 control slots

#### Sections:
- **Bits** (slots 3-6): SRR, BT, Filter, Mix
- **Chorus** (slots 7-12): Depth, Speed, Width, Mix (14-bit)
- **Delay** (slots 13-23): Time, Pingpong, Width, Feedback, HPF, LPF, Amount, Mode (14-bit)
- **Reverb** (slots 24-31): Pre-delay, Decay, Frequency, Gain, HPF, LPF, Amount, Mode
- **Compressor** (slots 32-38): Threshold, Attack, Release, Makeup Gain, Ratio, SC Filter, Mix
- **Warble** (slots 39-46): Mix, Depth, Speed, Base, Width, Stereo, Noise Level, Noise HPF
- **Bass Focus** (slots 47-50): X Freq, HP Level, LP Level, Bass

## Notable Parameters

### Heat Character - Circuit (CC 108)
8 analog distortion types:
- 0 : Clean Boost
- 1 : Saturation
- 2 : Enhance
- 3 : Mid Drive
- 4 : Rough Crunch
- 5 : Classic Distortion
- 6 : Round Fuzz
- 7 : High Gain

### Filter Mode (CC 30)
Filter modes:
- 1 : LP2 (Low Pass 2-pole)
- 3 : LP1 (Low Pass 1-pole)
- 5 : BP (Band Pass)
- 7 : HP1 (High Pass 1-pole)
- 9 : HP2 (High Pass 2-pole)
- 11 : BS (Band Stop)
- 13 : PK (Peak)
- 0-13 : Off

### LFO Waveforms (CC 66, 76, 86)
Available waveforms:
- 0 : Triangle
- 1 : Sine
- 2 : Square
- 3 : Saw
- 4 : Exponential
- 5 : Ramp
- 6 : Random

### Compressor Ratio (CC 24 - Channel 2)
Compression ratios:
- 0 : 1.50
- 1 : 2.00
- 2 : 3.00
- 3 : 4.00
- 4 : 6.00
- 5 : 8.00
- 6 : 16.00
- 7 : 20.00

### Mix Modes (Delay/Reverb)
- 0 : Send
- 1 : Return
- 2 : Mix

## 14-bit Control (MSB + LSB)

Several parameters use 14-bit control for precise resolution:
- Drive (CC 109 + 37)
- Level (CC 110 + 39)
- Mix (CC 111 + 40)
- EQ Low/High (CC 28+40, 29+42)
- Filter Frequency (CC 22 + 43)
- Filter Resonance (CC 23 + 44)
- LFO Depths (CC 73+34, 83+35, 93+36)
- Chorus Depth/Speed (CC 102+36, 103+37)
- Delay Time/Filters (CC 107+39, 111+40, 112+41)

## Using with Cirklon

### Basic Setup

1. **Load instruments**:
   - Copy `analog_heat_fx.cki` and `analog_heat_fx_effects.cki` to Cirklon's SD card
   - DISK → LOAD → INSTR

2. **Assign to tracks**:
   - Track 1: AH-FX (main controls)
   - Track 2: AH-EFX (effects)

3. **Analog Heat MIDI Configuration**:
   - SETTINGS → MIDI CONFIG → CHANNELS
   - MIDI CH MAIN: 1
   - MIDI CH FX: 2

### Recommended Workflow

#### Live Performance Setup
- **Track 1 (AH-FX)**: Tweak Drive, Mix, Filter Frequency in real-time
- **Track 2 (AH-EFX)**: Automate Delay Time, Reverb Amount, Chorus Mix

#### Advanced Automation
- Use LFOs to automatically modulate parameters
- Modulation destinations: see complete list in CC 18, 20, 72, 74, 84, 92, 94
- Depths are 14-bit controllable for smooth transitions

## Modulation Destinations

LFOs and Envelope can be routed to 112 different destinations, including:
- All Heat parameters (Drive, Level, Mix)
- Filter parameters (Frequency, Resonance, Dirt)
- Effects parameters (Delay, Reverb, Chorus, etc.)
- Modulation parameters (LFO Speed, Envelope Attack, etc.)

See complete destination list (0-112) in the source CSV.

## Resources

### Manuals
- [Analog Heat +FX User Manual (PDF)](https://www.elektron.se/wp-content/uploads/2024/09/Analog_Heat_FX_User_Manual_ENG_OS1.01_240325.pdf)

### MIDI Implementation
- [MIDI CC/NRPN Database](https://midi.guide/d/elektron/analog-heat-fx/)

### Elektron Support
- [Analog Heat +FX Support](https://www.elektron.se/support-downloads/analog-heat-fx)

## Technical Notes

### Centered Values
Some parameters have a "centered" value (0 = minimum, 64 = center, 127 = maximum):
- Filter Frequency Pan (CC 26)
- LFO Depths (CC 73, 83, 93)
- Chorus Depth/Speed (CC 102, 103)
- Bits Filter (CC 90)
- Delay Width (CC 109)
- CV/Expression Depths (CC 101, 103, 105, 107)
- Compressor SC Filter (CC 26 - Channel 2)

### Reverb Decay Time (CC 13 - Channel 2)
- 0-126: Variable decay time
- 127: Infinite (infinite reverb)

## Author

Configuration created for the Cirklon Instruments project by Fred Hasselot (2025)
