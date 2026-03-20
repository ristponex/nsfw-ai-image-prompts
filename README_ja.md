# 🎨 NSFW AI画像プロンプト集 — 120以上の実用的なアダルトAIアートプロンプト

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Prompts](https://img.shields.io/badge/プロンプト-120+-blue)]()
[![Last Updated](https://img.shields.io/badge/最終更新-2026年3月-green)]()
[![Platform](https://img.shields.io/badge/プラットフォーム-Atlas%20Cloud-purple)](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)
[![SOC Certified](https://img.shields.io/badge/SOC%20I%20%26%20II-認証済-brightgreen)]()
[![HIPAA](https://img.shields.io/badge/HIPAA-準拠-brightgreen)]()

> **厳選された120以上の実戦テスト済みNSFW AIイメージプロンプト集。モデル別の最適化、ネガティブプロンプト、LoRA推奨、APIコード例を完備。全プロンプトは[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)で実際にテスト済み。**

[English](./README.md) | [中文版](./README_zh-CN.md) | [한국어](./README_ko.md)

---

## 目次

- [このリポジトリの目的](#このリポジトリの目的)
- [1. モデル早見表](#1-モデル早見表)
- [2. プロンプトエンジニアリングの基本](#2-プロンプトエンジニアリングの基本)
- [3. フォトリアリスティックプロンプト（30件）](#3-フォトリアリスティックプロンプト30件)
- [4. アート・ファインアートプロンプト（20件）](#4-アートファインアートプロンプト20件)
- [5. アニメ・漫画プロンプト（25件）](#5-アニメ漫画プロンプト25件)
- [6. ファンタジー・SFプロンプト（20件）](#6-ファンタジーsfプロンプト20件)
- [7. ピンナップ・レトロプロンプト（15件）](#7-ピンナップレトロプロンプト15件)
- [8. カップル・インタラクションプロンプト（15件）](#8-カップルインタラクションプロンプト15件)
- [9. ネガティブプロンプトライブラリ](#9-ネガティブプロンプトライブラリ)
- [10. LoRAリファレンスガイド](#10-loraリファレンスガイド)
- [11. API統合ガイド](#11-api統合ガイド)
- [12. モデル別最適化テクニック](#12-モデル別最適化テクニック)
- [13. コスト比較とプラットフォーム分析](#13-コスト比較とプラットフォーム分析)
- [14. 始め方](#14-始め方)
- [15. Star History & 貢献](#15-star-history--貢献)

---

## このリポジトリの目的

ネット上のほとんどの「プロンプト集」は：
1. 漠然としている（「美しい女性、高画質」）
2. 有料コンテンツの壁の向こう側
3. 重要なパラメータが欠けている（ネガティブプロンプト、LoRA重み、CFGスケール）
4. 実際のモデルでテストされていない

このリポジトリは、正確なパラメータを含む**そのまま使えるプロンプト**を提供します。すべてのプロンプトは複数のモデルで5回以上生成してクオリティと一貫性を検証済みです。

---

## 1. モデル早見表

### NSFWコンテンツ対応モデル

| モデル | 1枚あたりのコスト | 解像度 | NSFW方法 | 最適な用途 |
|--------|-----------------|--------|----------|-----------|
| **Flux Dev** | $0.012 | 最大 2048×2048 | `safety_checker=false` | コスパ最高のフォトリアル |
| **Flux Dev LoRA** | $0.032 | 最大 2048×2048 | `safety_checker=false` + カスタムLoRA | アニメ、カスタムスタイル |
| **Seedream v5.0 Lite** | $0.032 | 最大 4704×4704 | ホワイトリスト必要 | 超高解像度、肌のディテール |
| **Nano Banana 2** | $0.072 | 最大 2048×2048 | ネイティブNSFW対応 | 最速生成 |
| **SDXL** | $0.008 | 1024×1024 | コミュニティモデル | 予算重視 |
| **SDXL Lightning** | $0.004 | 1024×1024 | 4ステップ高速推論 | ラピッドプロトタイピング |
| **Pony Diffusion V6 XL** | $0.012 | 1024×1024 | ネイティブNSFW | アニメ/二次元専門 |
| **Flux Kontext Pro** | $0.05 | 最大 2048×2048 | 制限あり | キャラクター一貫性 |

### モデル別キーパラメータ

| モデル | CFGスケール | ステップ数 | スケジューラ | 推奨アスペクト比 |
|--------|-----------|----------|------------|----------------|
| Flux Dev | 3.5–7.0 | 28–50 | Euler | 2:3（縦）, 3:2（横） |
| Flux Dev LoRA | 3.5–7.0 | 28–50 | Euler | 2:3, 9:16 |
| Seedream v5.0 | 4.0–7.0 | 30–50 | DPM++ 2M | 2:3, 3:4 |
| Nano Banana 2 | 5.0–8.0 | 20–35 | Euler A | 2:3, 1:1 |
| SDXL | 7.0–12.0 | 30–50 | DPM++ 2M Karras | 1:1（ネイティブ） |
| Pony V6 XL | 7.0–10.0 | 25–40 | Euler A | 2:3, 3:4 |

---

## 2. プロンプトエンジニアリングの基本

### 2.1 優れたNSFWプロンプトの構造

高品質なプロンプトは以下の構造に従います：

```
[被写体の説明] + [身体の詳細] + [ポーズ/アクション] + [場面/背景] +
[照明] + [カメラ/構図] + [スタイル/メディア] + [品質タグ]
```

**分解例：**

```
A stunning 25-year-old woman with long auburn hair,          ← 被写体
athletic build, toned abs, perky breasts, smooth tan skin,   ← 身体の詳細
reclining on silk sheets with one arm behind her head,       ← ポーズ
in a luxury hotel penthouse bedroom with city lights          ← 場面
visible through floor-to-ceiling windows,
warm golden hour light filtering through sheer curtains,     ← 照明
shot from a slightly elevated angle, shallow depth of field, ← カメラ
professional boudoir photography, 85mm lens,                 ← スタイル
masterpiece, best quality, ultra-detailed, 8K UHD            ← 品質タグ
```

### 2.2 効果的な品質タグ

**汎用品質ブースター**（全モデル共通）：
```
masterpiece, best quality, ultra-detailed, highres, 8K UHD, RAW photo,
photorealistic, professional photography, sharp focus, intricate details
```

**フォトリアリズム専用：**
```
DSLR photo, Nikon D850, Canon EOS R5, 85mm f/1.4,
subsurface scattering, natural skin texture, skin pores visible,
studio lighting, Rembrandt lighting, rim light
```

**アニメ/漫画専用：**
```
anime style, cel shading, vibrant colors, clean lineart,
detailed eyes, anime face, manga illustration,
score_9, score_8_up, score_7_up（Pony V6 XL専用）
```

### 2.3 身体描写のトークン順序

モデルは位置に基づいてトークンに異なる重みを付けます。最良の結果のために：

1. **年齢/人種** → "25-year-old Japanese woman"
2. **体型** → "petite, slender build"
3. **主な特徴** → "large expressive eyes, full lips"
4. **髪** → "long black hair with bangs"
5. **肌** → "flawless porcelain skin"
6. **身体の具体** → "slim waist, wide hips, C-cup breasts"
7. **衣服/状態** → "wearing a sheer white negligee, partially unbuttoned"

### 2.4 結果を変えるライティングキーワード

| キーワード | 効果 | 最適な用途 |
|-----------|------|-----------|
| `golden hour lighting` | 暖かく、柔らかく、美しく | 屋外ブードワール |
| `Rembrandt lighting` | 頬の三角光、ドラマチック | アーティスティックポートレート |
| `rim lighting` | 光る輪郭ハイライト | シルエット、ボディライン |
| `neon lighting` | カラフル、サイバーパンク | ファンタジー、SF |
| `natural window light` | 柔らかい、リアルな室内 | ベッドルームシーン |
| `candlelight` | 暖かい、親密、ソフトシャドウ | ロマンチックシーン |
| `studio strobe` | クリーン、プロフェッショナル | グラマー写真 |
| `backlighting` | シルエット、ヘアグロー | アーティスティックボディ |
| `chiaroscuro` | 明暗の高コントラスト | ファインアートヌード |
| `volumetric lighting` | ゴッドレイ、大気感 | ファンタジーシーン |

### 2.5 カメラ＆構図キーワード

| キーワード | 効果 |
|-----------|------|
| `shot from below, low angle` | 高さ、パワーの強調 |
| `bird's eye view` | 全身俯瞰ショット |
| `over the shoulder` | 親密なPOV |
| `dutch angle` | ダイナミックな緊張感 |
| `macro close-up` | ディテールショット |
| `full body shot` | 完全な人物像 |
| `medium shot, waist up` | クラシックポートレート |
| `rule of thirds` | バランスの取れた構図 |
| `shallow depth of field, bokeh` | 被写体の分離 |
| `wide angle lens, 24mm` | 環境コンテキスト |

---

## 3. フォトリアリスティックプロンプト（30件）

### 3.1 ブードワール・ベッドルーム

**PR-01: シルクシートラグジュアリー**
```
A gorgeous 26-year-old woman with flowing chestnut hair and green eyes,
athletic yet curvy figure, lying seductively on white silk sheets in a
minimalist luxury bedroom, one shoulder strap of her black lace slip
falling off her shoulder, soft morning light streaming through sheer
linen curtains, shallow depth of field, shot with Canon EOS R5 85mm
f/1.2, warm color palette, professional boudoir photography, subsurface
scattering on skin, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **モデル**: Flux Dev (`safety_checker=false`)
- **ネガティブ**: `deformed, bad anatomy, extra fingers, blurry, low quality, watermark`
- **CFG**: 5.0 | **ステップ**: 35 | **サイズ**: 832×1216

**PR-02: モーニングライト**
```
Beautiful 28-year-old blonde woman with blue eyes and freckles across
her nose, naturally curvy body, sitting on the edge of an unmade bed
wearing only an oversized white button-down shirt partially open
revealing cleavage and bare legs, holding a coffee mug, warm morning
sunlight creating long shadows, messy bedroom background with books
and plants, candid lifestyle photography, natural skin texture with
visible pores, Fujifilm X-T5 simulation, film grain, masterpiece,
best quality
```
- **モデル**: Flux Dev
- **ネガティブ**: `plastic skin, airbrushed, mannequin, extra limbs, bad hands`
- **CFG**: 4.5 | **ステップ**: 30 | **サイズ**: 832×1216

**PR-03: バスタブシーン**
```
Stunning 24-year-old mixed-race woman with curly dark hair piled up
in a messy bun, caramel skin, relaxing in a freestanding clawfoot
bathtub filled with milky water and rose petals, one leg draped over
the edge, steam rising, marble bathroom with brass fixtures, soft
diffused natural light from frosted window, water droplets on skin,
intimate candid photography, 50mm lens, slight film grain,
masterpiece, ultra-detailed, photorealistic, 8K
```
- **モデル**: Seedream v5.0 Lite（超高精細ディテール用）
- **ネガティブ**: `deformed, ugly, blurry, bad proportions, watermark, text`
- **CFG**: 5.5 | **ステップ**: 40 | **サイズ**: 1280×1920

**PR-04: ミラーリフレクション**
```
Elegant 30-year-old East Asian woman with straight black hair to her
waist, slender figure, standing before a full-length vintage mirror
in a dimly lit dressing room, wearing a black lace bodysuit, her
reflection visible in the mirror creating a dual composition, warm
tungsten lamp light, velvet curtains in the background, shot at f/2.0
with beautiful bokeh, fashion editorial photography style, detailed
skin texture, masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev
- **ネガティブ**: `deformed reflection, extra limbs, disfigured, low quality`
- **CFG**: 5.0 | **ステップ**: 35 | **サイズ**: 832×1216

**PR-05: プールサイドラウンジング**
```
Attractive 27-year-old Mediterranean woman with olive skin and dark
wavy hair, toned athletic body, sunbathing on a luxury pool lounger
wearing a tiny white string bikini, glistening with suntan oil,
infinity pool with ocean view in the background, harsh midday sunlight
creating defined shadows, water reflections dancing on her skin,
fashion magazine photography, Sony A7R V, 70-200mm lens, vibrant
summer colors, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **モデル**: Flux Dev
- **ネガティブ**: `bad anatomy, extra fingers, deformed, blurry, text, watermark`
- **CFG**: 5.0 | **ステップ**: 30 | **サイズ**: 1216×832

**PR-06: シャワーシーン**
```
Beautiful 25-year-old Scandinavian woman with platinum blonde wet hair
slicked back, tall athletic build with long legs, standing in a
modern walk-in rain shower, water streaming down her body, one hand
pressed against the glass partition, steam filling the space, cool
blue-white LED lighting from above contrasting with warm skin tones,
water droplets visible on glass, hyper-realistic photography,
detailed water physics, natural skin texture, masterpiece,
best quality, ultra-detailed
```
- **モデル**: Seedream v5.0 Lite
- **ネガティブ**: `deformed, plastic skin, blurry, bad hands, extra fingers`
- **CFG**: 5.5 | **ステップ**: 40 | **サイズ**: 1280×1920

**PR-07: モノクロアート**
```
Striking 32-year-old African American woman with short natural hair,
statuesque figure, posing nude with arms crossed beneath her breasts,
dramatic black and white photography, high contrast chiaroscuro
lighting with a single studio strobe from the left, deep shadows,
simple dark background, classic Helmut Newton inspired composition,
skin highlights emphasizing muscle definition, Hasselblad medium
format quality, fine grain, masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev
- **ネガティブ**: `color, saturated, low contrast, blurry, deformed, extra limbs`
- **CFG**: 5.5 | **ステップ**: 35 | **サイズ**: 832×1216

**PR-08: ウィンドウライトヌード**
```
Graceful 29-year-old woman with auburn hair and pale skin dotted with
freckles, dancer's body with lean muscles, standing in profile near a
large industrial window, completely nude, natural daylight casting
geometric shadow patterns across her body from window panes, loft
apartment with exposed brick walls, dust particles visible in light
beams, fine art nude photography, contemplative expression, eyes
closed, 85mm f/1.4 lens, masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev
- **ネガティブ**: `deformed, bad anatomy, extra fingers, oversaturated, cartoon`
- **CFG**: 4.5 | **ステップ**: 35 | **サイズ**: 832×1216

### 3.2 屋外・環境

**PR-09: ビーチサンセット**
```
Gorgeous 26-year-old Brazilian woman with long dark hair blowing in
the wind, sun-kissed golden skin, curvaceous figure, walking along a
deserted tropical beach at sunset wearing a tiny coral bikini bottom
only, topless with arms slightly raised, ocean waves lapping at her
ankles, dramatic orange and purple sunset sky, wet sand reflections,
backlit with golden rim lighting on hair and body, professional
travel photography, Sony A1, 135mm f/1.8, masterpiece, best quality,
ultra-detailed, 8K UHD
```
- **モデル**: Flux Dev
- **ネガティブ**: `deformed, bad anatomy, extra limbs, blurry, text, watermark`
- **CFG**: 5.0 | **ステップ**: 35 | **サイズ**: 1216×832

**PR-10: 森の妖精**
```
Ethereal 23-year-old woman with long flowing red hair adorned with
wildflowers, pale freckled skin, petite natural body, sitting nude on
a mossy rock beside a woodland stream, dappled sunlight filtering
through the canopy above, ferns and wildflowers surrounding her,
mist rising from the water, enchanted forest atmosphere, dreamy soft
focus, natural lifestyle photography with fantasy undertones, Earth
tones, green and gold color palette, masterpiece, best quality,
ultra-detailed
```
- **モデル**: Flux Dev
- **ネガティブ**: `deformed, bad anatomy, plastic skin, harsh lighting, urban`
- **CFG**: 4.5 | **ステップ**: 35 | **サイズ**: 832×1216

**PR-11: 屋上の夜**
```
Confident 28-year-old South Korean woman with a sleek black bob cut,
toned slender body, leaning against a rooftop railing wearing a
sheer black mesh top and leather mini skirt, city skyline illuminated
behind her, neon signs reflecting in her eyes, wind slightly lifting
her hair, cool blue and warm orange mixed lighting from city lights
below, urban night photography, slight motion blur in background,
Sony A7 IV 35mm f/1.4, cyberpunk aesthetic, masterpiece, best quality,
ultra-detailed
```
- **モデル**: Flux Dev
- **ネガティブ**: `deformed, bad anatomy, blurry face, extra fingers, low quality`
- **CFG**: 5.0 | **ステップ**: 30 | **サイズ**: 832×1216

**PR-12: 砂漠のオアシス**
```
Exotic 27-year-old Middle Eastern woman with long dark wavy hair,
olive skin, voluptuous figure, reclining on colorful Moroccan
cushions beside a small desert oasis pool, wearing flowing sheer
white fabric draped loosely around her body leaving little to
imagination, golden jewelry on wrists and ankles, warm desert sunset
light, palm trees and sand dunes in background, editorial fashion
photography, rich warm color palette, 85mm lens, masterpiece,
best quality, ultra-detailed, 8K
```
- **モデル**: Flux Dev
- **ネガティブ**: `deformed, bad anatomy, extra fingers, blurry, watermark`
- **CFG**: 5.0 | **ステップ**: 35 | **サイズ**: 1216×832

### 3.3 グラマー＆ファッション

**PR-13 ～ PR-15: クイックリファレンス**

| ID | 説明 | キータグ | 推奨モデル |
|----|------|---------|-----------|
| PR-13 | 濡れたTシャツ、ビーチクラブ | `wet, clinging, summer, laughing` | Flux Dev |
| PR-14 | ランジェリーエディトリアル、パリ | `Vogue, lingerie, velvet, chandelier` | Flux Dev |
| PR-15 | スポーツイラストレイテッド風 | `bikini, athletic, tan lines, tropical` | Flux Dev |

### 3.4 スタジオ・プロフェッショナル

**PR-16 ～ PR-20: クイックリファレンス**

| ID | 説明 | キータグ | 推奨モデル |
|----|------|---------|-----------|
| PR-16 | クラシックプレイボーイ風 | `fur rug, fireplace, 1980s, film grain` | Flux Dev |
| PR-17 | ボディペイント | `peacock feathers, UV paint, studio` | Seedream v5.0 |
| PR-18 | フィットネスモデル | `six-pack, competition, stage lighting` | Flux Dev |
| PR-19 | シフォンファブリック | `implied nude, dance, high-key, ethereal` | Flux Dev |
| PR-20 | ヴィンテージポラロイド | `1970s, Polaroid, nostalgic, overexposed` | Flux Dev |

### 3.5 アドバンストフォトリアリスティック

**PR-21 ～ PR-30: クイックリファレンス**

| ID | 説明 | キータグ | 推奨モデル |
|----|------|---------|-----------|
| PR-21 | ダブルエクスポージャー | `cityscape, silhouette, neon, composite` | Flux Dev |
| PR-22 | 水中ヌード | `underwater, red hair, caustic light, bubbles` | Seedream v5.0 |
| PR-23 | サウナ/スチームルーム | `Finnish, wooden, steam, towel, Nordic` | Flux Dev |
| PR-24 | 雨のシーン | `rain, wet shirt, neon, noir, puddles` | Flux Dev |
| PR-25 | ブードワールクローズアップ | `body chain, macro, satin, goosebumps` | Seedream v5.0 |
| PR-26 | ヨガスタジオ | `yoga mat, stretching, athletic, natural light` | Flux Dev |
| PR-27 | ヴィンテージカー | `1960s Mustang, denim shorts, Route 66` | Flux Dev |
| PR-28 | 日本の温泉 | `outdoor onsen, towel, mountains, steam` | Seedream v5.0 |
| PR-29 | アートギャラリー | `gallery, marble floor, classical paintings` | Flux Dev |
| PR-30 | バイクライダー | `Harley Davidson, leather jacket, wind` | Flux Dev |

---

## 4. アート・ファインアートプロンプト（20件）

### 4.1 油絵スタイル

**ART-01: ルネサンスヴィーナス**
```
A modern reinterpretation of Botticelli's Birth of Venus, beautiful
woman with flowing golden hair standing in a giant seashell,
Renaissance oil painting style, rich pigments, visible brushstrokes,
classical composition, rose petals floating in the wind, ocean waves
and zephyr winds, warm earthy color palette with ultramarine blue
sky, craquelure texture overlay, museum quality fine art,
masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev LoRA（ルネサンスアートLoRA）
- **ネガティブ**: `modern, photography, digital art, anime, deformed`
- **CFG**: 6.0 | **ステップ**: 40 | **サイズ**: 1024×1024

**ART-02: バロックドラマティック**
```
Sensual Baroque-style oil painting of a reclining nude woman on red
velvet drapery, Caravaggio-inspired dramatic chiaroscuro lighting,
deep shadows contrasting with luminous skin painted with visible
impasto technique, rich jewel tones — deep crimson, gold, midnight
blue, elaborate gilded frame visible at edges, classical figure
proportions, oil on canvas texture, museum quality reproduction,
masterpiece, best quality
```
- **モデル**: Flux Dev LoRA
- **ネガティブ**: `flat lighting, cartoon, anime, digital, modern, photography`
- **CFG**: 6.5 | **ステップ**: 40 | **サイズ**: 1216×832

**ART-03: 印象派バス**
```
Impressionist oil painting of a woman bathing in a sunlit room,
inspired by Pierre-Auguste Renoir's bather paintings, soft dappled
light, loose expressive brushstrokes, warm peach and rose skin tones,
blue and lavender shadows, white porcelain tub, floral wallpaper
background painted with visible texture, casual intimate moment,
late 19th century French Impressionism, canvas weave texture,
masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev LoRA
- **ネガティブ**: `photorealistic, sharp, digital, modern, anime, cartoon`
- **CFG**: 6.0 | **ステップ**: 40 | **サイズ**: 832×1216

**ART-04: アール・ヌーヴォー**
```
Art Nouveau illustration of a sensual woman with extremely long
flowing hair intertwined with morning glory vines and butterflies,
Alphonse Mucha inspired style, decorative circular halo frame behind
her, ornamental patterns, muted pastel colors with gold leaf accents,
elegant sinuous lines, partially nude with flowing fabric draping
strategically, mosaic-like background elements, lithograph print
texture, masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev LoRA
- **ネガティブ**: `photorealistic, modern, 3D render, anime, harsh colors`
- **CFG**: 6.0 | **ステップ**: 40 | **サイズ**: 832×1216

**ART-05: 水彩ヌード**
```
Delicate watercolor painting of a woman's back and shoulders, sitting
with her hair pinned up revealing her neck, wet-on-wet watercolor
technique with paint bleeding at the edges, soft undefined
boundaries, paper texture visible through transparent washes,
limited palette of indigo blue, burnt sienna, and raw umber,
white paper showing through as highlights on skin, minimalist
composition, Japanese-influenced aesthetic, traditional watercolor
on cold-pressed paper, masterpiece, best quality
```
- **モデル**: Flux Dev LoRA
- **ネガティブ**: `digital, photorealistic, opaque, oil painting, sharp lines`
- **CFG**: 5.0 | **ステップ**: 35 | **サイズ**: 832×1216

### 4.2 コンテンポラリー＆デジタルアート

**ART-06 ～ ART-10: クイックリファレンス**

| ID | スタイル | 説明 | キータグ |
|----|---------|------|---------|
| ART-06 | ヴェイパーウェーブ | ピンクとパープル、グリッチ | `CRT, glitch, neon, VHS, synthwave` |
| ART-07 | ポップアート | ベンデイドット、コミック風 | `Lichtenstein, primary colors, bold` |
| ART-08 | 木炭デッサン | ライフドローイング | `charcoal, gestural, paper texture` |
| ART-09 | シュルレアリスム | ダリ風、溶ける身体 | `melting, desert, clocks, surreal` |
| ART-10 | ミニマリストライン | 一筆描きヌード | `continuous line, Picasso, minimal` |

**ART-11 ～ ART-20: クイックリファレンス**

| ID | スタイル | 説明 | キータグ |
|----|---------|------|---------|
| ART-11 | 浮世絵 | 日本の木版画、遊女 | `shunga, woodblock, Utamaro style` |
| ART-12 | アール・デコ | 幾何学的女性、金と黒 | `1920s, Tamara de Lempicka, geometric` |
| ART-13 | 表現主義 | 歪んだ人物、鮮やかな色彩 | `Egon Schiele, angular, raw emotion` |
| ART-14 | 鉛筆スケッチ | 詳細な石墨人物習作 | `HB pencil, hatching, anatomy study` |
| ART-15 | ステンドグラス | 大聖堂の窓のような女性 | `Gothic, lead lines, jewel colors` |
| ART-16 | モザイク | ローマモザイクの裸体 | `tesserae, ancient Roman, bath scene` |
| ART-17 | スプレーペイント | レンガ壁のストリートアート | `Banksy style, stencil, urban` |
| ART-18 | 水墨画 | 墨絵風ヌード | `Chinese ink, rice paper, bamboo brush` |
| ART-19 | パステル画 | ドガ風の柔らかい人物 | `soft pastel, dancer, warm tones` |
| ART-20 | コラージュ | 切り紙ヌード構成 | `magazine cut-outs, layered, mixed media` |

---

## 5. アニメ・漫画プロンプト（25件）

### 5.1 モダンアニメスタイル

**AN-01: ビーチ回**
```
score_9, score_8_up, score_7_up, 1girl, solo, anime style,
beautiful detailed eyes, long pink hair with twintails, large
breasts, slender waist, wide hips, wearing a tiny white string
bikini, standing in shallow ocean water, splashing, bright summer
day, blue sky with fluffy clouds, tropical beach background,
sparkling water, happy expression, blush, dynamic pose with one
arm raised, water droplets on skin, cel shading, vibrant colors,
clean lineart, detailed coloring, masterpiece, best quality,
absurdres, highres
```
- **モデル**: Pony Diffusion V6 XL または Flux Dev LoRA（アニメLoRA）
- **ネガティブ**: `worst quality, low quality, normal quality, bad anatomy, bad hands, extra fingers, fewer fingers, extra limbs, bad proportions, watermark, text, signature, 3d, photorealistic`
- **CFG**: 7.0 | **ステップ**: 28 | **サイズ**: 832×1216

**AN-02: 温泉**
```
score_9, score_8_up, 1girl, solo, anime style, short blue hair,
red eyes, medium breasts, nude, sitting in outdoor hot spring,
water up to chest level, steam rising, towel on head, wooden fence
background, autumn maple leaves falling, rocks around the onsen,
evening sky with orange gradient, relaxed expression, slight blush,
detailed water reflections, beautiful lighting, anime coloring,
cel shading, masterpiece, best quality, absurdres
```
- **モデル**: Pony V6 XL
- **ネガティブ**: `worst quality, low quality, bad anatomy, extra fingers, 3d, photorealistic, western`
- **CFG**: 7.0 | **ステップ**: 28 | **サイズ**: 832×1216

**AN-03: 放課後の女子**
```
score_9, score_8_up, 1girl, solo, anime style, black hair with
bangs, brown eyes, glasses, medium breasts, wearing partially
unbuttoned white school shirt with visible black bra underneath,
navy pleated skirt hiked up, black thigh-high stockings, sitting
on teacher's desk in empty classroom, golden sunset light through
windows, chalkboard in background, shy expression, blushing,
legs crossed, indoor shoes, detailed fabric wrinkles, school
interior, cel shading, masterpiece, best quality, absurdres
```
- **モデル**: Flux Dev LoRA（アニメLoRA）
- **ネガティブ**: `worst quality, low quality, bad anatomy, extra fingers, deformed, ugly, blurry`
- **CFG**: 7.0 | **ステップ**: 30 | **サイズ**: 832×1216

**AN-04: メイド服**
```
score_9, score_8_up, score_7_up, 1girl, solo, anime style, long
silver hair, heterochromia red and blue eyes, large breasts,
wearing a revealing french maid outfit with very short skirt, white
apron, black stockings with garters, maid headband, holding a
feather duster, bending forward slightly, cleavage visible, playful
wink, one eye closed, cat ear accessories, in an ornate Victorian
mansion hallway, marble floor, chandeliers, detailed outfit,
frills and lace details, anime coloring, masterpiece, best quality,
absurdres, highres
```
- **モデル**: Pony V6 XL
- **ネガティブ**: `worst quality, low quality, bad anatomy, extra fingers, realistic, 3d`
- **CFG**: 7.0 | **ステップ**: 28 | **サイズ**: 832×1216

**AN-05: ファンタジー戦士**
```
score_9, score_8_up, 1girl, solo, anime style, long blonde hair
with braid, green eyes, athletic muscular body, large breasts,
wearing revealing fantasy armor — metal bikini top, armored thong,
thigh-high armored boots, gauntlets, wielding a glowing magic
sword, battle stance, dynamic action pose, cape flowing behind,
ancient ruins battlefield, magic particles and sparks flying,
dramatic sky with storm clouds, epic fantasy atmosphere, detailed
armor design with engravings, cel shading, masterpiece, best quality,
absurdres, highres
```
- **モデル**: Flux Dev LoRA（アニメLoRA）
- **ネガティブ**: `worst quality, low quality, bad anatomy, extra limbs, realistic, simple background`
- **CFG**: 7.0 | **ステップ**: 30 | **サイズ**: 832×1216

### 5.2 特定のアニメアートスタイル

**AN-06 ～ AN-10: クイックリファレンス**

| ID | スタイル | 説明 | キータグ |
|----|---------|------|---------|
| AN-06 | 90年代レトロ | EVA風、セルアニメ | `Gainax, CRT, VHS, plugsuit` |
| AN-07 | 漫画パネル | 白黒、集中線 | `screentone, ink, speed lines, panel` |
| AN-08 | ちびエッチ | SD、可愛くセクシー | `chibi, big head, kawaii, blush` |
| AN-09 | アダルト画風 | 詳細な成人向けイラスト | `ahegao, explicit, detailed shading` |
| AN-10 | 原神風 | ゲームCG、エレメント | `Genshin Impact, vision, cel shading` |

### 5.3 その他のアニメプロンプト

| ID | テーマ | 説明 | スタイルタグ |
|----|-------|------|------------|
| AN-11 | サキュバス | 悪魔少女、角、尾、翼 | `demon, fantasy, dark, bat wings` |
| AN-12 | ナース | セクシーアニメナース | `hospital, white outfit, stethoscope` |
| AN-13 | バニーガール | バニースーツ、網タイツ | `bunny ears, bowtie, cocktail, bar` |
| AN-14 | 魔女 | ヌード魔女、帽子、箒 | `halloween, magic, cauldron, moon` |
| AN-15 | 猫耳娘 | ネコミミ、尻尾、ランジェリー | `cat ears, paws, collar, bell` |
| AN-16 | 巫女 | 巫女装、半脱ぎ | `torii gate, shrine, sacred, kimono` |
| AN-17 | サイバーパンク | ネオン義体、露出度高い衣装 | `circuits, hologram, rain, neon` |
| AN-18 | エルフプリンセス | 長耳、森、露出度高いドレス | `fantasy, crown, magic, nature` |
| AN-19 | ジムトレーナー | スポーツブラ、レギンス、汗 | `gym, weights, mirror, athletic` |
| AN-20 | アイドル | ステージ衣装、キラキラ | `concert, microphone, spotlight` |
| AN-21 | ヴァンパイア | ゴシックドレス、血、牙 | `castle, moon, bats, pale skin` |
| AN-22 | マーメイド | 海、貝殻ブラ、魚の尾 | `underwater, coral, bubbles, scales` |
| AN-23 | アンドロイド | ロボ少女、露出回路 | `mechanical, chrome, blue glow` |
| AN-24 | くノ一 | 忍者少女、破れた衣装 | `shuriken, smoke, bamboo forest` |
| AN-25 | 花嫁 | ウェディングドレス、赤面 | `church, veil, flowers, white lace` |

---

## 6. ファンタジー・SFプロンプト（20件）

### 6.1 ファンタジー

**FAN-01: ダークエルフの魔女**
```
A dark elf sorceress with obsidian skin and silver-white hair flowing
to her waist, glowing violet eyes, pointed ears, athletic statuesque
body, wearing nothing but intricate silver body chains and a tattered
dark purple loincloth, casting a spell with swirling arcane energy
around her hands, standing in an ancient underground temple lit by
bioluminescent crystals, carved stone pillars with elvish runes,
dark fantasy art style, dramatic rim lighting in purple and blue,
detailed jewelry and body ornamentation, epic fantasy illustration,
masterpiece, best quality, ultra-detailed, 8K
```
- **モデル**: Flux Dev LoRA（ファンタジーアートLoRA）
- **ネガティブ**: `deformed, bad anatomy, bright cheerful, modern, photo, anime`
- **CFG**: 6.0 | **ステップ**: 40 | **サイズ**: 832×1216

**FAN-02: ドラゴンライダー**
```
A fierce warrior woman with scarlet hair in warrior braids, battle
scars across her toned muscular body, topless with leather pants and
knee-high boots, riding bareback on a massive black dragon in flight,
wind whipping her hair, dragon's wings spread wide against a sunset
sky of crimson and gold, looking back over her shoulder at the viewer
with fierce determination, clouds swirling below, epic scale fantasy
landscape with mountains, oil painting style with bold brushwork,
Frank Frazetta inspired, masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev LoRA
- **ネガティブ**: `deformed, bad anatomy, cute, kawaii, modern, simple, boring`
- **CFG**: 6.5 | **ステップ**: 40 | **サイズ**: 1216×832

**FAN-03 ～ FAN-20: クイックリファレンス**

| ID | テーマ | 説明 | キータグ |
|----|-------|------|---------|
| FAN-03 | 森の妖精 | 蝶の羽、キノコ、蛍 | `fairy, mushroom, fireflies, enchanted` |
| FAN-04 | 月の女神 | 湖上に浮かぶ銀髪の女神 | `moon, silver, divine, reflection` |
| FAN-05 | ヴァンパイア | ゴシック大聖堂、黒レース | `Gothic, moonlight, fangs, cathedral` |
| FAN-06 | サイバーパンク義体 | 半機械の身体、ネオン路地 | `cybernetic, neon, rain, Blade Runner` |
| FAN-07 | エイリアンクイーン | 四本腕、生物発光 | `alien, bioluminescent, HR Giger` |
| FAN-08 | 無重力 | 宇宙ステーション内 | `zero-g, ISS, floating, Earth view` |
| FAN-09 | アマゾネス | ジャングルの女戦士 | `tribal, spear, tiger, primal` |
| FAN-10 | 氷の女王 | 凍った城、氷の鎧 | `frost, crystal, winter, blue` |
| FAN-11 | フェニックス | 炎の女性、再生 | `flames, ash, wings, ember` |
| FAN-12 | メデューサ | 蛇の髪、石化した犠牲者 | `Greek myth, scales, golden eyes` |
| FAN-13 | ヴァルキリー | 北欧戦士、オーロラ | `winged helmet, spear, Asgard` |
| FAN-14 | スペースオペラ | 異星の姫、宇宙船 | `hologram, stars, chrome, regal` |
| FAN-15 | スチームパンク | ヴィクトリア朝機械 | `brass, steam, clockwork, goggles` |
| FAN-16 | 触手 | クトゥルフ的存在、深海 | `Lovecraftian, deep sea, bioluminescent` |
| FAN-17 | ジーニー | ランプ、煙形態 | `Arabian nights, gold, silk, magic` |
| FAN-18 | ドリアード | 樹木の精霊 | `forest spirit, roots, flowers, green` |
| FAN-19 | セイレーン | 岩の上で歌う、船乗り | `ocean, waves, moonlight, deadly beauty` |
| FAN-20 | アンドロイド | 完璧なクロームボディ | `factory, cables, blue eyes, synthetic` |

---

## 7. ピンナップ・レトロプロンプト（15件）

**PIN-01: クラシック1950年代ピンナップ**
```
Classic 1950s pin-up girl illustration, voluptuous woman with bright
red lipstick and victory rolls hairstyle, surprised expression with
hand on cheek in "oops" pose, her polka dot dress blown up by wind
revealing stockings and garter belt, white high heels, clean graphic
illustration style in the tradition of Gil Elvgren, solid color
background in mint green, slightly exaggerated proportions, warm
nostalgic color palette, vintage paper texture overlay, hand-painted
look, masterpiece, best quality
```
- **モデル**: Flux Dev LoRA（ピンナップLoRA）
- **ネガティブ**: `photorealistic, modern, anime, dark, gritty, monochrome`
- **CFG**: 6.0 | **ステップ**: 35 | **サイズ**: 832×1216

**PIN-02: ヴァーガスガール**
```
Alberto Vargas style pin-up illustration, elegant woman with long
legs in sheer nude stockings and high heels, wearing only a feather
boa draped strategically, reclining on a crescent moon prop,
delicate watercolor-like rendering with soft edges, peachy skin
tones, minimal background, Esquire magazine centerfold style from
the 1940s, graceful elongated proportions, subtle sensuality,
vintage glamour, soft pastel palette, masterpiece, best quality,
ultra-detailed
```
- **モデル**: Flux Dev LoRA
- **ネガティブ**: `photorealistic, harsh, dark, crude, modern, digital, anime`
- **CFG**: 5.5 | **ステップ**: 35 | **サイズ**: 832×1216

**PIN-03 ～ PIN-15: クイックリファレンス**

| ID | 時代/スタイル | 説明 | キータグ |
|----|-------------|------|---------|
| PIN-03 | ロカビリー | ホットロッド、ダイナー | `Chevy Bel Air, milkshake, neon` |
| PIN-04 | セーラージェリー | タトゥーフラッシュアート | `anchor, nautical, bold outlines` |
| PIN-05 | アール・デコ | 1920年代ショーガール | `Ziegfeld, gold, geometric, pearls` |
| PIN-06 | WWII | 爆撃機ノーズアート | `B-17, leather jacket, military` |
| PIN-07 | 60年代ゴーゴー | ゴーゴーブーツ、ミニスカート | `mod, geometric, white boots` |
| PIN-08 | 70年代ディスコ | グリッター、プラットフォーム | `mirror ball, gold lame, afro` |
| PIN-09 | 80年代エアロビクス | レオタード、レッグウォーマー | `neon, VHS, gym, synthwave` |
| PIN-10 | バーレスク | フェザーファン、コルセット | `cabaret, sequins, spotlight` |
| PIN-11 | ティキバー | ハワイアン、フラスカート | `bamboo, torch, tropical, lei` |
| PIN-12 | カウガール | 帽子、ブーツ、投げ縄 | `western, denim, sunset, country` |
| PIN-13 | フレンチメイド | クラシックメイドピンナップ | `feather duster, stockings, frills` |
| PIN-14 | ナース | ヴィンテージナース制服 | `red cross, cap, thermometer` |
| PIN-15 | カレンダーガール | 月ごとのテーマ | `calendar page, seasonal, posed` |

---

## 8. カップル・インタラクションプロンプト（15件）

**COU-01: ロマンティックな抱擁**
```
A romantic couple in an intimate embrace, handsome man with dark hair
holding a beautiful woman with flowing auburn hair, both partially
nude, his muscular chest pressed against her back, his arms wrapped
around her waist, her head tilted back against his shoulder with
eyes closed in ecstasy, standing in a dimly lit bedroom with candles
casting warm flickering light, silk curtains billowing, romance novel
cover photography style, warm golden tones, shallow depth of field,
passionate and sensual mood, masterpiece, best quality, ultra-detailed
```
- **モデル**: Flux Dev (`safety_checker=false`)
- **ネガティブ**: `deformed, bad anatomy, extra limbs, extra fingers, merged bodies, blurry`
- **CFG**: 5.0 | **ステップ**: 40 | **サイズ**: 832×1216

**COU-02 ～ COU-15: クイックリファレンス**

| ID | テーマ | 説明 | キータグ |
|----|-------|------|---------|
| COU-02 | ビーチカップル | 夕日の砂浜で | `beach, sunset, minimal swimwear` |
| COU-03 | シャワー | 一緒にシャワー | `water, steam, glass, marble` |
| COU-04 | ルネサンスの恋人 | ティツィアーノ風油絵 | `Renaissance, oil painting, velvet` |
| COU-05 | アニメカップル | ベッドで親密に | `anime, blush, fairy lights` |
| COU-06 | ダンス | タンゴ、ドラマチックなディップ | `dance hall, spotlight, passion` |
| COU-07 | マッサージ | センシュアルなマッサージ | `oil, candles, spa, hands on back` |
| COU-08 | 翌朝 | 一緒に目覚める | `sunlight, messy hair, lazy morning` |
| COU-09 | ホットタブ | ジャグジーのカップル | `bubbles, steam, wine, night sky` |
| COU-10 | ペイントプレイ | 互いにボディペイント | `colorful, messy, playful, studio` |
| COU-11 | ファンタジーエルフ | エルフのカップル、魔法の森 | `pointed ears, magic, moonlight` |
| COU-12 | ノワール | 探偵とファム・ファタール | `1940s, shadows, venetian blinds` |
| COU-13 | ヴァンパイア | 吸血シーン | `gothic, castle, moonlight, blood` |
| COU-14 | 水中 | 水中に浮かぶカップル | `bubbles, light rays, swimming` |
| COU-15 | アニメ入浴 | 共同入浴、恥ずかしそう | `onsen, blush, steam, intimate` |

---

## 9. ネガティブプロンプトライブラリ

### 9.1 ユニバーサルネガティブ（全場面共通）

```
deformed, bad anatomy, disfigured, poorly drawn face, mutation,
mutated, extra limbs, extra legs, extra arms, malformed limbs,
missing arms, missing legs, extra fingers, too many fingers,
fewer fingers, fused fingers, long neck, bad proportions,
duplicate, morbid, mutilated, out of frame, ugly, blurry,
bad quality, low quality, worst quality, watermark, text,
signature, logo, banner, username, cropped
```

### 9.2 フォトリアリズム専用

```
（上記ユニバーサル） + illustration, cartoon, anime, drawing,
painting, sketch, 3d render, CGI, plastic skin, mannequin,
wax figure, airbrushed, overprocessed, HDR artifacts
```

### 9.3 アニメ/漫画専用

```
（上記ユニバーサル） + photorealistic, realistic, 3d, photograph,
western art, Disney style, Pixar, bad anime art, off-model
```

### 9.4 身体の問題別対策

| 問題 | ネガティブプロンプト修正 |
|------|----------------------|
| 余分な指 | `extra fingers, too many fingers, fused fingers, six fingers` |
| 手の不具合 | `bad hands, poorly drawn hands, missing fingers, deformed hands` |
| 顔の歪み | `deformed face, asymmetric face, crossed eyes, bad teeth` |
| 身体のホラー | `extra limbs, conjoined, fused bodies, merged bodies, extra torso` |
| 肌の異常 | `plastic skin, waxy skin, grey skin, green skin, zombie` |
| プロポーション | `child proportions, dwarf, giant head, tiny head, elongated` |

### 9.5 モデル別ネガティブプロンプト

**Flux Dev専用：**
```
worst quality, jpeg artifacts, blurry, noisy, chromatic aberration,
lens distortion, overexposed, underexposed
```

**SDXL専用：**
```
(worst quality:1.4), (low quality:1.4), (normal quality:1.4),
lowres, bad anatomy, bad hands, text, error, missing fingers,
extra digit, fewer digits, cropped, jpeg artifacts, signature,
watermark, username, blurry, artist name
```

**Pony V6 XL専用：**
```
score_1, score_2, score_3, score_4, worst quality, low quality,
text, censored, deformed, bad hand, blurry, (watermark),
multiple phones, extra limbs
```

---

## 10. LoRAリファレンスガイド

### 10.1 LoRAとは？

LoRA（Low-Rank Adaptation）は、ベースモデル全体を再トレーニングすることなく出力スタイルを変更できる小型の微調整モデル重みです。Atlas Cloudでは、**Flux Dev LoRA**（$0.032/枚）でLoRAを使用できます。

### 10.2 API経由でのLoRA使用方法

```python
# Specify LoRA in your API call
payload = {
    "model_name": "flux-dev-lora",
    "prompt": "your prompt here",
    "lora_url": "https://huggingface.co/user/lora-name/resolve/main/lora.safetensors",
    "lora_scale": 0.8,  # 0.0 to 1.0 — LoRA effect strength
    "safety_checker": False
}
```

### 10.3 推奨LoRAウェイト

| LoRAタイプ | 推奨スケール | 低すぎる場合 | 高すぎる場合 |
|-----------|-----------|------------|------------|
| アニメスタイル | 0.7–0.85 | スタイル変化がほぼ見えない | 過飽和、アーティファクト |
| リアリスティック強化 | 0.5–0.7 | 効果が微弱 | 不気味の谷 |
| 特定キャラクター | 0.75–0.9 | キャラクターが認識できない | オーバーフィット |
| 画風（油絵、水彩） | 0.6–0.8 | デジタルっぽく見える | 被写体ディテールが失われる |
| 服装/衣装 | 0.7–0.85 | 衣装が不正確 | 衣装と身体が融合 |

### 10.4 人気のNSFW対応LoRA

| カテゴリ | LoRA名 | ソース | 最適スケール |
|---------|--------|--------|-------------|
| アニメ汎用 | Anime Art Style | CivitAI / HuggingFace | 0.75 |
| 90年代アニメ | Retro Anime | HuggingFace | 0.7 |
| リアル肌質 | Detail Tweaker | CivitAI | 0.5 |
| アダルト | 各アーティスト | CivitAI | 0.8 |
| ピンナップ | Vintage Pin-Up | CivitAI | 0.75 |
| ファンタジー | Epic Fantasy | HuggingFace | 0.7 |
| 漫画白黒 | Manga Style | HuggingFace | 0.75 |
| ルネサンス | Classical Painting | CivitAI | 0.65 |

---

## 11. API統合ガイド

### 11.1 Python — 完全な例

```python
import requests
import base64
import os

API_KEY = os.environ.get("ATLAS_API_KEY")
BASE_URL = "https://api.atlascloud.ai/v1"

def generate_nsfw_image(
    prompt: str,
    negative_prompt: str = "",
    model: str = "flux-dev",
    width: int = 832,
    height: int = 1216,
    steps: int = 35,
    cfg_scale: float = 5.0,
    safety_checker: bool = False
) -> bytes:
    """Generate an NSFW image using the Atlas Cloud API."""

    payload = {
        "model_name": model,
        "prompt": prompt,
        "negative_prompt": negative_prompt,
        "width": width,
        "height": height,
        "num_inference_steps": steps,
        "guidance_scale": cfg_scale,
        "safety_checker": safety_checker,
    }

    headers = {
        "Authorization": f"Bearer {API_KEY}",
        "Content-Type": "application/json"
    }

    response = requests.post(
        f"{BASE_URL}/images/generations",
        json=payload,
        headers=headers
    )
    response.raise_for_status()

    result = response.json()
    image_data = base64.b64decode(result["images"][0]["b64_json"])
    return image_data


# Usage example
image = generate_nsfw_image(
    prompt="""A gorgeous 26-year-old woman with flowing chestnut hair,
    lying seductively on white silk sheets, soft morning light,
    Canon EOS R5 85mm f/1.2, boudoir photography,
    masterpiece, best quality, ultra-detailed, 8K UHD""",
    negative_prompt="deformed, bad anatomy, extra fingers, blurry",
)

with open("output.png", "wb") as f:
    f.write(image)
```

### 11.2 cURL

```bash
curl -X POST "https://api.atlascloud.ai/v1/images/generations" \
  -H "Authorization: Bearer $ATLAS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model_name": "flux-dev",
    "prompt": "A beautiful woman in elegant lingerie, professional boudoir photography, masterpiece, best quality",
    "negative_prompt": "deformed, bad anatomy, extra fingers, blurry",
    "width": 832,
    "height": 1216,
    "safety_checker": false
  }' | jq -r '.images[0].b64_json' | base64 -d > output.png
```

### 11.3 JavaScript / Node.js

```javascript
const axios = require('axios');
const fs = require('fs');

const API_KEY = process.env.ATLAS_API_KEY;

async function generateNSFWImage({ prompt, negativePrompt = '', model = 'flux-dev' }) {
  const response = await axios.post(
    'https://api.atlascloud.ai/v1/images/generations',
    {
      model_name: model,
      prompt,
      negative_prompt: negativePrompt,
      width: 832,
      height: 1216,
      safety_checker: false,
    },
    { headers: { 'Authorization': `Bearer ${API_KEY}` } }
  );

  return Buffer.from(response.data.images[0].b64_json, 'base64');
}

(async () => {
  const image = await generateNSFWImage({
    prompt: 'A stunning woman in black lace lingerie, Parisian apartment, masterpiece',
    negativePrompt: 'deformed, bad anatomy, blurry',
  });
  fs.writeFileSync('output.png', image);
  console.log('Image saved');
})();
```

---

## 12. モデル別最適化テクニック

### 12.1 Flux Dev — ベストバリュー ($0.012/枚)

**強み：** 優れたフォトリアリズム、正確な解剖学、複雑シーンの処理、超低価格。

**最適化のコツ：**
- `safety_checker=false` の設定が**必須**（NSFWコンテンツには）
- CFGは3.5–5.5で自然な肌に
- ステップ28–35がベスト、40以上は改善がわずか
- ポートレートには2:3比率（832×1216）
- カメラ参照ワードに非常に反応する（"Canon EOS R5", "85mm f/1.4"）

### 12.2 Flux Dev LoRA — カスタムスタイル ($0.032/枚)

**強み：** 適切なLoRAで任意の画風、アニメスペシャリスト。

**最適化のコツ：**
- LoRAスケール0.7から始め、0.05ずつ増加
- アニメLoRAにはアニメ専用タグを含める
- すべてのHuggingFace LoRAが互換ではない—SDXLのLoRAはFluxでは使えない

### 12.3 Seedream v5.0 Lite — 超高解像度 ($0.032/枚)

**強み：** 最高解像度出力（最大4704×4704）、驚異的な肌ディテール。

**最適化のコツ：**
- ホワイトリスト必要—Atlas Cloudサポートに連絡
- クローズアップとディテール重視のショットに最適
- ステップ40–50で解像度を最大限に活用

### 12.4 モデル選択ディシジョンツリー

```
何が必要？
│
├─ フォトリアルなアダルトコンテンツ？
│  ├─ 予算重視 → Flux Dev ($0.012) ★ ベストバリュー
│  ├─ 最高ディテール → Seedream v5.0 ($0.032)
│  └─ 最速スピード → Nano Banana 2 ($0.072)
│
├─ アニメ/漫画スタイル？
│  ├─ 特定LoRAスタイル → Flux Dev LoRA ($0.032)
│  └─ 一般アニメ → Pony V6 XL ($0.012)
│
├─ アーティスティック/ペインタリー？
│  ├─ 油絵/クラシカル → Flux Dev LoRA ($0.032)
│  └─ クイックコンセプト → Flux Dev ($0.012)
│
└─ バッチ生成（100枚以上）？
   ├─ 品質重視 → Flux Dev ($0.012) — 100枚 = $1.20
   └─ 最低コスト → SDXL ($0.008) — 100枚 = $0.80
```

---

## 13. コスト比較とプラットフォーム分析

### 13.1 Atlas Cloud vs fal.ai 価格比較

| モデル | Atlas Cloud | fal.ai | より安い | 差額 |
|--------|-----------|--------|---------|------|
| **Flux Dev** | $0.012/枚 | ~$0.025/枚 | Atlas ✅ | 52%安い |
| **Flux Dev LoRA** | $0.032/枚 | ~$0.032/枚 | 同額 | — |
| **Nano Banana 2** | $0.072/枚 | $0.0398/枚 | fal.ai ✅ | fal 45%安い |
| **Flux Kontext Pro** | $0.05/枚 | $0.04/枚 | fal.ai ✅ | fal 20%安い |
| **Seedream v5.0** | $0.032/枚 | N/A | Atlas限定 | — |
| **SDXL** | $0.008/枚 | ~$0.01/枚 | Atlas ✅ | 20%安い |

### 13.2 なぜAtlas Cloudを選ぶのか？

| 要素 | Atlas Cloud | fal.ai |
|------|-----------|--------|
| **統一API** | ✅ 全モデル1つのAPI | ❌ モデルごとに異なるエンドポイント |
| **NSFWポリシー** | ✅ safety_checker=falseで明確に対応 | ⚠️ モデルにより異なる |
| **モデル種類** | ✅ 50+モデル（画像、動画、テキスト、音声） | ✅ 良い選択肢 |
| **動画モデル** | ✅ Wan 2.2 Spicy、Seedance等 | NSFWビデオ限定的 |
| **テキスト/LLM** | ✅ DeepSeek、Llama等 | ❌ LLMサポートなし |
| **初回チャージボーナス** | ✅ **25%ボーナス（最大$100）** | ❌ ボーナスなし |
| **コンプライアンス** | ✅ SOC I & II認証、HIPAA準拠 | 不明 |
| **会社所在地** | 🇺🇸 米国企業 | 🇺🇸 米国企業 |

### 13.3 コスト計算 — $10でどれだけ生成できる？

| モデル | 1枚あたり | $10で生成可能 | 25%ボーナス込み（$12.50） |
|--------|---------|-------------|------------------------|
| SDXL Lightning | $0.004 | 2,500枚 | 3,125枚 |
| SDXL | $0.008 | 1,250枚 | 1,562枚 |
| Flux Dev | $0.012 | 833枚 | 1,041枚 |
| Pony V6 XL | $0.012 | 833枚 | 1,041枚 |
| Flux Dev LoRA | $0.032 | 312枚 | 390枚 |
| Seedream v5.0 | $0.032 | 312枚 | 390枚 |
| Flux Kontext Pro | $0.05 | 200枚 | 250枚 |
| Nano Banana 2 | $0.072 | 138枚 | 173枚 |

### 13.4 信頼性とコンプライアンス

[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)は米国企業でエンタープライズグレードのセキュリティを備えています：

- **SOC I & SOC II認証** — 独立監査済みのセキュリティコントロール
- **HIPAA準拠** — 医療グレードのデータ保護基準
- **米国インフラ** — データは米国内に保管
- **データでのトレーニングなし** — プロンプトと画像は完全にプライベート
- **従量課金** — 月額なし、サブスクリプション不要

---

## 14. 始め方

### ステップ1：アカウント作成

[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)で登録 — わずか30秒。

### ステップ2：25%ボーナスを獲得

初回チャージで**25%ボーナス**を自動取得（最大$100ボーナス）。$10チャージで$12.50のクレジット。

### ステップ3：APIキーの取得

ダッシュボード → API Keys → 新しいキーを作成。

### ステップ4：生成開始

このリポジトリの任意のプロンプトと上記のAPI例を使用してください。Flux Dev（$0.012/枚）から始めるのがおすすめ — 品質、コスト、NSFW機能のベストバランス。

```bash
export ATLAS_API_KEY="your-key-here"

curl -X POST "https://api.atlascloud.ai/v1/images/generations" \
  -H "Authorization: Bearer $ATLAS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model_name": "flux-dev",
    "prompt": "A beautiful woman in elegant lingerie, professional boudoir photography, masterpiece, best quality",
    "width": 832,
    "height": 1216,
    "safety_checker": false
  }' | jq -r '.images[0].b64_json' | base64 -d > my_first_image.png
```

---

## 15. Star History & 貢献

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=thoughtincode/nsfw-ai-image-prompts&type=Date)](https://star-history.com/#thoughtincode/nsfw-ai-image-prompts&Date)

### 貢献

貢献を歓迎します！テスト済みで一貫した良い結果を生むプロンプトをお持ちの場合：

1. このリポジトリをフォーク
2. 既存のフォーマットに従ってプロンプトを追加（モデル、ネガティブ、パラメータを含む）
3. プルリクエストを送信（可能であればサンプル出力を添付）

### 関連リソース

- [NSFW AIモデル比較 2026](https://github.com/thoughtincode/nsfw-ai-model-comparison) — 17のAIモデルの包括的ベンチマーク
- [Atlas Cloud APIドキュメント](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)

---

## ライセンス

このプロジェクトはMITライセンスの下でライセンスされています — 詳細は[LICENSE](LICENSE)ファイルをご覧ください。

---

**免責事項：** このリポジトリは成人ユーザー（18歳以上）による合法的な使用のみを目的としています。AI生成コンテンツに関する現地の法律を常に遵守してください。この集のプロンプトは芸術的・創造的目的のためのものです。ユーザーはこれらのプロンプトの使用方法と生成されるコンテンツに対して責任を負います。

---

<p align="center">
  <a href="https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts">
    <img src="https://img.shields.io/badge/Powered%20by-Atlas%20Cloud-purple?style=for-the-badge" alt="Powered by Atlas Cloud">
  </a>
</p>
<p align="center">
  <sub>全プロンプトは<a href="https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts">Atlas Cloud</a>でテスト済み — SOC I & II認証、HIPAA準拠、米国企業</sub>
</p>
