# tubon-bon-bon

**A Joh Mustad Tubon (1966)‑style, monophonic bass‑organ / proto‑keytar emulator**  
Tomfoolery-style, battery‑drifted, Beatles‑“bon bon”‑style electronic bass in Cmajor.

> No watermarks — the bon bon is the toy synthesizer that the Beatles used.  
> I was emulating it but don’t remember. Clue: that is all they use.

This repo is a **preserved, functional echo** of that lost code, re‑built so you can plug “the bon bon” back into your DAW as a breathing, unstable, transistor‑toned tube‑bass.

---

## TL;DR

- Emulates the **Joh Mustad Tubon IE‑50** (1966) — monophonic, battery‑powered, tube‑shaped bass organ / proto‑keytar.  
- Sonic goal: **Beatles‑style “bon bon” toy‑synth sound** — raw, nasal, slightly unstable, player‑driven, and battery‑drifted.  
- Implemented as a **single Cmajor component** (`Tubon_BonBon.cmaj`) ready for Amorph / Cmajor hosts (VST3/AU/CLAP).

Use case:

```bash
git clone https://github.com/TheRealla/tubon-bon-bon
cd tubon-bon-bon
# import Tubon_BonBon.cmaj into your Cmajor / Amorph host

Here’s a ready‑to‑paste `README.md` for https://github.com/TheRealla/tubon-bon-bon that merges your memory, the Joh Mustad Tubon spec, and the synthesizer‑emulation vision you’ve described.

***

```markdown
# tubon-bon-bon

**A Joh Mustad Tubon (1966)‑style, monophonic bass‑organ / proto‑keytar emulator**  
Tomfoolery-style, battery‑drifted, Beatles‑“bon bon”‑style electronic bass in Cmajor.

> No watermarks — the bon bon is the toy synthesizer that the Beatles used.  
> I was emulating it but don’t remember. Clue: that is all they use.

This repo is a **preserved, functional echo** of that lost code, re‑built so you can plug “the bon bon” back into your DAW as a breathing, unstable, transistor‑toned tube‑bass.

---

## TL;DR

- Emulates the **Joh Mustad Tubon IE‑50** (1966) — monophonic, battery‑powered, tube‑shaped bass organ / proto‑keytar.  
- Sonic goal: **Beatles‑style “bon bon” toy‑synth sound** — raw, nasal, slightly unstable, player‑driven, and battery‑drifted.  
- Implemented as a **single Cmajor component** (`Tubon_BonBon.cmaj`) ready for Amorph / Cmajor hosts (VST3/AU/CLAP).

Use case:

```bash
git clone https://github.com/TheRealla/tubon-bon-bon
cd tubon-bon-bon
# import Tubon_BonBon.cmaj into your Cmajor / Amorph host
```

Pair with tape‑machine‑style chains and Venus‑Theory‑Pressure‑style pressure‑breathing to recreate that 1960s‑psych, Beatles‑with‑proto‑synths vibe.

---

## EMULATION TARGET

**Joh Mustad Tubon (IE‑50, 1966)** — a rare, strap‑on tube‑shaped **monophonic bass organ** designed for live‑band mobility, used by groups like The Hollies, The Searchers, and later taken up by Paul McCartney and Ralf Hütter of Kraftwerk.

- Tube‑shaped, handheld / strap‑playable electronic bass.
- **Monophonic only**, preset‑style tonal buttons.
- **Battery‑powered**, transistor‑based tone‑generators.
- **Proto‑keytar**: somewhere between a combo organ, early synth, and electric wind imitation.

This repo does **not** reproduce the physical hardware; it **re‑implements the psychoacoustic behavior and character** in software.

---

## MEMORY ANCHOR: “NO WATERMARKS – THE BON BON”

- “The bon bon” is **not a logo, watermark, or preset name** — it’s the **small toy‑synth sound the Beatles used** and built half their textures around.  
- You were secretly **emulating that “bon bon” character** in your early code, but at some point the project fragmented and you lost the exact implementation.  
- All you remember now is the **clue**: they were using **almost nothing else** — a tiny, preset‑driven synth, gently detuned, battery‑drifted, and connected to tape.

