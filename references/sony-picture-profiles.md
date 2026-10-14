# Sony Picture Profiles (a6600) & Menu-Settings Export

Two different exports live here: Picture Profiles (color/tone science, PP1-PP10) and a plain menu-settings cheat sheet (everything else — AF, drive, metering, etc.). Neither is a file format Lightroom or any external app reads; these are things the user types into the camera's own menu, or saves/loads via the camera's native Save/Load Settings feature.

## Important caveat to tell the user

**Picture Profile only affects JPEG/HEIF rendering and video — it does not touch RAW data.** If the user shoots RAW (recommended per the settings profiles in this skill), Picture Profile is cosmetic for their JPEG preview/thumbnail only; the actual grading happens in Lightroom via the preset in `references/lightroom-xmp-template.md`. Picture Profile matters for real when: shooting video (baked into the footage, no RAW equivalent on this body), or shooting JPEG-only.

## Factory Picture Profile defaults (PP1–PP10)

- **PP1** — Gamma: Movie. General-purpose video gamma, moderate contrast.
- **PP2** — Gamma: Still. Mimics the camera's still-photo tone response for video.
- **PP3** — Gamma: ITU709 (Natural preset). Flatter, natural color — a reasonable base for light grading.
- **PP4** — Gamma: ITU709. Standard broadcast-style contrast/color.
- **PP5** — Gamma: Cine1. Soft gradation in dark tones, deep colors — good for a cinematic look with easy grading.
- **PP6** — Gamma: Cine2. Similar to Cine1 but tuned to retain more highlight detail (less clipping) — easier for broadcast/delivery.
- **PP7** — Gamma: S-Log2, Color Mode: S-Gamut. Flat log profile for heavy grading; wide dynamic range, needs grading to look normal. Shoot at base ISO 1600 for best noise performance on this body.
- **PP8** — Gamma: S-Log2, Color Mode: S-Gamut3.cine. Same log curve as PP7, wider/cinema-oriented color gamut.
- **PP9** — Gamma: S-Log3, Color Mode: S-Gamut3. Even flatter, wider dynamic range than S-Log2; more grading latitude but needs confident grading skills. Base ISO is higher on this profile — check exposure carefully, don't just eyeball the flat image.
- **PP10** — Gamma: HLG2/HLG3 (Hybrid Log-Gamma). For direct HDR delivery (HDR TVs) without a grading pass — not a log profile to grade, closer to "shoot and play back as-is."

## Recommended Picture Profile by scenario

- **Portrait** — PP3 or Off/standard JPEG rendering; avoid log profiles unless grading every shoot — skin tones are easiest to get right straight out of camera.
- **Action/Wildlife (stills)** — Picture Profile is irrelevant if shooting RAW (the normal recommendation here); leave off.
- **Low-light/Astro (stills)** — same: irrelevant for RAW. Leave off; don't add log gamma noise/latitude tradeoffs to an already-high-ISO RAW workflow.
- **Video (general handheld)** — PP1 or PP4 for straight-out-of-camera footage with minimal grading; PP5/PP6 (Cine1/Cine2) for a filmic look that still grades easily; PP8/PP9 (S-Log2/S-Log3) only if the user is comfortable grading and wants maximum dynamic range — mention the higher base ISO requirement.
- **Street** — leave off if RAW; PP3 if shooting JPEG for a natural, true-to-scene look.

## Menu-settings cheat sheet (Save/Load Settings)

The a6600 can save its entire menu configuration to the SD card and reload it (Setup menu → Reset/Setting → Save/Load Settings), but this writes a proprietary binary file only another a6600 (or compatible body) can read — not something this skill can generate or edit as a file. What the skill *can* do is produce a readable cheat sheet: a menu-path-by-menu-path checklist the user can follow to manually configure the camera to match a given settings profile from `references/settings-profiles.md` or a saved profile in `/topics/camera-gear.md`.

When asked for this, format it as a short checklist, menu tab → item → value, e.g.:

```
Camera Settings 1 → Drive Mode → Continuous Hi
Camera Settings 2 → Focus Mode → AF-C
Camera Settings 2 → Focus Area → Zone
Camera Settings 2 → Metering Mode → Multi
Exposure/Color → ISO → Auto (cap at 6400 via ISO Range Limit)
```

Pull the actual values from the relevant settings profile rather than inventing new ones — this cheat sheet is a restatement of the same profile in menu-navigable form, not a new recommendation.
