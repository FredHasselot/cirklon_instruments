```
╔════════════════════════════════════════════════════════════════════════════════════════╗
║  (c) Fred Hasselot                                                               v0.8  ║
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

- **MD-Hybrid-CK.cki** - Main CK pattern for real-time performance (all 16 tracks via notes)
- **MD-CC-CH1.cki** - P3 pattern for Channel 1 CC automation (BD, SD, HT, MT)
- **MD-CC-CH2.cki** - P3 pattern for Channel 2 CC automation (LT, CP, RS, CB)
- **MD-CC-CH3.cki** - P3 pattern for Channel 3 CC automation (CH, OH, RC, CC)
- **MD-CC-CH4.cki** - P3 pattern for Channel 4 CC automation (M1, M2, M3, M4)

**Usage:** Load MD-Hybrid-CK on a CK track for playing/recording all 16 tracks in real-time. Use the 4 P3 patterns for precise CC automation per channel group.

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
- Channel 1: Tracks 1-4 (BD, SD, HT, MT)
- Channel 2: Tracks 5-8 (LT, CP, RS, CB)
- Channel 3: Tracks 9-12 (CH, OH, RC, CC)
- Channel 4: Tracks 13-16 (M1, M2, M3, M4)

## Installation

1. Copy the desired .cki files to your Cirklon's SD card
2. Load them via the Cirklon's instrument definition menu
3. Assign to tracks as needed

## Contributing

Feel free to submit pull requests with new instrument definitions or improvements to existing ones.

## Author

Fred Hasselot (2025)

## License

MIT License - See [LICENSE](LICENSE) file for details