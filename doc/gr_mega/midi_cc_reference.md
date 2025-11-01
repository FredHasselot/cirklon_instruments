# GR-Mega - Référence MIDI CC

Liste complète des contrôles MIDI CC et NRPN pour le Tasty Chips GR-Mega.

## Table des matières
- [Messages MIDI Standards](#messages-midi-standards)
- [Control Changes (CC 0-127)](#control-changes-cc-0-127)
- [NRPN (Non-Registered Parameter Numbers)](#nrpn-non-registered-parameter-numbers)
- [Tables de Valeurs](#tables-de-valeurs)

---

## Messages MIDI Standards

### Messages de Base

| Message | Hex | Range | Description |
|---------|-----|-------|-------------|
| Note On | - | 0-127 | Déclenchement de note (vélocité = volume) |
| Note Off | - | 0-127 | Arrêt de note |
| Pitch Bend | - | 0-16383 | Pitch bend (range configurable via CC 2) |
| Channel Aftertouch | - | 0-127 | Pression globale |
| Poly Aftertouch | - | 0-127 | Pression par note |
| Program Change | - | 0-127 | Changement de preset |

### Program Change Mapping

```
PGM 0-7    : Preset 1-8,  Sub-bank 1, Bank 1
PGM 8-15   : Preset 1-8,  Sub-bank 2, Bank 1
PGM 16-23  : Preset 1-8,  Sub-bank 3, Bank 1
PGM 24-31  : Preset 1-8,  Sub-bank 4, Bank 1
PGM 32-39  : Preset 1-8,  Sub-bank 1, Bank 2
...
PGM 120-127: Preset 1-8,  Sub-bank 16, Bank 4
```

### Transport & Sync

| Message | Hex | Description |
|---------|-----|-------------|
| Timing Clock | 0xF8 | MIDI beat clock (24 PPQN) |
| Start | 0xFA | Démarre à la position 0 |
| Continue | 0xFB | Continue où le séquenceur s'est arrêté |
| Stop | 0xFC | Arrêt du séquenceur |
| Song Position | 0xF2 | Position * 4 (0=pos 1, max=pos 64) |

**Note** : SysEx non implémenté actuellement (MTS prévu pour tuning non-tempéré)

---

## Control Changes (CC 0-127)

### Configuration & Layer

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 0 | Bank Change | 0-127 | - | Non utilisé |
| 1 | Mod Wheel MSB | 0-127 | linear | Assignable dans matrice de modulation |
| 2 | Pitchbend Range | 0-127 | linear | 0-48.0 demi-tons |
| 3 | Enable & Focus Layer | 0-127 | - | 0=disable, 1=enable, 2=enable & focus |
| 33 | Mod Wheel LSB | 0-127 | - | LSB du Mod Wheel (14-bit) |

### Sub-Oscillator

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 4 | Subosc Pitch | 0-127 | linear | Pitch relatif (64=-1oct, 32=-2oct) |
| 5 | Subosc Amp | 0-127 | linear | Amplitude du sub-oscillateur |

### Volume & Mix

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 7 | Layer Volume | 0-127 | cubic | Volume du layer |
| 18 | Patch Volume | 0-127 | cubic | Volume du patch |
| 42 | Dry Audio Input Volume | 0-127 | cubic | Volume entrée audio non-granulée |
| 43 | Wet (granulated) Volume | 0-127 | cubic | Volume audio granulé |

### Moteur Granulaire - Paramètres de Base

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 8 | Position | 0-127 | linear | Position de début dans le sample |
| 9 | Rate or Density | 0-127 | cubic | Taux ou densité selon mode granulaire |
| 12 | Grain Size | 0-127 | cubic | Taille du grain (0.1ms - 5s) |
| 13 | Spray | 0-127 | cubic | Randomisation position (0-full sample ou FFT block) |
| 14 | Direction (probability) | 0-127 | linear | 0=100% reverse, 64=50/50, 127=100% forward |
| 15 | Scan | 0-127 | linear | 0=-2x, 64=stop, 127=+2x |
| 49 | Granular Mode | 0-4 | - | 0=Free, 1=DensitySize, 2=DensityRate, 3=ScanRate, 4=ScanOverlap |

### Moteur Granulaire - Fenêtrage

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 44 | Grain Window Sides | 0-127 | - | 0=square, 127=triangle (PowAR only) |
| 45 | Grain Window Tilt | 0-127 | linear | 0=left, 64=center, 127=right |
| 46 | Grain Window Curve | 0-127 | linear | 0=hollow, 64=linear, 127=bulging |
| 47 | Grain Window AM | 0-127 | - | Fréquence AM relative à grain size (RaisedCosine only) |
| 48 | Window Type | 0-1 | - | 0=RaisedCosine, 1=PowAR |

### Positions d'Échantillon

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 28 | Start Pos | 0-127 | linear | 0=sample start, 127=sample end |
| 29 | Stop Pos | 0-127 | linear | 0=sample start, 127=sample end |
| 30 | Loop Start | 0-127 | linear | 0=sample start, 127=sample end |
| 31 | Loop End | 0-127 | linear | 0=sample start, 127=sample end |
| 32 | Scan Mode | 0-2 | - | 0=looping, 1=oneshot, 2=pingpong |

### Panoramique

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 10 | Panning | 0-127 | linear | 0=100% left, 64=center, 127=100% right |
| 11 | Pan Spray | 0-127 | linear | 0=no spray, 127=full stereo field |
| 17 | M-S | 0-127 | linear | Mid-Side (0=100% left, 64=center, 127=100% right) |

### Pitch & Tuning

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 16 | Tune | 0-127 | 2^n | 0=-1oct, 64=center, 127=+1oct |
| 24 | Glide Time | 0-127 | cubic | 0=0ms, 127=2000ms |
| 25 | Glide Always | 0/≥1 | - | 0=OFF, ≥1=ON |
| 26 | Pitch Per Grain | 0/≥1 | - | 0=même pitch, 1=nouveau pitch par grain |
| 84 | Glide / Porta | 0-127 | - | Alternative à CC 24 (0=0ms, 127=2000ms) |

### Polyphonie & Voicing

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 23 | Patch Polyphony | 0-19 | - | Max voices - 1 (0=mono, 19=20 voices) |
| 27 | Grain ARP Mode | 0-9 | - | Voir table Grain ARP Modes |

### Synchronisation - Grain & Scan

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 19 | Grain Clock Sync | 0/≥1 | - | 0=free, ≥1=synced |
| 20 | Scan Clock Sync | 0/≥1 | - | 0=free, ≥1=synced |
| 21 | Grain Key Sync | 0/≥1 | - | 0=OFF, ≥1=ON |
| 22 | Scan Key Sync | 0-3 | - | 0=OFF, 1=ON, 2=Legato, 3=Poly |

### Filtres

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 50 | LPF Cutoff | 0-127 | cubic | 0=0.0Hz, 127=20kHz |
| 51 | LPF Resonance | 0-127 | linear | Résonance du filtre passe-bas |
| 52 | HPF Cutoff | 0-127 | cubic | 0=0.0Hz, 127=20kHz |
| 53 | HPF Resonance | 0-127 | linear | Résonance du filtre passe-haut |

### Enveloppes - Pitch

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 54 | Pitch Env Amount | 0-127 | linear | 0=-1.0, 64=0.0, 127=+1.0 |
| 55 | Pitch Env Attack Time | 0-127 | cubic | 0=0ms, 127=45s |
| 56 | Pitch Env Decay Time | 0-127 | cubic | 0=0ms, 127=45s |
| 57 | Pitch Env Sustain Level | 0-127 | linear | Niveau de sustain |
| 58 | Pitch Env Release Time | 0-127 | cubic | 0=0ms, 127=45s |

### Enveloppes - Filter

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 59 | Filter Env Amount | 0-127 | linear | 0=-1.0, 64=0.0, 127=+1.0 |
| 60 | Filter Env Attack Time | 0-127 | cubic | 0=0ms, 127=45s |
| 61 | Filter Env Decay Time | 0-127 | cubic | 0=0ms, 127=45s |
| 62 | Filter Env Sustain Level | 0-127 | linear | Niveau de sustain |
| 63 | Filter Env Release Time | 0-127 | cubic | 0=0ms, 127=45s |

### Sustain Pedal

| CC | Paramètre | Range | Description |
|----|-----------|-------|-------------|
| 64 | Sustain Pedal | 0-127 | <64=OFF, ≥64=ON |

### Enveloppes - Amp

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 65 | Amp Env Amount | 0-127 | linear | 0=-1.0, 64=0.0, 127=+1.0 |
| 66 | Amp Env Attack Time | 0-127 | cubic | 0=0ms, 127=45s |
| 67 | Amp Env Decay Time | 0-127 | cubic | 0=0ms, 127=45s |
| 68 | Amp Env Sustain Level | 0-127 | linear | Niveau de sustain |
| 69 | Amp Env Release Time | 0-127 | cubic | 0=0ms, 127=45s |

### Enveloppes - Aux

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 70 | Aux Env Amount | 0-127 | linear | 0=-1.0, 64=0.0, 127=+1.0 |
| 71 | Aux Env Attack Time | 0-127 | cubic | 0=0ms, 127=45s |
| 72 | Aux Env Decay Time | 0-127 | cubic | 0=0ms, 127=45s |
| 73 | Aux Env Sustain Level | 0-127 | linear | Niveau de sustain |
| 75 | Aux Env Release Time | 0-127 | cubic | 0=0ms, 127=45s |

### MPE (MIDI Polyphonic Expression)

| CC | Paramètre | Range | Description |
|----|-----------|-------|-------------|
| 74 | MPE Timbre MSB | 0-127 | MPE Timbre (high byte) |
| 106 | MPE Timbre LSB | 0-127 | MPE Timbre (low byte) |

### Matrice de Modulation

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 76 | Mod List Row | 0-49 | - | Index de ligne (slot 0-49) |
| 77 | Mod Row Enable | 0/≥1 | - | 0=OFF, ≥1=ON |
| 78 | Mod Source | 0-18 | - | Source de modulation (voir table) |
| 79 | Mod Curve | 0-127 | linear | 0=low flatline, 64=linear, 127=high flatline |
| 80 | Mod Amount | 0-127 | linear | Intensité de modulation |
| 81 | Mod Polarity | 0-3 | - | 0=+uni, 1=-uni, 2=+bi, 3=-bi |
| 82 | Mod Destination | 0-90 | - | Destination (voir table) |

### CV (Control Voltage)

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 83 | CV1 Destination | 0-127 | - | Destination pour CV1 (voir table) |
| 85 | CV1 Amount | 0-127 | linear | Intensité CV1 |
| 86 | CV2 Destination | 0-90 | - | Destination pour CV2 (voir table) |
| 87 | CV2 Amount | 0-127 | linear | Intensité CV2 |

### LFO 1

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 88 | LFO1 Clock Sync | 0-2 | - | 0=free, 1=MIDI, 2=sequencer |
| 89 | LFO1 Frequency | 0-127 | cubic | 0=stopped, 127=50Hz |
| 90 | LFO1 Wave | 0-5 | - | 0=sine, 1=tri, 2=saw, 3=-saw, 4=square, 5=random |
| 91 | LFO1 Amount | 0-127 | - | Intensité |
| 92 | LFO1 Destination | 0-90 | - | Destination (voir table) |

### LFO 2

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 93 | LFO2 Clock Sync | 0-2 | - | 0=free, 1=MIDI, 2=sequencer |
| 94 | LFO2 Frequency | 0-127 | cubic | 0=stopped, 127=50Hz |
| 95 | LFO2 Wave | 0-5 | - | 0=sine, 1=tri, 2=saw, 3=-saw, 4=square, 5=random |
| 96 | LFO2 Amount | 0-127 | - | Intensité |
| 97 | LFO2 Destination | 0-90 | - | Destination (voir table) |

### NRPN Control

| CC | Paramètre | Range | Description |
|----|-----------|-------|-------------|
| 6 | NRPN Value MSB | 0-127 | Data Entry MSB (high 7 bits) |
| 38 | NRPN Value LSB | 0-127 | Data Entry LSB (low 7 bits) |
| 98 | NRPN Parameter LSB | 0-127 | NRPN number (low 7 bits) |
| 99 | NRPN Parameter MSB | 0-127 | NRPN number (high 7 bits) |

### RPN (Registered Parameter Number)

| CC | Paramètre | Range | Description |
|----|-----------|-------|-------------|
| 100 | RPN Parameter LSB | 0-127 | RPN number (low byte) |
| 101 | RPN Parameter MSB | 0-127 | RPN number (high byte) |

### LFO 3

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 102 | LFO3 Clock Sync | 0-2 | - | 0=free, 1=MIDI, 2=sequencer |
| 103 | LFO3 Frequency | 0-127 | cubic | 0=stopped, 127=50Hz |
| 104 | LFO3 Wave | 0-5 | - | 0=sine, 1=tri, 2=saw, 3=-saw, 4=square, 5=random |
| 105 | LFO3 Amount | 0-127 | - | Intensité |
| 107 | LFO3 Destination | 0-90 | - | Destination (voir table) |

### LFO 4

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 108 | LFO4 Clock Sync | 0-2 | - | 0=free, 1=MIDI, 2=sequencer |
| 109 | LFO4 Frequency | 0-127 | cubic | 0=stopped, 127=50Hz |
| 110 | LFO4 Wave | 0-5 | - | 0=sine, 1=tri, 2=saw, 3=-saw, 4=square, 5=random |
| 111 | LFO4 Amount | 0-127 | - | Intensité |
| 112 | LFO4 Destination | 0-90 | - | Destination (voir table) |

### Effets

| CC | Paramètre | Range | Description |
|----|-----------|-------|-------------|
| 113 | Focus Layer FX | 0-3 | Focus sur FX 1, 2, 3 ou 4 dans la chaîne |
| 114 | Set Layer FX Type | 0-7 | 0=None, 1=Compressor, 2=Delay, 3=Ping Pong, 4=Distortion, 5=Large Reverb, 6=Reducer, 7=Reverb |
| 115 | FX Dry | 0-127 | Volume dry |
| 116 | FX Wet | 0-127 | Volume wet |
| 117 | FX1 Knob Assign | 0-127 | Assignation knob (dépend de l'effet) |
| 118 | FX1 Value | 0-127 | Valeur du paramètre FX1 |
| 119 | FX2 Knob Assign | 0-127 | Assignation knob (dépend de l'effet) |
| 124 | FX2 Value | 0-127 | Valeur du paramètre FX2 |

### Commandes Système

| CC | Paramètre | Description |
|----|-----------|-------------|
| 120 | All Sound Off | Tue tous les sons immédiatement (panic MIDI) |
| 121 | Reset Layer CC's | Reset des CCs reçus |
| 122 | Local Keyboard OFF | - |
| 123 | All Notes OFF | Relâche toutes les notes (enveloppes continuent) |
| 126 | Mono Mode | - |
| 127 | Poly Mode | - |

### Séquenceur Interne

| CC | Paramètre | Range | Courbe | Description |
|----|-----------|-------|--------|-------------|
| 34 | Sequencer BPM | 0-127 | linear | Tempo (meilleur en NRPN 14-bit) |
| 35 | Sequencer Rate | 0-21 | - | Division rythmique (voir table) |
| 36 | Sequencer Pos | 0-63 | - | Position actuelle (pas 1-64) |
| 37 | Sequencer Length | 0-63 | - | Longueur de séquence (1-64 pas) |
| 39 | Sequencer Mode | 0-3 | - | 0=Forward, 1=Reverse, 2=Pingpong, 3=Random |

### Recording

| CC | Paramètre | Range | Description |
|----|-----------|-------|-------------|
| 40 | Record Trigger Level | 0-127 | Niveau de déclenchement (TODO) |
| 41 | Record Sample | - | Toggle (valeur ignorée) |

---

## NRPN (Non-Registered Parameter Numbers)

Les NRPN offrent une précision 14-bit (16384 valeurs) et accès à des paramètres avancés.

### Format NRPN

Pour envoyer un NRPN :
```
CC 99 = NRPN MSB (upper 7 bits du numéro paramètre)
CC 98 = NRPN LSB (lower 7 bits du numéro paramètre)
CC 6  = Data MSB (high 7 bits de la valeur)
CC 38 = Data LSB (low 7 bits de la valeur)
```

### NRPN - Séquenceur

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 128 | Sequencer Record | 0/≥1 | 0=OFF, ≥1=ON (enregistrement) |
| 1007 | Sequencer Clock Div | 0-127 | Division d'horloge (1-128) |
| 1014 | Sequencer Clock Mul | 0-127 | Multiplication d'horloge (1-128) |

### NRPN - LFO Phase & Quantization

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 188 | LFO1 Phase | 0-16383 | Phase initiale LFO1 |
| 189 | LFO2 Phase | 0-16383 | Phase initiale LFO2 |
| 190 | LFO3 Phase | 0-16383 | Phase initiale LFO3 |
| 191 | LFO4 Phase | 0-16383 | Phase initiale LFO4 |
| 192 | LFO1 Amp Quantization | 0-16383 | Quantification amplitude LFO1 |
| 193 | LFO2 Amp Quantization | 0-16383 | Quantification amplitude LFO2 |
| 194 | LFO3 Amp Quantization | 0-16383 | Quantification amplitude LFO3 |
| 195 | LFO4 Amp Quantization | 0-16383 | Quantification amplitude LFO4 |

### NRPN - LFO Polarity & Key Sync

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 196 | LFO1 Polarity | 0-3 | 0=+uni, 1=-uni, 2=+bi, 3=-bi |
| 197 | LFO2 Polarity | 0-3 | 0=+uni, 1=-uni, 2=+bi, 3=-bi |
| 198 | LFO3 Polarity | 0-3 | 0=+uni, 1=-uni, 2=+bi, 3=-bi |
| 199 | LFO4 Polarity | 0-3 | 0=+uni, 1=-uni, 2=+bi, 3=-bi |
| 184 | LFO1 Key Sync | 0/≥1 | Sync sur note |
| 185 | LFO2 Key Sync | 0/≥1 | Sync sur note |
| 186 | LFO3 Key Sync | 0/≥1 | Sync sur note |
| 187 | LFO4 Key Sync | 0/≥1 | Sync sur note |

### NRPN - LFO Clock Multipliers/Dividers

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 1010 | LFO3 Clock Mul | 0-127 | Multiplicateur (1-128) |
| 1011 | LFO4 Clock Mul | 0-127 | Multiplicateur (1-128) |
| 1012 | LFO3 Clock Div | 0-127 | Diviseur (1-128) |
| 1013 | LFO4 Clock Div | 0-127 | Diviseur (1-128) |

### NRPN - Audio Processing

| NRPN | Paramètre | Range | Courbe | Description |
|------|-----------|-------|--------|-------------|
| 210 | Anti-alias | 0/≥1 | - | 0=OFF, ≥1=ON |
| 211 | Tape Slew | 0-16383 | linear | Simulation inertie bande magnétique |
| 294 | Input Level | 0-16383 | cubic | Niveau d'entrée audio |

### NRPN - Effets (14-bit)

| NRPN | Paramètre | Range | Courbe | Description |
|------|-----------|-------|--------|-------------|
| 249 | Delay Feedback | 0-16383 | linear | Feedback du delay |
| 250 | Delay Time | 0-16383 | cubic | Temps de delay |
| 253 | Reverb Time | 0-16383 | linear | Temps de reverb |
| 261 | Distortion Level | 0-16383 | linear | Niveau de distortion |
| 269 | Reducer Bit | 0-16383 | inv cubic | Bit reduction |
| 270 | Reducer Rate | 0-16383 | inv cubic | Sample rate reduction |
| 279 | Reverb Width | 0-16383 | linear | Largeur stéréo du reverb |
| 280 | Reverb Dampening | 0-16383 | linear | Amortissement haute fréquence |

### NRPN - Navigation UI

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 283 | Navigate Right | 0-16383 | Navigation menu (droite) |
| 284 | Navigate Down | 0-16383 | Navigation menu (bas) |
| 285 | Navigate Left | 0-16383 | Navigation menu (gauche) |
| 286 | Navigate Up | 0-16383 | Navigation menu (haut) |

### NRPN - Filtres & Routing

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 289 | Bypass Filter | 0/≥1 | 0=filter actif, 1=filter bypassé |
| 293 | Filter Routing | 0-2 | 0=LPF only, 1=LPF+HPF, 2=HPF |

### NRPN - Rate Mode & Grain

| NRPN | Paramètre | Range | Courbe | Description |
|------|-----------|-------|--------|-------------|
| 291 | Rate Mode | 0-... | - | Mode de rate granulaire (voir table) |
| 1006 | Grain Rate | 0-16383 | cubic | Taux de grains (14-bit) |

### NRPN - Courbes d'Enveloppes

Toutes les enveloppes supportent des courbes customisées (0.0=low flat hollow, 0.5=linear, 1.0=high flat).

**Amp Envelope Curves** :
| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 166 | Amp Attack Curve | 0-16383 | Courbe d'attaque |
| 167 | Amp Decay Curve | 0-16383 | Courbe de decay |
| 168 | Amp Release Curve | 0-16383 | Courbe de release |

**Pitch Envelope Curves** :
| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 156 | Pitch Attack Curve | 0-16383 | Courbe d'attaque |
| 157 | Pitch Decay Curve | 0-16383 | Courbe de decay |
| 158 | Pitch Release Curve | 0-16383 | Courbe de release |

**Filter Envelope Curves** :
| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 161 | Filter Attack Curve | 0-16383 | Courbe d'attaque |
| 162 | Filter Decay Curve | 0-16383 | Courbe de decay |
| 163 | Filter Release Curve | 0-16383 | Courbe de release |

**Aux Envelope Curves** :
| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 171 | Aux Attack Curve | 0-16383 | Courbe d'attaque |
| 172 | Aux Decay Curve | 0-16383 | Courbe de decay |
| 173 | Aux Release Curve | 0-16383 | Courbe de release |

### NRPN - Inversions d'Enveloppes

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 159 | Invert Pitch Env | 0/≥1 | Inversion enveloppe pitch |
| 164 | Invert Filter Env | 0/≥1 | Inversion enveloppe filter |
| 174 | Invert Aux Env | 0/≥1 | Inversion enveloppe aux |

### NRPN - Multi-Layer Configuration

| NRPN | Paramètre | Range | Description |
|------|-----------|-------|-------------|
| 158 | Layer 1 MIDI Channel | 0-15 | Canal MIDI layer 1 (0=ch1...15=ch16) |
| 159 | Layer 2 MIDI Channel | 0-15 | Canal MIDI layer 2 |
| 160 | Layer 3 MIDI Channel | 0-15 | Canal MIDI layer 3 |
| 161 | Layer 4 MIDI Channel | 0-15 | Canal MIDI layer 4 |
| 175 | Layer 1 Preset | 0-127 | Preset du layer 1 (0=preset 1...127=preset 128) |
| 176 | Layer 2 Preset | 0-127 | Preset du layer 2 |
| 177 | Layer 3 Preset | 0-127 | Preset du layer 3 |
| 178 | Layer 4 Preset | 0-127 | Preset du layer 4 |

### NRPN - Scan per Layer

| NRPN | Paramètre | Range | Courbe | Description |
|------|-----------|-------|--------|-------------|
| 140 | Scan Layer 1 | 0-16383 | linear | Scan layer 1 (14-bit) |
| 141 | Scan Layer 2 | 0-16383 | linear | Scan layer 2 (14-bit) |
| 142 | Scan Layer 3 | 0-16383 | linear | Scan layer 3 (14-bit) |
| 143 | Scan Layer 4 | 0-16383 | linear | Scan layer 4 (14-bit) |

### NRPN - Layer Mixing (À implémenter)

| NRPN | Paramètre | Range | Courbe | Description |
|------|-----------|-------|--------|-------------|
| 500 | Layer Bias | - | linear | À implémenter |
| 501 | Layer Spray | - | linear | À implémenter |

---

## Tables de Valeurs

### Table 1 : Grain ARP Modes (CC 27)

| Valeur | Mode | Description |
|--------|------|-------------|
| 0 | Up | Montant |
| 1 | Down | Descendant |
| 2 | UpDown | Montant puis descendant |
| 3 | DownUp | Descendant puis montant |
| 4 | Random | Aléatoire |
| 5 | Shuffle | Mélangé |
| 6 | Forward | Avant |
| 7 | Reverse | Arrière |
| 8 | Forward-Reverse | Avant-Arrière |
| 9 | Reverse-Forward | Arrière-Avant |

### Table 2 : LFO Wave Types (CC 90, 95, 104, 110)

| Valeur | Forme d'onde |
|--------|--------------|
| 0 | Sine |
| 1 | Triangle |
| 2 | Saw |
| 3 | -Saw (inverse) |
| 4 | Square |
| 5 | Random |

### Table 3 : Sequencer Rate Divisions (CC 35)

| Valeur | Division |
|--------|----------|
| 0-21 | Divisions rythmiques (détails dans le manuel GR-Mega) |

### Table 4 : Modulation Sources (CC 78)

| Valeur | Source |
|--------|--------|
| 0-18 | 19 sources de modulation (LFOs, Enveloppes, Velocity, Aftertouch, etc.) |

**Note** : Voir manuel GR-Mega pour liste complète des sources

### Table 5-11 : Modulation/LFO Destinations (CC 82, 92, 97, 107, 112)

| Valeur | Destination |
|--------|-------------|
| 0-90 | 91 destinations possibles |

**Destinations principales** :
- Position, Grain Size, Rate, Spray, Scan
- Filter Cutoff, Resonance
- Pitch, Volume
- Pan, M-S
- FX parameters
- Envelope amounts
- Et bien d'autres...

**Note** : Voir manuel GR-Mega pour liste complète des destinations

### Table 6-7 : CV Destinations (CC 83, 86)

Même mapping que les destinations de modulation (0-90).

### Table 12 : Rate Mode (NRPN 291)

Différents modes de calcul du taux de grains (détails dans le manuel GR-Mega).

---

## Notes d'Implémentation

### Courbes de Contrôle

- **linear** : Progression linéaire
- **cubic** : Progression cubique (plus de résolution en bas de plage)
- **2^n** : Progression exponentielle base 2
- **inv cubic** : Cubique inversé (plus de résolution en haut de plage)

### Précision 14-bit

Tous les CC avec range 0-127 peuvent être utilisés en NRPN 14-bit pour précision maximale, sauf :
- Toggles (0/≥1)
- Sélecteurs de mode (valeurs discrètes)
- Triggers (CC 41)

### CC au-dessus de 127

Accessibles uniquement via NRPN. Utiliser le format NRPN standard avec numéro > 127.

---

## Ressources

- [GR-Mega User Manual](https://tastychips.nl/product/gr-mega/)
- GR-Mega Manual 1.4 - MIDI Implementation (PDF inclus)
- [Tasty Chips Support](https://tastychips.nl/support/)

---

**Auteur** : Fred Hasselot (2025)
**Source** : GR-Mega Manual 1.4 - Tasty Chips Electronics