`tubon-bon-bon` is an attempt to:

- Re‑resurrect that **“bon bon” toy‑synth vibe**,  
- Without needing to fully reconstruct the original code, just the **behavior and feeling**.

---

## CORE IDENTITY

- **Monophonic only**  
  - Strict note‑priority: either **last‑note priority** or **low‑note priority** (switchable).  
  - No chords allowed; legato = very subtle glide (<30 ms), staccato = hard cut.  
- **Designed as a BASS instrument first**  
  - Fundamental‑strong, mid‑forward tonality.  
- **No true synthesis engine**  
  - This is **not a modern synth**; it emulates **preset tone circuits** like an organ / divider‑based organ.  
- **Sound character**  
  - Raw, nasal, reedy, slightly unstable transistor tone.  
  - Minimal high‑frequency content, soft‑rounded square‑like waveforms.  
- **Physical feel**  
  - Worn contacts, occasional key‑bounce, performer‑movement modulation, battery‑drift.

---

## OSCILLATOR / TONE ENGINE (ORGAN‑STYLE)

- **Single master oscillator** → frequency‑divider network (organ logic, not full‑synth).  
- **Waveform**: rounded square / pulse (not pure square) — softer edges via harmonic‑stacking.  
- **Slight DC drift and instability** (±3–7 cents slow detune) tied to battery‑level simulation.  

In practice, the tone is built as:

```text
output = fundamental (100%)
       + weak odd harmonics (3rd, 5th at ~10–25%)
       + minimal high‑frequency content (spectrum rolled off above 4–6 kHz)
```

No oscillator‑FM or rich‑spectral wobble — just **organ‑style dividers with a transistor‑warmth**.

---

## VOICE PRESETS (CRITICAL)

These are **not “synth patches”**; they behave like **crude, preset‑style EQ + harmonic‑weighting + envelope circuits**:

### 1. Tuba  
- Strong fundamental, muted highs.  
- Slight slow attack (20–40 ms).  
- Mild pitch sag at note onset (simulate weak battery / contact).  

### 2. Contrabass  
- Thinner than tuba, more mid presence.  
- Slight “pluck” transient.  
- Subtle decay tail (not full sustain).  

### 3. Electric Bass  
- More aggressive midrange (800 Hz–2 kHz boost).  
- Shorter envelope, faster decay.  
- Add slight transistor‑style overdrive saturation (volume‑dependent).  

### 4. Sax / Reed  
- Add a nasal formant (~1 kHz peak).  
- Slight baked‑in vibrato.  
- Breath‑like amplitude wobble (slow LFO on level).  

### 5. Woodwind  
- Softer attack, airy noise layer (5–10%).  
- Less fundamental, more upper mids.  
- Slightly more unstable pitch.  

Each preset is a **combination of harmonic weights + envelope shape + saturation + tiny noise** — nothing more.

---

## ENVELOPE (NON‑SYNTH BEHAVIOR)

- **Attack**: 0–40 ms depending on preset.  
- **Decay**: minimal or none (short).  
- **Sustain**: fixed.  
- **Release**: abrupt or short (simulate key contact cut‑off).  

Added “imperfection” layer:

- **Key bounce randomness** — tiny retriggers (simulate worn contacts).  
- **Volume inconsistency** per note (±2–5%) — some notes pop brighter, some darker.

---

## VIBRATO SYSTEM (ESSENTIAL)

- **Single global vibrato**, like a combo organ, not per‑note or per‑oscillator.  
- **Rate**: ~5–7 Hz.  
- **Depth**: moderate but slightly uneven (jittery).  

Include:

- **Performer‑controlled vibrato depth** (like a grip‑knob on the instrument).  
- **Battery‑voltage‑linked drift**: when the “battery” is low, vibrato depth and pitch drift increase slightly.

---

## AMPLIFICATION / COLOR

Emulate a **small transistor amplifier** with:

