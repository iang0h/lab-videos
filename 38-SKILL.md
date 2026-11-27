---
name: infographic-videos
description: Produce short vertical infographic explainer videos (map or paper style) from an approved script, with beat-matched scenes, phrase-boundary captions, continuous motion and a loudness-checked voiceover. Use for social-feed explainers, especially a recurring series with a consistent house style.
---

# Infographic videos

Pipeline: brief -> script -> voiceover -> storyboard -> frames -> encode -> QC -> delivery. Nothing reaches the owner without an independent review.

Tags: **MUST** = correctness or reliability. **CHECK** = depends on a platform or standard; confirm the current spec. **HOUSE** = a deliberate series identity rule (look, motion, loudness target). House rules are enforced across a series, but they are design decisions, not platform or safety facts. **STYLE** = author choice; change freely, but stay consistent across a series. Numbers not tied to a source are author-chosen starting points.

Provenance: the HOUSE rules and numbers are the working spec of the delivered Ian Goh Lab videos (see the repo README catalog); every delivered video was built and QC'd under them. Change a house rule only from reviewed real-video evidence (see section 4).

## 0. Brief (MUST)

Audience, one-sentence takeaway, target platform, a source for every fact, a licence for every asset (voice, music, fonts, map data, icons), and the house style. Keep the brief with the project.

## 1. Script first

- MUST: one idea per video; every number, date and claim has a source; illustrative figures are labelled as examples. Never show invented numbers as facts.
- MUST: get the script approved before building. The spoken script is the post caption, write it once, approve it, then build.
- STYLE: ~30 seconds, 5–7 scenes as a starting point; the first frame must hook; read aloud to check pace.
- STYLE (story shape that works): hook -> problem -> first-person story -> method -> question to the viewer -> closing line + end card. Skeleton:
  1. Hook: name the pain in one line.
  2. Problem: show why the obvious fix fails.
  3. Story: what you actually did, first person.
  4. Method: the repeatable rule, shown as steps or a ladder.
  5. Question card: turn it to the viewer.
  6. Closing line + end card.

### Scene plan (MUST; one row per scene, kept with the project)

| Field | Content |
| --- | --- |
| time | start–end in seconds, set from the checked audio timings |
| narration | exact words spoken in this scene |
| visual | what is on screen, including icons and map area |
| motion | what moves, which direction, and how it carries into the next cut |
| caption | on-screen text for the scene |
| source | where each fact or figure comes from, or "example" |

## 2. Voiceover and timing

- MUST: use a voice you are licensed to use. HOUSE: keep the same voice across a series. Listen to the whole take for wrong names, numbers and acronyms; fix and regenerate.
- MUST: get word timings from forced alignment or speech recognition, then check them against the audio. Recognition can mis-time or mis-hear; never treat it as truth. Captions must show the script's words, patch recognition errors (names, coined terms) before rendering text.
- MUST: the video ends with the narration, plus any planned tail. Set the end time from the checked audio duration, not the beat sheet. Every narrated word is covered by a visual that is on screen while it is spoken.
- HOUSE: the closing line is narrated over the end card, so the end card is the last narration visual and the video ends when that line ends (plus any planned tail, such as a short music tail, recorded in the scene plan). A silent beat before the end card carries no narration.
- HOUSE loudness: target −14 to −15 LUFS integrated, true peak ≤ −1 dBTP, measured on the encoded file. Recipe: apply gain and a limiter, encode, measure (QC step 4), adjust the gain, repeat until the measured values are in range. Real house pass: `ffmpeg -i mix.mp4 -c:v copy -af "volume=12.9dB,alimiter=limit=0.668:level=false" -c:a aac -b:a 160k out.mp4` (landed −15.0 LUFS, −3.3 dBTP on a delivered master; tune the gain per mix, and always measure the encoded result because the AAC re-encode can move the peak). CHECK: platforms and standards differ and may adjust playback level; broadcast EBU R 128 is −23 LUFS. State your target and measure the final file.
- Music (STYLE): only licensed music, kept under the voice; record the credit.

## 3. Visual language

