# IMPORT HANDOFF — style_v2 painted_v4 → import_v4

## Freeze / 冻结
- **painted_v4 OK for import**（2026-09-23 冻结）
- **No reference image** used in this pack（v3 voided for likeness）
- Turnarounds **NOT yet** — OK to use 3/4 fullbody for battle idle now
- Size: **256×256** PNG transparent（TA override；原 `EXPORT_SPEC.md` 写 512，对本波 style_v2 由 TA 覆盖为 256，便于整包 ≤800KB、battle_units ≤250KB，后续还要叠 atk/hit）

## File table / 文件表

| key | file | size | bytes | class CN/EN | handedness lock | anchor |
|---|---|---|---|---|---|---|
| `unit_ally_01` | `unit_ally_01.png` | 256×256 | 41966 B | 剑士 / Swordsman | sword RIGHT (左手握拳) | originX=0.4231363859617789, originY=0.980 |
| `unit_ally_02` | `unit_ally_02.png` | 256×256 | 52847 B | 弓手 / Archer | bow LEFT | originX=0.21023029233070364, originY=0.980 |
| `unit_ally_03` | `unit_ally_03.png` | 256×256 | 55960 B | 守护者/重盾 / Guardian | shield RIGHT / hammer LEFT | originX=0.3196310457324408, originY=0.980 |
| `unit_ally_04` | `unit_ally_04.png` | 256×256 | 40549 B | 刺客 / Assassin | dual daggers BOTH hands | originX=0.5150922851902584, originY=0.980 |
| `unit_ally_05` | `unit_ally_05.png` | 256×256 | 70052 B | 治疗师 / Healer | staff RIGHT | originX=0.5008844679973022, originY=0.980 |
| `unit_ally_06` | `unit_ally_06.png` | 256×256 | 48657 B | 法师 / Mage | staff RIGHT | originX=0.3929697745449734, originY=0.980 |
| `unit_ally_07` | `unit_ally_07.png` | 256×256 | 44258 B | 召唤师 / Summoner | tome BOTH hands (chest) | originX=0.2613339887250493, originY=0.980 |
| `unit_ally_08` | `unit_ally_08.png` | 256×256 | 53289 B | 吟游诗人 / Bard | lute chest BOTH hands | originX=0.29131532702507434, originY=0.980 |

## Handedness locks / 左右锁定（角色自身）
| Class | Lock |
|---|---|
| 剑士 Swordsman | sword **RIGHT** |
| 弓手 Archer | bow **LEFT** |
| 守护 Guardian | shield **RIGHT** / hammer **LEFT** |
| 刺客 Assassin | dual daggers **BOTH** |
| 治疗 Healer | staff **RIGHT** |
| 法师 Mage | staff **RIGHT** |
| 召唤 Summoner | tome **BOTH** (chest) |
| 诗人 Bard | lute **chest BOTH hands** |

## Anchor / 锚点
- **Foot bottom center**（脚底中心）
- `originX = 0.5`，`originY ≈ 0.92–0.98`（见上表逐文件）
- 设计坐标约定同 MVP：单位脚底中心锚点；bleed ≥4px

## Atlas / 图集
- Recommend **`battle_units` separate from `ui_common`**
- This pack ships: `battle_units_style_v2.png` + JSON (1024×512, 458071 B)
- TA：WebP/compress guidance **≤250KB** for battle_units atlas if known
- Ally teal ID `#2EC4B6` / enemy coral `#E85D4C` — **enemy skins NOT in this pack**（allies only；enemy recolors later）

## Suggested Phaser path
`assets/units/style_v2/`
（或加载 `battle_units_style_v2.json` hash atlas）

## Pending / 仍待
- Turnaround sheets（正/侧/背）
- Idle / attack / hit frames
- Enemy variants（coral ID recolors）
- Final TA WebP compress into game package

## QA self-check (2026-09-23)
- unit_ally_01: 256×256 alpha=true 41966B trim=1018×714 → place 248×174 @(4,78) OK
- unit_ally_02: 256×256 alpha=true 52847B trim=816×718 → place 248×218 @(4,34) OK
- unit_ally_03: 256×256 alpha=true 55960B trim=1017×706 → place 248×172 @(4,80) OK
- unit_ally_04: 256×256 alpha=true 40549B trim=950×702 → place 248×183 @(4,69) OK
- unit_ally_05: 256×256 alpha=true 70052B trim=449×674 → place 165×248 @(29,4) OK
- unit_ally_06: 256×256 alpha=true 48657B trim=958×706 → place 248×183 @(4,69) OK
- unit_ally_07: 256×256 alpha=true 44258B trim=841×711 → place 248×210 @(4,42) OK
- unit_ally_08: 256×256 alpha=true 53289B trim=883×713 → place 248×200 @(4,52) OK
- Checkerboard: **not painted in**（true alpha）
- No 512 outputs in this wave
- Thumbs: 128×128 under `thumbs/`（optional silhouette check）

## Rebuild
```bash
cd /workspace/art-benchmarks && node scripts/build_import_v4.mjs
```

## Source
`mvp/export/style_v2_classes/painted_v4/class_0N_*.png`（named .png, actually 1280×720 JPEG RGB）

### BG removal notes
- Sources confirmed **JPEG RGB 1280×720** (named `.png`); corners flood-fill near-white → alpha with 1px dilate + feather.
- Soft cream/gold speculars **kept** (not connected to edge flood); healer has more near-white opaque pixels by design (robe highlights), not halo.
- Edge alpha on all 8 = 0 (bleed ≥4 satisfied). No checkerboard baked in.
- Atlas PNG ~458KB raw — **TA must WebP/compress toward ≤250KB** battle_units budget; individuals also OK for Phaser multi-load.
- Per-sprite `originX` varies (weapons/cape force asymmetric bbox); use manifest/atlas pivot, not hardcode 0.5.