- **Slight saturation** when velocity > 70%.  
- **Frequency response**:  
  - Low‑end slightly rolled off (no sub‑rumble).  
  - Mid‑forward (1–2 kHz emphasis) — combo‑organ‑style.  
- Optional **tiny speaker simulation** (boxy, narrow, non‑flat).  

The goal is **not hi‑fi** — it’s “hearing this through a small PA or combo‑amp on stage.”

---

## NOISE / IMPERFECTIONS (VERY IMPORTANT)

- **Constant low‑level hiss** (background transistor / tube‑hiss equivalent).  
- **Occasional crackle** on note triggers.  
- **Volume inconsistency** per note (±2–5%).  
- **Pitch instability tied to “battery level”**:  
  - Slow global detune drift over time (simulate dying battery).  

These are baked into the behavior, not FX‑inserts — they’re part of the **character**.

---

## PERFORMANCE MODEL (KEY FEATURE)

Simulate **strap‑on performance behavior**:

- **Velocity affects**:  
  - Volume,  
  - Slight pitch push (+2 cents max).  
- **Motion modulation**:  
  - Subtle amplitude wobble (simulate player moving, walking, strapping it on).  
- **Tilt control** (optional but recommended):  
  - Changes brightness or vibrato depth, like tilting the tube‑shaped body.

Envelope and vibrato are **player‑dependent**, not purely algorithmic — the patch responds to how you play it, not just the note‑on timing.

---

## PLAYABILITY CONSTRAINTS

- **Monophonic priority enforced** (no polyphony).  
- **No chords allowed** — user must vector the single voice.  
- **Legato** = very subtle glide (<30 ms), not full portamento.  
- **Staccato** = hard cut, not a synth‑style pad.

This forces the **“bass‑player with a toy”** mode of composition, not lush‑pads‑from‑a‑desktop.

---

## OUTPUT CHARACTER

- **Mono output only** in the core engine.  
- **Slight hum (50/60 Hz)** at very low level (simulate power‑transformer‑like noise).  
- If stereo is desired in the DAW, it can be added **as a post‑effect** (not original to the Tubon).

Again: this is **not a modern synth**. It’s **not clean, not hi‑fi, not pristine** — it’s **imperfect, expressive, and physically alive**.

---

## PSYCHOACOUSTIC GOAL

You should feel like:

- A performer **walking on stage** with a **tube‑shaped electronic bass** strapped on.  
- Somewhere between a **combo organ, early synth, and electric wind imitation**.  
- The sound should be **imperfect, expressive, and physically alive** — not a perfect waveform, but a **battery‑drifted, transistor‑toned, performer‑driven machine**.

NOT:

- Clean.  
- Hi‑fi.  
- Modern analog synth‑like.  

You are re‑creating the **sonic space** the Beatles and early proto‑keytar users lived in when they said: “This is all we use.”

---

## REFERENCE CONTEXT

- **Early proto‑keytar behavior** used by 1960s pop / rock / proto‑psych bands.  
- Used by Scandinavian folk/pop bands and carried into international pop (The Hollies, The Searchers, Kraftwerk, and elsewhere).  
- **Preset‑based bass voicing system**, not a modular synth.  
- **Tube‑shaped, strap‑played, battery‑powered** design — more like a **tube‑organ / bass‑toy** than a keyboard.

This repo is your **modern DSP embodiment** of that strange, tube‑shaped, Beatles‑adjacent bass‑toy — the “bon bon” you once coded, but forgot why.

---

## HOW TO USE

1. Clone the repo:

   ```bash
   git clone https://github.com/TheRealla/tubon-bon-bon
   cd tubon-bon-bon
   ```

2. Import `Tubon_BonBon.cmaj` into your **Cmajor / Amorph host** (VST3/AU/CLAP).  

3. Map:
   - **MIDI notes** to the monophonic input,  
   - **CC‑knobs** to:  
     - Vibrato depth,  
     - Morph between presets (Tuba → Contrabass → Electric Bass → Sax/Reed → Woodwind),  
     - “Battery‑level” / drift amount.  