- CHECK: 9:16 vertical; 1080×1920 is a common working size. Apps overlay buttons and captions, so keep text off the edges and preview on a real phone. Treat any safe-zone percentage as a starting point you verify.
- MUST: text contrast at least 4.5:1 (3:1 for large text) per WCAG 2.2 SC 1.4.3; do not use colour alone to carry meaning.
- HOUSE: one aspect ratio per series. Series consistency: same title strip, same footer, numbered scene tags ("LABEL / 03"), same end card. A viewer should recognise the series from one frame.
- HOUSE (map style): cream paper, ink, one red accent; blue only for people. Dim the map background to ~40% so the foreground pops.
- HOUSE: one icon language: solid pictogram people, clean geometric props, 8–11px strokes. Do not mix styles.
- HOUSE: fixed type scale: condensed bold strip titles, same size in every scene; note-card labels large enough to read on a phone.
- HOUSE end card: red slam word with an iris wipe; the narrated closing line lands here; contact details once, centred. Captions continue on the end card for the narrated line, kept clear of the slam word and contact details. Licence and credit text, if required, goes in the delivery notes or post text.
- Branding with real footage: real screen recordings of the product can play inside phone, badge or doorway frames. Crop OS status and nav bars; keep the app's own UI chrome, that chrome is the branding. Get the owner's OK for whatever is visible in the clip, and leave out any clip that shows a child.

## 4. Motion (HOUSE rules, tuned by review of real delivered video)

- HOUSE: no frozen frames. Near-still scenes keep a slow drift (a slow camera move or a gentle element loop). QC step 2 flags any hold for review.
- HOUSE: cuts carry motion. Every seam has one element mid-motion: the exiting element sets up the entering one, same direction and similar speed, and the cut lands while it is moving. A hard cut that fails this is a QC fail. If a seam cannot carry an element (for example a scene change to the end card), use the planned transition (such as the iris wipe) and record it in the scene plan.
- HOUSE: sound first. Cut scenes on the voiceover beats; visual cues land on the spoken word.
- HOUSE: one dominant direction per film. Vary shot lengths at least 4x between longest and shortest, with one near-still stretch of about 1 s (the question card or a pre-end-card beat) before the closing line slams in; the contrast makes the end land.
- HOUSE: the camera leads the subject by about 0.1 s. Moves above roughly 80 px per frame at 30 fps are the house trigger for the shutter-trail ghost look, as used in the delivered videos. If ghost trails are the intended look, apply them deliberately and keep them consistent.
- MUST (accessibility): avoid more than three flashes in any one-second period (WCAG 2.2 SC 2.3.1; that page also allows below-threshold flashes, so the three-flash line is not a complete safety test). If a design has strobing, rapid light/dark alternation, or a full-screen white or red flash (the iris wipe and slam word included), check it with a flash analyser. Whip-pans and slams are motion, so also check them by eye.
- Changing a motion rule: argue the change from a reviewed real delivered video, with the frames or timecodes that show the problem. Synthetic test clips can check that a command runs, not whether a motion rule works.

## 5. Captions

- MUST (accessibility, WCAG 2.2 SC 1.2.2): captions cover the speech and meaningful non-speech sounds. HOUSE: the on-screen captions are the narration, verbatim, in phrase chunks timed to the checked audio, including the closing line on the end card. Break at phrase boundaries: no mid-word splits, no conjunctions or articles at line ends. HOUSE goal: no single-word lines. If a chunk would leave one, retime or reflow the chunks; never drop or change words to fix a line break. A chunk is a caption cue; scenes contain several cues. Short summary text, labels and strip titles are separate design elements, not captions.
- STYLE: two lines at most (~32–42 characters per line); condensed bold white on an ink bar in the lower third; shrink one step when a two-line split does not fit.
- CHECK: where the platform accepts a sidecar caption file, provide one (SRT cues from the same chunk list). Example cue: `1` / `00:00:00,200 --> 00:00:02,600` / `Where does your parcel go` / `after you click buy?`
- Verify caption breaks on the encoded file, not in the editor.

## 6. Encode

- CHECK: H.264 video and AAC audio in MP4, yuv420p, constant frame rate, `-movflags +faststart`; Main profile with `-bf 0` is a conservative compatibility choice. Example: `ffmpeg -i in.mov -c:v libx264 -profile:v main -bf 0 -pix_fmt yuv420p -crf 20 -r 30 -c:a aac -b:a 160k -movflags +faststart master.mp4`
- HOUSE delivery rule: a master plus a share copy under 15 MB. CHECK: size limits differ by route and change; confirm the limit for the route you use.

## 7. QC (run on the encoded file; record results)

