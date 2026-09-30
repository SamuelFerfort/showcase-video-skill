# showcase-video

An agent skill that makes polished motion-design product videos (launch films, promos,
app showcases) entirely in code, with an original soundtrack. You approve one plan; the
agent then builds, reviews and fixes the video on its own until it passes QA.

```bash
npx skills add SamuelFerfort/showcase-video-skill
```

Then ask your agent something like *"make a 60-second launch video for our app"*.

## What it does

1. **Researches** 4–6 reference launch videos (it measures their cuts, shot lengths,
   light/dark and music with ffmpeg, and reads contact sheets). It also studies your
   real product from its source code: theme tokens, strings, components, logo, icons,
   fonts.
2. **Proposes three distinct directions,** built from your product's own visual DNA:
   logo shapes, its core verb, its "magic moment". A storyboard on a musical grid and an
   asset sheet show where every image comes from. You approve once.
3. **Produces autonomously.** Scenes are frame-exact HTML (every frame is a pure function
   of time), rendered by headless Chromium and ffmpeg. The music and SFX are synthesized
   from the same timeline, so every sound lands on its frame, and nothing needs
   licensing.
4. **Loops until it's right:**
   - review packs (scene sheets, filmstrips across every cut, lint for text cut off by
     the frame) judged by a fresh reviewer subagent against a rubric;
   - automated QA of the final file: frame count, colour, loudness, and unplanned jumps
     detected per frame.
5. **Delivers versions side by side:** master, web and a share copy (≤ 15 MB), plus a
   live browser preview with sound for the human check.

A per-user profile (`~/.config/showcase-video/profile.md`) remembers your preferences
and past videos, so the next film is different.

## Requirements

Node ≥ 20, [bun](https://bun.sh), ffmpeg, ImageMagick 7, Playwright with
`chromium-headless-shell`, [uv](https://docs.astral.sh/uv/) (logo tracing), yt-dlp
(reference research), poppler (document pages). Linux or macOS (Windows through WSL).
Rendering 1080p60 supersampled needs about 2–3 GB of RAM per worker.

## Layout

```
skills/showcase-video/
  SKILL.md        the workflow
  references/     research, devices (creative vocabulary), engine, quality loop, audio, render
  scripts/        new_project, analyze_refs, asset_sheet, store_badges, pdf_passage, qa
  template/       a working 12 s project: engine, synth, renderer, review and QA hooks
```

## Notes

- Reference videos are downloaded only for private analysis. Never reuse their footage
  or music.
- Store badges are fetched from Apple's and Google's official sources and must be used
  unmodified.

## License

MIT (see LICENSE). Bundled third-party files keep their licenses: the Inter font
(SIL OFL 1.1, `template/assets/fonts/Inter-OFL.txt`) and Lucide icons (ISC,
`template/assets/Lucide-LICENSE.txt`).