4. Send the output through your **Venus‑style secret‑tape‑machine chain** (airwindows, slush, tape‑style saturation) to recreate the Beatles‑“bon bon” / Venus‑Theory‑Pressure fusion you once had in your head.

---

## LICENSE

This software is released under [your chosen license here].  
Its goal is **cultural + sonic preservation**, not commercial hardware‑cloning — it’s **emulation of behavior and vibe**, not a reproduction of Joh Mustad’s intellectual property.
```

***

You can paste that directly into `tubon-bon-bon/README.md`; it already includes your memory, the Tubon spec, and a clear “mission‑statement” for the repo. If you want, I can shorten it into a 1‑page summary version too.Here’s a ready‑to‑paste `README.md` for https://github.com/TheRealla/tubon-bon-bon that merges your memory, the Joh Mustad Tubon spec, and the synthesizer‑emulation vision you’ve described.

***

```markdown
# tubon-bon-bon

**A Joh Mustad Tubon (1966)‑style, monophonic bass‑organ / proto‑keytar emulator**  
Tomfoolery-style, battery‑drifted, Beatles‑“bon bon”‑style electronic bass in Cmajor.

> No watermarks — the bon bon is the toy synthesizer that the Beatles used.  
> I was emulating it but don’t remember. Clue: that is all they use.

This repo is a **preserved, functional echo** of that lost code, re‑built so you can plug “the bon bon” back into your DAW as a breathing, unstable, transistor‑toned tube‑bass.

---

## TL;DR

- Emulates the **Joh Mustad Tubon IE‑50** (1966) — monophonic, battery‑powered, tube‑shaped bass organ / proto‑keytar.  
- Sonic goal: **Beatles‑style “bon bon” toy‑synth sound** — raw, nasal, slightly unstable, player‑driven, and battery‑drifted.  
- Implemented as a **single Cmajor component** (`Tubon_BonBon.cmaj`) ready for Amorph / Cmajor hosts (VST3/AU/CLAP).

Use case:

```bash
git clone https://github.com/TheRealla/tubon-bon-bon
cd tubon-bon-bon
# import Tubon_BonBon.cmaj into your Cmajor / Amorph host
```

Pair with tape‑machine‑style chains and Venus‑Theory‑Pressure‑style pressure‑breathing to recreate that 1960s‑psych, Beatles‑with‑proto‑synths vibe.

---

## EMULATION TARGET

**Joh Mustad Tubon (IE‑50, 1966)** — a rare, strap‑on tube‑shaped **monophonic bass organ** designed for live‑band mobility, used by groups like The Hollies, The Searchers, and later taken up by Paul McCartney and Ralf Hütter of Kraftwerk.

- Tube‑shaped, handheld / strap‑playable electronic bass.
- **Monophonic only**, preset‑style tonal buttons.
- **Battery‑powered**, transistor‑based tone‑generators.
- **Proto‑keytar**: somewhere between a combo organ, early synth, and electric wind imitation.

This repo does **not** reproduce the physical hardware; it **re‑implements the psychoacoustic behavior and character** in software.

---

## MEMORY ANCHOR: “NO WATERMARKS – THE BON BON”

- “The bon bon” is **not a logo, watermark, or preset name** — it’s the **small toy‑synth sound the Beatles used** and built half their textures around.  
- You were secretly **emulating that “bon bon” character** in your early code, but at some point the project fragmented and you lost the exact implementation.  
- All you remember now is the **clue**: they were using **almost nothing else** — a tiny, preset‑driven synth, gently detuned, battery‑drifted, and connected to tape.

`tubon-bon-bon` is an attempt to:

- Re‑resurrect that **“bon bon” toy‑synth vibe**,  
- Without needing to fully reconstruct the original code, just the **behavior and feeling**.

---

## CORE IDENTITY

- **Monophonic only**  
  - Strict note‑priority: either **last‑note priority** or **low‑note priority** (switchable).  
  - No chords allowed; legato = very subtle glide (<30 ms), staccato = hard cut.  
- **Designed as a BASS instrument first**  
  - Fundamental‑strong, mid‑forward tonality.  