1. Probe: `ffprobe -v error -show_entries format=duration:stream=codec_type,codec_name,profile,width,height,r_frame_rate,pix_fmt,duration -of default=nw=1 file.mp4`. Check specs against the plan; audio and video durations match the planned end.
2. Freeze: `ffmpeg -i f.mp4 -vf freezedetect=n=-55dB:d=0.4 -an -f null -` (house values, verified on delivered builds: slow-drift scenes pass, real holds are caught; recalibrate if your drift scenes are flagged or a real hold slips through). A reported freeze is reviewed, and an unintended hold is a fail.
3. Black and silence: `-vf blackdetect=d=0.5:pix_th=0.10` and `-af silencedetect=n=-50dB:d=0.5`. Unintended hits fail.
4. Loudness and true peak: `ffmpeg -i f.mp4 -af ebur128=peak=true -vn -f null -`; read the Summary, compare with the stated target.
5. Flash: watch for rapid light/dark change; run an analyser for strobing, wipes or slams that flash.
6. Captions: watch the full file with sound; check that cues match the script verbatim, spelling, numbers, timing, line breaks, and that the closing line is captioned on the end card.
7. Facts: trace each claim to its source.
8. Cuts: a 1-frame-per-second sheet is only an overview. To inspect a cut at 3.000s, tile six consecutive frames around it: `ffmpeg -ss 2.9 -i f.mp4 -vf "select='lt(n,6)',scale=270:-1,tile=6x1" -frames:v 1 -vsync 0 cut.png` (older ffmpeg builds use `-vsync 0`; newer ones use `-fps_mode passthrough`; this form ran on ffmpeg 4.4 with a synthetic clip). The seek lands on the frame nearest 2.9 s, so the six tiles show the frames around the cut; for an exact frame, use `select='between(n,87,92)'` on the numbered frames instead. Per the house rule, the outgoing and incoming shots share the planned moving element, with no jump or flash. A still sheet cannot prove motion continuity, so also step through the cut in a player.
9. Phone check, with and without sound, including that captions clear the app's overlays.
10. Independent review: someone other than the builder passes the video before the owner sees it.

Common failures (check these first):

- Caption orphans: a single word alone on a line. Retime or reflow; never drop words.
- ASR names: recognition mis-hears names, coined terms and numbers. Patch them to the script before rendering text.
- Frozen frames: a still scene with no drift. Add slow motion; freezedetect flags it.
- Loudness after AAC: levels measured before encoding drift after it. Measure the encoded file.

## 8. Delivery

- Deliver: master, share copy, approved script, sources and licence notes; caption file where the platform takes one.
- Post text comes from the approved script, verbatim; keep claims unchanged if shortened.
- MUST: nothing is posted without the owner's explicit OK.

## Worked storyboard example (invented scenario and figures, labelled as examples)

Takeaway: "A parcel usually crosses several hubs before it reaches your door."

| time | narration | visual | motion | caption cues (verbatim) | source |
| --- | --- | --- | --- | --- | --- |
| 0.0–3.0 | Where does your parcel go after you click buy? | Dimmed map, red pin at a warehouse | Pin pulses, camera drifts right | "Where does your parcel go" / "after you click buy?" | example |
| 3.0–9.0 | First it moves to a regional hub. | Truck icon drives right to hub 1 | Truck exits right and enters the next scene from the left | "First it moves" / "to a regional hub." | example |
| 9.0–16.0 | Then it may cross several more before the last mile. | Line extends through hubs 2 and 3 | Same direction, same speed | "Then it may cross several more" / "before the last mile." | example |
| 16.0–22.0 | A courier carries it to your door. | Courier icon, house icon | Courier moves right, stops at the door and the camera keeps drifting | "A courier carries it" / "to your door." | example |
| 22.0–23.0 | (no narration) | Near-still map, slow drift | Slow drift, no hold | (none) | n/a |
| 23.0–28.0 | Delivery is part of the product. | End card: red slam word, contact once | Slam word lands on "product"; iris wipe from the courier's door | "Delivery is part of" / "the product." | n/a |

Shot lengths run from 1 s to 7 s (7x), with the near-still beat before the end card. The closing line is the last narration and plays over the end card. Times are placeholders: set them from the checked audio. Replace the example rows with sourced facts for a real video.

## Sources

- EBU R 128 (broadcast loudness, context only): https://tech.ebu.ch/docs/r/r128v5_0.pdf
- WCAG 2.2 Understanding 2.3.1 (flashes): https://www.w3.org/WAI/WCAG22/Understanding/three-flashes-or-below-threshold.html
- WCAG 2.2 Understanding 1.4.3 (contrast): https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
- WCAG 2.2 Understanding 1.2.2 (captions): https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded.html
- FFmpeg filters (freezedetect, blackdetect, silencedetect, ebur128, loudnorm): https://ffmpeg.org/ffmpeg-filters.html