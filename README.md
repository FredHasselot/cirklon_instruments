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
│   ├── analog_heat_fx/           # Elektron Analog Heat +FX
│   ├── analog_rytm_mk2/          # Elektron Analog Rytm MKII
│   ├── digitone_ii/              # Elektron Digitone II
│   │   ├── multi_p3_mode/        # Synth tracks P3 (melodic)
│   │   ├── drum_p3_mode/         # FM Drum P3 (percussion)
│   │   └── fx_p3_mode/           # Global FX P3
│   ├── gr_mega/                  # Tasty Chips GR-Mega
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

Three modes for different workflows:

1. **Multi P3 Mode** - 4 synth tracks (sound design)
   - All CC parameters including LFOs
   - 85+ parameters per track
   - Ideal for pads, leads, bass

2. **Drum P3 Mode** - 8 FM drum tracks
   - Complete FM drum synthesis control
   - One instrument, 8 channels (1-8)
   - 55 parameters per track

3. **FX P3 Mode** - Global effects automation
   - Chorus, Delay, Reverb, Compressor
   - 32 effect parameters

⚠️ **Limitation**: Le Digitone II ne supporte pas le mode drum sur un seul canal MIDI (contrairement au Machinedrum ou Rytm). Chaque track nécessite son propre canal.

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

### 🎹 Additional Instruments
*More instrument definitions coming soon...*

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

### Resources
- [Sequentix Official Website](https://www.sequentix.com)
- [Cirklon FAQ](https://www.sequentix.com/pages/faq)
- [Elektron Support](https://www.elektron.se/support/)

## License

MIT License - See [LICENSE](LICENSE) file for details