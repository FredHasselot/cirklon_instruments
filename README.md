```
╔════════════════════════════════════════════════════════════════════════════════════════╗
║  (c) Fred Hasselot                                                            v0.1.25  ║
║  cirklon instruments definitions                                                       ║
║                                                                                        ║
║   ██████ ██ ██████  ██   ██ ██       ██████  ███    ██                                 ║
║  ██      ██ ██   ██ ██  ██  ██      ██    ██ ████   ██                                 ║
║  ██      ██ ██████  █████   ██      ██    ██ ██ ██  ██                                 ║
║  ██      ██ ██   ██ ██  ██  ██      ██    ██ ██  ██ ██                                 ║
║   ██████ ██ ██   ██ ██   ██ ███████  ██████  ██   ████                                 ║
║                                                                                        ║
║  ╔══════════════════════════════════════════════════════════════════════════════════╗  ║
║  ║                    INSTRUMENTS DEFINITIONS COLLECTION                            ║  ║
║  ╚══════════════════════════════════════════════════════════════════════════════════╝  ║
╚════════════════════════════════════════════════════════════════════════════════════════╝
```

# Cirklon Instruments Definitions

Collection of instrument definition files (.cki) for the Sequentix Cirklon hardware sequencer.

## Repository Structure

```
cirklon_instruments/
├── doc/                           # Documentation
├── instruments/                   # Instrument definitions
│   ├── 2box_drumit/              # 2Box DrumIt
│   ├── analog_heat_fx/           # Elektron Analog Heat +FX
│   ├── analog_rytm_mk2/          # Elektron Analog Rytm MKII
│   ├── digitone_ii/              # Elektron Digitone II
│   │   ├── multi_p3_mode/        # Synth tracks P3 (melodic)
│   │   └── fx_p3_mode/           # Global FX P3
│   ├── gr_mega/                  # Tasty Chips GR-Mega
│   ├── jomox_alpha_base_mk2/     # Jomox Alpha Base MK2
│   │   ├── alpha_base_mk2.cki   # CK pattern (all instruments)
│   │   ├── AB-KD/MB/CHH/...     # 11 P3 instruments
│   │   └── AB-FX.cki            # FX global P3
│   └── machinedrum_sps1_mk2+/    # Elektron Machinedrum definitions
│       ├── hybrid_mode/          # Hybrid approach (1 CK + 4 P3)
│       ├── pure_p3_mode/         # 16 individual P3 patterns
│       └── quad_ck_mode/         # 4 CK patterns approach
```

## Instrument Definitions

### 🥁 Elektron Machinedrum
**Location:** `instruments/machinedrum_sps1_mk2+/`

Three approaches for controlling the Machinedrum:

1. **Hybrid Mode** - 1 CK + 4 P3 patterns (recommended)
2. **Pure P3 Mode** - 16 individual P3 tracks (maximum control)
3. **Quad CK Mode** - 4 CK patterns (live performance)

📚 **[Full Machinedrum Documentation](doc/machinedrum/)**
- Firmware guides, MIDI setup, preset sharing, and more

### 🔥 Elektron Analog Heat +FX
**Location:** `instruments/analog_heat_fx/`

Two P3 patterns for complete control:

1. **analog_heat_fx.cki** - Main controls (Canal 1) - 77 parameters
   - Heat Character, EQ, Filter, Envelope, LFO 1/2/3, CV/Expression, Gate, Volume

2. **analog_heat_fx_effects.cki** - Effects (Canal 2) - 50 parameters
   - Bits, Chorus, Delay, Reverb, Compressor, Warble, Bass Focus

📚 **[Full Analog Heat +FX Documentation](doc/analog_heat_fx/)**
- MIDI implementation, 14-bit controls, modulation routing, and more

### 🥁 Elektron Analog Rytm MKII
**Location:** `instruments/analog_rytm_mk2/`

Two modes to adapt to your workflow:

1. **CK Pattern Mode** - Single Channel (recommended for live)
   - Global AR control via single MIDI channel
   - Sequence 12 tracks via notes C0-B0
   - ~67 parameters: Sample, Filter, Amp, LFO, FX, Performance

2. **P3 Multi-Timbral Mode** - 12 Channels (recommended for studio)
   - Independent control of each track
   - 12 P3 instances for total control
   - ~55 parameters per track

📚 **[Full Analog Rytm MKII Documentation](doc/analog_rytm_mk2/)**
- MIDI implementation, machine types, workflow examples, and more

### 🎹 Elektron Digitone II
**Location:** `instruments/digitone_ii/`

Two modes for different workflows:

1. **Synth P3 Mode** - 16 synth tracks (sound design)
   - All CC parameters including LFOs
   - 82 parameters per track
   - One instrument (DN2-SYN), select channel 1-16

2. **FX P3 Mode** - Global effects automation
   - Chorus, Delay, Reverb
   - 32 effect parameters

⚠️ **Limitation**: The Digitone II does not support drum mode on a single MIDI channel (unlike Machinedrum or Rytm). Each track requires its own channel.

📚 **[Full Digitone II Documentation](doc/digitone_ii/)**
- MIDI implementation, FM synthesis workflows, and more

### 🌊 Tasty Chips GR-Mega
**Location:** `instruments/gr_mega/`

P3 polyphonic pattern for granular synthesis:

