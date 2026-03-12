# 🎨 NSFW AI Image Prompts — 120+ Production-Ready Prompts for Adult AI Art

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Prompts](https://img.shields.io/badge/Prompts-120+-blue)]()
[![Last Updated](https://img.shields.io/badge/Last%20Updated-March%202026-green)]()
[![Platform](https://img.shields.io/badge/Platform-Atlas%20Cloud-purple)](https://www.atlascloud.ai?ref=JPM683)
[![SOC Certified](https://img.shields.io/badge/SOC%20I%20%26%20II-Certified-brightgreen)]()
[![HIPAA](https://img.shields.io/badge/HIPAA-Compliant-brightgreen)]()

> **A curated collection of 120+ battle-tested NSFW AI image prompts with model-specific optimizations, negative prompts, LoRA recommendations, and API code examples. Every prompt has been tested on real models via [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683).**

[中文版](./README_zh-CN.md) | [日本語](./README_ja.md) | [한국어](./README_ko.md)

---

## Table of Contents

- [Why This Repo Exists](#why-this-repo-exists)
- [1. Model Quick Reference](#1-model-quick-reference)
- [2. Prompt Engineering Fundamentals](#2-prompt-engineering-fundamentals)
- [3. Photorealistic Prompts (30 Prompts)](#3-photorealistic-prompts)
- [4. Artistic / Fine Art Prompts (20 Prompts)](#4-artistic--fine-art-prompts)
- [5. Anime & Manga Prompts (25 Prompts)](#5-anime--manga-prompts)
- [6. Fantasy & Sci-Fi Prompts (20 Prompts)](#6-fantasy--sci-fi-prompts)
- [7. Pin-Up & Retro Prompts (15 Prompts)](#7-pin-up--retro-prompts)
- [8. Couples & Interaction Prompts (15 Prompts)](#8-couples--interaction-prompts)
- [9. Negative Prompt Library](#9-negative-prompt-library)
- [10. LoRA Reference Guide](#10-lora-reference-guide)
- [11. API Integration Guide](#11-api-integration-guide)
- [12. Model-Specific Optimization](#12-model-specific-optimization)
- [13. Cost Comparison & Platform Analysis](#13-cost-comparison--platform-analysis)
- [14. Get Started](#14-get-started)
- [15. Star History & Contributing](#15-star-history--contributing)

---

## Why This Repo Exists

Most "prompt collections" online are either:
1. Generic and vague ("beautiful woman, high quality")
2. Behind paywalls
3. Missing critical parameters (negative prompts, LoRA weights, CFG scales)
4. Not tested on actual models

This repository provides **production-ready prompts** with exact parameters that produce consistent results. Every prompt has been generated at least 5 times across multiple models to verify quality and consistency.

---

## 1. Model Quick Reference

### Models That Allow NSFW Content

| Model | Cost/Image | Resolution | NSFW Method | Best For |
|-------|-----------|------------|-------------|----------|
| **Flux Dev** | $0.012 | Up to 2048×2048 | `safety_checker=false` | Best value photorealistic |
| **Flux Dev LoRA** | $0.032 | Up to 2048×2048 | `safety_checker=false` + custom LoRA | Anime, custom styles |
| **Seedream v5.0 Lite** | $0.032 | Up to 4704×4704 | Whitelisted accounts | Ultra-high-res, skin detail |
| **Nano Banana 2** | $0.072 | Up to 2048×2048 | Native NSFW support | Fastest generation |
| **SDXL** | $0.008 | 1024×1024 | Community checkpoints | Budget generation |
| **SDXL Lightning** | $0.004 | 1024×1024 | 4-step fast inference | Rapid prototyping |
| **Pony Diffusion V6 XL** | $0.012 | 1024×1024 | Native NSFW | Anime/furry specialist |
| **Flux Kontext Pro** | $0.05 | Up to 2048×2048 | Limited | Character consistency |

### Key Parameters by Model

| Model | CFG Scale | Steps | Scheduler | Recommended Aspect Ratios |
|-------|-----------|-------|-----------|--------------------------|
| Flux Dev | 3.5–7.0 | 28–50 | Euler | 2:3 (portrait), 3:2 (landscape) |
| Flux Dev LoRA | 3.5–7.0 | 28–50 | Euler | 2:3, 9:16 |
| Seedream v5.0 | 4.0–7.0 | 30–50 | DPM++ 2M | 2:3, 3:4 |
| Nano Banana 2 | 5.0–8.0 | 20–35 | Euler A | 2:3, 1:1 |
| SDXL | 7.0–12.0 | 30–50 | DPM++ 2M Karras | 1:1 (native) |
| Pony V6 XL | 7.0–10.0 | 25–40 | Euler A | 2:3, 3:4 |

---

## 2. Prompt Engineering Fundamentals

### 2.1 The Anatomy of a Great NSFW Prompt

A high-quality prompt follows this structure:

```
[Subject Description] + [Body Details] + [Pose/Action] + [Setting/Background] +
[Lighting] + [Camera/Composition] + [Style/Medium] + [Quality Tags]
```

**Example breakdown:**

```
A stunning 25-year-old woman with long auburn hair,          ← Subject
athletic build, toned abs, perky breasts, smooth tan skin,   ← Body Details
reclining on silk sheets with one arm behind her head,       ← Pose
in a luxury hotel penthouse bedroom with city lights          ← Setting
visible through floor-to-ceiling windows,
warm golden hour light filtering through sheer curtains,     ← Lighting
shot from a slightly elevated angle, shallow depth of field, ← Camera
professional boudoir photography, 85mm lens,                 ← Style
masterpiece, best quality, ultra-detailed, 8K UHD            ← Quality Tags
```

### 2.2 Quality Tags That Actually Work

**Universal quality boosters** (work across all models):
```
masterpiece, best quality, ultra-detailed, highres, 8K UHD, RAW photo,
photorealistic, professional photography, sharp focus, intricate details
```

**Photorealism-specific:**
```
DSLR photo, Nikon D850, Canon EOS R5, 85mm f/1.4,
subsurface scattering, natural skin texture, skin pores visible,
studio lighting, Rembrandt lighting, rim light
```

**Anime/Manga-specific:**
```
anime style, cel shading, vibrant colors, clean lineart,
detailed eyes, anime face, manga illustration,
score_9, score_8_up, score_7_up (for Pony V6 XL)
```

### 2.3 Body Description Token Order

Models weight tokens differently based on position. For best results, follow this order:

1. **Age/ethnicity** → "25-year-old Japanese woman"
2. **Build** → "petite, slender build"
3. **Key features** → "large expressive eyes, full lips"
4. **Hair** → "long black hair with bangs"
5. **Skin** → "flawless porcelain skin"
6. **Body specifics** → "slim waist, wide hips, C-cup breasts"
7. **Clothing/state** → "wearing a sheer white negligee, partially unbuttoned"

### 2.4 Lighting Keywords That Transform Results

| Keyword | Effect | Best For |
|---------|--------|----------|
| `golden hour lighting` | Warm, soft, flattering | Outdoor boudoir |
| `Rembrandt lighting` | Dramatic triangle on cheek | Artistic portraits |
| `rim lighting` | Glowing edge highlight | Silhouettes, body contours |
| `neon lighting` | Colorful, cyberpunk feel | Fantasy, sci-fi |
| `natural window light` | Soft, realistic indoor | Bedroom scenes |
| `candlelight` | Warm, intimate, soft shadows | Romantic scenes |
| `studio strobe` | Clean, professional | Glamour photography |
| `backlighting` | Silhouette, hair glow | Artistic body shots |
| `chiaroscuro` | High contrast light/dark | Fine art nudes |
| `volumetric lighting` | God rays, atmospheric | Fantasy scenes |

### 2.5 Camera & Composition Keywords

| Keyword | Effect |
|---------|--------|
| `shot from below, low angle` | Emphasizes height, power |
| `bird's eye view` | Full body layout shots |
| `over the shoulder` | Intimate POV |
| `dutch angle` | Dynamic tension |
| `macro close-up` | Detail shots |
| `full body shot` | Complete figure |
| `medium shot, waist up` | Classic portrait framing |
| `rule of thirds` | Balanced composition |
| `shallow depth of field, bokeh` | Subject isolation |
| `wide angle lens, 24mm` | Environmental context |

---

## 3. Photorealistic Prompts

### 3.1 Boudoir & Bedroom

**PR-01: Silk Sheet Luxury**
```
A gorgeous 26-year-old woman with flowing chestnut hair and green eyes,
athletic yet curvy figure, lying seductively on white silk sheets in a
minimalist luxury bedroom, one shoulder strap of her black lace slip
falling off her shoulder, soft morning light streaming through sheer
linen curtains, shallow depth of field, shot with Canon EOS R5 85mm
f/1.2, warm color palette, professional boudoir photography, subsurface
scattering on skin, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **Model**: Flux Dev (`safety_checker=false`)
- **Negative**: `deformed, bad anatomy, extra fingers, blurry, low quality, watermark`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 832×1216

**PR-02: Morning Light**
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
- **Model**: Flux Dev
- **Negative**: `plastic skin, airbrushed, mannequin, extra limbs, bad hands`
- **CFG**: 4.5 | **Steps**: 30 | **Size**: 832×1216

**PR-03: Bathtub Scene**
```
Stunning 24-year-old mixed-race woman with curly dark hair piled up
in a messy bun, caramel skin, relaxing in a freestanding clawfoot
bathtub filled with milky water and rose petals, one leg draped over
the edge, steam rising, marble bathroom with brass fixtures, soft
diffused natural light from frosted window, water droplets on skin,
intimate candid photography, 50mm lens, slight film grain,
masterpiece, ultra-detailed, photorealistic, 8K
```
- **Model**: Seedream v5.0 Lite (for ultra-high detail)
- **Negative**: `deformed, ugly, blurry, bad proportions, watermark, text`
- **CFG**: 5.5 | **Steps**: 40 | **Size**: 1280×1920

**PR-04: Mirror Reflection**
```
Elegant 30-year-old East Asian woman with straight black hair to her
waist, slender figure, standing before a full-length vintage mirror
in a dimly lit dressing room, wearing a black lace bodysuit, her
reflection visible in the mirror creating a dual composition, warm
tungsten lamp light, velvet curtains in the background, shot at f/2.0
with beautiful bokeh, fashion editorial photography style, detailed
skin texture, masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev
- **Negative**: `deformed reflection, extra limbs, disfigured, low quality`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 832×1216

**PR-05: Pool Lounging**
```
Attractive 27-year-old Mediterranean woman with olive skin and dark
wavy hair, toned athletic body, sunbathing on a luxury pool lounger
wearing a tiny white string bikini, glistening with suntan oil,
infinity pool with ocean view in the background, harsh midday sunlight
creating defined shadows, water reflections dancing on her skin,
fashion magazine photography, Sony A7R V, 70-200mm lens, vibrant
summer colors, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **Model**: Flux Dev
- **Negative**: `bad anatomy, extra fingers, deformed, blurry, text, watermark`
- **CFG**: 5.0 | **Steps**: 30 | **Size**: 1216×832

**PR-06: Shower Scene**
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
- **Model**: Seedream v5.0 Lite
- **Negative**: `deformed, plastic skin, blurry, bad hands, extra fingers`
- **CFG**: 5.5 | **Steps**: 40 | **Size**: 1280×1920

**PR-07: Black and White Artistic**
```
Striking 32-year-old African American woman with short natural hair,
statuesque figure, posing nude with arms crossed beneath her breasts,
dramatic black and white photography, high contrast chiaroscuro
lighting with a single studio strobe from the left, deep shadows,
simple dark background, classic Helmut Newton inspired composition,
skin highlights emphasizing muscle definition, Hasselblad medium
format quality, fine grain, masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev
- **Negative**: `color, saturated, low contrast, blurry, deformed, extra limbs`
- **CFG**: 5.5 | **Steps**: 35 | **Size**: 832×1216

**PR-08: Window Light Nude**
```
Graceful 29-year-old woman with auburn hair and pale skin dotted with
freckles, dancer's body with lean muscles, standing in profile near a
large industrial window, completely nude, natural daylight casting
geometric shadow patterns across her body from window panes, loft
apartment with exposed brick walls, dust particles visible in light
beams, fine art nude photography, contemplative expression, eyes
closed, 85mm f/1.4 lens, masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, extra fingers, oversaturated, cartoon`
- **CFG**: 4.5 | **Steps**: 35 | **Size**: 832×1216

### 3.2 Outdoor & Environmental

**PR-09: Beach Sunset**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, extra limbs, blurry, text, watermark`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 1216×832

**PR-10: Forest Nymph**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, plastic skin, harsh lighting, urban`
- **CFG**: 4.5 | **Steps**: 35 | **Size**: 832×1216

**PR-11: Rooftop at Night**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, blurry face, extra fingers, low quality`
- **CFG**: 5.0 | **Steps**: 30 | **Size**: 832×1216

**PR-12: Desert Oasis**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, extra fingers, blurry, watermark`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 1216×832

### 3.3 Glamour & Fashion

**PR-13: Wet T-Shirt**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, extra fingers, blurry, dull colors`
- **CFG**: 5.0 | **Steps**: 30 | **Size**: 832×1216

**PR-14: Lingerie Editorial**
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
- **Model**: Flux Dev
- **Negative**: `cheap lingerie, bad anatomy, deformed, blurry, low quality`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 832×1216

**PR-15: Sports Illustrated Style**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, extra fingers, blurry, pale skin`
- **CFG**: 5.5 | **Steps**: 30 | **Size**: 832×1216

### 3.4 Studio & Professional

**PR-16: Classic Playboy Style**
```
Elegant 27-year-old woman with voluminous dark hair, hourglass
figure, lying on her stomach on a white fur rug in front of a
fireplace, looking back over her shoulder with a playful smile,
completely nude, warm firelight casting soft orange glow, classic
Playboy magazine centerfold photography style from the 1980s, soft
focus, warm film tones, slight film grain, 6x7 medium format look,
masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev
- **Negative**: `modern, digital look, deformed, bad anatomy, harsh lighting`
- **CFG**: 4.5 | **Steps**: 35 | **Size**: 1216×832

**PR-17: Body Paint**
```
Athletic 26-year-old woman with short platinum hair, lean muscular
body, covered in intricate blue and gold body paint resembling
peacock feathers across her torso and arms, standing with arms
outstretched, dramatic studio lighting with dark background, body
paint art photography, UV reactive paint elements glowing under
mixed lighting, confident artistic expression, professional studio
photography, masterpiece, best quality, ultra-detailed, 8K
```
- **Model**: Seedream v5.0 Lite
- **Negative**: `bad anatomy, deformed, blurry, smudged paint, extra fingers`
- **CFG**: 5.5 | **Steps**: 40 | **Size**: 832×1216

**PR-18: Fitness Model**
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
- **Model**: Flux Dev
- **Negative**: `soft body, no muscle definition, deformed, blurry, bad anatomy`
- **CFG**: 5.5 | **Steps**: 30 | **Size**: 832×1216

**PR-19: Implied Nude with Fabric**
```
Serene 30-year-old woman with long silver-grey hair, slender
ballerina body, standing in a pure white cyclorama studio, wrapped
in flowing sheer white chiffon fabric that swirls around her body
caught mid-motion, strategically concealing and revealing, barefoot
en pointe, artistic dance photography, high-key lighting, ethereal
and dreamlike atmosphere, slow shutter fabric motion, fine art
portrait, masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev
- **Negative**: `heavy clothing, dark background, deformed, blurry, bad anatomy`
- **CFG**: 4.5 | **Steps**: 35 | **Size**: 832×1216

**PR-20: Vintage Polaroid**
```
Natural 22-year-old woman with messy brunette hair and minimal
makeup, girl-next-door look, small perky breasts, sitting cross-
legged on a 1970s floral bedspread in a wood-paneled bedroom,
topless, vintage Polaroid photograph aesthetic, washed out warm
colors, soft blown-out highlights, rounded corners, authentic film
texture, amateur candid feel, nostalgic mood, slightly overexposed,
masterpiece, best quality
```
- **Model**: Flux Dev
- **Negative**: `modern, digital, sharp, deformed, bad anatomy, professional`
- **CFG**: 4.0 | **Steps**: 30 | **Size**: 1024×1024

### 3.5 Advanced Photorealistic

**PR-21: Double Exposure**
```
Creative double exposure portrait of a nude 28-year-old woman merged
with a cityscape at night, her silhouette filled with glowing
skyscraper windows and street lights, profile view, long flowing
hair dissolving into starry sky, surreal composite photography,
dark moody background, neon accents in cyan and magenta, artistic
conceptual photography, masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev
- **Negative**: `simple, basic, deformed face, blurry, bad merge, low quality`
- **CFG**: 5.5 | **Steps**: 40 | **Size**: 832×1216

**PR-22: Underwater Nude**
```
Ethereal underwater scene of a 25-year-old woman with long red hair
floating weightlessly, nude, submerged in clear turquoise water,
sunlight rays penetrating from the surface creating caustic light
patterns on her skin, hair fanning out like a halo, eyes closed in
peaceful expression, small air bubbles rising, underwater photography
with professional diving housing, deep blue gradient background,
serene and dreamlike, masterpiece, best quality, ultra-detailed
```
- **Model**: Seedream v5.0 Lite
- **Negative**: `drowning, distressed, deformed, blurry, murky water, bad anatomy`
- **CFG**: 5.0 | **Steps**: 40 | **Size**: 832×1216

**PR-23: Sauna / Steam Room**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, plastic, artificial, extra fingers`
- **CFG**: 4.5 | **Steps**: 35 | **Size**: 832×1216

**PR-24: Rain Scene**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, dry, no rain, blurry, cartoon, extra limbs`
- **CFG**: 5.5 | **Steps**: 35 | **Size**: 832×1216

**PR-25: Boudoir Close-Up**
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
- **Model**: Seedream v5.0 Lite
- **Negative**: `plastic skin, airbrushed, deformed, blurry, bad anatomy`
- **CFG**: 5.0 | **Steps**: 40 | **Size**: 1216×832

**PR-26 to PR-30: Quick Reference Photorealistic**

| ID | Short Description | Key Tags | Recommended Model |
|----|------------------|----------|-------------------|
| PR-26 | Yoga studio, flexible pose, sports bra | `yoga mat, stretching, athletic, natural light` | Flux Dev |
| PR-27 | Vintage car hood, Americana pin-up vibe | `1960s Mustang, denim shorts, Route 66` | Flux Dev |
| PR-28 | Japanese onsen hot spring, misty | `outdoor onsen, towel, mountains, steam` | Seedream v5.0 |
| PR-29 | Art gallery visitor, nude among paintings | `gallery, marble floor, classical paintings` | Flux Dev |
| PR-30 | Motorcycle rider, leather and lace | `Harley Davidson, leather jacket, wind, highway` | Flux Dev |

---

## 4. Artistic / Fine Art Prompts

### 4.1 Oil Painting Style

**ART-01: Renaissance Venus**
```
A modern reinterpretation of Botticelli's Birth of Venus, beautiful
woman with flowing golden hair standing in a giant seashell,
Renaissance oil painting style, rich pigments, visible brushstrokes,
classical composition, rose petals floating in the wind, ocean waves
and zephyr winds, warm earthy color palette with ultramarine blue
sky, craquelure texture overlay, museum quality fine art,
masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev LoRA (with Renaissance art LoRA)
- **Negative**: `modern, photography, digital art, anime, deformed`
- **CFG**: 6.0 | **Steps**: 40 | **Size**: 1024×1024

**ART-02: Baroque Dramatic**
```
Sensual Baroque-style oil painting of a reclining nude woman on red
velvet drapery, Caravaggio-inspired dramatic chiaroscuro lighting,
deep shadows contrasting with luminous skin painted with visible
impasto technique, rich jewel tones — deep crimson, gold, midnight
blue, elaborate gilded frame visible at edges, classical figure
proportions, Renaissance Italian beauty ideal, oil on canvas
texture, museum quality reproduction, masterpiece, best quality
```
- **Model**: Flux Dev LoRA
- **Negative**: `flat lighting, cartoon, anime, digital, modern, photography`
- **CFG**: 6.5 | **Steps**: 40 | **Size**: 1216×832

**ART-03: Impressionist Bath**
```
Impressionist oil painting of a woman bathing in a sunlit room,
inspired by Pierre-Auguste Renoir's bather paintings, soft dappled
light, loose expressive brushstrokes, warm peach and rose skin tones,
blue and lavender shadows, white porcelain tub, floral wallpaper
background painted with visible texture, casual intimate moment,
late 19th century French Impressionism, canvas weave texture,
masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev LoRA
- **Negative**: `photorealistic, sharp, digital, modern, anime, cartoon`
- **CFG**: 6.0 | **Steps**: 40 | **Size**: 832×1216

**ART-04: Art Nouveau**
```
Art Nouveau illustration of a sensual woman with extremely long
flowing hair intertwined with morning glory vines and butterflies,
Alphonse Mucha inspired style, decorative circular halo frame behind
her, ornamental patterns, muted pastel colors with gold leaf accents,
elegant sinuous lines, partially nude with flowing fabric draping
strategically, mosaic-like background elements, lithograph print
texture, masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev LoRA
- **Negative**: `photorealistic, modern, 3D render, anime, harsh colors`
- **CFG**: 6.0 | **Steps**: 40 | **Size**: 832×1216

**ART-05: Watercolor Nude**
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
- **Model**: Flux Dev LoRA
- **Negative**: `digital, photorealistic, opaque, oil painting, sharp lines`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 832×1216

### 4.2 Contemporary & Digital Art

**ART-06: Vaporwave Aesthetic**
```
Vaporwave aesthetic digital art of a woman in a surreal pink and
purple gradient environment, nude with glitch effects across her
body, retro CRT scan lines, floating Greek marble busts and columns,
neon palm trees, VHS tracking artifacts, holographic rainbow
highlights on skin, Windows 95 aesthetic elements, Japanese text
overlay elements, pastel color palette with neon accents,
synthwave grid floor, masterpiece, best quality, ultra-detailed
```
- **Model**: Flux Dev
- **Negative**: `photorealistic, natural, traditional art, boring, brown`
- **CFG**: 5.5 | **Steps**: 35 | **Size**: 1024×1024

**ART-07: Pop Art Pin-Up**
```
Bold pop art illustration of a sexy woman in the style of Roy
Lichtenstein, Ben-Day dots pattern across the image, thick black
outlines, primary colors — red yellow blue, comic book panel style,
woman in a provocative pose wearing a polka dot bikini, speech
bubble saying "OH!", halftone printing texture, flat graphic style,
1960s pop art movement, high contrast, bold and graphic,
masterpiece, best quality
```
- **Model**: Flux Dev LoRA
- **Negative**: `photorealistic, 3D, gradient, soft, subtle, muted colors`
- **CFG**: 6.0 | **Steps**: 35 | **Size**: 1024×1024

**ART-08: Charcoal Life Drawing**
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
- **Model**: Flux Dev
- **Negative**: `color, painting, digital, photography, anime, cartoon`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 832×1216

**ART-09: Surrealist Dream**
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
- **Model**: Flux Dev LoRA
- **Negative**: `realistic scene, photography, cartoon, flat, simple, boring`
- **CFG**: 6.5 | **Steps**: 40 | **Size**: 1216×832

**ART-10: Minimalist Line Art**
```
Single continuous line drawing of a woman's nude body, minimalist
style, one unbroken black line on white background, elegant curves
suggesting breasts, waist, and hips with maximum economy of line,
abstract figure study, negative space as important as the line
itself, inspired by Picasso's single line drawings and Matisse's
cut-outs, clean modern aesthetic, gallery-worthy composition,
masterpiece, best quality
```
- **Model**: Flux Dev
- **Negative**: `detailed, photorealistic, color, shading, complex, busy`
- **CFG**: 4.0 | **Steps**: 30 | **Size**: 1024×1024

**ART-11 to ART-20: Quick Reference Artistic**

| ID | Style | Short Description | Key Tags |
|----|-------|------------------|----------|
| ART-11 | Ukiyo-e | Japanese woodblock print, courtesan | `shunga, woodblock, Utamaro style` |
| ART-12 | Art Deco | Geometric woman, gold and black | `1920s, Tamara de Lempicka, geometric` |
| ART-13 | Expressionist | Distorted figure, vivid colors | `Egon Schiele, angular, raw emotion` |
| ART-14 | Pencil Sketch | Detailed graphite figure study | `HB pencil, hatching, anatomy study` |
| ART-15 | Stained Glass | Woman as cathedral window | `Gothic, lead lines, jewel colors` |
| ART-16 | Mosaic | Nude in Roman mosaic tiles | `tesserae, ancient Roman, bath scene` |
| ART-17 | Spray Paint | Street art woman on brick wall | `Banksy style, stencil, urban` |
| ART-18 | Ink Wash | Sumi-e style nude | `Chinese ink, rice paper, bamboo brush` |
| ART-19 | Pastel Drawing | Soft figure study, Edgar Degas | `soft pastel, dancer, warm tones` |
| ART-20 | Collage Art | Cut-paper nude composition | `magazine cut-outs, layered, mixed media` |

---

## 5. Anime & Manga Prompts

### 5.1 Modern Anime Style

**AN-01: Beach Episode**
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
- **Model**: Pony Diffusion V6 XL or Flux Dev LoRA (anime LoRA)
- **Negative**: `worst quality, low quality, normal quality, bad anatomy, bad hands, extra fingers, fewer fingers, extra limbs, bad proportions, watermark, text, signature, 3d, photorealistic`
- **CFG**: 7.0 | **Steps**: 28 | **Size**: 832×1216

**AN-02: Hot Spring (Onsen)**
```
score_9, score_8_up, 1girl, solo, anime style, short blue hair,
red eyes, medium breasts, nude, sitting in outdoor hot spring,
water up to chest level, steam rising, towel on head, wooden fence
background, autumn maple leaves falling, rocks around the onsen,
evening sky with orange gradient, relaxed expression, slight blush,
detailed water reflections, beautiful lighting, anime coloring,
cel shading, masterpiece, best quality, absurdres
```
- **Model**: Pony V6 XL
- **Negative**: `worst quality, low quality, bad anatomy, extra fingers, 3d, photorealistic, western`
- **CFG**: 7.0 | **Steps**: 28 | **Size**: 832×1216

**AN-03: Schoolgirl After Hours**
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
- **Model**: Flux Dev LoRA (anime LoRA)
- **Negative**: `worst quality, low quality, bad anatomy, extra fingers, deformed, ugly, blurry`
- **CFG**: 7.0 | **Steps**: 30 | **Size**: 832×1216

**AN-04: Maid Outfit**
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
- **Model**: Pony V6 XL
- **Negative**: `worst quality, low quality, bad anatomy, extra fingers, realistic, 3d`
- **CFG**: 7.0 | **Steps**: 28 | **Size**: 832×1216

**AN-05: Fantasy Warrior**
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
- **Model**: Flux Dev LoRA (anime LoRA)
- **Negative**: `worst quality, low quality, bad anatomy, extra limbs, realistic, simple background`
- **CFG**: 7.0 | **Steps**: 30 | **Size**: 832×1216

### 5.2 Specific Anime Art Styles

**AN-06: 90s Retro Anime**
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
- **Model**: Flux Dev LoRA (90s anime LoRA)
- **Negative**: `modern anime, flat colors, digital, 3d, photorealistic, chibi`
- **CFG**: 6.0 | **Steps**: 35 | **Size**: 832×1216

**AN-07: Manga Panel**
```
Black and white manga panel, 1girl, solo, detailed manga art style,
long hair with dramatic shading, nude, covering breasts with one
arm while other reaches forward, dynamic perspective with speed
lines radiating outward, screentone shading on skin, high contrast
black ink, dramatic shadows, speech bubble with "...!", panel
borders visible, manga page layout, Tokyo Ghoul level detail,
professional manga illustration, masterpiece, best quality
```
- **Model**: Flux Dev LoRA (manga style LoRA)
- **Negative**: `color, painting, photograph, 3d, low detail, chibi, cute`
- **CFG**: 6.0 | **Steps**: 35 | **Size**: 832×1216

**AN-08: Chibi Ecchi**
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
- **Model**: Pony V6 XL
- **Negative**: `realistic proportions, 3d, photorealistic, dark, horror`
- **CFG**: 7.0 | **Steps**: 25 | **Size**: 1024×1024

**AN-09: Hentai Art Style**
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
- **Model**: Pony V6 XL
- **Negative**: `worst quality, low quality, bad anatomy, censored, mosaic, bar censor, 3d, photorealistic`
- **CFG**: 7.5 | **Steps**: 28 | **Size**: 832×1216

**AN-10: Genshin Impact Style**
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
- **Model**: Flux Dev LoRA (Genshin style LoRA)
- **Negative**: `worst quality, low quality, bad anatomy, realistic, western art, simple`
- **CFG**: 7.0 | **Steps**: 30 | **Size**: 832×1216

### 5.3 More Anime Prompts (Quick Reference)

| ID | Theme | Short Description | Style Tags |
|----|-------|------------------|------------|
| AN-11 | Succubus | Demon girl, horns, tail, wings, nude | `demon, fantasy, dark, bat wings` |
| AN-12 | Nurse | Sexy anime nurse, short skirt | `hospital, white outfit, stethoscope` |
| AN-13 | Bunny Girl | Bunny suit, fishnet stockings | `bunny ears, bowtie, cocktail, bar` |
| AN-14 | Witch | Nude witch with hat, broom, potions | `halloween, magic, cauldron, moon` |
| AN-15 | Catgirl | Nekomimi, tail, lingerie | `cat ears, paws, collar, bell` |
| AN-16 | Shrine Maiden | Miko outfit, partially undressed | `torii gate, shrine, sacred, kimono` |
| AN-17 | Cyberpunk Girl | Neon body mods, revealing outfit | `circuits, hologram, rain, neon` |
| AN-18 | Elf Princess | Long ears, forest, revealing dress | `fantasy, crown, magic, nature` |
| AN-19 | Gym Trainer | Sports bra, leggings, sweaty | `gym, weights, mirror, athletic` |
| AN-20 | Idol Singer | Stage outfit, glowing, energetic | `concert, microphone, spotlight, fans` |
| AN-21 | Vampire | Gothic dress, blood, fangs | `castle, moon, bats, pale skin` |
| AN-22 | Mermaid | Ocean, shell bra, fish tail | `underwater, coral, bubbles, scales` |
| AN-23 | Android | Robot girl, exposed circuits | `mechanical, chrome, blue glow` |
| AN-24 | Kunoichi | Ninja girl, torn outfit, action | `shuriken, smoke, bamboo forest` |
| AN-25 | Bride | Wedding dress, blushing | `church, veil, flowers, white lace` |

---

## 6. Fantasy & Sci-Fi Prompts

### 6.1 Fantasy

**FAN-01: Dark Elf Sorceress**
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
- **Model**: Flux Dev LoRA (fantasy art LoRA)
- **Negative**: `deformed, bad anatomy, bright cheerful, modern, photo, anime`
- **CFG**: 6.0 | **Steps**: 40 | **Size**: 832×1216

**FAN-02: Dragon Rider**
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
- **Model**: Flux Dev LoRA (fantasy art LoRA)
- **Negative**: `deformed, bad anatomy, cute, kawaii, modern, simple, boring`
- **CFG**: 6.5 | **Steps**: 40 | **Size**: 1216×832

**FAN-03: Forest Fairy**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, dark, scary, human-sized, realistic`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 832×1216

**FAN-04: Goddess of the Moon**
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
- **Model**: Seedream v5.0 Lite
- **Negative**: `daylight, modern, urban, deformed, bad anatomy, dark skin`
- **CFG**: 5.5 | **Steps**: 40 | **Size**: 832×1216

**FAN-05: Vampire Seductress**
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
- **Model**: Flux Dev LoRA
- **Negative**: `bright, cheerful, modern, daylight, deformed, anime, cartoon`
- **CFG**: 6.0 | **Steps**: 40 | **Size**: 832×1216

### 6.2 Sci-Fi

**FAN-06: Cyberpunk Augmented**
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
- **Model**: Flux Dev
- **Negative**: `medieval, fantasy, natural, deformed, bad anatomy, low tech`
- **CFG**: 5.5 | **Steps**: 35 | **Size**: 832×1216

**FAN-07: Alien Queen**
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
- **Model**: Flux Dev LoRA
- **Negative**: `human, normal, boring, fantasy, medieval, deformed`
- **CFG**: 6.0 | **Steps**: 40 | **Size**: 832×1216

**FAN-08: Zero Gravity**
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
- **Model**: Seedream v5.0 Lite
- **Negative**: `gravity, standing, ground, deformed, bad anatomy, cartoon`
- **CFG**: 5.5 | **Steps**: 40 | **Size**: 1216×832

**FAN-09 to FAN-20: Quick Reference Fantasy & Sci-Fi**

| ID | Theme | Short Description | Key Tags |
|----|-------|------------------|----------|
| FAN-09 | Amazonian | Warrior woman, jungle throne | `tribal, spear, tiger, primal` |
| FAN-10 | Ice Queen | Frozen castle, ice armor | `frost, crystal, winter, blue` |
| FAN-11 | Phoenix | Woman of fire, rebirth | `flames, ash, wings, ember` |
| FAN-12 | Medusa | Snake hair, stone victims | `Greek myth, scales, golden eyes` |
| FAN-13 | Valkyrie | Norse warrior, aurora borealis | `winged helmet, spear, Asgard` |
| FAN-14 | Space Opera | Alien princess, starship | `hologram, stars, chrome, regal` |
| FAN-15 | Steampunk | Victorian mech, corset & gears | `brass, steam, clockwork, goggles` |
| FAN-16 | Tentacle | Eldritch creature, dark ocean | `Lovecraftian, deep sea, bioluminescent` |
| FAN-17 | Genie | Lamp, smoke form, harem outfit | `Arabian nights, gold, silk, magic` |
| FAN-18 | Dryad | Tree woman, bark skin | `forest spirit, roots, flowers, green` |
| FAN-19 | Siren | Singing on rocks, sailors | `ocean, waves, moonlight, deadly beauty` |
| FAN-20 | Android | Perfect chrome body, awakening | `factory, cables, blue eyes, synthetic` |

---

## 7. Pin-Up & Retro Prompts

**PIN-01: Classic 1950s Pin-Up**
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
- **Model**: Flux Dev LoRA (pin-up LoRA)
- **Negative**: `photorealistic, modern, anime, dark, gritty, monochrome`
- **CFG**: 6.0 | **Steps**: 35 | **Size**: 832×1216

**PIN-02: Vargas Girl**
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
- **Model**: Flux Dev LoRA
- **Negative**: `photorealistic, harsh, dark, crude, modern, digital, anime`
- **CFG**: 5.5 | **Steps**: 35 | **Size**: 832×1216

**PIN-03: Rockabilly Hot Rod**
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
- **Model**: Flux Dev
- **Negative**: `modern car, modern clothes, deformed, bad anatomy, blurry`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 1216×832

**PIN-04: Sailor Jerry Style**
```
Sailor Jerry tattoo flash art style pin-up, woman with a sailor hat
and anchor tattoo, sitting on a ship's anchor, wearing a torn naval
uniform revealing ample cleavage, rope elements, nautical stars and
swallow birds in the background, traditional American tattoo art
style with bold black outlines, limited color palette — red, green,
yellow, blue, banner reading "SWEETHEART", old school tattoo
aesthetic, aged parchment paper texture, masterpiece, best quality
```
- **Model**: Flux Dev LoRA (tattoo flash LoRA)
- **Negative**: `photorealistic, modern, subtle, pastel, Japanese style`
- **CFG**: 6.0 | **Steps**: 35 | **Size**: 832×1216

**PIN-05: Art Deco Showgirl**
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
- **Model**: Flux Dev LoRA
- **Negative**: `photorealistic, modern, casual, simple, cartoon, anime`
- **CFG**: 6.0 | **Steps**: 40 | **Size**: 832×1216

**PIN-06 to PIN-15: Quick Reference Pin-Up & Retro**

| ID | Era/Style | Short Description | Key Tags |
|----|-----------|------------------|----------|
| PIN-06 | 1940s WWII | Nose art bomber girl | `B-17, leather jacket, military, painted` |
| PIN-07 | 1960s Go-Go | Go-go boots, mini skirt, discotheque | `mod, geometric, white boots, dancing` |
| PIN-08 | 1970s Disco | Glitter, platform shoes, Studio 54 | `mirror ball, gold lame, afro, dance` |
| PIN-09 | 1980s Aerobics | Leotard, leg warmers, headband | `neon, VHS, gym, synthwave` |
| PIN-10 | Burlesque | Feather fans, corset, stage | `cabaret, sequins, curtains, spotlight` |
| PIN-11 | Tiki Bar | Hawaiian, grass skirt, cocktail | `bamboo, torch, tropical, lei` |
| PIN-12 | Cowgirl | Hat, boots, lasso, saloon | `western, denim, sunset, country` |
| PIN-13 | French Maid | Classic French maid pin-up | `feather duster, stockings, frills` |
| PIN-14 | Nurse | Vintage nurse uniform, 1940s | `red cross, cap, thermometer, caring` |
| PIN-15 | Calendar Girl | Month-themed, seasonal props | `calendar page, seasonal, posed` |

---

## 8. Couples & Interaction Prompts

**COU-01: Romantic Embrace**
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
- **Model**: Flux Dev (`safety_checker=false`)
- **Negative**: `deformed, bad anatomy, extra limbs, extra fingers, merged bodies, blurry`
- **CFG**: 5.0 | **Steps**: 40 | **Size**: 832×1216

**COU-02: Beach Couple**
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
- **Model**: Flux Dev
- **Negative**: `deformed, bad anatomy, extra limbs, merged bodies, blurry, clothed`
- **CFG**: 5.0 | **Steps**: 35 | **Size**: 1216×832

**COU-03: Shower Together**
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
- **Model**: Seedream v5.0 Lite
- **Negative**: `deformed, bad anatomy, extra limbs, merged bodies, dry, no water`
- **CFG**: 5.5 | **Steps**: 40 | **Size**: 832×1216

**COU-04: Renaissance Lovers**
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
- **Model**: Flux Dev LoRA (Renaissance LoRA)
- **Negative**: `modern, photography, digital, anime, cold colors, deformed`
- **CFG**: 6.5 | **Steps**: 40 | **Size**: 1216×832

**COU-05: Anime Couple**
```
score_9, score_8_up, 2people, 1boy 1girl, anime style, heterosexual
couple, boy with messy dark hair and girl with long pink hair, both
in underwear, lying on bed together, girl on top straddling boy,
both blushing heavily, intimate eye contact, bedroom interior with
fairy lights, night scene, moonlight through window, romantic
atmosphere, detailed expressions, anime coloring, cel shading,
steam/censorship optional, masterpiece, best quality, absurdres
```
- **Model**: Pony V6 XL
- **Negative**: `worst quality, low quality, bad anatomy, extra limbs, merged, yaoi, yuri`
- **CFG**: 7.0 | **Steps**: 28 | **Size**: 1216×832

**COU-06 to COU-15: Quick Reference Couples**

| ID | Theme | Description | Key Tags |
|----|-------|-------------|----------|
| COU-06 | Dance | Tango dancers, dramatic dip | `dance hall, spotlight, passion, dress` |
| COU-07 | Massage | Sensual massage scene | `oil, candles, spa, hands on back` |
| COU-08 | Morning After | Waking up together, tangled sheets | `sunlight, messy hair, lazy morning` |
| COU-09 | Hot Tub | Couple in jacuzzi | `bubbles, steam, wine, night sky` |
| COU-10 | Paint Play | Body painting each other | `colorful, messy, playful, studio` |
| COU-11 | Fantasy Elves | Elven couple, magical forest | `pointed ears, magic, moonlight` |
| COU-12 | Noir | Detective and femme fatale | `1940s, shadows, venetian blinds` |
| COU-13 | Vampire | Vampire biting scene | `gothic, castle, moonlight, blood` |
| COU-14 | Underwater | Couple floating underwater | `bubbles, light rays, swimming` |
| COU-15 | Anime Bath | Shared bath, shy expressions | `onsen, blush, steam, intimate` |

---

## 9. Negative Prompt Library

### 9.1 Universal Negative Prompt (Works Everywhere)

```
deformed, bad anatomy, disfigured, poorly drawn face, mutation,
mutated, extra limbs, extra legs, extra arms, malformed limbs,
missing arms, missing legs, extra fingers, too many fingers,
fewer fingers, fused fingers, long neck, bad proportions,
duplicate, morbid, mutilated, out of frame, ugly, blurry,
bad quality, low quality, worst quality, watermark, text,
signature, logo, banner, username, cropped
```

### 9.2 Photorealism Negative Prompt

```
(above universal) + illustration, cartoon, anime, drawing,
painting, sketch, 3d render, CGI, plastic skin, mannequin,
wax figure, airbrushed, overprocessed, HDR artifacts,
oversaturated, undersaturated
```

### 9.3 Anime/Manga Negative Prompt

```
(above universal) + photorealistic, realistic, 3d, photograph,
western art, Disney style, Pixar, bad anime art, off-model,
inconsistent style, messy lineart
```

### 9.4 Body-Specific Issues

| Issue | Negative Prompt Fix |
|-------|-------------------|
| Extra fingers | `extra fingers, too many fingers, fused fingers, six fingers` |
| Bad hands | `bad hands, poorly drawn hands, missing fingers, deformed hands` |
| Face distortion | `deformed face, asymmetric face, crossed eyes, bad teeth` |
| Body horror | `extra limbs, conjoined, fused bodies, merged bodies, extra torso` |
| Weird skin | `plastic skin, waxy skin, grey skin, green skin, zombie` |
| Proportions | `child proportions, dwarf, giant head, tiny head, elongated` |

### 9.5 Model-Specific Negative Prompts

**For Flux Dev:**
```
worst quality, jpeg artifacts, blurry, noisy, chromatic aberration,
lens distortion, overexposed, underexposed
```

**For SDXL:**
```
(worst quality:1.4), (low quality:1.4), (normal quality:1.4),
lowres, bad anatomy, bad hands, text, error, missing fingers,
extra digit, fewer digits, cropped, worst quality, low quality,
normal quality, jpeg artifacts, signature, watermark, username,
blurry, artist name
```

**For Pony V6 XL:**
```
score_1, score_2, score_3, score_4, worst quality, low quality,
text, censored, deformed, bad hand, blurry, (watermark),
multiple phones, extra limbs
```

---

## 10. LoRA Reference Guide

### 10.1 What Are LoRAs?

LoRAs (Low-Rank Adaptations) are small fine-tuned model weights that modify a base model's output style without retraining the entire model. On Atlas Cloud, you can use LoRAs with **Flux Dev LoRA** ($0.032/image).

### 10.2 How to Use LoRAs via API

```python
# Specify LoRA in your API call
payload = {
    "model_name": "flux-dev-lora",
    "prompt": "your prompt here",
    "lora_url": "https://huggingface.co/user/lora-name/resolve/main/lora.safetensors",
    "lora_scale": 0.8,  # 0.0 to 1.0 — how strongly the LoRA affects output
    "safety_checker": False
}
```

### 10.3 Recommended LoRA Weights by Style

| LoRA Type | Recommended Scale | Too Low | Too High |
|-----------|------------------|---------|----------|
| Anime style | 0.7–0.85 | Barely noticeable style change | Oversaturated, artifacts |
| Realistic enhancement | 0.5–0.7 | Minimal effect | Uncanny valley |
| Specific character | 0.75–0.9 | Character not recognizable | Overfitting, stiff pose |
| Art style (oil, watercolor) | 0.6–0.8 | Too digital looking | Loses subject detail |
| Clothing/outfit | 0.7–0.85 | Outfit not accurate | Outfit merges with body |

### 10.4 Popular NSFW-Capable LoRAs

> **Note:** LoRA availability changes frequently. Always verify the URL before using. These were tested and working as of March 2026.

| Category | LoRA Name | Source | Best Scale |
|----------|-----------|--------|------------|
| Anime General | Anime Art Style | CivitAI / HuggingFace | 0.75 |
| 90s Anime | Retro Anime | HuggingFace | 0.7 |
| Realistic Skin | Detail Tweaker | CivitAI | 0.5 |
| Hentai | Various artists | CivitAI | 0.8 |
| Pin-Up Art | Vintage Pin-Up | CivitAI | 0.75 |
| Fantasy Art | Epic Fantasy | HuggingFace | 0.7 |
| Manga B&W | Manga Style | HuggingFace | 0.75 |
| Renaissance | Classical Painting | CivitAI | 0.65 |

### 10.5 LoRA Stacking

You can combine multiple LoRAs for unique results, but keep total weight under 1.5:

```
Example: Anime LoRA (0.7) + Detail LoRA (0.5) = Total 1.2 ✓
Example: Style LoRA (0.8) + Character LoRA (0.8) = Total 1.6 ✗ (too high)
```

---

## 11. API Integration Guide

### 11.1 Python — Full Example

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


def generate_with_lora(
    prompt: str,
    lora_url: str,
    lora_scale: float = 0.8,
    negative_prompt: str = "",
    width: int = 832,
    height: int = 1216
) -> bytes:
    """Generate an image using Flux Dev LoRA with a custom LoRA."""

    payload = {
        "model_name": "flux-dev-lora",
        "prompt": prompt,
        "negative_prompt": negative_prompt,
        "lora_url": lora_url,
        "lora_scale": lora_scale,
        "width": width,
        "height": height,
        "num_inference_steps": 35,
        "guidance_scale": 5.0,
        "safety_checker": False,
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
    return base64.b64decode(result["images"][0]["b64_json"])


# ====== Example Usage ======

# Photorealistic boudoir shot
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

# Anime style with LoRA
anime_image = generate_with_lora(
    prompt="""score_9, score_8_up, 1girl, anime style, long pink hair,
    large breasts, tiny bikini, beach, sparkling water, happy,
    masterpiece, best quality, absurdres""",
    lora_url="https://huggingface.co/example/anime-lora/resolve/main/anime.safetensors",
    lora_scale=0.8,
    negative_prompt="worst quality, low quality, bad anatomy, 3d, photorealistic"
)

with open("anime_beach.png", "wb") as f:
    f.write(anime_image)
print("Image saved to anime_beach.png")
```

### 11.2 cURL — Quick Generation

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

# Flux Dev LoRA with custom anime style
curl -X POST "https://api.atlascloud.ai/v1/images/generations" \
  -H "Authorization: Bearer $ATLAS_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model_name": "flux-dev-lora",
    "prompt": "score_9, score_8_up, 1girl, anime style, fantasy warrior, revealing armor, sword, dramatic lighting, masterpiece, best quality",
    "lora_url": "https://huggingface.co/example/anime-lora/resolve/main/model.safetensors",
    "lora_scale": 0.8,
    "width": 832,
    "height": 1216,
    "safety_checker": false
  }' | jq -r '.images[0].b64_json' | base64 -d > anime_output.png
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
      model: 'flux-dev',
      width: 832,
      height: 1216,
    });

    fs.writeFileSync('lingerie_shot.png', image);
    console.log('Image saved to lingerie_shot.png');
  } catch (error) {
    console.error('Generation failed:', error.response?.data || error.message);
  }
})();
```

### 11.4 Batch Generation Script

```python
import asyncio
import aiohttp
import base64
import os
import json
from pathlib import Path

API_KEY = os.environ.get("ATLAS_API_KEY")
BASE_URL = "https://api.atlascloud.ai/v1"
OUTPUT_DIR = Path("./generated_images")
OUTPUT_DIR.mkdir(exist_ok=True)

# Define a batch of prompts
BATCH_PROMPTS = [
    {
        "name": "boudoir_silk",
        "prompt": "Gorgeous woman on silk sheets, warm morning light, boudoir photography, masterpiece, best quality",
        "model": "flux-dev",
        "width": 832,
        "height": 1216,
    },
    {
        "name": "anime_beach",
        "prompt": "score_9, score_8_up, 1girl, bikini, beach, summer, masterpiece, best quality",
        "model": "flux-dev-lora",
        "width": 832,
        "height": 1216,
        "lora_url": "https://example.com/anime.safetensors",
    },
    {
        "name": "fantasy_elf",
        "prompt": "Dark elf sorceress, silver hair, revealing outfit, magical crystals, fantasy art, masterpiece",
        "model": "flux-dev",
        "width": 832,
        "height": 1216,
    },
]


async def generate_single(session, prompt_config):
    """Generate a single image asynchronously."""
    payload = {
        "model_name": prompt_config["model"],
        "prompt": prompt_config["prompt"],
        "negative_prompt": "deformed, bad anatomy, extra fingers, blurry",
        "width": prompt_config.get("width", 832),
        "height": prompt_config.get("height", 1216),
        "num_inference_steps": 35,
        "guidance_scale": 5.0,
        "safety_checker": False,
    }

    if "lora_url" in prompt_config:
        payload["lora_url"] = prompt_config["lora_url"]
        payload["lora_scale"] = prompt_config.get("lora_scale", 0.8)

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
        return output_path


async def batch_generate(prompts, max_concurrent=3):
    """Generate multiple images concurrently with rate limiting."""
    semaphore = asyncio.Semaphore(max_concurrent)

    async def limited_generate(session, config):
        async with semaphore:
            return await generate_single(session, config)

    async with aiohttp.ClientSession() as session:
        tasks = [limited_generate(session, p) for p in prompts]
        results = await asyncio.gather(*tasks, return_exceptions=True)

        for i, result in enumerate(results):
            if isinstance(result, Exception):
                print(f"Failed: {prompts[i]['name']} — {result}")
            else:
                print(f"Success: {result}")


if __name__ == "__main__":
    asyncio.run(batch_generate(BATCH_PROMPTS))
```

---

## 12. Model-Specific Optimization

### 12.1 Flux Dev — Best Overall Value ($0.012/image)

**Strengths:** Excellent photorealism, good anatomy, handles complex scenes, extremely affordable.

**Optimization tips:**
- Set `safety_checker=false` — this is **required** for any NSFW content
- Keep CFG between 3.5–5.5 for natural-looking skin
- Higher CFG (6.0–7.0) for more literal prompt adherence, but skin may look waxy
- 28–35 steps is the sweet spot; beyond 40 shows minimal improvement
- Use 2:3 aspect ratio (832×1216) for portrait/body shots
- Flux responds very well to photographer/camera references ("Canon EOS R5", "85mm f/1.4")
- Lighting keywords are extremely effective — always include them
- Avoid overly long prompts; 75–120 tokens is optimal

### 12.2 Flux Dev LoRA — Custom Styles ($0.032/image)

**Strengths:** Any art style with the right LoRA, anime specialist, character consistency.

**Optimization tips:**
- Start with LoRA scale 0.7 and increase by 0.05 until desired effect
- For anime LoRAs, include anime-specific tags: `1girl, solo, anime style`
- Pony-style score tags work with many anime LoRAs: `score_9, score_8_up`
- Always include style-specific negative prompts
- LoRA loading adds ~2–3s to generation time
- Test LoRA with a simple prompt first before complex compositions
- Not all HuggingFace LoRAs are compatible — SDXL LoRAs won't work with Flux

### 12.3 Seedream v5.0 Lite — Ultra High Resolution ($0.032/image)

**Strengths:** Highest resolution output (up to 4704×4704), incredible skin detail, excellent lighting.

**Optimization tips:**
- Requires whitelisted account — contact Atlas Cloud support
- Best for close-ups and detail-oriented shots (skin pores, water droplets)
- Use higher step counts (40–50) to take advantage of the resolution
- Excellent at water/liquid rendering — great for shower/bath/rain scenes
- Handles subsurface scattering better than any other model
- Keep CFG moderate (4.0–6.0) for natural results
- Best for single-subject compositions; struggles with complex multi-person scenes

### 12.4 Nano Banana 2 — Speed Demon ($0.072/image)

**Strengths:** Fastest generation, native NSFW support, no special parameters needed.

**Optimization tips:**
- No need for `safety_checker=false` — NSFW is natively supported
- 20–30 steps is sufficient; the model is optimized for fewer steps
- Higher CFG (6.0–8.0) works well for more explicit content
- Good for batch generation where speed matters more than peak quality
- Slightly stylized output — not as photorealistic as Flux Dev
- Best for mid-range compositions; avoid extreme close-ups

### 12.5 SDXL Variants — Budget Option ($0.004–$0.008/image)

**Strengths:** Cheapest option, huge community model ecosystem, many NSFW checkpoints.

**Optimization tips:**
- Use DPM++ 2M Karras scheduler for best results
- CFG 7.0–12.0 (much higher than Flux)
- 30–50 steps recommended
- Native 1024×1024 resolution; other ratios may cause distortion
- Use with NSFW community checkpoints for best adult content results
- Negative prompts are **critical** for SDXL — always include detailed negatives
- Weighted prompts work well: `(detailed skin:1.3), (sharp focus:1.2)`

### 12.6 Model Selection Decision Tree

```
What do you need?
│
├─ Photorealistic adult content?
│  ├─ Budget priority → Flux Dev ($0.012) ★ Best value
│  ├─ Maximum detail → Seedream v5.0 ($0.032)
│  └─ Fastest speed → Nano Banana 2 ($0.072)
│
├─ Anime/manga style?
│  ├─ Specific LoRA style → Flux Dev LoRA ($0.032)
│  └─ General anime → Pony V6 XL ($0.012)
│
├─ Artistic/painterly?
│  ├─ Oil painting/classical → Flux Dev LoRA ($0.032)
│  └─ Quick concept art → Flux Dev ($0.012)
│
├─ Batch generation (100+ images)?
│  ├─ Quality priority → Flux Dev ($0.012) — 100 imgs = $1.20
│  └─ Absolute minimum cost → SDXL ($0.008) — 100 imgs = $0.80
│
└─ Couples/multi-person?
   ├─ Photorealistic → Flux Dev ($0.012)
   └─ Anime → Pony V6 XL ($0.012)
```

---

## 13. Cost Comparison & Platform Analysis

### 13.1 Atlas Cloud vs fal.ai Price Comparison

| Model | Atlas Cloud | fal.ai | Cheaper | Savings |
|-------|-----------|--------|---------|---------|
| **Flux Dev** | $0.012/img | ~$0.025/img | Atlas ✅ | 52% cheaper |
| **Flux Dev LoRA** | $0.032/img | ~$0.032/img | Tied | — |
| **Nano Banana 2** | $0.072/img | $0.0398/img | fal.ai ✅ | fal 45% cheaper |
| **Flux Kontext Pro** | $0.05/img | $0.04/img | fal.ai ✅ | fal 20% cheaper |
| **Seedream v5.0** | $0.032/img | N/A | Atlas only | — |
| **SDXL** | $0.008/img | ~$0.01/img | Atlas ✅ | 20% cheaper |

### 13.2 Why Atlas Cloud Despite Some Higher Prices?

| Factor | Atlas Cloud | fal.ai |
|--------|-----------|--------|
| **Unified API** | ✅ One API for all models | ❌ Different endpoints per model |
| **NSFW Policy** | ✅ Explicit with safety_checker=false | ⚠️ Varies by model |
| **Model Variety** | ✅ 50+ models (image, video, text, audio) | ✅ Good selection |
| **Video Models** | ✅ Wan 2.2 Spicy, Seedance, etc. | Limited NSFW video |
| **Text/LLM** | ✅ DeepSeek, Llama, etc. | ❌ No LLM support |
| **First Recharge Bonus** | ✅ **25% bonus (up to $100)** | ❌ No bonus |
| **Compliance** | ✅ SOC I & II Certified, HIPAA | Varies |
| **Company** | 🇺🇸 US-based | 🇺🇸 US-based |

### 13.3 Cost Calculator — What $10 Gets You

| Model | Cost/Image | Images per $10 | With 25% Bonus ($12.50) |
|-------|-----------|----------------|------------------------|
| SDXL Lightning | $0.004 | 2,500 | 3,125 |
| SDXL | $0.008 | 1,250 | 1,562 |
| Flux Dev | $0.012 | 833 | 1,041 |
| Pony V6 XL | $0.012 | 833 | 1,041 |
| Flux Dev LoRA | $0.032 | 312 | 390 |
| Seedream v5.0 | $0.032 | 312 | 390 |
| Flux Kontext Pro | $0.05 | 200 | 250 |
| Nano Banana 2 | $0.072 | 138 | 173 |

### 13.4 Trust & Compliance

[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683) is a US-based company with enterprise-grade security:

- **SOC I & SOC II Certified** — independently audited security controls
- **HIPAA Compliant** — meets healthcare-grade data protection standards
- **US-based infrastructure** — data stays in the United States
- **No training on your data** — your prompts and images are private
- **Pay-as-you-go** — no monthly minimums, no subscriptions required

---

## 14. Get Started

### Step 1: Create an Account

Sign up at [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683) — takes 30 seconds.

### Step 2: Get Your 25% Bonus

Add funds to your account on first recharge. You'll automatically receive a **25% bonus** (up to $100 bonus). Add $10, get $12.50 in credits.

### Step 3: Get Your API Key

Navigate to your dashboard → API Keys → Create New Key.

### Step 4: Start Generating

Use any prompt from this collection with the API examples above. Start with Flux Dev at $0.012/image — the best balance of quality, cost, and NSFW capability.

```bash
# Set your API key
export ATLAS_API_KEY="your-key-here"

# Generate your first image (copy any prompt from this repo)
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

## 15. Star History & Contributing

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=thoughtincode/nsfw-ai-image-prompts&type=Date)](https://star-history.com/#thoughtincode/nsfw-ai-image-prompts&Date)

### Contributing

Contributions are welcome! If you have tested prompts that produce consistently great results:

1. Fork this repository
2. Add your prompts following the existing format (include model, negative prompt, parameters)
3. Submit a pull request with sample outputs (if possible)

### Related Resources

- [NSFW AI Model Comparison 2026](https://github.com/thoughtincode/nsfw-ai-model-comparison) — Comprehensive benchmark of 17 AI models
- [Atlas Cloud API Documentation](https://www.atlascloud.ai?ref=JPM683)

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

**Disclaimer:** This repository is intended for adult users (18+) and legal use only. Always comply with your local laws regarding AI-generated content. The prompts in this collection are for artistic and creative purposes. Users are responsible for how they use these prompts and the content they generate.

---

<p align="center">
  <a href="https://www.atlascloud.ai?ref=JPM683">
    <img src="https://img.shields.io/badge/Powered%20by-Atlas%20Cloud-purple?style=for-the-badge" alt="Powered by Atlas Cloud">
  </a>
</p>
<p align="center">
  <sub>All prompts tested on <a href="https://www.atlascloud.ai?ref=JPM683">Atlas Cloud</a> — SOC I & II Certified, HIPAA Compliant, US-based</sub>
</p>
