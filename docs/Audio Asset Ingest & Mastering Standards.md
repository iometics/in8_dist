GAME AUDIO  
LOUDNESS & DELIVERY SPECIFICATION  
Version 1.0  
For all audio contributors — music, sound effects, and ambiences  

---

## 1. Purpose & Philosophy

This document defines the loudness, dynamic range, and file delivery requirements for all in-game audio assets. All assets submitted for inclusion in the game must meet these specifications before they will be accepted into the asset pipeline.

The core principle is straightforward: **the mix lives in the files, not the engine.** The playback system provides a single master volume control for the player. There are no per-asset gain overrides. There are no runtime normalization passes. What you deliver is what the player hears.

This approach has several important benefits:

- Mix decisions are made by the people who understand the creative intent of each asset.  
- There are no surprise volume jumps caused by conflicting engine-side gain adjustments.  
- The relative balance between categories (music, SFX, ambiences) is predictable and consistent across all scenes.  
- Validation can be automated at ingest time, catching problems before they ship.  

---

## 2. Measurement Standards

All loudness measurements must follow broadcast-grade standards:

- **Integrated Loudness:** LUFS (EBU R128 / ITU-R BS.1770)
- **True Peak:** dBTP
- **Short-Term Loudness:** LUFS (for transient-heavy assets)
- **Loudness Range (LRA):** used to evaluate dynamic consistency

Meters must be compliant with ITU-R BS.1770-4 or later.

Acceptable tools include:

- iZotope Insight
- Waves WLM
- Youlean Loudness Meter
- ffmpeg loudnorm
- r128gain

---

## 3. Global Loudness Targets

All assets must fall within these boundaries before delivery.

| Category   | Integrated LUFS | True Peak Ceiling | Loudness Range Target |
|------------|------------------|-------------------|-----------------------|
| Music      | -16 LUFS         | -1.0 dBTP         | 6–12 LU               |
| SFX        | -14 LUFS         | -1.0 dBTP         | 4–10 LU               |
| Ambiences  | -20 LUFS         | -2.0 dBTP         | 6–14 LU               |
| UI Sounds  | -18 LUFS         | -1.0 dBTP         | 2–6 LU                |
| Cinematics | -20 LUFS         | -2.0 dBTP         | 10–18 LU              |

Tolerance: ±1 LUFS

Any asset outside tolerance will be rejected at ingest.

---

## 4. Category-Specific Guidance

### 4.1 Music

Music defines emotional continuity and must maintain stable perceived loudness across tracks.

Requirements:

- Target: -16 LUFS integrated
- Maintain musical dynamics; avoid over-limiting
- Avoid loudness chasing across tracks
- Album-style mastering consistency required across all music assets

Prohibited:

- Brickwall mastering for loudness maximization
- Over-compression that collapses transient detail

---

### 4.2 Sound Effects (SFX)

SFX must feel impactful without overpowering music or ambience.

Requirements:

- Target: -14 LUFS integrated
- True peaks must remain below -1 dBTP
- Transients may exceed short-term loudness targets but must not distort

Design note:

Perceived loudness should be appropriate to the object scale and gameplay context — not artificially boosted.

---

### 4.3 Ambiences

Ambiences establish space and mood and must not compete with SFX or music.

Requirements:

- Target: -20 LUFS integrated
- Must remain stable and non-fatiguing
- Avoid midrange congestion

Ambience loudness should support layering without requiring runtime gain control.

---

### 4.4 UI Sounds

UI sounds must be clear, consistent, and never startling.

Requirements:

- Target: -18 LUFS integrated
- Very low dynamic range
- Minimal peak transients

---

### 4.5 Cinematic Audio

Cinematics may use wider dynamic range but must still align with overall mix balance.

Requirements:

- Target: -20 LUFS integrated
- True peak ceiling: -2 dBTP
- Dialogue intelligibility takes precedence

---

## 5. True Peak & Clipping Rules

Hard requirements:

- No inter-sample clipping
- True peak must not exceed defined category ceiling
- Waveform clipping = automatic rejection

All assets must be checked using true peak metering, not sample peak.

---

## 6. Dynamic Range Policy

Dynamic range is preserved unless it compromises intelligibility.

Minimum expectations:

- Music: ≥6 LU LRA
- Ambience: ≥6 LU LRA
- SFX: sufficient transient expression without distortion
- UI: controlled and narrow

Over-compression that flattens assets will be rejected.

---

## 7. Silence & Headroom

- Leading silence: ≤10 ms
- Trailing silence: allowed if natural (reverb tails)
- Headroom required during mastering; do not normalize to 0 dBFS

Target headroom: -3 dBFS peak prior to limiting.

---

## 8. Category Balance Philosophy

The following perceived hierarchy must be preserved:

1. Player-critical SFX
2. Dialogue
3. Music
4. Ambience
5. UI reinforcement

Assets must be mastered with awareness of this relationship.

Engine mixing will not compensate for poor balance decisions.

---

## 9. Delivery Requirements

Each asset must be delivered with loudness verification.

Required metadata:

- Integrated LUFS measurement
- True peak measurement
- Loudness range (LRA)
- Measurement tool used

Example:

```

Asset: sfx_explosion_large_v2.wav
Integrated LUFS: -14.3
True Peak: -1.1 dBTP
LRA: 7.2 LU
Meter: Youlean Loudness Meter 2

```

---

## 10. Validation & Ingest Enforcement

Automated checks will reject assets if:

- LUFS outside tolerance
- True peak exceeds ceiling
- Detected clipping
- Incorrect measurement standard
- Missing loudness metadata

Validation is performed before assets enter source control.

---

## 11. Mix Responsibility

Responsibility for correct loudness rests with:

- Composer
- Sound designer
- Audio engineer
- Outsourced audio vendor

The engine is not a corrective environment.

---

## 12. Practical Workflow Recommendation

Suggested mastering pipeline:

1. Creative mix at comfortable monitoring level
2. Loudness measurement pass
3. Dynamic adjustment
4. Peak limiting
5. True peak validation
6. Export
7. Final LUFS verification

Never master by waveform appearance alone.

---

## 13. Reference Monitoring

Recommended monitoring calibration:

- 79–82 dB SPL nearfield
- Neutral room response
- No loudness compensation EQ

Consistency of monitoring environment is essential to maintaining mix stability.

---

## 14. Non-Compliance Outcomes

Assets that do not meet spec:

- Will not enter the repository
- Will not be reviewed for creative quality
- Will be returned for correction

Repeated violations may result in contributor removal from the pipeline.

---

## 15. Summary

A consistent loudness strategy ensures:

- Predictable player experience
- No in-game gain conflicts
- Stable cross-scene mixing
- Clean category hierarchy
- Efficient QA automation

In this pipeline:

**There is one mix. It happens before delivery.**
