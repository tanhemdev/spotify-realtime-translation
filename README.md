# Spotify Real-Time Translation

> Live podcast translation using NLP and speech synthesis

**Status:** product concept and PRD, no code yet. For a working, tested translation product, see [LyricSync](https://github.com/tanhemdev/lyric-sync) ([live demo](https://tanhemdev.github.io/lyric-sync/)).

<p align="center">
  <img src="https://img.shields.io/static/v1?style=for-the-badge&label=type&message=AI%20%2F%20NLP&color=10b981" alt="AI / NLP" />
  <img src="https://img.shields.io/static/v1?style=for-the-badge&label=role&message=product%20design&color=6366f1" alt="Product Design" />
  <img src="https://img.shields.io/static/v1?style=for-the-badge&label=delivery&message=full%20PRD&color=f59e0b" alt="Full PRD" />
</p>

---

<table>
  <tr>
    <td align="center"><b>NLP</b><br /><sub>pipeline design</sub></td>
    <td align="center"><b>4+</b><br /><sub>target languages</sub></td>
    <td align="center"><b>RT</b><br /><sub>latency target</sub></td>
    <td align="center"><b>PRD</b><br /><sub>stage</sub></td>
  </tr>
</table>

---

## Problem

Podcasts are locked to their original language. A Hindi speaker can't access a top English-language podcast in real time. Existing translation tools are built for text or pre-recorded video — not for audio-first, real-time consumption where latency and tone preservation matter.

## Solution

Designed a real-time translation layer that sits between the audio stream and the listener. The pipeline chains NLP transcription → neural machine translation → voice synthesis, delivering translated audio with minimal perceptible delay.

**What I did:**

- Designed the end-to-end **NLP pipeline architecture** — transcription, translation, synthesis
- Mapped edge cases that break naive translation: multiple speakers, code-switching, music segments, crosstalk
- Wrote a **full PRD** with technical requirements for the ML engineering team
- Designed **latency-aware mode switching** — different latency tolerances for news (strict) vs. comedy (looser) vs. interview (adaptive)
- Estimated addressable market across multilingual podcast audiences

## Pipeline Design

```
Audio Stream → ASR Transcription → Speaker Diarization
     ↓
Neural Machine Translation (4+ language pairs)
     ↓
Voice Synthesis (tone-matched) → Translated Audio Stream
```

## Edge Cases Addressed

| Scenario | Solution |
|---|---|
| **Multiple speakers** | Speaker diarization before translation, per-speaker voice profiles |
| **Code-switching** | Language detection at segment level, skip-translate for native segments |
| **Music segments** | Audio classifier to detect music vs. speech, passthrough for non-speech |
| **Humor / idioms** | Content-type aware translation with cultural adaptation layer |
| **Latency spikes** | Buffer management with graceful degradation, mode-specific thresholds |

## Deliverables

- Full PRD covering 4+ target languages (Hindi, Spanish, Mandarin, Portuguese)
- Technical architecture spec for ML team
- Latency budget analysis per content type
- User research on multilingual podcast consumption patterns

---

<sub>Built by <a href="https://github.com/tanhemdev">Tanya Hemdev</a> · UC Berkeley · Cognitive Science + Data Science</sub>
