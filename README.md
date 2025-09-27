```
╔════════════════════════════════════════════════════════════════════════════════════════╗
║  (c) Fred Hasselot                                                            v0.1.18  ║
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
│   └── machinedrum_sps1_mk2+/    # Elektron Machinedrum definitions
│       ├── hybrid_mode/          # Hybrid approach (1 CK + 4 P3)
│       ├── pure_p3_mode/         # 16 individual P3 patterns
│       └── quad_ck_mode/         # 4 CK patterns approach
```

## Elektron Machinedrum SPS-1 MK2+

Three different approaches for controlling the Machinedrum from Cirklon:

### 1. Hybrid Mode (Recommended for versatility)
**Location:** `instruments/machinedrum_sps1_mk2+/hybrid_mode/`

- **MD-Hybrid-CK.cki** - Main CK pattern (sends on single MIDI channel, MD routes notes to all 16 tracks)
- **MD-CC-CH1.cki** - P3 pattern for Channel 1 CC automation (BD, SD, HT, MT)
- **MD-CC-CH2.cki** - P3 pattern for Channel 2 CC automation (LT, CP, RS, CB)
- **MD-CC-CH3.cki** - P3 pattern for Channel 3 CC automation (CH, OH, RC, CC)
- **MD-CC-CH4.cki** - P3 pattern for Channel 4 CC automation (M1, M2, M3, M4)

**Usage:** Load MD-Hybrid-CK on a CK track for playing/recording all 16 tracks (the MD internally routes notes to correct drums). Use the 4 P3 patterns for precise CC automation per channel group (CK patterns cannot send CC on multiple channels).

### 2. Pure P3 Mode (Maximum flexibility)
**Location:** `instruments/machinedrum_sps1_mk2+/pure_p3_mode/`

16 individual instrument definitions, one per Machinedrum track:
- MD-BD.cki through MD-M4.cki

**Usage:** Assign each .cki file to a separate Cirklon P3 track for complete individual control over each Machinedrum track.

### 3. Quad CK Mode (Best for live performance)
**Location:** `instruments/machinedrum_sps1_mk2+/quad_ck_mode/`

- **MD-CK-CH1.cki** - CK pattern for Channel 1 (BD, SD, HT, MT)
- **MD-CK-CH2.cki** - CK pattern for Channel 2 (LT, CP, RS, CB)
- **MD-CK-CH3.cki** - CK pattern for Channel 3 (CH, OH, RC, CC)
- **MD-CK-CH4.cki** - CK pattern for Channel 4 (M1, M2, M3, M4)

**Usage:** Use 4 Cirklon CK tracks, each controlling 4 Machinedrum tracks with full CC automation capability.

## Machinedrum MIDI Implementation Notes

The Machinedrum uses a unique MIDI implementation:
- 16 tracks are distributed across 4 MIDI channels
- Each channel controls 4 tracks
- CC numbers are reused across channels
- The MD internally routes incoming notes to the correct drum tracks
- CK patterns send on a single MIDI channel (cannot send CC on multiple channels)
- Channel 1: Tracks 1-4 (BD, SD, HT, MT)
- Channel 2: Tracks 5-8 (LT, CP, RS, CB)
- Channel 3: Tracks 9-12 (CH, OH, RC, CC)
- Channel 4: Tracks 13-16 (M1, M2, M3, M4)

## Installation

1. Copy the desired .cki files to your Cirklon's SD card
2. Load them via the Cirklon's instrument definition menu (DISK → LOAD → INSTR)
3. Assign to tracks as needed
4. **Configure your Machinedrum MIDI settings** - See [Documentation](doc/)

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
- [Machinedrum User Manual (PDF)](https://www.elektron.se/wp-content/uploads/2021/05/Machinedrum-User-Manual_ENG.pdf)

### Resources
- [Sequentix Official Website](https://www.sequentix.com)
- [Cirklon FAQ](https://www.sequentix.com/pages/faq)
- [Elektron Support](https://www.elektron.se/support/)

## License

MIT License - See [LICENSE](LICENSE) file for details