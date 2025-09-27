# Machinedrum MIDI CC Mapping Reference

## MIDI Channel Organization

The Machinedrum splits its 16 tracks across 4 MIDI channels:

| MIDI Channel | Tracks | Machine Names |
|--------------|--------|---------------|
| Channel 1 | 1-4 | BD, SD, HT, MT |
| Channel 2 | 5-8 | LT, CP, RS, CB |
| Channel 3 | 9-12 | CH, OH, RC, CC |
| Channel 4 | 13-16 | M1, M2, M3, M4 |

## Note Mapping

Each track responds to a specific MIDI note:

| Track | Machine | Note |
|-------|---------|------|
| 1 | BD (Bass Drum) | C3 |
| 2 | SD (Snare Drum) | C#3 |
| 3 | HT (High Tom) | D3 |
| 4 | MT (Mid Tom) | D#3 |
| 5 | LT (Low Tom) | E3 |
| 6 | CP (Clap) | F3 |
| 7 | RS (Rim Shot) | F#3 |
| 8 | CB (Cowbell) | G3 |
| 9 | CH (Closed Hat) | G#3 |
| 10 | OH (Open Hat) | A3 |
| 11 | RC (Ride Cymbal) | A#3 |
| 12 | CC (Crash Cymbal) | B3 |
| 13 | M1 (Machine 1) | C4 |
| 14 | M2 (Machine 2) | C#4 |
| 15 | M3 (Machine 3) | D4 |
| 16 | M4 (Machine 4) | D#4 |

## CC Mapping Structure

CC numbers are reused across channels. The same CC number controls different tracks depending on the MIDI channel:

### Track Position 1 (BD, LT, CH, M1)
- CC 8: Level
- CC 12: Mute
- CC 16-23: Parameters 1-8
- CC 24-25: AM Depth/Rate
- CC 26-27: EQ Freq/Gain
- CC 28-31: Freq/Width/Q/SR
- CC 32-36: Dist/Vol/Pan/DelSend/RevSend
- CC 37-39: Speed/Amount/Shape

### Track Position 2 (SD, CP, OH, M2)
- CC 9: Level
- CC 13: Mute
- CC 40-47: Parameters 1-8
- CC 48-49: AM Depth/Rate
- CC 50-51: EQ Freq/Gain
- CC 52-55: Freq/Width/Q/SR
- CC 56-60: Dist/Vol/Pan/DelSend/RevSend
- CC 61-63: Speed/Amount/Shape

### Track Position 3 (HT, RS, RC, M3)
- CC 10: Level
- CC 14: Mute
- CC 72-79: Parameters 1-8
- CC 80-81: AM Depth/Rate
- CC 82-83: EQ Freq/Gain
- CC 84-87: Freq/Width/Q/SR
- CC 88-92: Dist/Vol/Pan/DelSend/RevSend
- CC 93-95: Speed/Amount/Shape

### Track Position 4 (MT, CB, CC, M4)
- CC 11: Level
- CC 15: Mute
- CC 96-103: Parameters 1-8
- CC 104-105: AM Depth/Rate
- CC 106-107: EQ Freq/Gain
- CC 108-111: Freq/Width/Q/SR
- CC 112-116: Dist/Vol/Pan/DelSend/RevSend
- CC 117-119: Speed/Amount/Shape

## Parameter Details

### Parameters 1-8
Machine-specific parameters that vary depending on the selected drum machine/synthesis type.

### Common Parameters
- **Level**: Track volume
- **Mute**: Track mute on/off
- **AM Depth/Rate**: Amplitude modulation controls
- **EQ Freq/Gain**: Built-in EQ controls
- **Freq**: Base frequency/pitch
- **Width**: Stereo width
- **Q**: Filter resonance
- **SR**: Sample rate reduction
- **Dist**: Distortion amount
- **Volume**: Track volume (fine control)
- **Pan**: Stereo panning
- **DelSend**: Delay send amount
- **RevSend**: Reverb send amount
- **Speed/Amount/Shape**: LFO controls

## Usage Tips

1. **Channel Base Setting**: Set your Machinedrum's MIDI base channel in Global settings
2. **Multi-timbral Mode**: Enable for using multiple channels simultaneously
3. **CC Recording**: The Machinedrum can send CC data when tweaking knobs (enable in Global settings)
4. **Parameter Locks**: Internal sequencer p-locks don't transmit via MIDI

## Cirklon Integration

### CK Mode
- Best for recording performances with multiple tracks simultaneously
- Use multi-channel setup or separate CK patterns per channel

### P3 Mode
- Ideal for step-sequencing individual tracks
- Allows independent pattern lengths per track
- Perfect for detailed CC automation

### Hybrid Mode
- Combines CK for note triggering with P3 for CC automation
- Offers best of both worlds for complex arrangements