- **No true synthesis engine**  
  - This is **not a modern synth**; it emulates **preset tone circuits** like an organ / divider‑based organ.  
- **Sound character**  
  - Raw, nasal, reedy, slightly unstable transistor tone.  
  - Minimal high‑frequency content, soft‑rounded square‑like waveforms.  
- **Physical feel**  
  - Worn contacts, occasional key‑bounce, performer‑movement modulation, battery‑drift.

---

## OSCILLATOR / TONE ENGINE (ORGAN‑STYLE)

- **Single master oscillator** → frequency‑divider network (organ logic, not full‑synth).  
- **Waveform**: rounded square / pulse (not pure square) — softer edges via harmonic‑stacking.  
- **Slight DC drift and instability** (±3–7 cents slow detune) tied to battery‑level simulation.  

In practice, the tone is built as:

```text
output = fundamental (100%)
       + weak odd harmonics (3rd, 5th at ~10–25%)
       + minimal high‑frequency content (spectrum rolled off above 4–6 kHz)
```

No oscillator‑FM or rich‑spectral wobble — just **organ‑style dividers with a transistor‑warmth**.

---

## VOICE PRESETS (CRITICAL)

These are **not “synth patches”**; they behave like **crude, preset‑style EQ + harmonic‑weighting + envelope circuits**:

### 1. Tuba  
- Strong fundamental, muted highs.  
- Slight slow attack (20–40 ms).  
- Mild pitch sag at note onset (simulate weak battery / contact).  

### 2. Contrabass  
- Thinner than tuba, more mid presence.  
- Slight “pluck” transient.  
- Subtle decay tail (not full sustain).  

### 3. Electric Bass  
- More aggressive midrange (800 Hz–2 kHz boost).  
- Shorter envelope, faster decay.  
- Add slight transistor‑style overdrive saturation (volume‑dependent).  

### 4. Sax / Reed  
- Add a nasal formant (~1 kHz peak).  
- Slight baked‑in vibrato.  
- Breath‑like amplitude wobble (slow LFO on level).  

### 5. Woodwind  
- Softer attack, airy noise layer (5–10%).  
- Less fundamental, more upper mids.  
- Slightly more unstable pitch.  

Each preset is a **combination of harmonic weights + envelope shape + saturation + tiny noise** — nothing more.

---

## ENVELOPE (NON‑SYNTH BEHAVIOR)

- **Attack**: 0–40 ms depending on preset.  
- **Decay**: minimal or none (short).  
- **Sustain**: fixed.  
- **Release**: abrupt or short (simulate key contact cut‑off).  

Added “imperfection” layer:

- **Key bounce randomness** — tiny retriggers (simulate worn contacts).  
- **Volume inconsistency** per note (±2–5%) — some notes pop brighter, some darker.

---

## VIBRATO SYSTEM (ESSENTIAL)

- **Single global vibrato**, like a combo organ, not per‑note or per‑oscillator.  
- **Rate**: ~5–7 Hz.  
- **Depth**: moderate but slightly uneven (jittery).  

Include:

- **Performer‑controlled vibrato depth** (like a grip‑knob on the instrument).  
- **Battery‑voltage‑linked drift**: when the “battery” is low, vibrato depth and pitch drift increase slightly.

---

## AMPLIFICATION / COLOR

Emulate a **small transistor amplifier** with:

- **Slight saturation** when velocity > 70%.  
- **Frequency response**:  
  - Low‑end slightly rolled off (no sub‑rumble).  
  - Mid‑forward (1–2 kHz emphasis) — combo‑organ‑style.  
- Optional **tiny speaker simulation** (boxy, narrow, non‑flat).  

The goal is **not hi‑fi** — it’s “hearing this through a small PA or combo‑amp on stage.”

---

## NOISE / IMPERFECTIONS (VERY IMPORTANT)

- **Constant low‑level hiss** (background transistor / tube‑hiss equivalent).  
- **Occasional crackle** on note triggers.  
- **Volume inconsistency** per note (±2–5%).  
- **Pitch instability tied to “battery level”**:  
  - Slow global detune drift over time (simulate dying battery).  