- **gr_mega.cki** - Complete granular synthesis control (P3 Pattern)
  - 117 CC parameter slots
  - Granular engine: Position, Grain Size, Rate, Spray, Scan, Direction
  - 5 granular modes (Free, DensitySize, DensityRate, ScanRate, ScanOverlap)
  - Dual filters (LPF/HPF), 4 ADSR envelopes (Pitch, Filter, Amp, Aux)
  - 4 independent LFOs with sync
  - 50-slot modulation matrix
  - Effects chain (Compressor, Delay, Distortion, Reverb, Reducer)
  - 14-bit NRPN high-precision control
  - Multi-layer support (4 layers)
  - Up to 20 voices polyphony

📚 **[Full GR-Mega Documentation](doc/gr_mega/)**
- MIDI CC reference, NRPN implementation, granular workflows, and more

### 🥁 Jomox Alpha Base MK2
**Location:** `instruments/jomox_alpha_base_mk2/`

Two modes for different workflows:

1. **CK Pattern Mode** - Global Channel (CH16)
   - All 11 instruments on single channel via key mapping
   - 4 pitch variants per instrument (+0, +6, +12, +18 semitones)
   - 44 row definitions total
   - Ideal for live drumming

2. **P3 Multi-Channel Mode** - Individual Channels (CH1-CH11)
   - 11 independent P3 instruments, one per MIDI channel
   - Full CC automation per instrument:
     - **AB-KD** (CH1): Kick Drum - 19 CCs (Tune, Pitch, Decay, Harmonics, Pulse, Noise, EQ, Compression, LFO)
     - **AB-MB** (CH2): MBrane/Snare - 25 CCs (Dual membrane, Coupling, 2 LFOs)
     - **AB-CHH** (CH3): Closed HH - 28 CCs (Sample engine, Filter, VCA ADSR, LFO)
     - **AB-OHH** (CH4): Open HH - 28 CCs
     - **AB-CLP** (CH5): Clap - 27 CCs
     - **AB-RIM** (CH6): Rim Shot - 27 CCs
     - **AB-CRH** (CH7): Crash - 27 CCs
     - **AB-RID** (CH8): Ride - 27 CCs
     - **AB-X1** (CH9): X1 Sample - 27 CCs
     - **AB-X2** (CH10): X2 Sample - 27 CCs
     - **AB-FM** (CH11): FM Synth - 35 CCs (4 operators, full FM matrix, polyphonic)

3. **FX Global P3** - Effects Channel (CH16)
   - **AB-FX**: Reverb (15 CCs) + Delay (15 CCs) + Pan (10 CCs) = 40 parameters

📚 **[Full Jomox Alpha Base MK2 Documentation](doc/jomox_alpha_base_mk2/)**
- MIDI implementation, FM matrix, instrument details, and more

### 🥁 2Box DrumIt
**Location:** `instruments/2box_drumit/`

CK pattern for electronic drum module:

- **2box_drumit.cki** - Complete drum kit (Channel 10, GM standard)
  - 24 row definitions across 10 instruments
  - Multiple articulations: Bow, Edge, Bell, Rim, Choke
  - Hi-Hat pedal control (CC 1)
  - 4 track values: HH Pedal, Volume, Pan, Expression

📚 **[Full 2Box DrumIt Documentation](doc/2box_drumit/)**
- Key mapping, articulations, and setup guide

## Installation

1. Copy the desired .cki files to your Cirklon's SD card
2. Load them via the Cirklon's instrument definition menu (DISK → LOAD → INSTR)
3. Assign to tracks as needed
4. Configure your hardware MIDI settings as needed


## Documentation & Community

📚 **[View Full Documentation](doc/)**

### Contributing

We welcome contributions from the Cirklon community!

- **Documentation improvements**: Help us clarify and expand our guides
- **New instrument definitions**: Share your creations
- **Bug reports & discussions**: [Open an issue](https://github.com/FredHasselot/cirklon_instruments/issues)
- **Questions about track_values**: See [Track Values Limitations](doc/track_values_limitations.md) and help us understand

The best way to contribute is through GitHub Issues where you can reference specific documentation and discuss with other users.

## Author

Fred Hasselot (2025)

Created for [Patrick Pattern](https://soundcloud.com/patrick-packard) productions.

## Documentation

### Manuals
- [Cirklon Operation Manual v1.20 (PDF)](http://files.sequentix.com/cirklon-manual-1.20.pdf)
- [Machinedrum User Manual (PDF)](https://www.elektron.se/wp-content/uploads/2024/09/machinedrum_manual_OS1.63_1.pdf)
- [Analog Heat +FX User Manual (PDF)](https://www.elektron.se/wp-content/uploads/2024/09/Analog_Heat_FX_User_Manual_ENG_OS1.01_240325.pdf)
- [Analog Rytm MKII User Manual (PDF)](https://elektron-software.s3.eu-west-1.amazonaws.com/firmware/Analog+Rytm+MKII+User+Manual_ENG_OS1.70_231122.pdf)
- [Digitone II User Manual](https://www.elektron.se/support-downloads/) - Elektron Support
- [GR-Mega Product Page](https://tastychips.nl/product/gr-mega/) - Tasty Chips Electronics
- [Jomox Alpha Base MK2](https://www.jomox.de/alpha-base/) - Jomox Official
- [2Box Drums](https://www.2box-drums.com/) - 2Box Official

### Resources
- [Sequentix Official Website](https://www.sequentix.com)
- [Cirklon FAQ](https://www.sequentix.com/pages/faq)
- [Elektron Support](https://www.elektron.se/support/)

## License

MIT License - See [LICENSE](LICENSE) file for details