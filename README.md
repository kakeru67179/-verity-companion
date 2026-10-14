# Verity Companion PWA (prototype)

A Japanese/English, mobile-first PWA prototype for Destiny 2: Salvation's Edge, Encounter 4 (Verity).

## Prototype features
- Main Room dissection helper: enter three Solo Room 2D statue symbols and three current Main Room 3D shapes.
- Computes target 3D shapes and searches for a candidate sequence of component swaps.
- Solo Room mechanics checklist.
- Ghost-phase identity checklist (manual only; no Bungie API connection).
- Japanese/English toggle, copy results, offline caching after first visit.

## Run locally
The simplest option is to serve the folder with any static web server. For example, with Python installed:
```bash
python -m http.server 8000
```
Then open `http://localhost:8000` on the same device, or use a LAN address to test from a phone. Service workers require HTTPS or localhost.

## Deploy as a public PWA
### GitHub Pages
1. Create a GitHub repository and upload the contents of this folder (not just the ZIP).
2. In repository Settings → Pages, select deployment from the `main` branch and `/ (root)`.
3. Wait for deployment, then open the HTTPS URL on iPhone/Android.
4. iPhone Safari: Share → Add to Home Screen.
5. Android Chrome: menu → Install app / Add to Home screen.

### Other static hosting
Upload the files to any HTTPS static host (for example Netlify, Cloudflare Pages, or Vercel). No backend or API keys are required.

## Important caveats
- This is an initial prototype, not a fully validated raid solver. Verify every generated swap against the encounter state before acting.
- The solver models each 3D shape as two 2D components and searches swaps between components while preserving the total component count. It does not model Knight drop positions, timing, or every encounter-specific execution constraint.
- Ghost phase is a manual checklist; automatic Bungie identity lookup is not implemented.
- The first successful load needs network access; the service worker caches the app for later offline use.
- Use original artwork only if you have rights to it. This prototype uses CSS/Unicode symbols and no Destiny game assets.

## Reference material used to inform mechanics
- https://github.com/saffronrust/VerityCompanion
- https://destiny2.vaexil.tv/tools/verity
- https://www.destructoid.com/destiny-2-salvations-edge-fourth-encounter-raid-guide-verity/


## Detailed swap instructions
The outside solver now displays each candidate swap as two explicit direction statements (take a component from one statue and place it at the other), plus before/after 3D shapes for both statues. Treat the sequence as a planning aid and verify it against the live encounter mechanics.


## 平面図つき交換手順版
各交換ステップに、左・中央・右の像が持つ平面図形（○・△・□）を交換前／交換後で表示し、どの像からどの像へ図形が移るかを矢印で示します。黄色の図形がその手順で動かす図形です。


追加変更：メインルームの交換手順の最後に、左・中央・右それぞれの完成図形を平面図記号と立体名で表示します。
