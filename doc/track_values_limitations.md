# Track Values and Automation Limitations on Cirklon P3 Patterns

## Current Understanding (TO BE CONFIRMED BY COMMUNITY)

This document outlines our current understanding of track value limitations on the Sequentix Cirklon. **We are seeking confirmation and clarification from experienced Cirklon users.**

### Track Values Configuration

Track values allow pre-mapping of MIDI CC parameters to P3 pattern slots. In our instrument definitions, we have configured up to 81 track value slots per instrument, mapping comprehensive CC control for the Machinedrum.

Example: MD-CC-CH1 contains 81 slots:
- Slots 1-2: Track controls (quant%, leng%)
- Slots 3-26: BD parameters (24 CCs)
- Slots 27-50: SD parameters (24 CCs)
- Slots 51-74: HT parameters (24 CCs)
- Slots 75-81: MT parameters (partial)

### Automation Limitations

Based on our research of the manual, we understand the following limitations:

#### Per-Track Automation Limit
- **4 simultaneous automations per P3 track** via AUX A, B, C, D channels
- Even with 81 track values defined, only 4 can be automated within a single pattern
- To automate more parameters, multiple P3 tracks must be used

#### Questions for the Community

1. **Real-time CC Recording**: Can CC values from track_values be recorded in real-time by turning encoders during recording? Or must they be programmed step-by-step via AUX events?

2. **Track Value Persistence**: When changing patterns or songs, do track values:
   - Reset to default values?
   - Persist at their last state?
   - Load saved values from the new pattern?

3. **AUX Assignment**: Can AUX channels be dynamically reassigned to different track_values during playback, or is assignment fixed per pattern?

4. **VALUE Rows**: The manual mentions VALUE 1-6 rows for P3 tracks. How do these relate to:
   - The 81 track_values we've defined?
   - The 4 AUX channels?
   - Real-time control via encoders?

5. **Practical Workflow**: For users automating many parameters:
   - Is using multiple P3 tracks the only solution?
   - Are there tricks to maximize automation within the 4-channel limit?
   - How do you organize track_values for live performance?

### Contributing

If you have experience with Cirklon track values and automation, please help us clarify these points. You can:
- Open an issue on our GitHub repository
- Contact us with corrections or additional information
- Share your workflow tips and tricks

### Current Implementation Strategy

Given these assumed limitations, we've organized our Machinedrum instruments as:

1. **Hybrid Mode**: 1 CK track (notes) + 4 P3 tracks (CC automation)
   - Maximum 16 simultaneous automations (4 per P3 track)
   - Efficient use of Cirklon's 16 tracks

2. **Pure P3 Mode**: 16 individual P3 tracks
   - Maximum 64 simultaneous automations possible
   - Uses all available tracks

3. **Quad CK Mode**: 4 CK tracks
   - No CC automation via track_values
   - Manual CC control only

---

*This document reflects our current understanding and may contain inaccuracies. Please help us improve it with your expertise.*