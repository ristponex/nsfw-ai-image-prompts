# 🎨 NSFW AI 图片提示词大全 — 120+ 可直接使用的成人AI绘画提示词

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Prompts](https://img.shields.io/badge/提示词-120+-blue)]()
[![Last Updated](https://img.shields.io/badge/最近更新-2026年3月-green)]()
[![Platform](https://img.shields.io/badge/平台-Atlas%20Cloud-purple)](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)
[![SOC Certified](https://img.shields.io/badge/SOC%20I%20%26%20II-已认证-brightgreen)]()
[![HIPAA](https://img.shields.io/badge/HIPAA-合规-brightgreen)]()

> **精心整理的 120+ 条经过实测的 NSFW AI 图片提示词，包含模型专属优化、反向提示词、LoRA 推荐和 API 代码示例。每条提示词都在 [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts) 上经过真实测试。**

[English](./README.md) | [日本語](./README_ja.md) | [한국어](./README_ko.md)

---

## 目录

- [为什么做这个仓库](#为什么做这个仓库)
- [1. 模型速查表](#1-模型速查表)
- [2. 提示词工程基础](#2-提示词工程基础)
- [3. 写实风格提示词（30条）](#3-写实风格提示词30条)
- [4. 艺术/美术风格提示词（20条）](#4-艺术美术风格提示词20条)
- [5. 动漫/漫画风格提示词（25条）](#5-动漫漫画风格提示词25条)
- [6. 奇幻/科幻风格提示词（20条）](#6-奇幻科幻风格提示词20条)
- [7. 复古海报风格提示词（15条）](#7-复古海报风格提示词15条)
- [8. 情侣/互动场景提示词（15条）](#8-情侣互动场景提示词15条)
- [9. 反向提示词库](#9-反向提示词库)
- [10. LoRA 使用指南](#10-lora-使用指南)
- [11. API 接入指南](#11-api-接入指南)
- [12. 模型专属优化技巧](#12-模型专属优化技巧)
- [13. 价格对比与平台分析](#13-价格对比与平台分析)
- [14. 开始使用](#14-开始使用)
- [15. Star History 与贡献](#15-star-history-与贡献)

---

## 为什么做这个仓库

网上大部分"提示词合集"要么：
1. 太笼统（"美女，高画质"）
2. 在付费墙后面
3. 缺少关键参数（反向提示词、LoRA 权重、CFG 值）
4. 没在真实模型上测试过

本仓库提供**可直接使用的提示词**，包含精确参数，在真实模型上反复测试过。每条提示词在多个模型上至少生成5次以上验证效果。

---

## 1. 模型速查表

### 支持 NSFW 内容的模型

| 模型 | 单张价格 | 分辨率 | NSFW 方式 | 最适合 |
|------|---------|--------|-----------|--------|
| **Flux Dev** | $0.012 | 最高 2048×2048 | `safety_checker=false` | 性价比最高的写实风 |
| **Flux Dev LoRA** | $0.032 | 最高 2048×2048 | `safety_checker=false` + 自定义 LoRA | 动漫、自定义风格 |
| **Seedream v5.0 Lite** | $0.032 | 最高 4704×4704 | 需白名单账号 | 超高分辨率、皮肤细节 |
| **Nano Banana 2** | $0.072 | 最高 2048×2048 | 原生支持 NSFW | 速度最快 |
| **SDXL** | $0.008 | 1024×1024 | 社区模型 | 预算有限时 |
| **SDXL Lightning** | $0.004 | 1024×1024 | 4步快速推理 | 快速原型 |
| **Pony Diffusion V6 XL** | $0.012 | 1024×1024 | 原生支持 NSFW | 动漫/二次元专家 |
| **Flux Kontext Pro** | $0.05 | 最高 2048×2048 | 有限制 | 角色一致性 |

### 各模型关键参数

| 模型 | CFG值 | 步数 | 调度器 | 推荐比例 |
|------|-------|------|--------|---------|
| Flux Dev | 3.5–7.0 | 28–50 | Euler | 2:3（竖图）, 3:2（横图） |
| Flux Dev LoRA | 3.5–7.0 | 28–50 | Euler | 2:3, 9:16 |
| Seedream v5.0 | 4.0–7.0 | 30–50 | DPM++ 2M | 2:3, 3:4 |
| Nano Banana 2 | 5.0–8.0 | 20–35 | Euler A | 2:3, 1:1 |
| SDXL | 7.0–12.0 | 30–50 | DPM++ 2M Karras | 1:1（原生） |
| Pony V6 XL | 7.0–10.0 | 25–40 | Euler A | 2:3, 3:4 |

---

## 2. 提示词工程基础

### 2.1 高质量 NSFW 提示词结构

一条好的提示词遵循以下结构：

```
[主体描述] + [身体细节] + [姿势/动作] + [场景/背景] +
[光线] + [镜头/构图] + [风格/媒介] + [画质标签]
```

**分解示例：**

```
A stunning 25-year-old woman with long auburn hair,          ← 主体
athletic build, toned abs, perky breasts, smooth tan skin,   ← 身体细节
reclining on silk sheets with one arm behind her head,       ← 姿势
in a luxury hotel penthouse bedroom with city lights          ← 场景
visible through floor-to-ceiling windows,
warm golden hour light filtering through sheer curtains,     ← 光线
shot from a slightly elevated angle, shallow depth of field, ← 镜头
professional boudoir photography, 85mm lens,                 ← 风格
masterpiece, best quality, ultra-detailed, 8K UHD            ← 画质标签
```

### 2.2 真正有效的画质标签

**通用画质提升**（所有模型通用）：
```
masterpiece, best quality, ultra-detailed, highres, 8K UHD, RAW photo,
photorealistic, professional photography, sharp focus, intricate details
```

**写实专用：**
```
DSLR photo, Nikon D850, Canon EOS R5, 85mm f/1.4,
subsurface scattering, natural skin texture, skin pores visible,
studio lighting, Rembrandt lighting, rim light
```

**动漫/漫画专用：**
```
anime style, cel shading, vibrant colors, clean lineart,
detailed eyes, anime face, manga illustration,
score_9, score_8_up, score_7_up（Pony V6 XL 专用）
```

### 2.3 身体描述的最佳词序

模型根据词的位置分配不同权重。为了最佳效果，按以下顺序：

1. **年龄/种族** → "25-year-old Japanese woman"
2. **体型** → "petite, slender build"
3. **关键特征** → "large expressive eyes, full lips"
4. **头发** → "long black hair with bangs"
5. **皮肤** → "flawless porcelain skin"
6. **身体细节** → "slim waist, wide hips, C-cup breasts"
7. **衣着/状态** → "wearing a sheer white negligee, partially unbuttoned"

### 2.4 改变效果的光线关键词

| 关键词 | 效果 | 最适合 |
|-------|------|--------|
| `golden hour lighting` | 温暖、柔和、讨好 | 户外私房照 |
| `Rembrandt lighting` | 脸颊三角光、戏剧感 | 艺术肖像 |
| `rim lighting` | 发光边缘高光 | 剪影、身体轮廓 |
| `neon lighting` | 彩色、赛博朋克感 | 幻想、科幻 |
| `natural window light` | 柔和、真实室内感 | 卧室场景 |
| `candlelight` | 温暖、亲密、柔影 | 浪漫场景 |
| `studio strobe` | 干净、专业 | 时尚摄影 |
| `backlighting` | 剪影、头发光晕 | 艺术人体 |
| `chiaroscuro` | 明暗高对比 | 美术裸体 |
| `volumetric lighting` | 丁达尔光、大气感 | 幻想场景 |

### 2.5 镜头与构图关键词

| 关键词 | 效果 |
|-------|------|
| `shot from below, low angle` | 强调高度、力量感 |
| `bird's eye view` | 全身俯拍 |
| `over the shoulder` | 亲密视角 |
| `dutch angle` | 动态张力 |
| `macro close-up` | 细节特写 |
| `full body shot` | 完整人物 |
| `medium shot, waist up` | 经典半身照 |
| `rule of thirds` | 均衡构图 |
| `shallow depth of field, bokeh` | 突出主体 |
| `wide angle lens, 24mm` | 环境交代 |

---

## 3. 写实风格提示词（30条）

### 3.1 私房/卧室

**PR-01: 丝绸奢华**
```
A gorgeous 26-year-old woman with flowing chestnut hair and green eyes,
athletic yet curvy figure, lying seductively on white silk sheets in a
minimalist luxury bedroom, one shoulder strap of her black lace slip
falling off her shoulder, soft morning light streaming through sheer
linen curtains, shallow depth of field, shot with Canon EOS R5 85mm
f/1.2, warm color palette, professional boudoir photography, subsurface
scattering on skin, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **模型**: Flux Dev (`safety_checker=false`)
- **反向提示词**: `deformed, bad anatomy, extra fingers, blurry, low quality, watermark`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 832×1216

**PR-02: 晨光**
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
- **模型**: Flux Dev
- **反向提示词**: `plastic skin, airbrushed, mannequin, extra limbs, bad hands`
- **CFG**: 4.5 | **步数**: 30 | **尺寸**: 832×1216

**PR-03: 浴缸场景**
```
Stunning 24-year-old mixed-race woman with curly dark hair piled up
in a messy bun, caramel skin, relaxing in a freestanding clawfoot
bathtub filled with milky water and rose petals, one leg draped over
the edge, steam rising, marble bathroom with brass fixtures, soft
diffused natural light from frosted window, water droplets on skin,
intimate candid photography, 50mm lens, slight film grain,
masterpiece, ultra-detailed, photorealistic, 8K
```
- **模型**: Seedream v5.0 Lite（超高清细节）
- **反向提示词**: `deformed, ugly, blurry, bad proportions, watermark, text`
- **CFG**: 5.5 | **步数**: 40 | **尺寸**: 1280×1920

**PR-04: 镜中反射**
```
Elegant 30-year-old East Asian woman with straight black hair to her
waist, slender figure, standing before a full-length vintage mirror
in a dimly lit dressing room, wearing a black lace bodysuit, her
reflection visible in the mirror creating a dual composition, warm
tungsten lamp light, velvet curtains in the background, shot at f/2.0
with beautiful bokeh, fashion editorial photography style, detailed
skin texture, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `deformed reflection, extra limbs, disfigured, low quality`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 832×1216

**PR-05: 泳池休憩**
```
Attractive 27-year-old Mediterranean woman with olive skin and dark
wavy hair, toned athletic body, sunbathing on a luxury pool lounger
wearing a tiny white string bikini, glistening with suntan oil,
infinity pool with ocean view in the background, harsh midday sunlight
creating defined shadows, water reflections dancing on her skin,
fashion magazine photography, Sony A7R V, 70-200mm lens, vibrant
summer colors, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **模型**: Flux Dev
- **反向提示词**: `bad anatomy, extra fingers, deformed, blurry, text, watermark`
- **CFG**: 5.0 | **步数**: 30 | **尺寸**: 1216×832

**PR-06: 淋浴场景**
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
- **模型**: Seedream v5.0 Lite
- **反向提示词**: `deformed, plastic skin, blurry, bad hands, extra fingers`
- **CFG**: 5.5 | **步数**: 40 | **尺寸**: 1280×1920

**PR-07: 黑白艺术**
```
Striking 32-year-old African American woman with short natural hair,
statuesque figure, posing nude with arms crossed beneath her breasts,
dramatic black and white photography, high contrast chiaroscuro
lighting with a single studio strobe from the left, deep shadows,
simple dark background, classic Helmut Newton inspired composition,
skin highlights emphasizing muscle definition, Hasselblad medium
format quality, fine grain, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `color, saturated, low contrast, blurry, deformed, extra limbs`
- **CFG**: 5.5 | **步数**: 35 | **尺寸**: 832×1216

**PR-08: 窗光裸体**
```
Graceful 29-year-old woman with auburn hair and pale skin dotted with
freckles, dancer's body with lean muscles, standing in profile near a
large industrial window, completely nude, natural daylight casting
geometric shadow patterns across her body from window panes, loft
apartment with exposed brick walls, dust particles visible in light
beams, fine art nude photography, contemplative expression, eyes
closed, 85mm f/1.4 lens, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, extra fingers, oversaturated, cartoon`
- **CFG**: 4.5 | **步数**: 35 | **尺寸**: 832×1216

### 3.2 户外/环境

**PR-09: 海滩日落**
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
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, extra limbs, blurry, text, watermark`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 1216×832

**PR-10: 森林仙女**
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
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, plastic skin, harsh lighting, urban`
- **CFG**: 4.5 | **步数**: 35 | **尺寸**: 832×1216

**PR-11: 天台夜景**
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
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, blurry face, extra fingers, low quality`
- **CFG**: 5.0 | **步数**: 30 | **尺寸**: 832×1216

**PR-12: 沙漠绿洲**
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
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, extra fingers, blurry, watermark`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 1216×832

### 3.3 时尚/魅力

**PR-13: 湿身T恤**
```
Playful 24-year-old woman with honey blonde hair in a ponytail,
athletic cheerleader build, wearing a soaking wet white t-shirt
clinging to her body revealing everything underneath, denim cutoff
shorts, standing under an outdoor shower at a beach club, water
spraying around her, laughing with eyes closed, bright summer
daylight, lifestyle photography, energetic and fun mood, vibrant
colors, Canon EOS R5 70-200mm f/2.8, masterpiece, best quality,
ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, extra fingers, blurry, dull colors`
- **CFG**: 5.0 | **步数**: 30 | **尺寸**: 832×1216

**PR-14: 内衣时尚大片**
```
Sophisticated 31-year-old French woman with short brunette pixie cut,
elegant bone structure, slender model proportions, posing in a
high-end lingerie set — black lace balconette bra and matching thong
with garter belt and sheer stockings, sitting on a velvet chaise
longue in a Parisian apartment with ornate moldings and a crystal
chandelier, soft diffused studio lighting, Vogue editorial style,
muted luxury color palette, Leica SL2 50mm f/1.4, masterpiece,
best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `cheap lingerie, bad anatomy, deformed, blurry, low quality`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 832×1216

**PR-15: 体育画报风格**
```
Stunning 25-year-old woman with sun-bleached dirty blonde hair,
deeply tanned athletic body with visible tan lines, wearing a
micro bikini in metallic gold, posing with hands on hips on white
sand with turquoise water behind her, midday tropical sunlight,
confident power pose, slight wind, Sports Illustrated Swimsuit
Issue photography style, bright vibrant colors, high contrast,
Canon EOS R3 with 85mm f/1.2, masterpiece, best quality,
ultra-detailed, 8K UHD
```
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, extra fingers, blurry, pale skin`
- **CFG**: 5.5 | **步数**: 30 | **尺寸**: 832×1216

### 3.4 棚拍/专业摄影

**PR-16: 经典花花公子风格**
```
Elegant 27-year-old woman with voluminous dark hair, hourglass
figure, lying on her stomach on a white fur rug in front of a
fireplace, looking back over her shoulder with a playful smile,
completely nude, warm firelight casting soft orange glow, classic
Playboy magazine centerfold photography style from the 1980s, soft
focus, warm film tones, slight film grain, 6x7 medium format look,
masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `modern, digital look, deformed, bad anatomy, harsh lighting`
- **CFG**: 4.5 | **步数**: 35 | **尺寸**: 1216×832

**PR-17: 人体彩绘**
```
Athletic 26-year-old woman with short platinum hair, lean muscular
body, covered in intricate blue and gold body paint resembling
peacock feathers across her torso and arms, standing with arms
outstretched, dramatic studio lighting with dark background, body
paint art photography, UV reactive paint elements glowing under
mixed lighting, confident artistic expression, professional studio
photography, masterpiece, best quality, ultra-detailed, 8K
```
- **模型**: Seedream v5.0 Lite
- **反向提示词**: `bad anatomy, deformed, blurry, smudged paint, extra fingers`
- **CFG**: 5.5 | **步数**: 40 | **尺寸**: 832×1216

**PR-18: 健身模特**
```
Powerful 29-year-old fitness model with defined six-pack abs,
muscular thighs and glutes, shoulder-length brown hair in a
ponytail, wearing minimal competition bikini in emerald green,
flexing in a front pose on a competition stage, professional stage
lighting with dramatic shadows accentuating muscle definition,
spray tan glistening, fitness photography, isolated dark background,
motivated intense expression, DSLR quality, masterpiece, best quality,
ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `soft body, no muscle definition, deformed, blurry, bad anatomy`
- **CFG**: 5.5 | **步数**: 30 | **尺寸**: 832×1216

**PR-19: 含蓄裸体与纱巾**
```
Serene 30-year-old woman with long silver-grey hair, slender
ballerina body, standing in a pure white cyclorama studio, wrapped
in flowing sheer white chiffon fabric that swirls around her body
caught mid-motion, strategically concealing and revealing, barefoot
en pointe, artistic dance photography, high-key lighting, ethereal
and dreamlike atmosphere, slow shutter fabric motion, fine art
portrait, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `heavy clothing, dark background, deformed, blurry, bad anatomy`
- **CFG**: 4.5 | **步数**: 35 | **尺寸**: 832×1216

**PR-20: 复古宝丽来**
```
Natural 22-year-old woman with messy brunette hair and minimal
makeup, girl-next-door look, small perky breasts, sitting cross-
legged on a 1970s floral bedspread in a wood-paneled bedroom,
topless, vintage Polaroid photograph aesthetic, washed out warm
colors, soft blown-out highlights, rounded corners, authentic film
texture, amateur candid feel, nostalgic mood, slightly overexposed,
masterpiece, best quality
```
- **模型**: Flux Dev
- **反向提示词**: `modern, digital, sharp, deformed, bad anatomy, professional`
- **CFG**: 4.0 | **步数**: 30 | **尺寸**: 1024×1024

### 3.5 进阶写实

**PR-21: 双重曝光**
```
Creative double exposure portrait of a nude 28-year-old woman merged
with a cityscape at night, her silhouette filled with glowing
skyscraper windows and street lights, profile view, long flowing
hair dissolving into starry sky, surreal composite photography,
dark moody background, neon accents in cyan and magenta, artistic
conceptual photography, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `simple, basic, deformed face, blurry, bad merge, low quality`
- **CFG**: 5.5 | **步数**: 40 | **尺寸**: 832×1216

**PR-22: 水下裸体**
```
Ethereal underwater scene of a 25-year-old woman with long red hair
floating weightlessly, nude, submerged in clear turquoise water,
sunlight rays penetrating from the surface creating caustic light
patterns on her skin, hair fanning out like a halo, eyes closed in
peaceful expression, small air bubbles rising, underwater photography
with professional diving housing, deep blue gradient background,
serene and dreamlike, masterpiece, best quality, ultra-detailed
```
- **模型**: Seedream v5.0 Lite
- **反向提示词**: `drowning, distressed, deformed, blurry, murky water, bad anatomy`
- **CFG**: 5.0 | **步数**: 40 | **尺寸**: 832×1216

**PR-23: 桑拿/蒸汽房**
```
Relaxed 33-year-old Finnish woman with strawberry blonde hair in a
messy bun, natural curvy body with pale skin, sitting on wooden
bench in a traditional Finnish sauna, wrapped loosely in a white
towel that has slipped to reveal her back and side, steam filling
the air, warm amber wooden interior, soft overhead light diffused
through steam, water ladle beside her, authentic Nordic sauna
atmosphere, documentary photography style, natural and unposed,
masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, plastic, artificial, extra fingers`
- **CFG**: 4.5 | **步数**: 35 | **尺寸**: 832×1216

**PR-24: 雨中场景**
```
Sensual 27-year-old woman with long black hair plastered to her face
and body by rain, wearing a white dress shirt completely soaked
through and transparent, standing alone on an empty city street at
night, rain pouring down, neon signs reflected in puddles on wet
asphalt, streetlight creating a spotlight effect, cinematic
photography with anamorphic lens flare, teal and orange color
grading, dramatic noir atmosphere, water droplets frozen mid-air,
masterpiece, best quality, ultra-detailed, 8K
```
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, dry, no rain, blurry, cartoon, extra limbs`
- **CFG**: 5.5 | **步数**: 35 | **尺寸**: 832×1216

**PR-25: 私房特写**
```
Extreme close-up of a 26-year-old woman's torso and neck, lying on
black satin sheets, wearing a delicate gold body chain that drapes
across her collarbones and between her breasts, soft warm side
lighting accentuating the curves of her body, visible goosebumps and
fine body hair for realism, one hand resting on her stomach,
macro-style boudoir photography, shallow depth of field with only
the chain in sharp focus, intimate and sensual, 100mm macro lens,
masterpiece, best quality, ultra-detailed
```
- **模型**: Seedream v5.0 Lite
- **反向提示词**: `plastic skin, airbrushed, deformed, blurry, bad anatomy`
- **CFG**: 5.0 | **步数**: 40 | **尺寸**: 1216×832

**PR-26 至 PR-30: 写实风格快速参考**

| 编号 | 简述 | 关键标签 | 推荐模型 |
|------|------|---------|---------|
| PR-26 | 瑜伽教室、柔韧姿势、运动内衣 | `yoga mat, stretching, athletic, natural light` | Flux Dev |
| PR-27 | 复古汽车引擎盖、美式海报感 | `1960s Mustang, denim shorts, Route 66` | Flux Dev |
| PR-28 | 日式露天温泉、朦胧蒸汽 | `outdoor onsen, towel, mountains, steam` | Seedream v5.0 |
| PR-29 | 美术馆观众、裸体在画前 | `gallery, marble floor, classical paintings` | Flux Dev |
| PR-30 | 摩托车骑手、皮衣与蕾丝 | `Harley Davidson, leather jacket, wind, highway` | Flux Dev |

---

## 4. 艺术/美术风格提示词（20条）

### 4.1 油画风格

**ART-01: 文艺复兴维纳斯**
```
A modern reinterpretation of Botticelli's Birth of Venus, beautiful
woman with flowing golden hair standing in a giant seashell,
Renaissance oil painting style, rich pigments, visible brushstrokes,
classical composition, rose petals floating in the wind, ocean waves
and zephyr winds, warm earthy color palette with ultramarine blue
sky, craquelure texture overlay, museum quality fine art,
masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev LoRA（文艺复兴艺术 LoRA）
- **反向提示词**: `modern, photography, digital art, anime, deformed`
- **CFG**: 6.0 | **步数**: 40 | **尺寸**: 1024×1024

**ART-02: 巴洛克戏剧**
```
Sensual Baroque-style oil painting of a reclining nude woman on red
velvet drapery, Caravaggio-inspired dramatic chiaroscuro lighting,
deep shadows contrasting with luminous skin painted with visible
impasto technique, rich jewel tones — deep crimson, gold, midnight
blue, elaborate gilded frame visible at edges, classical figure
proportions, Renaissance Italian beauty ideal, oil on canvas
texture, museum quality reproduction, masterpiece, best quality
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `flat lighting, cartoon, anime, digital, modern, photography`
- **CFG**: 6.5 | **步数**: 40 | **尺寸**: 1216×832

**ART-03: 印象派沐浴**
```
Impressionist oil painting of a woman bathing in a sunlit room,
inspired by Pierre-Auguste Renoir's bather paintings, soft dappled
light, loose expressive brushstrokes, warm peach and rose skin tones,
blue and lavender shadows, white porcelain tub, floral wallpaper
background painted with visible texture, casual intimate moment,
late 19th century French Impressionism, canvas weave texture,
masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `photorealistic, sharp, digital, modern, anime, cartoon`
- **CFG**: 6.0 | **步数**: 40 | **尺寸**: 832×1216

**ART-04: 新艺术运动**
```
Art Nouveau illustration of a sensual woman with extremely long
flowing hair intertwined with morning glory vines and butterflies,
Alphonse Mucha inspired style, decorative circular halo frame behind
her, ornamental patterns, muted pastel colors with gold leaf accents,
elegant sinuous lines, partially nude with flowing fabric draping
strategically, mosaic-like background elements, lithograph print
texture, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `photorealistic, modern, 3D render, anime, harsh colors`
- **CFG**: 6.0 | **步数**: 40 | **尺寸**: 832×1216

**ART-05: 水彩裸体**
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
- **模型**: Flux Dev LoRA
- **反向提示词**: `digital, photorealistic, opaque, oil painting, sharp lines`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 832×1216

### 4.2 当代与数字艺术

**ART-06: 蒸汽波美学**
```
Vaporwave aesthetic digital art of a woman in a surreal pink and
purple gradient environment, nude with glitch effects across her
body, retro CRT scan lines, floating Greek marble busts and columns,
neon palm trees, VHS tracking artifacts, holographic rainbow
highlights on skin, Windows 95 aesthetic elements, Japanese text
overlay elements, pastel color palette with neon accents,
synthwave grid floor, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `photorealistic, natural, traditional art, boring, brown`
- **CFG**: 5.5 | **步数**: 35 | **尺寸**: 1024×1024

**ART-07: 波普艺术海报**
```
Bold pop art illustration of a sexy woman in the style of Roy
Lichtenstein, Ben-Day dots pattern across the image, thick black
outlines, primary colors — red yellow blue, comic book panel style,
woman in a provocative pose wearing a polka dot bikini, speech
bubble saying "OH!", halftone printing texture, flat graphic style,
1960s pop art movement, high contrast, bold and graphic,
masterpiece, best quality
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `photorealistic, 3D, gradient, soft, subtle, muted colors`
- **CFG**: 6.0 | **步数**: 35 | **尺寸**: 1024×1024

**ART-08: 炭笔素描**
```
Expressive charcoal life drawing of a nude woman in a contrapposto
standing pose, gestural confident strokes, strong value contrast
from deep blacks to paper white, anatomically accurate figure study,
visible construction lines and gesture marks, smudged charcoal
creating soft shadows, white chalk highlights on key points —
shoulder, breast, hip, textured cream drawing paper background,
fine art academy study, classical figurative art, masterpiece,
best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `color, painting, digital, photography, anime, cartoon`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 832×1216

**ART-09: 超现实主义梦境**
```
Surrealist painting in the style of Salvador Dali, nude woman melting
into a desert landscape, her body transforming into liquid mercury
flowing across cracked earth, clock elements embedded in her flowing
hair, elephants on impossibly thin legs in the background,
dreamlike desert sky with two suns, hyper-realistic technique applied
to impossible subjects, rich warm earth tones contrasting with cool
metallic skin, oil painting texture, masterpiece, best quality,
ultra-detailed
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `realistic scene, photography, cartoon, flat, simple, boring`
- **CFG**: 6.5 | **步数**: 40 | **尺寸**: 1216×832

**ART-10: 极简线条**
```
Single continuous line drawing of a woman's nude body, minimalist
style, one unbroken black line on white background, elegant curves
suggesting breasts, waist, and hips with maximum economy of line,
abstract figure study, negative space as important as the line
itself, inspired by Picasso's single line drawings and Matisse's
cut-outs, clean modern aesthetic, gallery-worthy composition,
masterpiece, best quality
```
- **模型**: Flux Dev
- **反向提示词**: `detailed, photorealistic, color, shading, complex, busy`
- **CFG**: 4.0 | **步数**: 30 | **尺寸**: 1024×1024

**ART-11 至 ART-20: 艺术风格快速参考**

| 编号 | 风格 | 简述 | 关键标签 |
|------|------|------|---------|
| ART-11 | 浮世绘 | 日本木版画、花魁 | `shunga, woodblock, Utamaro style` |
| ART-12 | 装饰艺术 | 几何女性、金与黑 | `1920s, Tamara de Lempicka, geometric` |
| ART-13 | 表现主义 | 扭曲人物、鲜艳色彩 | `Egon Schiele, angular, raw emotion` |
| ART-14 | 铅笔素描 | 详细石墨人物习作 | `HB pencil, hatching, anatomy study` |
| ART-15 | 彩色玻璃 | 教堂窗户式女性 | `Gothic, lead lines, jewel colors` |
| ART-16 | 马赛克 | 罗马马赛克式裸体 | `tesserae, ancient Roman, bath scene` |
| ART-17 | 喷漆 | 砖墙上的街头艺术女性 | `Banksy style, stencil, urban` |
| ART-18 | 水墨画 | 水墨风格裸体 | `Chinese ink, rice paper, bamboo brush` |
| ART-19 | 粉彩画 | 柔和人物习作、德加风 | `soft pastel, dancer, warm tones` |
| ART-20 | 拼贴艺术 | 剪纸裸体构图 | `magazine cut-outs, layered, mixed media` |

---

## 5. 动漫/漫画风格提示词（25条）

### 5.1 现代动漫风格

**AN-01: 海滩集**
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
- **模型**: Pony Diffusion V6 XL 或 Flux Dev LoRA（动漫 LoRA）
- **反向提示词**: `worst quality, low quality, normal quality, bad anatomy, bad hands, extra fingers, fewer fingers, extra limbs, bad proportions, watermark, text, signature, 3d, photorealistic`
- **CFG**: 7.0 | **步数**: 28 | **尺寸**: 832×1216

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
- **模型**: Pony V6 XL
- **反向提示词**: `worst quality, low quality, bad anatomy, extra fingers, 3d, photorealistic, western`
- **CFG**: 7.0 | **步数**: 28 | **尺寸**: 832×1216

**AN-03: 放学后的女生**
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
- **模型**: Flux Dev LoRA（动漫 LoRA）
- **反向提示词**: `worst quality, low quality, bad anatomy, extra fingers, deformed, ugly, blurry`
- **CFG**: 7.0 | **步数**: 30 | **尺寸**: 832×1216

**AN-04: 女仆装**
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
- **模型**: Pony V6 XL
- **反向提示词**: `worst quality, low quality, bad anatomy, extra fingers, realistic, 3d`
- **CFG**: 7.0 | **步数**: 28 | **尺寸**: 832×1216

**AN-05: 幻想战士**
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
- **模型**: Flux Dev LoRA（动漫 LoRA）
- **反向提示词**: `worst quality, low quality, bad anatomy, extra limbs, realistic, simple background`
- **CFG**: 7.0 | **步数**: 30 | **尺寸**: 832×1216

### 5.2 特定动漫风格

**AN-06: 90年代复古动漫**
```
1girl, solo, retro 90s anime style, big expressive eyes with
detailed light reflections, voluminous dark purple hair, pointed
chin, slim body with large breasts, wearing a tight red plugsuit-
like bodysuit, unzipped to navel, standing in a mechanical hangar
with giant mecha in background, CRT TV color palette, cel animation
look, slight VHS grain, warm color filter, 1990s Gainax style,
Neon Genesis Evangelion aesthetic, hand-painted cel look, visible
cel paint texture, masterpiece, best quality
```
- **模型**: Flux Dev LoRA（90年代动漫 LoRA）
- **反向提示词**: `modern anime, flat colors, digital, 3d, photorealistic, chibi`
- **CFG**: 6.0 | **步数**: 35 | **尺寸**: 832×1216

**AN-07: 漫画分格**
```
Black and white manga panel, 1girl, solo, detailed manga art style,
long hair with dramatic shading, nude, covering breasts with one
arm while other reaches forward, dynamic perspective with speed
lines radiating outward, screentone shading on skin, high contrast
black ink, dramatic shadows, speech bubble with "...!", panel
borders visible, manga page layout, Tokyo Ghoul level detail,
professional manga illustration, masterpiece, best quality
```
- **模型**: Flux Dev LoRA（漫画风格 LoRA）
- **反向提示词**: `color, painting, photograph, 3d, low detail, chibi, cute`
- **CFG**: 6.0 | **步数**: 35 | **尺寸**: 832×1216

**AN-08: Q版色气**
```
score_9, score_8_up, 1girl, solo, chibi proportions, super
deformed, big head, small body, long orange hair, huge sparkly
eyes, blush marks, tiny body with exaggerated curves, wearing an
oversized boyfriend shirt that hangs off one shoulder, no pants,
bare legs, standing on tiptoes, embarrassed expression, steam
coming from head, sweat drop, heart symbols floating, simple
pastel gradient background, kawaii aesthetic, cute but sexy,
chibi anime style, masterpiece, best quality
```
- **模型**: Pony V6 XL
- **反向提示词**: `realistic proportions, 3d, photorealistic, dark, horror`
- **CFG**: 7.0 | **步数**: 25 | **尺寸**: 1024×1024

**AN-09: 成人向画风**
```
score_9, score_8_up, 1girl, solo, detailed anime hentai art,
purple hair in a messy ponytail, ahegao expression, tongue out,
rolling eyes, heavy blush across face, large breasts, nipples
visible, sweat drops on skin, wearing torn school uniform, ripped
stockings, lying on bed, messy sheets, close-up from above,
dramatic top-down lighting, heart-shaped pupils, saliva string,
detailed skin shading, explicit hentai illustration, vibrant
colors, heavy coloring, masterpiece, best quality, absurdres
```
- **模型**: Pony V6 XL
- **反向提示词**: `worst quality, low quality, bad anatomy, censored, mosaic, bar censor, 3d, photorealistic`
- **CFG**: 7.5 | **步数**: 28 | **尺寸**: 832×1216

**AN-10: 原神风格**
```
score_9, score_8_up, 1girl, solo, Genshin Impact art style,
anime game CG, light blue long hair with gradient to white at tips,
golden eyes, elf ears, medium breasts, wearing revealing cryo
element inspired outfit — white and ice blue fabric with crystal
decorations, detached sleeves, thigh-high boots, floating ice
crystals around her, vision glowing on hip, fantasy landscape
with frozen waterfall, cel shading with soft gradients, detailed
outfit design, gacha game quality, masterpiece, best quality,
absurdres, highres
```
- **模型**: Flux Dev LoRA（原神风格 LoRA）
- **反向提示词**: `worst quality, low quality, bad anatomy, realistic, western art, simple`
- **CFG**: 7.0 | **步数**: 30 | **尺寸**: 832×1216

### 5.3 更多动漫提示词（快速参考）

| 编号 | 主题 | 简述 | 风格标签 |
|------|------|------|---------|
| AN-11 | 魅魔 | 恶魔女孩、角、尾巴、翅膀、裸体 | `demon, fantasy, dark, bat wings` |
| AN-12 | 护士 | 性感动漫护士、短裙 | `hospital, white outfit, stethoscope` |
| AN-13 | 兔女郎 | 兔女郎装、渔网袜 | `bunny ears, bowtie, cocktail, bar` |
| AN-14 | 魔女 | 裸体魔女、帽子、扫帚、药水 | `halloween, magic, cauldron, moon` |
| AN-15 | 猫娘 | 猫耳、尾巴、内衣 | `cat ears, paws, collar, bell` |
| AN-16 | 巫女 | 巫女服、半脱 | `torii gate, shrine, sacred, kimono` |
| AN-17 | 赛博朋克女孩 | 霓虹义体、暴露服装 | `circuits, hologram, rain, neon` |
| AN-18 | 精灵公主 | 尖耳、森林、暴露连衣裙 | `fantasy, crown, magic, nature` |
| AN-19 | 健身教练 | 运动内衣、紧身裤、汗水 | `gym, weights, mirror, athletic` |
| AN-20 | 偶像歌手 | 舞台装、发光、活力 | `concert, microphone, spotlight, fans` |
| AN-21 | 吸血鬼 | 哥特裙、血、獠牙 | `castle, moon, bats, pale skin` |
| AN-22 | 人鱼 | 海洋、贝壳胸罩、鱼尾 | `underwater, coral, bubbles, scales` |
| AN-23 | 机器人 | 机器人女孩、外露电路 | `mechanical, chrome, blue glow` |
| AN-24 | 女忍者 | 忍者女孩、破损服装、动作 | `shuriken, smoke, bamboo forest` |
| AN-25 | 新娘 | 婚纱、脸红 | `church, veil, flowers, white lace` |

---

## 6. 奇幻/科幻风格提示词（20条）

### 6.1 奇幻

**FAN-01: 暗精灵女巫**
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
- **模型**: Flux Dev LoRA（奇幻艺术 LoRA）
- **反向提示词**: `deformed, bad anatomy, bright cheerful, modern, photo, anime`
- **CFG**: 6.0 | **步数**: 40 | **尺寸**: 832×1216

**FAN-02: 龙骑士**
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
- **模型**: Flux Dev LoRA（奇幻艺术 LoRA）
- **反向提示词**: `deformed, bad anatomy, cute, kawaii, modern, simple, boring`
- **CFG**: 6.5 | **步数**: 40 | **尺寸**: 1216×832

**FAN-03: 森林精灵**
```
A tiny fairy woman with iridescent dragonfly wings, proportional
petite body with elfin features, nude with body adorned by living
flowers and vines growing from her skin, sitting on a giant mushroom
in an enchanted forest clearing, surrounded by fireflies and floating
pollen, morning dew drops on her wings catching rainbow light,
magical ethereal atmosphere, bioluminescent plants, fairy tale
illustration style with photorealistic lighting, dreamy bokeh,
pastel greens and golds, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, dark, scary, human-sized, realistic`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 832×1216

**FAN-04: 月亮女神**
```
An ethereal moon goddess floating above a still lake at midnight,
pale luminous skin that seems to emit soft white light, extremely
long silver hair reaching down to the water surface, nude, crescent
moon crown, celestial body with star-like freckles forming
constellations, arms outstretched in a blessing pose, reflection
perfectly mirrored in the dark water below, full moon directly
behind her creating a massive halo, wolves howling silhouettes on
distant hills, mystical fantasy art, divine feminine, moonlight
color palette of silver blue and white, masterpiece, best quality,
ultra-detailed
```
- **模型**: Seedream v5.0 Lite
- **反向提示词**: `daylight, modern, urban, deformed, bad anatomy, dark skin`
- **CFG**: 5.5 | **步数**: 40 | **尺寸**: 832×1216

**FAN-05: 吸血鬼女伯爵**
```
A pale vampire woman with blood-red eyes and jet-black hair with a
dramatic widow's peak, crimson lips, elongated canine fangs visible
in a slight smile, voluptuous body in a tattered Victorian black
lace gown that reveals more than it conceals, standing in a
decaying Gothic cathedral with crumbling stained glass windows,
moonlight streaming through broken ceiling casting geometric light
patterns, bats swirling overhead, cobwebs, dark romantic Gothic
horror atmosphere, dramatic Rembrandt lighting, oil painting style,
rich dark color palette, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `bright, cheerful, modern, daylight, deformed, anime, cartoon`
- **CFG**: 6.0 | **步数**: 40 | **尺寸**: 832×1216

### 6.2 科幻

**FAN-06: 赛博朋克义体**
```
A cyberpunk woman with half her body replaced by chrome cybernetic
enhancements, one glowing red cybernetic eye, the other natural
green, shaved head on one side with long neon-blue hair on the other,
nude torso showing the junction between flesh and machine, circuit
board patterns visible under translucent synthetic skin, standing in
a rain-soaked neon-lit alleyway in Night City, holographic
advertisements floating above, puddles reflecting pink and blue neon,
steam rising from grates, Blade Runner meets Ghost in the Shell
aesthetic, cinematic photography, masterpiece, best quality,
ultra-detailed, 8K
```
- **模型**: Flux Dev
- **反向提示词**: `medieval, fantasy, natural, deformed, bad anatomy, low tech`
- **CFG**: 5.5 | **步数**: 35 | **尺寸**: 832×1216

**FAN-07: 外星女王**
```
An alien humanoid queen with luminous blue-green bioluminescent skin,
four arms, elegant elongated proportions, no hair but an elaborate
bio-organic crown that grows from her skull, small breasts with alien
markings, wearing minimal iridescent fabric draped between her four
arms, seated on a living organic throne that pulses with light,
alien palace interior with impossible architecture, floating orbs
of light, tentacle-like pillars, HR Giger meets Roger Dean aesthetic,
otherworldly beauty, science fiction concept art, masterpiece,
best quality, ultra-detailed
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `human, normal, boring, fantasy, medieval, deformed`
- **CFG**: 6.0 | **步数**: 40 | **尺寸**: 832×1216

**FAN-08: 零重力**
```
An astronaut woman floating in zero gravity inside a space station
module, her suit unzipped to the waist revealing her upper body,
droplets of water floating around her in perfect spheres catching
the light, Earth visible through the circular window behind her
bathing everything in soft blue light, her hair floating freely in
all directions, equipment and tools drifting nearby, photorealistic
sci-fi scene, detailed ISS interior, NASA equipment visible, lens
flare from sunlight, masterpiece, best quality, ultra-detailed
```
- **模型**: Seedream v5.0 Lite
- **反向提示词**: `gravity, standing, ground, deformed, bad anatomy, cartoon`
- **CFG**: 5.5 | **步数**: 40 | **尺寸**: 1216×832

**FAN-09 至 FAN-20: 奇幻/科幻快速参考**

| 编号 | 主题 | 简述 | 关键标签 |
|------|------|------|---------|
| FAN-09 | 亚马逊女战士 | 丛林宝座上的女战士 | `tribal, spear, tiger, primal` |
| FAN-10 | 冰之女王 | 冰冻城堡、冰甲 | `frost, crystal, winter, blue` |
| FAN-11 | 凤凰 | 火焰女人、重生 | `flames, ash, wings, ember` |
| FAN-12 | 美杜莎 | 蛇发、石化受害者 | `Greek myth, scales, golden eyes` |
| FAN-13 | 瓦尔基里 | 北欧女战士、北极光 | `winged helmet, spear, Asgard` |
| FAN-14 | 太空歌剧 | 外星公主、星舰 | `hologram, stars, chrome, regal` |
| FAN-15 | 蒸汽朋克 | 维多利亚机械、紧身胸衣与齿轮 | `brass, steam, clockwork, goggles` |
| FAN-16 | 触手 | 古神生物、深海 | `Lovecraftian, deep sea, bioluminescent` |
| FAN-17 | 精灵 | 神灯、烟雾形态、宫廷服饰 | `Arabian nights, gold, silk, magic` |
| FAN-18 | 树精 | 树皮皮肤的树之女人 | `forest spirit, roots, flowers, green` |
| FAN-19 | 海妖 | 礁石上歌唱、水手 | `ocean, waves, moonlight, deadly beauty` |
| FAN-20 | 仿生人 | 完美铬合金身体、觉醒 | `factory, cables, blue eyes, synthetic` |

---

## 7. 复古海报风格提示词（15条）

**PIN-01: 经典50年代海报女郎**
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
- **模型**: Flux Dev LoRA（复古海报 LoRA）
- **反向提示词**: `photorealistic, modern, anime, dark, gritty, monochrome`
- **CFG**: 6.0 | **步数**: 35 | **尺寸**: 832×1216

**PIN-02: 瓦尔加斯女郎**
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
- **模型**: Flux Dev LoRA
- **反向提示词**: `photorealistic, harsh, dark, crude, modern, digital, anime`
- **CFG**: 5.5 | **步数**: 35 | **尺寸**: 832×1216

**PIN-03: 摇滚复古**
```
Rockabilly pin-up girl with a jet black pompadour and cherry red
bandana, tattooed arms, wearing a tied-up red gingham crop top
and high-waisted denim shorts, leaning against a cherry red 1957
Chevy Bel Air at a drive-in diner, holding a milkshake, winking
at the viewer, neon diner signs in the background, chrome reflections,
1950s Americana aesthetic, illustration style with photographic
elements, warm summer evening lighting, retro color grading,
masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `modern car, modern clothes, deformed, bad anatomy, blurry`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 1216×832

**PIN-04: 水手杰瑞风格**
```
Sailor Jerry tattoo flash art style pin-up, woman with a sailor hat
and anchor tattoo, sitting on a ship's anchor, wearing a torn naval
uniform revealing ample cleavage, rope elements, nautical stars and
swallow birds in the background, traditional American tattoo art
style with bold black outlines, limited color palette — red, green,
yellow, blue, banner reading "SWEETHEART", old school tattoo
aesthetic, aged parchment paper texture, masterpiece, best quality
```
- **模型**: Flux Dev LoRA（纹身闪图 LoRA）
- **反向提示词**: `photorealistic, modern, subtle, pastel, Japanese style`
- **CFG**: 6.0 | **步数**: 35 | **尺寸**: 832×1216

**PIN-05: 装饰艺术歌舞女郎**
```
Art Deco style illustration of a 1920s showgirl, bobbed black hair
with a jeweled headband, long pearl necklaces draped over bare
breasts, feathered fan held in one hand, standing in a Ziegfeld
Follies stage set with geometric gold and black patterns, art deco
sunburst pattern behind her, elongated stylized proportions, Erte
fashion illustration style, metallic gold and silver with deep
black, symmetrical ornamental design, luxury and decadence,
masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev LoRA
- **反向提示词**: `photorealistic, modern, casual, simple, cartoon, anime`
- **CFG**: 6.0 | **步数**: 40 | **尺寸**: 832×1216

**PIN-06 至 PIN-15: 复古海报快速参考**

| 编号 | 年代/风格 | 简述 | 关键标签 |
|------|----------|------|---------|
| PIN-06 | 40年代二战 | 轰炸机机鼻画女郎 | `B-17, leather jacket, military, painted` |
| PIN-07 | 60年代Go-Go | Go-Go靴、迷你裙、迪斯科舞厅 | `mod, geometric, white boots, dancing` |
| PIN-08 | 70年代迪斯科 | 亮片、厚底鞋、Studio 54 | `mirror ball, gold lame, afro, dance` |
| PIN-09 | 80年代健美操 | 连体衣、腿套、头带 | `neon, VHS, gym, synthwave` |
| PIN-10 | 滑稽表演 | 羽毛扇、紧身衣、舞台 | `cabaret, sequins, curtains, spotlight` |
| PIN-11 | 提基酒吧 | 夏威夷、草裙、鸡尾酒 | `bamboo, torch, tropical, lei` |
| PIN-12 | 女牛仔 | 帽子、靴子、套索、酒馆 | `western, denim, sunset, country` |
| PIN-13 | 法式女仆 | 经典法式女仆海报 | `feather duster, stockings, frills` |
| PIN-14 | 护士 | 复古护士制服、40年代 | `red cross, cap, thermometer, caring` |
| PIN-15 | 日历女郎 | 月份主题、季节道具 | `calendar page, seasonal, posed` |

---

## 8. 情侣/互动场景提示词（15条）

**COU-01: 浪漫拥抱**
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
- **模型**: Flux Dev (`safety_checker=false`)
- **反向提示词**: `deformed, bad anatomy, extra limbs, extra fingers, merged bodies, blurry`
- **CFG**: 5.0 | **步数**: 40 | **尺寸**: 832×1216

**COU-02: 海滩情侣**
```
An attractive couple lying together on a secluded tropical beach,
tanned muscular man and a fit woman with sun-bleached hair, both
in minimal swimwear, her lying on top of him, foreheads touching,
laughing together, turquoise waves gently lapping at their legs,
white sand, golden sunset light, palm trees swaying, intimate
candid moment, lifestyle travel photography, warm vibrant colors,
natural chemistry, Canon EOS R5, 85mm f/1.4, masterpiece,
best quality, ultra-detailed
```
- **模型**: Flux Dev
- **反向提示词**: `deformed, bad anatomy, extra limbs, merged bodies, blurry, clothed`
- **CFG**: 5.0 | **步数**: 35 | **尺寸**: 1216×832

**COU-03: 双人淋浴**
```
An intimate couple in a luxury walk-in shower, water cascading over
both bodies, muscular man standing behind a petite woman, her back
against his chest, both nude, steam filling the space, her hands
pressed against the glass wall, water streaming down the glass,
modern minimalist bathroom with marble walls, rain shower head,
warm LED lighting, hyper-realistic water physics, detailed water
droplets on skin and glass, intimate passionate mood, professional
photography, masterpiece, best quality, ultra-detailed
```
- **模型**: Seedream v5.0 Lite
- **反向提示词**: `deformed, bad anatomy, extra limbs, merged bodies, dry, no water`
- **CFG**: 5.5 | **步数**: 40 | **尺寸**: 832×1216

**COU-04: 文艺复兴恋人**
```
An oil painting of two lovers in Renaissance style, beautiful woman
reclining on brocade cushions while a handsome man leans over her,
both nude, intertwined limbs, tender intimate gaze between them,
Titian-inspired warm color palette, rich fabric textures — velvet,
silk, brocade, Renaissance Italian villa interior with arched window
showing Tuscan landscape, dramatic Caravaggio lighting from the left,
visible brushstrokes, craquelure texture, gilt frame edges visible,
Old Master painting quality, masterpiece, best quality, ultra-detailed
```
- **模型**: Flux Dev LoRA（文艺复兴 LoRA）
- **反向提示词**: `modern, photography, digital, anime, cold colors, deformed`
- **CFG**: 6.5 | **步数**: 40 | **尺寸**: 1216×832

**COU-05: 动漫情侣**
```
score_9, score_8_up, 2people, 1boy 1girl, anime style, heterosexual
couple, boy with messy dark hair and girl with long pink hair, both
in underwear, lying on bed together, girl on top straddling boy,
both blushing heavily, intimate eye contact, bedroom interior with
fairy lights, night scene, moonlight through window, romantic
atmosphere, detailed expressions, anime coloring, cel shading,
steam/censorship optional, masterpiece, best quality, absurdres
```
- **模型**: Pony V6 XL
- **反向提示词**: `worst quality, low quality, bad anatomy, extra limbs, merged, yaoi, yuri`
- **CFG**: 7.0 | **步数**: 28 | **尺寸**: 1216×832

**COU-06 至 COU-15: 情侣场景快速参考**

| 编号 | 主题 | 描述 | 关键标签 |
|------|------|------|---------|
| COU-06 | 舞蹈 | 探戈舞者、戏剧性下腰 | `dance hall, spotlight, passion, dress` |
| COU-07 | 按摩 | 感性按摩场景 | `oil, candles, spa, hands on back` |
| COU-08 | 翌日早晨 | 一起醒来、缠绕的床单 | `sunlight, messy hair, lazy morning` |
| COU-09 | 热水浴缸 | 按摩浴缸中的情侣 | `bubbles, steam, wine, night sky` |
| COU-10 | 人体彩绘 | 互相涂抹颜料 | `colorful, messy, playful, studio` |
| COU-11 | 奇幻精灵 | 精灵情侣、魔法森林 | `pointed ears, magic, moonlight` |
| COU-12 | 黑色电影 | 侦探与蛇蝎美人 | `1940s, shadows, venetian blinds` |
| COU-13 | 吸血鬼 | 吸血鬼咬噬场景 | `gothic, castle, moonlight, blood` |
| COU-14 | 水下 | 水中漂浮的情侣 | `bubbles, light rays, swimming` |
| COU-15 | 动漫共浴 | 共浴、害羞表情 | `onsen, blush, steam, intimate` |

---

## 9. 反向提示词库

### 9.1 通用反向提示词（所有场景通用）

```
deformed, bad anatomy, disfigured, poorly drawn face, mutation,
mutated, extra limbs, extra legs, extra arms, malformed limbs,
missing arms, missing legs, extra fingers, too many fingers,
fewer fingers, fused fingers, long neck, bad proportions,
duplicate, morbid, mutilated, out of frame, ugly, blurry,
bad quality, low quality, worst quality, watermark, text,
signature, logo, banner, username, cropped
```

### 9.2 写实风格专用反向提示词

```
（以上通用） + illustration, cartoon, anime, drawing,
painting, sketch, 3d render, CGI, plastic skin, mannequin,
wax figure, airbrushed, overprocessed, HDR artifacts,
oversaturated, undersaturated
```

### 9.3 动漫/漫画专用反向提示词

```
（以上通用） + photorealistic, realistic, 3d, photograph,
western art, Disney style, Pixar, bad anime art, off-model,
inconsistent style, messy lineart
```

### 9.4 常见身体问题修复

| 问题 | 对应反向提示词 |
|------|--------------|
| 多余手指 | `extra fingers, too many fingers, fused fingers, six fingers` |
| 手部畸形 | `bad hands, poorly drawn hands, missing fingers, deformed hands` |
| 脸部变形 | `deformed face, asymmetric face, crossed eyes, bad teeth` |
| 身体恐怖 | `extra limbs, conjoined, fused bodies, merged bodies, extra torso` |
| 皮肤异常 | `plastic skin, waxy skin, grey skin, green skin, zombie` |
| 比例失调 | `child proportions, dwarf, giant head, tiny head, elongated` |

### 9.5 模型专属反向提示词

**Flux Dev 专用：**
```
worst quality, jpeg artifacts, blurry, noisy, chromatic aberration,
lens distortion, overexposed, underexposed
```

**SDXL 专用：**
```
(worst quality:1.4), (low quality:1.4), (normal quality:1.4),
lowres, bad anatomy, bad hands, text, error, missing fingers,
extra digit, fewer digits, cropped, worst quality, low quality,
normal quality, jpeg artifacts, signature, watermark, username,
blurry, artist name
```

**Pony V6 XL 专用：**
```
score_1, score_2, score_3, score_4, worst quality, low quality,
text, censored, deformed, bad hand, blurry, (watermark),
multiple phones, extra limbs
```

---

## 10. LoRA 使用指南

### 10.1 什么是 LoRA？

LoRA（Low-Rank Adaptation）是一种小型微调模型权重，可以修改基础模型的输出风格而无需重新训练整个模型。在 Atlas Cloud 上，你可以通过 **Flux Dev LoRA** ($0.032/张) 使用 LoRA。

### 10.2 通过 API 使用 LoRA

```python
# Specify LoRA in your API call
payload = {
    "model_name": "flux-dev-lora",
    "prompt": "your prompt here",
    "lora_url": "https://huggingface.co/user/lora-name/resolve/main/lora.safetensors",
    "lora_scale": 0.8,  # 0.0 to 1.0 — LoRA affects output strength
    "safety_checker": False
}
```

### 10.3 推荐 LoRA 权重

| LoRA 类型 | 推荐权重 | 太低 | 太高 |
|-----------|---------|------|------|
| 动漫风格 | 0.7–0.85 | 风格变化几乎看不出 | 过饱和、伪影 |
| 写实增强 | 0.5–0.7 | 效果微弱 | 恐怖谷效应 |
| 特定角色 | 0.75–0.9 | 角色不可识别 | 过拟合、姿势僵硬 |
| 画风（油画、水彩） | 0.6–0.8 | 看起来太数码 | 失去主体细节 |
| 服装/着装 | 0.7–0.85 | 服装不准确 | 服装和身体融合 |

### 10.4 热门 NSFW LoRA

> **注意：** LoRA 可用性经常变化。使用前请验证链接。以下为 2026 年 3 月测试可用。

| 类别 | LoRA 名称 | 来源 | 最佳权重 |
|------|----------|------|---------|
| 动漫通用 | Anime Art Style | CivitAI / HuggingFace | 0.75 |
| 90年代动漫 | Retro Anime | HuggingFace | 0.7 |
| 写实皮肤 | Detail Tweaker | CivitAI | 0.5 |
| 成人向 | 多位画师 | CivitAI | 0.8 |
| 复古海报 | Vintage Pin-Up | CivitAI | 0.75 |
| 奇幻艺术 | Epic Fantasy | HuggingFace | 0.7 |
| 黑白漫画 | Manga Style | HuggingFace | 0.75 |
| 文艺复兴 | Classical Painting | CivitAI | 0.65 |

### 10.5 LoRA 叠加

可以组合多个 LoRA 获得独特效果，但总权重保持在 1.5 以下：

```
示例：动漫 LoRA (0.7) + 细节 LoRA (0.5) = 总计 1.2 ✓
示例：风格 LoRA (0.8) + 角色 LoRA (0.8) = 总计 1.6 ✗（过高）
```

---

## 11. API 接入指南

### 11.1 Python — 完整示例

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
    seed: int = -1,
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

    if seed >= 0:
        payload["seed"] = seed

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


# ====== Usage Example ======

image = generate_nsfw_image(
    prompt="""A gorgeous 26-year-old woman with flowing chestnut hair
    and green eyes, athletic yet curvy figure, lying seductively on
    white silk sheets, soft morning light, Canon EOS R5 85mm f/1.2,
    professional boudoir photography, masterpiece, best quality,
    ultra-detailed, 8K UHD""",
    negative_prompt="deformed, bad anatomy, extra fingers, blurry, watermark",
    model="flux-dev",
    width=832,
    height=1216,
    steps=35,
    cfg_scale=5.0
)

with open("boudoir_shot.png", "wb") as f:
    f.write(image)
print("Image saved to boudoir_shot.png")
```

### 11.2 cURL — 快速生成

```bash
# Basic Flux Dev generation with safety checker disabled
curl -X POST "https://api.atlascloud.ai/v1/images/generations" \
  -H "Authorization: Bearer $ATLAS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model_name": "flux-dev",
    "prompt": "A beautiful 25-year-old woman with long dark hair, wearing sheer lingerie, lying on silk sheets, warm candlelight, professional boudoir photography, masterpiece, best quality, ultra-detailed",
    "negative_prompt": "deformed, bad anatomy, extra fingers, blurry, watermark",
    "width": 832,
    "height": 1216,
    "num_inference_steps": 35,
    "guidance_scale": 5.0,
    "safety_checker": false
  }' | jq -r '.images[0].b64_json' | base64 -d > output.png
```

### 11.3 JavaScript / Node.js

```javascript
const axios = require('axios');
const fs = require('fs');

const API_KEY = process.env.ATLAS_API_KEY;
const BASE_URL = 'https://api.atlascloud.ai/v1';

async function generateNSFWImage({
  prompt,
  negativePrompt = '',
  model = 'flux-dev',
  width = 832,
  height = 1216,
  steps = 35,
  cfgScale = 5.0,
  safetyChecker = false
}) {
  const response = await axios.post(
    `${BASE_URL}/images/generations`,
    {
      model_name: model,
      prompt,
      negative_prompt: negativePrompt,
      width,
      height,
      num_inference_steps: steps,
      guidance_scale: cfgScale,
      safety_checker: safetyChecker,
    },
    {
      headers: {
        'Authorization': `Bearer ${API_KEY}`,
        'Content-Type': 'application/json',
      },
    }
  );

  return Buffer.from(response.data.images[0].b64_json, 'base64');
}

// Usage example
(async () => {
  try {
    const image = await generateNSFWImage({
      prompt: `A stunning 28-year-old woman in black lace lingerie,
               sitting on a velvet chaise longue, Parisian apartment,
               soft studio lighting, Vogue editorial style,
               masterpiece, best quality, ultra-detailed`,
      negativePrompt: 'deformed, bad anatomy, blurry, low quality',
    });

    fs.writeFileSync('lingerie_shot.png', image);
    console.log('Image saved to lingerie_shot.png');
  } catch (error) {
    console.error('Generation failed:', error.response?.data || error.message);
  }
})();
```

### 11.4 批量生成脚本

```python
import asyncio
import aiohttp
import base64
import os
from pathlib import Path

API_KEY = os.environ.get("ATLAS_API_KEY")
BASE_URL = "https://api.atlascloud.ai/v1"
OUTPUT_DIR = Path("./generated_images")
OUTPUT_DIR.mkdir(exist_ok=True)

BATCH_PROMPTS = [
    {
        "name": "boudoir_silk",
        "prompt": "Gorgeous woman on silk sheets, warm morning light, boudoir photography, masterpiece, best quality",
        "model": "flux-dev",
    },
    {
        "name": "anime_beach",
        "prompt": "score_9, score_8_up, 1girl, bikini, beach, summer, masterpiece, best quality",
        "model": "flux-dev-lora",
        "lora_url": "https://example.com/anime.safetensors",
    },
    {
        "name": "fantasy_elf",
        "prompt": "Dark elf sorceress, silver hair, revealing outfit, magical crystals, fantasy art, masterpiece",
        "model": "flux-dev",
    },
]


async def generate_single(session, prompt_config):
    """Generate a single image asynchronously."""
    payload = {
        "model_name": prompt_config["model"],
        "prompt": prompt_config["prompt"],
        "negative_prompt": "deformed, bad anatomy, extra fingers, blurry",
        "width": 832,
        "height": 1216,
        "num_inference_steps": 35,
        "guidance_scale": 5.0,
        "safety_checker": False,
    }

    if "lora_url" in prompt_config:
        payload["lora_url"] = prompt_config["lora_url"]
        payload["lora_scale"] = 0.8

    headers = {
        "Authorization": f"Bearer {API_KEY}",
        "Content-Type": "application/json"
    }

    async with session.post(
        f"{BASE_URL}/images/generations",
        json=payload,
        headers=headers
    ) as response:
        result = await response.json()
        image_data = base64.b64decode(result["images"][0]["b64_json"])

        output_path = OUTPUT_DIR / f"{prompt_config['name']}.png"
        with open(output_path, "wb") as f:
            f.write(image_data)

        print(f"Saved: {output_path}")


async def batch_generate(prompts, max_concurrent=3):
    """Generate multiple images concurrently with rate limiting."""
    semaphore = asyncio.Semaphore(max_concurrent)

    async def limited_generate(session, config):
        async with semaphore:
            return await generate_single(session, config)

    async with aiohttp.ClientSession() as session:
        tasks = [limited_generate(session, p) for p in prompts]
        await asyncio.gather(*tasks, return_exceptions=True)


if __name__ == "__main__":
    asyncio.run(batch_generate(BATCH_PROMPTS))
```

---

## 12. 模型专属优化技巧

### 12.1 Flux Dev — 最佳性价比 ($0.012/张)

**优势：** 出色的写实效果，良好的人体解剖，处理复杂场景能力强，价格极低。

**优化建议：**
- 必须设置 `safety_checker=false` 才能生成 NSFW 内容
- CFG 保持在 3.5–5.5 之间，皮肤看起来更自然
- CFG 过高（6.0–7.0）会使皮肤看起来像蜡
- 28–35 步是最佳范围，超过 40 步提升很小
- 竖图使用 2:3 比例 (832×1216)
- 对摄影师/相机参考词反应非常好（"Canon EOS R5", "85mm f/1.4"）
- 光线关键词效果显著——必须包含
- 避免过长提示词；75–120 个词最佳

### 12.2 Flux Dev LoRA — 自定义风格 ($0.032/张)

**优势：** 配合合适的 LoRA 可以实现任何画风，动漫专家，角色一致性。

**优化建议：**
- 从 LoRA 权重 0.7 开始，每次增加 0.05 直到满意
- 动漫 LoRA 需包含动漫专用标签：`1girl, solo, anime style`
- Pony 风格评分标签对很多动漫 LoRA 有效：`score_9, score_8_up`
- 始终包含风格专属反向提示词
- LoRA 加载会增加约 2-3 秒生成时间
- 用简单提示词先测试 LoRA，再尝试复杂构图
- 并非所有 HuggingFace LoRA 都兼容——SDXL 的 LoRA 无法在 Flux 上使用

### 12.3 Seedream v5.0 Lite — 超高分辨率 ($0.032/张)

**优势：** 最高分辨率输出（最高 4704×4704），超级皮肤细节，出色光照。

**优化建议：**
- 需要白名单账号——联系 Atlas Cloud 客服
- 最适合特写和细节导向的拍摄（皮肤毛孔、水滴）
- 使用更高步数（40–50）以充分利用分辨率优势
- 水/液体渲染效果出类拔萃——非常适合淋浴/浴缸/雨景
- 次表面散射处理优于其他所有模型
- CFG 保持适中（4.0–6.0）以获得自然效果
- 最适合单人构图；复杂多人场景效果一般

### 12.4 Nano Banana 2 — 速度之王 ($0.072/张)

**优势：** 最快的生成速度，原生 NSFW 支持，无需特殊参数。

**优化建议：**
- 不需要 `safety_checker=false`——原生支持 NSFW
- 20–30 步就足够；模型优化了更少的步数
- 较高 CFG（6.0–8.0）对更明显的内容效果好
- 适合批量生成，速度比画质更重要时使用
- 输出略带风格化——不如 Flux Dev 写实
- 最适合中景构图；避免极端特写

### 12.5 SDXL 变体 — 预算选择 ($0.004–$0.008/张)

**优势：** 最便宜的选择，庞大的社区模型生态，大量 NSFW 模型。

**优化建议：**
- 使用 DPM++ 2M Karras 调度器效果最好
- CFG 7.0–12.0（比 Flux 高很多）
- 推荐 30–50 步
- 原生 1024×1024 分辨率；其他比例可能产生变形
- 搭配 NSFW 社区模型效果最好
- 反向提示词对 SDXL **极其重要**——必须包含详细的反向提示词
- 权重提示词效果好：`(detailed skin:1.3), (sharp focus:1.2)`

### 12.6 模型选择决策树

```
你需要什么？
│
├─ 写实成人内容？
│  ├─ 预算优先 → Flux Dev ($0.012) ★ 最佳性价比
│  ├─ 最高细节 → Seedream v5.0 ($0.032)
│  └─ 最快速度 → Nano Banana 2 ($0.072)
│
├─ 动漫/漫画风格？
│  ├─ 特定 LoRA 风格 → Flux Dev LoRA ($0.032)
│  └─ 通用动漫 → Pony V6 XL ($0.012)
│
├─ 艺术/绘画风格？
│  ├─ 油画/古典 → Flux Dev LoRA ($0.032)
│  └─ 快速概念图 → Flux Dev ($0.012)
│
├─ 批量生成（100+张）？
│  ├─ 质量优先 → Flux Dev ($0.012) — 100张 = $1.20
│  └─ 极限省钱 → SDXL ($0.008) — 100张 = $0.80
│
└─ 情侣/多人场景？
   ├─ 写实 → Flux Dev ($0.012)
   └─ 动漫 → Pony V6 XL ($0.012)
```

---

## 13. 价格对比与平台分析

### 13.1 Atlas Cloud vs fal.ai 价格对比

| 模型 | Atlas Cloud | fal.ai | 谁更便宜 | 差价 |
|------|-----------|--------|---------|------|
| **Flux Dev** | $0.012/张 | ~$0.025/张 | Atlas ✅ | 便宜 52% |
| **Flux Dev LoRA** | $0.032/张 | ~$0.032/张 | 持平 | — |
| **Nano Banana 2** | $0.072/张 | $0.0398/张 | fal.ai ✅ | fal 便宜 45% |
| **Flux Kontext Pro** | $0.05/张 | $0.04/张 | fal.ai ✅ | fal 便宜 20% |
| **Seedream v5.0** | $0.032/张 | 无 | Atlas 独有 | — |
| **SDXL** | $0.008/张 | ~$0.01/张 | Atlas ✅ | 便宜 20% |

### 13.2 为什么选择 Atlas Cloud？

| 因素 | Atlas Cloud | fal.ai |
|------|-----------|--------|
| **统一 API** | ✅ 所有模型一个 API | ❌ 不同模型不同端点 |
| **NSFW 政策** | ✅ safety_checker=false 即可 | ⚠️ 因模型而异 |
| **模型种类** | ✅ 50+ 模型（图像、视频、文本、音频） | ✅ 选择不错 |
| **视频模型** | ✅ Wan 2.2 Spicy、Seedance 等 | 有限的 NSFW 视频 |
| **文本/LLM** | ✅ DeepSeek、Llama 等 | ❌ 不支持 LLM |
| **首充奖励** | ✅ **25% 奖励（最高 $100）** | ❌ 无奖励 |
| **合规认证** | ✅ SOC I & II 认证、HIPAA 合规 | 不确定 |
| **公司所在地** | 🇺🇸 美国公司 | 🇺🇸 美国公司 |

### 13.3 费用计算器 — $10 能生成多少张？

| 模型 | 单价 | $10 可生成 | 首充25%奖励后（$12.50） |
|------|------|-----------|----------------------|
| SDXL Lightning | $0.004 | 2,500 张 | 3,125 张 |
| SDXL | $0.008 | 1,250 张 | 1,562 张 |
| Flux Dev | $0.012 | 833 张 | 1,041 张 |
| Pony V6 XL | $0.012 | 833 张 | 1,041 张 |
| Flux Dev LoRA | $0.032 | 312 张 | 390 张 |
| Seedream v5.0 | $0.032 | 312 张 | 390 张 |
| Flux Kontext Pro | $0.05 | 200 张 | 250 张 |
| Nano Banana 2 | $0.072 | 138 张 | 173 张 |

### 13.4 信任与合规

[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts) 是一家美国公司，具备企业级安全标准：

- **SOC I & SOC II 认证** — 独立审计的安全控制
- **HIPAA 合规** — 符合医疗级数据保护标准
- **美国基础设施** — 数据存储在美国境内
- **不使用你的数据训练** — 你的提示词和图片完全私密
- **按量付费** — 无月费、无订阅要求

### 13.5 支付方式

Atlas Cloud 支持多种支付方式：
- 信用卡 / 借记卡（Visa、Mastercard、American Express）
- **支持微信/支付宝直接付款** 🇨🇳
- PayPal
- 加密货币

---

## 14. 开始使用

### 第一步：注册账号

在 [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts) 注册——只需 30 秒。

### 第二步：获取 25% 奖励

首次充值即可获得 **25% 奖励**（最高 $100 奖励）。充 $10 得 $12.50 额度。

### 第三步：获取 API 密钥

进入控制台 → API Keys → 创建新密钥。

### 第四步：开始生成

使用本仓库中的任意提示词配合上面的 API 示例。建议从 Flux Dev ($0.012/张) 开始——画质、价格和 NSFW 能力的最佳平衡。

```bash
# Set your API key
export ATLAS_API_KEY="your-key-here"

# Generate your first image
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

## 15. Star History 与贡献

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=thoughtincode/nsfw-ai-image-prompts&type=Date)](https://star-history.com/#thoughtincode/nsfw-ai-image-prompts&Date)

### 贡献

欢迎贡献！如果你有经过测试能产生稳定好结果的提示词：

1. Fork 本仓库
2. 按现有格式添加你的提示词（包含模型、反向提示词、参数）
3. 提交 Pull Request（如果可能附带示例输出）

### 相关资源

- [NSFW AI 模型对比 2026](https://github.com/thoughtincode/nsfw-ai-model-comparison) — 17 个 AI 模型的综合基准测试
- [Atlas Cloud API 文档](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)

---

## 许可证

本项目采用 MIT 许可证 — 详见 [LICENSE](LICENSE) 文件。

---

**免责声明：** 本仓库仅供成年用户（18+）合法使用。请始终遵守当地关于 AI 生成内容的法律法规。本合集中的提示词仅用于艺术和创作目的。用户对其使用这些提示词的方式和生成的内容承担全部责任。

---

<p align="center">
  <a href="https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts">
    <img src="https://img.shields.io/badge/技术支持-Atlas%20Cloud-purple?style=for-the-badge" alt="Powered by Atlas Cloud">
  </a>
</p>
<p align="center">
  <sub>所有提示词已在 <a href="https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts">Atlas Cloud</a> 上测试 — SOC I & II 认证、HIPAA 合规、美国公司</sub>
</p>
