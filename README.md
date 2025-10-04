```
╔════════════════════════════════════════════════════════════════════════════════════════╗
║  (c) Fred Hasselot                                                            v0.1.22  ║
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

### Resources
- [Sequentix Official Website](https://www.sequentix.com)
- [Cirklon FAQ](https://www.sequentix.com/pages/faq)
- [Elektron Support](https://www.elektron.se/support/)

## License

MIT License - See [LICENSE](LICENSE) file for details