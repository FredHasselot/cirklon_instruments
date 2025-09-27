# Machinedrum MIDI Configuration for Cirklon

## Quick Setup Guide

### Access MIDI Settings on Machinedrum

1. **Press FUNCTION + GLOBAL** to enter Global Settings
2. **Navigate to SLOT 4** (MIDI CONFIG)
3. **Press ENTER** to access MIDI configuration

### Required MIDI Settings

Configure the following parameters:

#### MIDI CHANNELS Section
- **BASE CHANNEL: 1**
  - This sets the base MIDI channel for note input
  - The Machinedrum automatically uses 4 consecutive channels from this base:
    - Channel 1: Tracks 1-4 (BD, SD, HT, MT)
    - Channel 2: Tracks 5-8 (LT, CP, RS, CB)
    - Channel 3: Tracks 9-12 (CH, OH, RC, CC)
    - Channel 4: Tracks 13-16 (M1, M2, M3, M4)

#### MIDI CONTROL Section
- **CONTROL IN: ALL** (or BASE CHAN)
  - Enables Control Change (CC) reception for parameter automation

- **PROG CHG IN: ON** (optional)
  - Enable if you want to change kits via MIDI Program Change

#### MIDI SYNC Section (optional)
- **CLOCK RECEIVE: ON**
  - If you want to sync tempo with Cirklon

- **TRANSPORT: ON**
  - If you want Cirklon to control MD start/stop

#### Performance Settings
- **TURBO SPEED: ON**
  - Improves MIDI response time
  - Found in GLOBAL → SLOT 5 (ROUTING)

- **OUT PORT FUNC: MIDI**
  - Set to MIDI (not THRU) for proper MIDI output
  - Found in GLOBAL → SLOT 5 (ROUTING)

### Verify Connection

1. Load **MD-Hybrid-CK** instrument on a Cirklon CK track
2. Set the Cirklon track to MIDI channel 1
3. Play notes C3 through D#4 on the Cirklon
4. You should trigger the corresponding Machinedrum tracks

### Troubleshooting

If no sound:
- Check MIDI cable connections (Cirklon OUT → MD IN)
- Verify BASE CHANNEL is set to 1 on both devices
- Ensure tracks are not muted on the Machinedrum
- Check that kit/sounds are loaded on MD tracks

### Using Different Modes

#### Hybrid Mode (Recommended)
- Use MD-Hybrid-CK on a CK track for triggering all 16 tracks
- Use MD-CC-CH1 through CH4 on P3 tracks for CC automation

#### Pure P3 Mode
- Requires BASE CHANNEL set to match your first P3 track
- Each MD track gets its own Cirklon track

#### Quad CK Mode
- Uses channels 1-4, one CK track per 4 MD tracks
- BASE CHANNEL must be 1

---

*Note: These settings are for Machinedrum SPS-1 MK2/MK2+ with OS 1.63 or later*