---
name: reel-editor
description: Use when turning long raw footage (B-roll, archive or public-domain video, your own clips) into a short vertical reel or short, or when reviewing one — picking the moments, where to cut, assembling montages, rhythm, sound, captions, originality and credit.
---

# Reel Editor

Editing judgement for 7–45 second vertical reels (Instagram Reels, TikTok, YouTube Shorts, Facebook Reels), built from long raw footage. Made by **The Ask Why Company** (github.com/theaskwhy). Examples use aviation footage, but the method works for any subject: sport, wildlife, events, product, travel.

## Two lanes — decide first
- **Social / entertainment lane:** spectacle, montages, POV, "whoa" moments, series. You may combine clips from different times and places and re-order them freely — but never caption a montage as one specific real event ("jets in action", not "this jet today").
- **News lane (real events only):** verified facts; only footage of that event, or footage clearly labelled "File footage".
- Keep branding light: no logo intro, no watermark on every shot; at most a small end card.
- A human approves twice: after the shots are chosen, and before publishing. Never publish automatically.

## 1. Find the moment (onset → peak → recovery)
- Work in **event beats**, not source shots: a 10 s shot may hold 1.4 s worth keeping.
- For each candidate mark **onset** (action first visible), **peak** (best visual/sound instant), **recovery** (viewer has understood it).
- Starting trims at 30 fps: in-point **3–8 frames before onset**, out-point **6–18 frames after peak**. Rare or complex events may hold 1–2 s after the peak.
- Frame test: remove 2 frames from the front — still understood? From the back — still satisfying?
- Prefer action toward or past the camera, visible transformation (ignition, contact, launch, landing, splash, catch), strong natural sound peaks, unusual angles, human reaction.
- Deprioritise (don't auto-delete) static wides, long setup, shaky shots, interviews — use them only when they do a job (scale, one key line).
- A new angle must add stage, scale, mechanism, perspective, emotion or context — otherwise drop it.

## 2. Score every candidate (100) — vetoes win
Motion 20 · Audio 15 · Clarity 15 · Novelty 15 · Relevance 15 (fits the theme / shows the actual event) · Emotion 10 · Represents the caption 10.
**Veto:** rights unknown · subject or event identity unsure · crop hides key context · speed or sound would mislead · needlessly graphic.

## 3. Discovery pipeline for long files (free tools)
1. One folder per job; `source.txt` with asset URL/ID, creator, date taken, official caption, licence/rights notes. Never overwrite the original.
2. Scene split: `scenedetect -i raw.mp4 detect-adaptive list-scenes save-images -n 3`
3. **Fixed-interval contact sheet every 2–5 s** (great moments hide inside long continuous takes): `ffmpeg -i raw.mp4 -vf "fps=1/3,scale=320:-1,tile=6x6" sheet_%02d.png`
4. Loudness peaks: `ffmpeg -i raw.mp4 -af ebur128=metadata=1,ametadata=print:key=lavfi.r128.M:file=loud.txt -f null -` — a peak means "something changed", not what changed.
5. Speech only if useful: `whisper raw.mp4 --model small --output_format srt` — hand-check names and jargon.
6. Look at the sheets; first pass mark only (event begins / wow / information / sound); second pass onset-peak-recovery and score.
7. Cut selects frame-accurately: `ffmpeg -ss <in> -to <out> -i raw.mp4 -c:v libx264 -crf 18 -c:a aac sel_01.mp4`. Reframe to 9:16 around the **action path**, not just the subject centre.
8. **Silent rough cut first.** If it confuses without text or music, it isn't ready. Then sound, then text, then frame-level fine cut.
9. Finish in any editor (DaVinci Resolve Free, Meta Edits, CapCut free).

## 4. Montages from many videos
- Pick a theme and a 5–8 beat sheet (e.g. start → build → peak → second peak → resolution). Templates: start-to-finish of one action, power montage (5 subjects, one hero moment each), night/day contrast, then-vs-now (archive → modern), product or app tie-in (real footage → your product screen showing the same thing).
- Search public archives per beat (e.g. NASA, DVIDS, Wikimedia Commons, your own library), shortlist 3–6 per beat, download only the shortlist.
- Continuity: same subject type, consistent motion direction, group night/day, one colour look, carry one natural sound across 2–3 cuts.

## 5. Hook and structure
- First 1–2 s = the event, imminent action, or a striking image that raises a question. Never a logo card. Start mid-motion; never on black.
- Cold-open the peak for short spectacular events; build tension only when the anticipation itself is visual — and pay off fast.
- Don't spend your only great shot first: **peak glimpse → cause → full peak from a new angle → loop back**.
- Shapes: spectacle 7–15 s (0–1.2 hero, 1.2–3 orientation, 3–10 escalation, 10–14 full payoff, 14–15 loop); news 20–35 s (decisive visual + verified headline → who/what/where → evidence → why it matters → source); series 30–45 s (hook → question → proof → payoff → "Tomorrow: …").

## 6. Rhythm
- Spectacle 0.7–1.6 s per shot, hero hold 1.8–3.5 s; vary it (0.8 → 1.1 → 0.7 → **2.4** → 0.9). Accent inserts 0.3–0.6 s, rarely.
- News 1.2–2.5 s; hold 2–4 s when the viewer must read what's happening.
- Don't hyper-cut. Cut on action; keep motion direction for a continuous event.
- J-cut: next shot's sound 3–8 frames before its picture. L-cut: outgoing sound 6–15 frames under the next shot.
- Speed-ramp dead transit only, never the decisive moment.

## 7. Sound
Natural event audio first → voice → music. Music never buries the event. Never fake sync. Music only from each platform's own library, added inside that app (TikTok business accounts: Commercial Music Library); keep a clean master without music. No clipping; a deliberate rise at the hero moment.

## 8. Text and accuracy
One idea per card, ≤7 words, 1–2 s each; central safe area, above the bottom ~15%, never over the subject. Text says what the picture can't (what, where, when), from source metadata or verified reporting only. Must work muted. Don't infer dramatic claims from appearance (e.g. a vapor cone is not proof of supersonic flight; close formation is not refuelling).

## 9. Originality on Meta and others
- A limited or blocked post can be a copyright/rights match, an originality (recommendation) decision, a monetization decision or an account issue — check the platform's notice each time.
- Captions, borders, watermarks, stitching or speed changes **alone** don't make reused footage original. Do at least three real things: your own selection and order, a story (facts, voiceover or analysis), your sound design and reframing, your own footage or product screens.
- Instagram: reposting others' content 10+ times in 30 days without real improvement can lose recommendations. Never upload another app's watermarked export.
- Legal permission to use footage is not the same as being "original" to an algorithm.

## 10. Credit and rights
- Check each asset's own rights notes. Public-domain government media (e.g. NASA, U.S. DoD/DVIDS) usually requires: credit the source, no implied endorsement, no agency logos as your branding, care with identifiable people in promotional use; some items contain third-party material.
- Never re-upload other creators' clips. Log every asset ID.

## 11. Export, QA, measure
- 1080×1920, H.264, no watermark. Watch full-screen at phone size once with sound, once muted; check crop, text, flash/black frames, duplicates, clipping, hero obvious.
- Measure at 24 h and 7 d: 1 s/3 s survival, midpoint, completion (definitions differ per platform), watch ratio, replays, shares and saves per 1,000 plays, follows per 1,000 reached. Never pool platforms. Test one variable at a time; adopt a rule only after it wins repeatedly on your own account.

---
Reel Editor by The Ask Why Company · MIT licence · https://github.com/theaskwhy/skills
