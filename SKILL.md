---
name: softserve
description: MJ's "Softserve" visual identity (v2, Aug 2026) — pure-black ground, his cream + pastel palette, Hotplate-style soft serif (Fraunces Soft) with Inter. Use whenever making ANY visual for MJ — LinkedIn infographic, carousel slide, poster, one-pager, lead-magnet PDF page, Substack header, slide deck, or any HTML that will be screenshotted — and when MJ says "softserve", "v2 style", "the new design", "hotplate style", or asks for something "in my style". Also load it when editing or reviewing an existing visual for brand consistency. (MJ's older v1 look — bold-caps Garamond, chalk underline, cream frame — is "Chalkboard"; only use that if he names it.)
---

# Softserve — MJ's design system v2

Soft serif, served on black. Locked on 2026-08-22. Reference doc (full spec with live specimens): `reference/design-doc.html`. Poster template: `template/poster.html`.

## Tokens

```
ground   #000000   pure black — the default poster/page ground
cream    #ffffeb   text on black, light ground  (PDF says #fffeb — typo, always #ffffeb)
pink     #ffbaff   hero accent / tags on black
mint     #c8ffba   positive, wins, receipts, CTA
sky      #baffff   tools, info, workflow
peach    #ffc8ba   old way, warnings, "before"
lemon    #f1ffba   highlight
ice      #ebffff   tint surface (screenshot bars, soft cards)
blush    #ffebff   tint surface
ink      #1a1a1a   text ON pastel grounds (soft ink — never pure black on pastel)
```

Dark surfaces on black: card `#121210`, inner row `#161614`, border `rgba(255,255,235,.16)`.
Light surfaces on cream: card `#ffffff`, border `rgba(26,26,26,.12)`, muted text `#6b6b60`.

## Type

```
display  "Fraunces"  wght 300–400, font-variation-settings "SOFT" 100, "opsz" 144
         letter-spacing -0.02em (−0.025em on posters), line-height 1.02–1.05, SENTENCE CASE
body     "Inter"  400 body · 500 lead/muted · 600 labels & tags
marker   "Permanent Marker"  hand notes only ("Step 1", list numerals). Max one note per slide.
```

Google Fonts link (the only font host that works in Artifacts):
`https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght,SOFT@9..144,300..500,100&family=Inter:ital,wght@0,400;0,500;0,600;1,400&family=Permanent+Marker&display=swap`

Fraunces is the stand-in for Hotplate's licensed Cooper Light BT. If MJ ever supplies Cooper, swap it in the `--display` stack.

Scale on a 1080×1350 poster: headline 72–88px, stat 200–240px, lead 30px, rows 26–28px, tag 24px, footer 22px.

## Shape

- Radius: poster/card 44px (20px in web docs), inner rows 26px (12–14px web), tags & buttons full pill (200px).
- Borders 1px at 12–16% of the text color. No glow, grain, chalk underline, drop-shadow rails, square corners, or cream frame — all of those are Chalkboard (v1).
- Screenshots: white card, 28px radius, `rotate(-2deg)`, one soft shadow `0 20px 60px rgba(0,0,0,.35)`. Real captures only.
- Pastels are FILLS (tags, pills, grounds), never outlines.

## Composition rules

1. One accent per poster, chosen by meaning (pink = hero claim, mint = win/number, peach = the old way, sky = tooling).
2. Headline ≤ 9 words, sentence case, Fraunces light. Caps only inside 13–24px labels.
3. At most two type sizes per poster beyond tag + footer.
4. Footer is always `MJ Jaindl` left and *Personal Brand, AI, & LinkedIn Growth* right (italic display). The headline never goes in the footer.
5. Build with real content. No lorem, no placeholder stats — pull numbers from MJ's context (`/mj` skill) or ask.
6. Three base layouts (all in `template/poster.html`, pick with `?layout=`):
   - `hero`  ("the Black") — black ground, pink tag, headline + one-line lead, tilted screenshot card bottom. Claim + receipt.
   - `list`  ("the Cream") — cream ground, black tag, headline + 3–5 white rows with marker numerals. Steps / files / checklist.
   - `stat`  ("the Mint") — pastel ground (mint default), cream tag, short headline, giant number, one-line muted proof. One number does the work. A non-mint ground is just "a peach stat", etc.
   MJ refers to layouts by ground color (the Black / the Cream / the Mint); the keys stay `hero|list|stat` in the template.
   Vary layouts across a batch; never ship three of the same.

## Render (JPG for LinkedIn / Airtable)

```bash
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --disable-gpu --hide-scrollbars --force-device-scale-factor=2 --window-size=1080,1350 --virtual-time-budget=6000 --screenshot=out.png "file:///path/to/poster.html?layout=hero" && sips -s format jpeg -s formatOptions 92 --resampleWidth 1080 out.png --out final.jpg
```

Then upload with `/Users/mj/Documents/GitHub/LinkedIn Posts/upload-to-airtable.sh final.jpg <recordId>` (see memory `infographic-pipeline`). Always view the PNG before sending — check footer clipping and text overflow first; those are the two recurring bugs.

## Process

1. Copy `template/poster.html` into the working dir, fill the layout's content, delete the other two layouts if shipping standalone.
2. Render, Read the PNG, fix overflow, re-render.
3. Show MJ the JPG before uploading anywhere.
