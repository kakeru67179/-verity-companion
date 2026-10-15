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


## 図形の納品ルートガイド（更新）
ソロルーム手順タブで「自分の像」と「2つの図形を集めるプレイヤー（納品先の像）」を選び、壁の影絵を選択してください。各影絵について、ナイトから回収する図形 → 選択したプレイヤーの像、という矢印付きのルートが表示されます。自分の像は納品先に選べません。表示は手順補助なので、実際の所持図形と像の状態をゲーム内で確認してください。

## ソロルーム：納品先自動案内（更新）
ソロルーム手順では左・中央・右の像の図形、自分の像、壁の影絵2つを入力すると、他の2人も正しい手順を進める前提で、ナイトから回収する図形と納品先の像を図形・矢印で案内します。スピード手順のルール（味方の図形はそれを持たない味方像へ、自分の図形は残る味方像へ）を使用します。像の図形が重複入力されている場合は案内を止めます。図形を納品すると壁の表示が変わるため、その都度選び直してください。


## Solo-room destination helper (assumed teammate flow)
The Solo Room helper now takes the left/middle/right statue symbols, the user's statue position, and the two current wall silhouettes. It gives a suggested destination statue for each wall symbol using the commonly documented speed-strat routing: a teammate symbol goes to the teammate statue that does not hold that symbol; when both wall symbols are the user's own statue symbol, send one to each other statue; when both are the same teammate symbol, recommend one transfer and ask the user to re-read the wall after the state changes. It validates that the three statue symbols are distinct.

This is a helper for a selected routing convention, not a live game-state reader. After a transfer, the room wall/knight drops may change; update the selected silhouettes before following another instruction. Confirm the visible buff and destination in-game.

Mechanics references consulted for this update:
- Traveler's Chosen Verity guide (Solo speed-strat rules): https://sites.google.com/view/travelerschosen/guides/salvations-edge/verity
- Salvation's Edge / Verity guide: https://www.destinypedia.com/Salvation%27s_Edge


更新：分配フェーズの各納品先に「納品した（記録）」ボタンを追加。押すと納品済みとして記録し、同じ像への重複記録を無効化します。入力条件を変更すると記録はリセットされます。


今回の更新：ソロルーム手順から指定された説明文を削除し、「集積フェーズ後に自分の所に来る図形（想定）」を①集積フェーズの納品手順の直後、②分配フェーズの前に表示するよう配置しました。
