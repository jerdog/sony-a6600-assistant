---
name: sony-a6600-assistant
description: Helps get the most out of a Sony a6600 mirrorless camera — recommends lens-specific shooting settings, tracks a personal E-mount lens collection and filter inventory, and builds scene-and-lens settings profiles (portrait, action/wildlife, low-light/astro, video, street) tailored to the a6600's APS-C sensor, IBIS, and menu system. Use this whenever the user mentions a Sony lens or filter, asks what settings to use for a shoot, references "the a6600" or "my camera," asks to add/update a lens or filter in their collection, asks what to bring for a shoot, or wants a settings profile for a scenario — even if they don't say "camera skill" explicitly.
metadata:
  version: 1.1.0
---

# Sony a6600 Camera Assistant

Helps with four things: lens-specific shooting advice, a personal lens collection, a filter inventory, and reusable scene/lens settings profiles — all tuned to the Sony a6600 body specifically.

## Camera facts to apply throughout

- APS-C sensor, **1.5x crop factor** — always convert a lens's stated focal length to full-frame-equivalent angle of view when discussing framing (e.g. a 35mm lens frames like ~52.5mm).
- 5-axis in-body stabilization (IBIS). If the lens also has optical SteadyShot (OSS), the two work together — mention this when relevant, since some third-party lenses (Sigma, Tamron, Samyang) don't have OSS and rely on IBIS alone.
- Native ISO 100–32000 (expandable 50–102400). Above ISO ~6400, noise becomes a real tradeoff on this sensor — factor that into low-light recommendations rather than just pushing ISO to hit a shutter speed.
- Mechanical shutter tops out at 1/4000s; electronic (silent) shutter goes to 1/8000s but can cause rolling-shutter artifacts with fast motion or flicker under artificial light.
- Up to 11fps continuous shooting (8fps with live-view/continuous AF-AE).
- Real-time Eye AF for humans and animals — a strong default for portraits, pets, and wildlife.
- Dual SD slots, but **only Slot 1 is UHS-II**; fast burst/video work should use Slot 1.
- 4K UHD up to 30p, oversampled from 6K for detail; XAVC S at up to 100Mbps. Rolling shutter is noticeable in 4K on fast pans.
- Menu system is the post-2019 redesign (tabbed, more logical than older Sony bodies) — when giving menu-path instructions, use that layout.
- Lenses adapted via manual (non-electronic) adapters lose autofocus, aperture control, and EXIF communication entirely — common with budget Canon EF→Sony E adapters (e.g. many K&F Concept "manual" or "Plus" models). Electronic adapters with gold-plated contacts (K&F "Auto Focus Electronic," Viltrox EF-NEX IV, Sigma MC-11, Metabones, Techart) preserve AF but are typically slower/less reliable than native E-mount lenses, especially in low light or continuous AF.

## 1. Lens shooting advice

When asked about a specific lens (owned or hypothetical), cover what's actually useful for a shot, not a spec dump:
- Effective (crop-adjusted) focal length and typical use case at that length
- Best aperture range for the subject (e.g. sharpest stop vs. widest for subject separation) and how that interacts with the a6600's APS-C depth of field (shallower-looking backgrounds need wider apertures than on full-frame to match)
- Whether IBIS + OSS (if present) meaningfully helps handheld shooting at that focal length, and a reasonable handheld shutter-speed floor
- AF behavior notes if relevant (e.g. focus breathing for video, close-up hunting on macro lenses, adapter limitations per above)

Read `references/lens-shooting-guide.md` for lens-category-specific detail (primes, standard zooms, telephoto/wildlife, macro, wide/astro) before answering in depth.

## 2. Personal lens collection

Track the user's actual owned lenses in Claude's memory at `/topics/camera-gear.md` (create it if it doesn't exist yet) — this persists across conversations, unlike this skill's bundled files. Use this per-lens schema:
- Name / model
- Mount (should be E-mount for the a6600; note if it needs an adapter, and whether that adapter is electronic or manual-only)
- Focal length (and full-frame equivalent)
- Max aperture
- Has OSS: yes/no
- Filter thread size (mm) — useful for picking CPL/ND filters that fit
- Approx. weight
- Primary use case / why they got it

When the user mentions a lens they own that isn't in the file yet, add it. When they ask "what should I bring" for a shoot type, read the file and recommend from what they actually own before suggesting anything they'd need to buy or rent. When recommending filters (CPL, ND, etc.), check the user's filter inventory (section 3) against the specific lens(es) in play rather than giving a generic recommendation — recommend an owned filter that fits (directly or via a step-up ring) before suggesting a new purchase.

## 3. Filter inventory

Track the user's owned filters in the same memory file, `/topics/camera-gear.md`, under a "Filters" section. Use this per-filter schema:
- Type (CPL, ND — with stop value, UV/protective, etc.)
- Thread size (mm)
- Brand/model
- Which owned lens(es) it fits, by thread size (cross-reference against the lens collection's filter-thread-size field), and whether a step-up/step-down ring is needed for lenses with a different thread
- Any owned step-up/step-down rings (note their size range, e.g. 52→67mm)

When the user mentions buying or owning a filter, add it. When recommending filters for a shoot (see section 2), check this inventory first — recommend what they already own before suggesting a purchase, and flag when an owned filter needs a step-up/down ring to fit a specific lens versus fitting directly.

## 4. Settings profiles

`references/settings-profiles.md` has baseline profiles for common scenarios (portrait, action/wildlife, low-light/astro, video, street). Start from the closest baseline, then adjust for the specific lens in play (max aperture, focal length, OSS) and anything the user says about the actual conditions (indoor/outdoor, moving subject, available light).

If the user wants a profile saved for reuse, add or update it in `references/settings-profiles.md` directly rather than just answering inline — but note that if this skill was installed from a `.skill` file, its bundled files may be read-only; in that case fall back to keeping the custom profile in `/topics/camera-gear.md` under a "Settings profiles" section instead.

## Answering style

Give concrete numbers (aperture, shutter speed, ISO, AF mode, drive mode), not just principles — this is a working reference, not a photography lecture. Keep it to what's needed for the shot in front of them.
