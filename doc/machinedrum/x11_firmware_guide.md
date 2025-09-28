# Machinedrum X.11 Firmware Installation Guide

## Introduction

This guide details the installation of the unofficial X.11 firmware for Elektron Machinedrum. This version brings numerous improvements and bug fixes while remaining 100% compatible with your existing data.

## ⚠️ Important Warning

- **Unofficial firmware**: Not supported by Elektron
- **Install at your own risk**: Though stable and used by thousands of users
- **Reversible**: You can always revert to official 1.63 version
- **Backup your data** before installation (patterns, kits, songs)

## Prerequisites

### Hardware
- Machinedrum (all models: SPS-1, UW, MK2, MK2+)
- MIDI interface connected to your computer
- Quality MIDI cable
- Stable power supply

### Software
- macOS, Windows or Linux
- SysEx utility (see below for your OS)

## Downloads

### Firmwares

1. **Official firmware 1.63** (backup just in case):
   - https://www.elektron.se/wp-content/uploads/2024/09/Elektron_SPS1-1UW_OS1.63.zip

2. **Unofficial firmware X.11**:
   - https://github.com/jmamma/MCL/releases/download/4.60/Machinedrum_SPS1-UW_OS_X.11.zip
   - Size: ~1.7 MB

### SysEx Tools

#### macOS
- **SysEx Librarian** (recommended): https://www.snoize.com/SysExLibrarian/
- **Elektron Transfer**: https://www.elektron.se/support-downloads/transfer

#### Windows
- **Elektron C6** : https://www.elektron.se/support-downloads/
- **MIDI-OX** : http://www.midiox.com/

#### Linux
- **amidi** (command line)
- **SysEx Librarian** via Wine

## Installation Procedure

### Step 1: Preparation

1. Create an "MD_Firmware" folder on your desktop
2. Download both firmwares (1.63 and X.11)
3. Unzip the archives
4. Verify the .syx files are present (~1.7 MB for X.11)
5. Install your chosen SysEx utility

### Step 2: Connection

1. Plug your Machinedrum into a stable power outlet (no sketchy power strips)
2. Connect MIDI cable: **MD MIDI IN** → **MIDI Interface OUT**
3. Do not power on the Machinedrum yet

### Step 3: Boot Mode

1. **Power on the Machinedrum while holding [FUNCTION]**
2. The Boot Menu appears on screen
3. **Press [5 LT]** to enter "MIDI Upgrade" mode
4. Screen displays "READY TO RECEIVE UPGRADE"

### Step 4: Sending the Firmware

#### With SysEx Librarian (macOS)

1. Open SysEx Librarian
2. Click "Add..." or drag the **Machinedrum_SPS1-UW_OS_X.11.syx** file
3. **IMPORTANT**: Select your MIDI interface in the "Destination" menu
4. Select the file in the list
5. Click "Play" or "Send"

#### With Elektron C6 (Windows)

1. Open C6
2. Configure your MIDI In/Out interface
3. Drag the .syx file into the window
4. Click "Send"

### Step 5: During Upload

- **Duration**: 5-10 minutes depending on interface speed
- **LEDs**: The 16 trig LEDs light up progressively (in cycles)
- **DO NOT**:
  - Power off the Machinedrum
  - Disconnect cables
  - Interrupt the transfer
  - Panic if it seems slow

### Step 6: Finalization

1. When transfer completes, the MD may reboot automatically
2. If it stays on "READY TO RECEIVE", power off and on normally
3. Check version: **GLOBAL → SYSTEM** → should display **"OS X.11"**

## New Features in X.11

### New Synthesis Machines

- **GND-SN-PRO**: Up to 4 sine oscillators
- **GND-SW**: Sawtooth/triangle with 3 variable oscillators
- **GND-PU**: Pulse wave with adjustable duty ratio

### New NFX Machines (Neighbor FX)

- **NFX-EV**: Envelope and ring modulation for neighbor tracks
- **NFX-CO**: Compression, side-chain and make-up gain
- **NFX-UC**: 2 universal comb filters (chorus, flanger, etc.)

### Improvements

- **Solo Mode**: In Mute menu, press ENTER to toggle
- **New LFO shapes**: Sine, reverse linear/exp, notch, step
- **Tonal tuning**: On GND, TRX and EFM machines
- **Improved MIDI**: Latency and jitter eliminated
- **Trigger groups**: Arbitrary trigger chaining

### Bug Fixes

- External MIDI sound no longer phase-inverted
- No more freeze with heavy CC MIDI stream
- Improved decay/noise sensitivity on TRX-S2
- Fixed parameter locks on first step

## Reverting to Official Version

If you want to revert to version 1.63:

1. Follow the same procedure
2. Use the **Elektron_SPS1-UW_OS1.63.syx** file
3. The Machinedrum will restore its official firmware

## Troubleshooting

### Upload doesn't start
- Check MIDI interface selection in SysEx Librarian
- Ensure MIDI cable is connected correctly
- Verify MD displays "READY TO RECEIVE"

### Upload interrupts
- Reduce transmission speed in preferences
- Use a shorter/better quality MIDI cable
- Avoid USB hubs, connect interface directly

### MD doesn't reboot
1. Power off and on manually
2. If problem persists, reinstall official 1.63
3. Check Elektronauts forum

## Resources

### Documentation
- **Complete X.11 README**: Included in firmware ZIP
- **Elektronauts Forum**: https://www.elektronauts.com/t/machinedrum-sps1-uw-x-11-released-unofficial/159097
- **ModWiggler**: https://www.modwiggler.com/forum/viewtopic.php?t=228441

### Community Support
- **Elektronauts**: Main forum for questions and support
- **GitHub Issues**: https://github.com/jmamma/MCL/issues
- **Facebook Group**: Elektron Machinedrum User Group

## Important Notes

- **MegaCommand not required**: X.11 works standalone on Machinedrum
- **Compatible all models**: MK1, MK2, UW, non-UW
- **Data preserved**: Your patterns, kits and samples are kept
- **Developers**: Yatao Li and Justin Mammarella (jmamma)

## Version History

- **1.63**: Last official Elektron version (2012)
- **X.04**: First major unofficial version (2020)
- **X.11**: Current version with NFX machines (2021)

---

*Guide created by Fred Hasselot - Successfully tested on Machinedrum MK2+*
*Last updated: January 2025*