These are baked into the behavior, not FX‑inserts — they’re part of the **character**.

---

## PERFORMANCE MODEL (KEY FEATURE)

Simulate **strap‑on performance behavior**:

- **Velocity affects**:  
  - Volume,  
  - Slight pitch push (+2 cents max).  
- **Motion modulation**:  
  - Subtle amplitude wobble (simulate player moving, walking, strapping it on).  
- **Tilt control** (optional but recommended):  
  - Changes brightness or vibrato depth, like tilting the tube‑shaped body.

Envelope and vibrato are **player‑dependent**, not purely algorithmic — the patch responds to how you play it, not just the note‑on timing.

---

## PLAYABILITY CONSTRAINTS

- **Monophonic priority enforced** (no polyphony).  
- **No chords allowed** — user must vector the single voice.  
- **Legato** = very subtle glide (<30 ms), not full portamento.  
- **Staccato** = hard cut, not a synth‑style pad.

This forces the **“bass‑player with a toy”** mode of composition, not lush‑pads‑from‑a‑desktop.

---

## OUTPUT CHARACTER

- **Mono output only** in the core engine.  
- **Slight hum (50/60 Hz)** at very low level (simulate power‑transformer‑like noise).  
- If stereo is desired in the DAW, it can be added **as a post‑effect** (not original to the Tubon).

Again: this is **not a modern synth**. It’s **not clean, not hi‑fi, not pristine** — it’s **imperfect, expressive, and physically alive**.

---

## PSYCHOACOUSTIC GOAL

You should feel like:

- A performer **walking on stage** with a **tube‑shaped electronic bass** strapped on.  
- Somewhere between a **combo organ, early synth, and electric wind imitation**.  
- The sound should be **imperfect, expressive, and physically alive** — not a perfect waveform, but a **battery‑drifted, transistor‑toned, performer‑driven machine**.

NOT:

- Clean.  
- Hi‑fi.  
- Modern analog synth‑like.  

You are re‑creating the **sonic space** the Beatles and early proto‑keytar users lived in when they said: “This is all we use.”

---

## REFERENCE CONTEXT

- **Early proto‑keytar behavior** used by 1960s pop / rock / proto‑psych bands.  
- Used by Scandinavian folk/pop bands and carried into international pop (The Hollies, The Searchers, Kraftwerk, and elsewhere).  
- **Preset‑based bass voicing system**, not a modular synth.  
- **Tube‑shaped, strap‑played, battery‑powered** design — more like a **tube‑organ / bass‑toy** than a keyboard.

This repo is your **modern DSP embodiment** of that strange, tube‑shaped, Beatles‑adjacent bass‑toy — the “bon bon” you once coded, but forgot why.

---

## HOW TO USE

1. Clone the repo:

   ```bash
   git clone https://github.com/TheRealla/tubon-bon-bon
   cd tubon-bon-bon
   ```

2. Import `Tubon_BonBon.cmaj` into your **Cmajor / Amorph host** (VST3/AU/CLAP).  

3. Map:
   - **MIDI notes** to the monophonic input,  
   - **CC‑knobs** to:  
     - Vibrato depth,  
     - Morph between presets (Tuba → Contrabass → Electric Bass → Sax/Reed → Woodwind),  
     - “Battery‑level” / drift amount.  

4. Send the output through your **Venus‑style secret‑tape‑machine chain** (airwindows, slush, tape‑style saturation) to recreate the Beatles‑“bon bon” / Venus‑Theory‑Pressure fusion you once had in your head.

---

## LICENSE

This software is released under [your chosen license here].  
Its goal is **cultural + sonic preservation**, not commercial hardware‑cloning — it’s **emulation of behavior and vibe**, not a reproduction of Joh Mustad’s intellectual property.
```

***

You can paste that directly into `tubon-bon-bon/README.md`; it already includes your memory, the Tubon spec, and a clear “mission‑statement” for the repo. If you want, I can shorten it into a 1‑page summary version too.
