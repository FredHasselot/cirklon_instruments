# Machinedrum Backup & Export Guide

## Quick Backup Methods

### Method 1: Using TM-1 (MIDI Interface)

The TM-1 is perfect for Machinedrum backup as it handles sysex data reliably.

#### Setup
1. Connect: **MD MIDI OUT → TM-1 MIDI IN**
2. Connect: **TM-1 → Mac via USB**
3. Open SysEx Librarian on Mac

#### Export Process

**Export EVERYTHING (Full Backup):**
1. On MD: **[GLOBAL] → [FILE] → [SEND] → [ALL]**
2. In SysEx Librarian: Click **Record**
3. On MD: Press **[YES]** to start
4. Wait for transfer (takes 2-3 minutes)
5. Save file as: `MD_Full_Backup_YYYY-MM-DD.syx`

**Export Individual Elements:**

**Single Kit:**
- **[GLOBAL] → [FILE] → [SEND] → [KIT]**
- Select kit number with encoder
- Press **[YES]**
- Save as: `MD_Kit_XX_name.syx`

**Single Pattern:**
- **[GLOBAL] → [FILE] → [SEND] → [PATTERN]**
- Select pattern (A01-H16)
- Press **[YES]**
- Save as: `MD_Pattern_A01.syx`

**Single Song:**
- **[GLOBAL] → [FILE] → [SEND] → [SONG]**
- Select song number
- Press **[YES]**
- Save as: `MD_Song_XX.syx`

**Global Settings:**
- **[GLOBAL] → [FILE] → [SEND] → [GLOBAL]**
- Saves all global settings
- Save as: `MD_Global.syx`

### Method 2: Using C6 (Windows/Old Mac)

If you have C6 working:
1. Set MIDI In/Out ports to TM-1
2. On MD: Navigate to send menu
3. In C6: Click **Receive**
4. On MD: Press **[YES]**
5. C6 automatically saves with timestamp

## File Organization

### Recommended Structure
```
MD_Backups/
├── Full_Backups/
│   ├── MD_Full_2025-01-28.syx
│   └── MD_Full_2025-01-15.syx
├── Kits/
│   ├── Drums/
│   │   ├── MD_Kit_01_808.syx
│   │   └── MD_Kit_02_909.syx
│   └── Synths/
│       └── MD_Kit_10_Bassline.syx
├── Patterns/
│   ├── Techno/
│   │   ├── MD_Pattern_A01_Kick.syx
│   │   └── MD_Pattern_A02_Full.syx
│   └── Ambient/
│       └── MD_Pattern_C01_Drone.syx
└── Songs/
    └── Live_Sets/
        └── MD_Song_01_Jan_Gig.syx
```

## TM-1 Specific Tips

### Why TM-1 is Great for MD
- Rock-solid sysex handling
- No driver issues on modern OS
- Class-compliant USB MIDI
- Fast transfer speed
- No data corruption

### TM-1 Settings for MD
- No special configuration needed
- Works immediately when connected
- Can handle largest sysex dumps

## Restore Process

### Full Restore
1. **BACKUP YOUR CURRENT DATA FIRST!**
2. On MD: **[GLOBAL] → [FILE] → [RECEIVE] → [ALL]**
3. MD shows: "READY TO RECEIVE"
4. In SysEx Librarian: Select your .syx file
5. Click **Play/Send**
6. Wait for completion
7. MD reboots automatically

### Individual Restore
- Kits load to current kit slot automatically
- Patterns overwrite selected pattern
- Songs load to selected song slot

## Important Notes

### What Gets Backed Up
- **ALL** includes:
  - All 64 kits
  - All 128 patterns
  - All 32 songs
  - Global settings
  - MIDI mappings

### What Doesn't Get Backed Up
- **UW Models**: Samples need separate backup
- Use MD's sample management for UW samples
- Firmware version (that's separate)

### File Sizes
- Full backup: ~300-500 KB
- Single kit: ~10 KB
- Single pattern: ~20 KB
- Single song: ~5 KB

## Troubleshooting

### Transfer Fails
- Check MIDI cables
- Verify TM-1 is selected in software
- Try slower transfer speed
- Ensure MD is in receive mode

### Corrupted Data
- Never disconnect during transfer
- Don't run other MIDI software simultaneously
- Use quality MIDI cables
- Keep backups of backups

## Pro Tips

### Regular Backup Schedule
- **Before each gig**: Full backup
- **After creative session**: Kit + Pattern backup
- **Weekly**: Full backup if actively using
- **Before firmware update**: ALWAYS full backup

### Naming Convention
```
MD_[Type]_[Number/Name]_[Date].syx

Examples:
MD_Full_2025-01-28.syx
MD_Kit_01_Punchy_2025-01-28.syx
MD_Pattern_A01_Techno_Loop.syx
```

### Quick Performance Backup
Before a show:
1. Export current song
2. Export used patterns (usually 10-20)
3. Export performance kits
4. Takes < 5 minutes total

### Share Your Work
- Export individual patterns/kits to share
- Include text file with:
  - BPM
  - Description
  - MD model (regular/UW)
  - Firmware version used

---

*Remember: The TM-1 makes this process bulletproof. No drivers, no hassle, just works!*