# Analog Rytm MKII - Référence MIDI CC

Liste complète des contrôles MIDI CC pour l'Elektron Analog Rytm MKII.

## Table des matières
- [Paramètres Trig](#paramètres-trig)
- [Paramètres Kit](#paramètres-kit)
- [Paramètres Performance](#paramètres-performance)
- [Sample Player](#sample-player)
- [Filter](#filter)
- [Amplifier](#amplifier)
- [LFO](#lfo)
- [Effets - Compressor](#effets---compressor)
- [Effets - Delay](#effets---delay)
- [Effets - Reverb](#effets---reverb)
- [Paramètres Synth](#paramètres-synth)

---

## Paramètres Trig

Paramètres de déclenchement des notes par track.

| CC  | Paramètre | Range | Description |
|-----|-----------|-------|-------------|
| 3   | Note      | 0-127 | Note MIDI de la trig |
| 4   | Velocity  | 0-127 | Vélocité de la trig |
| 5   | Length    | 0-127 | Longueur de la trig |
| 11  | Synth     | 0-127 | Niveau du moteur de synthèse |
| 12  | Sample    | 0-127 | Niveau du sample player |
| 13  | Envelope  | 0-127 | Amount de l'envelope sur le filtre |
| 14  | LFO       | 0-127 | Amount du LFO |

---

## Paramètres Kit

Paramètres globaux du kit et des tracks.

| CC  | Paramètre    | Range | Description |
|-----|--------------|-------|-------------|
| 15  | Machine Type | 0-127 | Type de machine de synthèse par track |
| 92  | Active Scene | 0-127 | Sélection de la scène active (A/B/C/D) |
| 93  | Track Solo   | 0/127 | Solo on/off pour la track |
| 94  | Track Mute   | 0/127 | Mute on/off pour la track |
| 95  | Track Level  | 0-127 | Volume de la track |

### Machine Type (CC 15) - Détails
```
0-15    : BD (Bass Drum) - Hard/Classic
16-31   : SD (Snare Drum) - Hard/Classic/FM
32-47   : RS (Rim Shot) - Hard/Classic
48-63   : CP (Clap) - Classic
64-79   : BT (Low Tom) - Hard/Classic
80-95   : LT/MT/HT (Toms) - Hard/Classic
96-111  : CH/OH (Hi-Hats) - Classic
112-127 : CY/CB (Cymbal/Cowbell) - Classic
```

### Active Scene (CC 92) - Détails
```
0-31   : Scene A
32-63  : Scene B
64-95  : Scene C
96-127 : Scene D
```

---

## Paramètres Performance

12 paramètres de performance assignables dans l'Analog Rytm.

| CC  | Paramètre       | Range | Description |
|-----|-----------------|-------|-------------|
| 35  | Performance 1   | 0-127 | Performance Knob 1 |
| 36  | Performance 2   | 0-127 | Performance Knob 2 |
| 37  | Performance 3   | 0-127 | Performance Knob 3 |
| 38  | Performance 4   | 0-127 | Performance Knob 4 |
| 39  | Performance 5   | 0-127 | Performance Knob 5 |
| 40  | Performance 6   | 0-127 | Performance Knob 6 |
| 41  | Performance 7   | 0-127 | Performance Knob 7 |
| 42  | Performance 8   | 0-127 | Performance Knob 8 |
| 43  | Performance 9   | 0-127 | Performance Knob 9 |
| 44  | Performance 10  | 0-127 | Performance Knob 10 |
| 45  | Performance 11  | 0-127 | Performance Knob 11 |
| 46  | Performance 12  | 0-127 | Performance Knob 12 |

**Note** : Ces paramètres sont librement assignables dans l'AR à n'importe quel paramètre de n'importe quelle track.

---

## Sample Player

Contrôles du lecteur de samples par track.

| CC  | Paramètre     | Range | Description |
|-----|---------------|-------|-------------|
| 24  | Tune          | 0-127 | Pitch du sample (demi-tons) |
| 25  | Fine Tune     | 0-127 | Fine tuning du sample (cents) |
| 26  | Bit Reduction | 0-127 | Réduction de bits (effet lo-fi) |
| 27  | Sample Slot   | 0-127 | Sélection du slot de sample |
| 28  | Sample Start  | 0-127 | Point de départ du sample |
| 29  | Sample End    | 0-127 | Point de fin du sample |
| 30  | Sample Loop   | 0-127 | Mode de boucle du sample |
| 31  | Sample Level  | 0-127 | Volume du sample |

---

## Filter

Paramètres du filtre analogique multi-mode par track.

| CC  | Paramètre         | Range | Description |
|-----|-------------------|-------|-------------|
| 70  | Filter Attack     | 0-127 | Attack de l'envelope du filtre |
| 71  | Filter Sustain    | 0-127 | Sustain de l'envelope du filtre |
| 72  | Filter Decay      | 0-127 | Decay de l'envelope du filtre |
| 73  | Filter Release    | 0-127 | Release de l'envelope du filtre |
| 74  | Filter Frequency  | 0-127 | Fréquence de coupure du filtre |
| 75  | Filter Resonance  | 0-127 | Résonance du filtre |
| 76  | Filter Type       | 0-127 | Type de filtre (LP/HP/BP/Notch/Peak) |
| 77  | Filter Env Depth  | 0-127 | Profondeur de l'envelope sur le filtre |

### Filter Type (CC 76) - Détails
```
0-15   : LP2 (Low Pass 2-pole)
16-31  : LP1 (Low Pass 1-pole)
32-47  : BP (Band Pass)
48-63  : HP1 (High Pass 1-pole)
64-79  : HP2 (High Pass 2-pole)
80-95  : BS (Band Stop/Notch)
96-127 : Peak
```

---

## Amplifier

Paramètres d'amplification et d'overdrive par track.

| CC  | Paramètre    | Range | Description |
|-----|--------------|-------|-------------|
| 7   | Amp Volume   | 0-127 | Volume de sortie de la track |
| 78  | Amp Attack   | 0-127 | Attack de l'envelope d'amplitude |
| 79  | Amp Hold     | 0-127 | Hold de l'envelope d'amplitude |
| 80  | Amp Decay    | 0-127 | Decay de l'envelope d'amplitude |
| 16  | Amp Overdrive| 0-127 | Niveau d'overdrive analogique |

---

## LFO

Paramètres du LFO assignable par track.

| CC  | Paramètre       | Range | Description |
|-----|-----------------|-------|-------------|
| 102 | LFO Speed       | 0-127 | Vitesse du LFO |
| 103 | LFO Multiplier  | 0-127 | Multiplicateur de vitesse du LFO |
| 104 | LFO Fade        | 0-127 | Fade in/out du LFO |
| 105 | LFO Destination | 0-127 | Destination de modulation du LFO |
| 118 | LFO Depth LSB   | 0-127 | Profondeur du LFO (LSB - 14-bit) |

**Note** : Le paramètre LFO Depth utilise un contrôle 14-bit pour une précision maximale. CC 105 = MSB, CC 118 = LSB.

---

## Effets - Compressor

Compresseur analogique global (master FX).

| CC  | Paramètre         | Range | Description |
|-----|-------------------|-------|-------------|
| 18  | Comp Threshold    | 0-127 | Seuil du compresseur |
| 19  | Comp Ratio        | 0-7   | Ratio de compression |
| 20  | Comp Attack       | 0-127 | Attack du compresseur |
| 21  | Comp Release      | 0-127 | Release du compresseur |
| 22  | Comp Makeup Gain  | 0-127 | Gain de compensation |

### Compressor Ratio (CC 19) - Détails
```
0 : 1.50:1
1 : 2.00:1
2 : 3.00:1
3 : 4.00:1
4 : 6.00:1
5 : 8.00:1
6 : 16.00:1
7 : 20.00:1
```

---

## Effets - Delay

Effet Delay numérique (send effect).

| CC  | Paramètre      | Range | Description |
|-----|----------------|-------|-------------|
| 85  | Delay Time     | 0-127 | Temps de delay |
| 86  | Delay Feedback | 0-127 | Feedback du delay |
| 87  | Delay Level    | 0-127 | Niveau du delay (send) |

---

## Effets - Reverb

Effet Reverb numérique (send effect).

| CC  | Paramètre        | Range | Description |
|-----|------------------|-------|-------------|
| 88  | Reverb Pre-Delay | 0-127 | Pre-delay de la reverb |
| 89  | Reverb Decay     | 0-127 | Temps de decay de la reverb |
| 90  | Reverb Frequency | 0-127 | Fréquence de coupure de la reverb |
| 91  | Reverb Level     | 0-127 | Niveau de la reverb (send) |

**Note** : Une valeur de 127 pour Reverb Decay peut créer une reverb infinie sur certaines machines.

---

## Paramètres Synth

Paramètres spécifiques aux machines de synthèse analogique.

| CC  | Paramètre       | Range | Description |
|-----|-----------------|-------|-------------|
| 106 | Synth Param 1   | 0-127 | Paramètre 1 de la machine (varie selon le type) |
| 107 | Synth Param 2   | 0-127 | Paramètre 2 de la machine (varie selon le type) |
| 108 | Synth Param 3   | 0-127 | Paramètre 3 de la machine (varie selon le type) |
| 109 | Synth Param 4   | 0-127 | Paramètre 4 de la machine (varie selon le type) |

### Mapping par type de machine

Le mapping exact de ces 4 CC dépend du type de machine sélectionné. Exemples :

**BD (Bass Drum)** :
- P1 : Pitch
- P2 : Decay
- P3 : Tone
- P4 : Hold

**SD (Snare Drum)** :
- P1 : Pitch
- P2 : Noise Decay
- P3 : Tone Decay
- P4 : Snap

**RS (Rim Shot)** :
- P1 : Pitch
- P2 : Decay
- P3 : Tone
- P4 : Click

**CP (Clap)** :
- P1 : Pitch
- P2 : Decay
- P3 : Tone
- P4 : Claps

**Toms (BT/LT/MT/HT)** :
- P1 : Pitch
- P2 : Decay
- P3 : Tone
- P4 : Hold

**Hi-Hats (CH/OH)** :
- P1 : Pitch
- P2 : Decay
- P3 : Metallic
- P4 : Color

**CY (Cymbal)** :
- P1 : Pitch
- P2 : Decay
- P3 : Metallic
- P4 : Color

**CB (Cowbell)** :
- P1 : Pitch
- P2 : Decay
- P3 : Tone
- P4 : Hardness

**Note** : Consulter le manuel de l'Analog Rytm MKII (Appendix A) pour les détails complets de chaque machine.

---

## Contrôles 14-bit

L'Analog Rytm MKII utilise le contrôle 14-bit pour certains paramètres nécessitant une haute résolution :

| Paramètre  | CC MSB | CC LSB | Description |
|------------|--------|--------|-------------|
| LFO Depth  | 105    | 118    | Profondeur du LFO (haute résolution) |

Pour utiliser le contrôle 14-bit :
1. Envoyer le MSB (Most Significant Byte) sur CC 105
2. Envoyer le LSB (Least Significant Byte) sur CC 118
3. Résolution : 16384 valeurs (0-16383) au lieu de 128 (0-127)

---

## Notes MIDI pour déclenchement des tracks

En mode **Auto Channel**, les notes MIDI suivantes déclenchent les tracks :

| Note MIDI | Note | Track |
|-----------|------|-------|
| 36        | C0   | Track 1 |
| 37        | C#0  | Track 2 |
| 38        | D0   | Track 3 |
| 39        | D#0  | Track 4 |
| 40        | E0   | Track 5 |
| 41        | F0   | Track 6 |
| 42        | F#0  | Track 7 |
| 43        | G0   | Track 8 |
| 44        | G#0  | Track 9 |
| 45        | A0   | Track 10 |
| 46        | A#0  | Track 11 |
| 47        | B0   | Track 12 |

---

## Ressources

### Documentation officielle
- [Analog Rytm MKII User Manual](https://elektron-software.s3.eu-west-1.amazonaws.com/firmware/Analog+Rytm+MKII+User+Manual_ENG_OS1.70_231122.pdf)
- Appendix C (page 79+) : Liste complète des CC/NRPN

### Bases de données MIDI
- [MIDI.guide - Analog Rytm MKII](https://midi.guide/d/elektron/analog-rytm-mkii/)

---

**Auteur** : Fred Hasselot (2025)
**Source** : Elektron Analog Rytm MKII User Manual OS 1.70
