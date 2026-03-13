# 🎨 NSFW AI 이미지 프롬프트 — 120+ 실전용 성인 AI 아트 프롬프트

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Prompts](https://img.shields.io/badge/프롬프트-120+-blue)]()
[![Last Updated](https://img.shields.io/badge/최종%20업데이트-2026년%203월-green)]()
[![Platform](https://img.shields.io/badge/플랫폼-Atlas%20Cloud-purple)](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)
[![SOC Certified](https://img.shields.io/badge/SOC%20I%20%26%20II-인증-brightgreen)]()
[![HIPAA](https://img.shields.io/badge/HIPAA-준수-brightgreen)]()

> **엄선된 120개 이상의 실전 테스트 완료 NSFW AI 이미지 프롬프트 모음. 모델별 최적화, 네거티브 프롬프트, LoRA 추천, API 코드 예제 포함. 모든 프롬프트는 [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)에서 실제 테스트 완료.**

[English](./README.md) | [中文版](./README_zh-CN.md) | [日本語](./README_ja.md)

---

## 목차

- [이 저장소를 만든 이유](#이-저장소를-만든-이유)
- [1. 모델 빠른 참조](#1-모델-빠른-참조)
- [2. 프롬프트 엔지니어링 기초](#2-프롬프트-엔지니어링-기초)
- [3. 포토리얼리스틱 프롬프트 (30개)](#3-포토리얼리스틱-프롬프트-30개)
- [4. 아트/파인아트 프롬프트 (20개)](#4-아트파인아트-프롬프트-20개)
- [5. 애니메/만화 프롬프트 (25개)](#5-애니메만화-프롬프트-25개)
- [6. 판타지/SF 프롬프트 (20개)](#6-판타지sf-프롬프트-20개)
- [7. 핀업/레트로 프롬프트 (15개)](#7-핀업레트로-프롬프트-15개)
- [8. 커플/인터랙션 프롬프트 (15개)](#8-커플인터랙션-프롬프트-15개)
- [9. 네거티브 프롬프트 라이브러리](#9-네거티브-프롬프트-라이브러리)
- [10. LoRA 레퍼런스 가이드](#10-lora-레퍼런스-가이드)
- [11. API 통합 가이드](#11-api-통합-가이드)
- [12. 모델별 최적화 기법](#12-모델별-최적화-기법)
- [13. 비용 비교 및 플랫폼 분석](#13-비용-비교-및-플랫폼-분석)
- [14. 시작하기](#14-시작하기)
- [15. Star History & 기여](#15-star-history--기여)

---

## 이 저장소를 만든 이유

온라인의 대부분의 "프롬프트 모음"은:
1. 너무 모호함 ("아름다운 여성, 고화질")
2. 유료 콘텐츠 벽 뒤에 있음
3. 핵심 매개변수가 빠져있음 (네거티브 프롬프트, LoRA 가중치, CFG 스케일)
4. 실제 모델에서 테스트하지 않았음

이 저장소는 정확한 매개변수가 포함된 **바로 사용 가능한 프롬프트**를 제공합니다. 모든 프롬프트는 여러 모델에서 5회 이상 생성하여 품질과 일관성을 검증했습니다.

---

## 1. 모델 빠른 참조

### NSFW 콘텐츠 지원 모델

| 모델 | 이미지당 비용 | 해상도 | NSFW 방법 | 최적 용도 |
|------|-------------|--------|-----------|----------|
| **Flux Dev** | $0.012 | 최대 2048×2048 | `safety_checker=false` | 가성비 최고 포토리얼 |
| **Flux Dev LoRA** | $0.032 | 최대 2048×2048 | `safety_checker=false` + 커스텀 LoRA | 애니메, 커스텀 스타일 |
| **Seedream v5.0 Lite** | $0.032 | 최대 4704×4704 | 화이트리스트 필요 | 초고해상도, 피부 디테일 |
| **Nano Banana 2** | $0.072 | 최대 2048×2048 | 네이티브 NSFW 지원 | 최고 속도 |
| **SDXL** | $0.008 | 1024×1024 | 커뮤니티 체크포인트 | 예산 절약 |
| **SDXL Lightning** | $0.004 | 1024×1024 | 4스텝 고속 추론 | 래피드 프로토타이핑 |
| **Pony Diffusion V6 XL** | $0.012 | 1024×1024 | 네이티브 NSFW | 애니메/이차원 전문 |
| **Flux Kontext Pro** | $0.05 | 최대 2048×2048 | 제한적 | 캐릭터 일관성 |

### 모델별 핵심 매개변수

| 모델 | CFG 스케일 | 스텝 수 | 스케줄러 | 권장 비율 |
|------|-----------|--------|---------|----------|
| Flux Dev | 3.5–7.0 | 28–50 | Euler | 2:3(세로), 3:2(가로) |
| Flux Dev LoRA | 3.5–7.0 | 28–50 | Euler | 2:3, 9:16 |
| Seedream v5.0 | 4.0–7.0 | 30–50 | DPM++ 2M | 2:3, 3:4 |
| Nano Banana 2 | 5.0–8.0 | 20–35 | Euler A | 2:3, 1:1 |
| SDXL | 7.0–12.0 | 30–50 | DPM++ 2M Karras | 1:1(네이티브) |
| Pony V6 XL | 7.0–10.0 | 25–40 | Euler A | 2:3, 3:4 |

---

## 2. 프롬프트 엔지니어링 기초

### 2.1 우수한 NSFW 프롬프트의 구조

고품질 프롬프트는 다음 구조를 따릅니다:

```
[피사체 설명] + [신체 디테일] + [포즈/액션] + [장면/배경] +
[조명] + [카메라/구도] + [스타일/매체] + [품질 태그]
```

**분해 예시:**

```
A stunning 25-year-old woman with long auburn hair,          ← 피사체
athletic build, toned abs, perky breasts, smooth tan skin,   ← 신체 디테일
reclining on silk sheets with one arm behind her head,       ← 포즈
in a luxury hotel penthouse bedroom with city lights          ← 장면
visible through floor-to-ceiling windows,
warm golden hour light filtering through sheer curtains,     ← 조명
shot from a slightly elevated angle, shallow depth of field, ← 카메라
professional boudoir photography, 85mm lens,                 ← 스타일
masterpiece, best quality, ultra-detailed, 8K UHD            ← 품질 태그
```

### 2.2 효과적인 품질 태그

**범용 품질 부스터** (모든 모델 공통):
```
masterpiece, best quality, ultra-detailed, highres, 8K UHD, RAW photo,
photorealistic, professional photography, sharp focus, intricate details
```

**포토리얼리즘 전용:**
```
DSLR photo, Nikon D850, Canon EOS R5, 85mm f/1.4,
subsurface scattering, natural skin texture, skin pores visible,
studio lighting, Rembrandt lighting, rim light
```

**애니메/만화 전용:**
```
anime style, cel shading, vibrant colors, clean lineart,
detailed eyes, anime face, manga illustration,
score_9, score_8_up, score_7_up (Pony V6 XL 전용)
```

### 2.3 신체 설명 토큰 순서

모델은 위치에 따라 토큰에 다른 가중치를 부여합니다. 최상의 결과를 위해:

1. **나이/인종** → "25-year-old Japanese woman"
2. **체형** → "petite, slender build"
3. **핵심 특징** → "large expressive eyes, full lips"
4. **머리카락** → "long black hair with bangs"
5. **피부** → "flawless porcelain skin"
6. **신체 세부** → "slim waist, wide hips, C-cup breasts"
7. **의상/상태** → "wearing a sheer white negligee, partially unbuttoned"

### 2.4 결과를 바꾸는 조명 키워드

| 키워드 | 효과 | 최적 용도 |
|--------|------|----------|
| `golden hour lighting` | 따뜻하고, 부드럽고, 돋보이는 | 야외 부드와르 |
| `Rembrandt lighting` | 볼의 삼각 광, 드라마틱 | 예술적 초상 |
| `rim lighting` | 빛나는 윤곽 하이라이트 | 실루엣, 바디라인 |
| `neon lighting` | 컬러풀, 사이버펑크 | 판타지, SF |
| `natural window light` | 부드러운, 현실적 실내 | 침실 장면 |
| `candlelight` | 따뜻한, 친밀한, 소프트 섀도우 | 로맨틱 장면 |
| `studio strobe` | 깨끗한, 전문적 | 글래머 사진 |
| `backlighting` | 실루엣, 헤어 글로우 | 예술적 바디샷 |
| `chiaroscuro` | 명암 고대비 | 파인아트 누드 |
| `volumetric lighting` | 빛줄기, 분위기 | 판타지 장면 |

### 2.5 카메라 & 구도 키워드

| 키워드 | 효과 |
|--------|------|
| `shot from below, low angle` | 높이, 파워감 강조 |
| `bird's eye view` | 전신 부감 |
| `over the shoulder` | 친밀한 POV |
| `dutch angle` | 다이내믹한 긴장감 |
| `macro close-up` | 디테일 클로즈업 |
| `full body shot` | 완전한 인물 |
| `medium shot, waist up` | 클래식 초상 프레이밍 |
| `rule of thirds` | 균형 잡힌 구도 |
| `shallow depth of field, bokeh` | 피사체 분리 |
| `wide angle lens, 24mm` | 환경 맥락 |

---

## 3. 포토리얼리스틱 프롬프트 (30개)

### 3.1 부드와르 & 침실

**PR-01: 실크 시트 럭셔리**
```
A gorgeous 26-year-old woman with flowing chestnut hair and green eyes,
athletic yet curvy figure, lying seductively on white silk sheets in a
minimalist luxury bedroom, one shoulder strap of her black lace slip
falling off her shoulder, soft morning light streaming through sheer
linen curtains, shallow depth of field, shot with Canon EOS R5 85mm
f/1.2, warm color palette, professional boudoir photography, subsurface
scattering on skin, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **모델**: Flux Dev (`safety_checker=false`)
- **네거티브**: `deformed, bad anatomy, extra fingers, blurry, low quality, watermark`
- **CFG**: 5.0 | **스텝**: 35 | **크기**: 832×1216

**PR-02: 모닝 라이트**
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
- **모델**: Flux Dev
- **네거티브**: `plastic skin, airbrushed, mannequin, extra limbs, bad hands`
- **CFG**: 4.5 | **스텝**: 30 | **크기**: 832×1216

**PR-03: 욕조 장면**
```
Stunning 24-year-old mixed-race woman with curly dark hair piled up
in a messy bun, caramel skin, relaxing in a freestanding clawfoot
bathtub filled with milky water and rose petals, one leg draped over
the edge, steam rising, marble bathroom with brass fixtures, soft
diffused natural light from frosted window, water droplets on skin,
intimate candid photography, 50mm lens, slight film grain,
masterpiece, ultra-detailed, photorealistic, 8K
```
- **모델**: Seedream v5.0 Lite (초고화질 디테일)
- **네거티브**: `deformed, ugly, blurry, bad proportions, watermark, text`
- **CFG**: 5.5 | **스텝**: 40 | **크기**: 1280×1920

**PR-04: 거울 반사**
```
Elegant 30-year-old East Asian woman with straight black hair to her
waist, slender figure, standing before a full-length vintage mirror
in a dimly lit dressing room, wearing a black lace bodysuit, her
reflection visible in the mirror creating a dual composition, warm
tungsten lamp light, velvet curtains in the background, shot at f/2.0
with beautiful bokeh, fashion editorial photography style, detailed
skin texture, masterpiece, best quality, ultra-detailed
```
- **모델**: Flux Dev
- **네거티브**: `deformed reflection, extra limbs, disfigured, low quality`
- **CFG**: 5.0 | **스텝**: 35 | **크기**: 832×1216

**PR-05: 수영장 일광욕**
```
Attractive 27-year-old Mediterranean woman with olive skin and dark
wavy hair, toned athletic body, sunbathing on a luxury pool lounger
wearing a tiny white string bikini, glistening with suntan oil,
infinity pool with ocean view in the background, harsh midday sunlight
creating defined shadows, water reflections dancing on her skin,
fashion magazine photography, Sony A7R V, 70-200mm lens, vibrant
summer colors, masterpiece, best quality, ultra-detailed, 8K UHD
```
- **모델**: Flux Dev
- **네거티브**: `bad anatomy, extra fingers, deformed, blurry, text, watermark`
- **CFG**: 5.0 | **스텝**: 30 | **크기**: 1216×832

**PR-06: 샤워 장면**
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
- **모델**: Seedream v5.0 Lite
- **네거티브**: `deformed, plastic skin, blurry, bad hands, extra fingers`
- **CFG**: 5.5 | **스텝**: 40 | **크기**: 1280×1920

**PR-07: 흑백 아트**
```
Striking 32-year-old African American woman with short natural hair,
statuesque figure, posing nude with arms crossed beneath her breasts,
dramatic black and white photography, high contrast chiaroscuro
lighting with a single studio strobe from the left, deep shadows,
simple dark background, classic Helmut Newton inspired composition,
skin highlights emphasizing muscle definition, Hasselblad medium
format quality, fine grain, masterpiece, best quality, ultra-detailed
```
- **모델**: Flux Dev
- **네거티브**: `color, saturated, low contrast, blurry, deformed, extra limbs`
- **CFG**: 5.5 | **스텝**: 35 | **크기**: 832×1216

**PR-08: 창문 빛 누드**
```
Graceful 29-year-old woman with auburn hair and pale skin dotted with
freckles, dancer's body with lean muscles, standing in profile near a
large industrial window, completely nude, natural daylight casting
geometric shadow patterns across her body from window panes, loft
apartment with exposed brick walls, dust particles visible in light
beams, fine art nude photography, contemplative expression, eyes
closed, 85mm f/1.4 lens, masterpiece, best quality, ultra-detailed
```
- **모델**: Flux Dev
- **네거티브**: `deformed, bad anatomy, extra fingers, oversaturated, cartoon`
- **CFG**: 4.5 | **스텝**: 35 | **크기**: 832×1216

### 3.2 야외 & 환경

**PR-09: 해변 일몰**
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
- **모델**: Flux Dev
- **네거티브**: `deformed, bad anatomy, extra limbs, blurry, text, watermark`
- **CFG**: 5.0 | **스텝**: 35 | **크기**: 1216×832

**PR-10: 숲속 요정**
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
- **모델**: Flux Dev
- **네거티브**: `deformed, bad anatomy, plastic skin, harsh lighting, urban`
- **CFG**: 4.5 | **스텝**: 35 | **크기**: 832×1216

**PR-11: 옥상의 밤**
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
- **모델**: Flux Dev
- **네거티브**: `deformed, bad anatomy, blurry face, extra fingers, low quality`
- **CFG**: 5.0 | **스텝**: 30 | **크기**: 832×1216

**PR-12: 사막 오아시스**
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
- **모델**: Flux Dev
- **네거티브**: `deformed, bad anatomy, extra fingers, blurry, watermark`
- **CFG**: 5.0 | **스텝**: 35 | **크기**: 1216×832

### 3.3 ~ 3.5 포토리얼리스틱 빠른 참조 (PR-13 ~ PR-30)

| ID | 설명 | 핵심 태그 | 권장 모델 |
|----|------|----------|----------|
| PR-13 | 젖은 티셔츠, 비치 클럽 | `wet, clinging, summer, laughing` | Flux Dev |
| PR-14 | 란제리 에디토리얼, 파리 | `Vogue, lingerie, velvet, chandelier` | Flux Dev |
| PR-15 | 스포츠 일러스트레이티드 스타일 | `bikini, athletic, tan lines, tropical` | Flux Dev |
| PR-16 | 클래식 플레이보이 스타일 | `fur rug, fireplace, 1980s, film grain` | Flux Dev |
| PR-17 | 바디 페인트 | `peacock feathers, UV paint, studio` | Seedream v5.0 |
| PR-18 | 피트니스 모델 | `six-pack, competition, stage lighting` | Flux Dev |
| PR-19 | 시폰 패브릭 임플라이드 누드 | `implied nude, dance, high-key, ethereal` | Flux Dev |
| PR-20 | 빈티지 폴라로이드 | `1970s, Polaroid, nostalgic, overexposed` | Flux Dev |
| PR-21 | 이중 노출 | `cityscape, silhouette, neon, composite` | Flux Dev |
| PR-22 | 수중 누드 | `underwater, red hair, caustic light, bubbles` | Seedream v5.0 |
| PR-23 | 사우나/스팀룸 | `Finnish, wooden, steam, towel, Nordic` | Flux Dev |
| PR-24 | 비 내리는 장면 | `rain, wet shirt, neon, noir, puddles` | Flux Dev |
| PR-25 | 부드와르 클로즈업 | `body chain, macro, satin, goosebumps` | Seedream v5.0 |
| PR-26 | 요가 스튜디오 | `yoga mat, stretching, athletic, natural light` | Flux Dev |
| PR-27 | 빈티지 차 | `1960s Mustang, denim shorts, Route 66` | Flux Dev |
| PR-28 | 일본 온천 | `outdoor onsen, towel, mountains, steam` | Seedream v5.0 |
| PR-29 | 아트 갤러리 | `gallery, marble floor, classical paintings` | Flux Dev |
| PR-30 | 바이크 라이더 | `Harley Davidson, leather jacket, wind` | Flux Dev |

---

## 4. 아트/파인아트 프롬프트 (20개)

### 4.1 유화 스타일

**ART-01: 르네상스 비너스**
```
A modern reinterpretation of Botticelli's Birth of Venus, beautiful
woman with flowing golden hair standing in a giant seashell,
Renaissance oil painting style, rich pigments, visible brushstrokes,
classical composition, rose petals floating in the wind, ocean waves
and zephyr winds, warm earthy color palette with ultramarine blue
sky, craquelure texture overlay, museum quality fine art,
masterpiece, best quality, ultra-detailed
```
- **모델**: Flux Dev LoRA (르네상스 아트 LoRA)
- **네거티브**: `modern, photography, digital art, anime, deformed`
- **CFG**: 6.0 | **스텝**: 40 | **크기**: 1024×1024

**ART-02: 바로크 드라마틱**
```
Sensual Baroque-style oil painting of a reclining nude woman on red
velvet drapery, Caravaggio-inspired dramatic chiaroscuro lighting,
deep shadows contrasting with luminous skin painted with visible
impasto technique, rich jewel tones — deep crimson, gold, midnight
blue, elaborate gilded frame visible at edges, classical figure
proportions, oil on canvas texture, museum quality reproduction,
masterpiece, best quality
```
- **모델**: Flux Dev LoRA
- **네거티브**: `flat lighting, cartoon, anime, digital, modern, photography`
- **CFG**: 6.5 | **스텝**: 40 | **크기**: 1216×832

**ART-03: 인상주의 목욕**
```
Impressionist oil painting of a woman bathing in a sunlit room,
inspired by Pierre-Auguste Renoir's bather paintings, soft dappled
light, loose expressive brushstrokes, warm peach and rose skin tones,
blue and lavender shadows, white porcelain tub, floral wallpaper
background painted with visible texture, casual intimate moment,
late 19th century French Impressionism, canvas weave texture,
masterpiece, best quality, ultra-detailed
```
- **모델**: Flux Dev LoRA
- **네거티브**: `photorealistic, sharp, digital, modern, anime, cartoon`
- **CFG**: 6.0 | **스텝**: 40 | **크기**: 832×1216

**ART-04: 아르누보**
```
Art Nouveau illustration of a sensual woman with extremely long
flowing hair intertwined with morning glory vines and butterflies,
Alphonse Mucha inspired style, decorative circular halo frame behind
her, ornamental patterns, muted pastel colors with gold leaf accents,
elegant sinuous lines, partially nude with flowing fabric draping
strategically, mosaic-like background elements, lithograph print
texture, masterpiece, best quality, ultra-detailed
```
- **모델**: Flux Dev LoRA
- **네거티브**: `photorealistic, modern, 3D render, anime, harsh colors`
- **CFG**: 6.0 | **스텝**: 40 | **크기**: 832×1216

**ART-05: 수채화 누드**
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
- **모델**: Flux Dev LoRA
- **네거티브**: `digital, photorealistic, opaque, oil painting, sharp lines`
- **CFG**: 5.0 | **스텝**: 35 | **크기**: 832×1216

### 4.2 현대 & 디지털 아트 (ART-06 ~ ART-20)

| ID | 스타일 | 설명 | 핵심 태그 |
|----|--------|------|----------|
| ART-06 | 베이퍼웨이브 | 핑크와 퍼플, 글리치 효과 | `CRT, glitch, neon, VHS, synthwave` |
| ART-07 | 팝 아트 | 벤데이 도트, 코믹 스타일 | `Lichtenstein, primary colors, bold` |
| ART-08 | 목탄 데생 | 라이프 드로잉 | `charcoal, gestural, paper texture` |
| ART-09 | 초현실주의 | 달리 스타일, 녹는 신체 | `melting, desert, clocks, surreal` |
| ART-10 | 미니멀 라인 | 원선 누드 | `continuous line, Picasso, minimal` |
| ART-11 | 우키요에 | 일본 목판화, 기생 | `shunga, woodblock, Utamaro style` |
| ART-12 | 아르데코 | 기하학적 여성, 금과 검정 | `1920s, Tamara de Lempicka, geometric` |
| ART-13 | 표현주의 | 왜곡된 인물, 선명한 색채 | `Egon Schiele, angular, raw emotion` |
| ART-14 | 연필 스케치 | 상세한 흑연 인물 습작 | `HB pencil, hatching, anatomy study` |
| ART-15 | 스테인드글라스 | 대성당 창문 같은 여성 | `Gothic, lead lines, jewel colors` |
| ART-16 | 모자이크 | 로마 모자이크 누드 | `tesserae, ancient Roman, bath scene` |
| ART-17 | 스프레이 페인트 | 벽돌 벽의 거리 예술 | `Banksy style, stencil, urban` |
| ART-18 | 수묵화 | 먹그림 스타일 누드 | `Chinese ink, rice paper, bamboo brush` |
| ART-19 | 파스텔화 | 드가 스타일 부드러운 인물 | `soft pastel, dancer, warm tones` |
| ART-20 | 콜라주 | 컷페이퍼 누드 구성 | `magazine cut-outs, layered, mixed media` |

---

## 5. 애니메/만화 프롬프트 (25개)

### 5.1 모던 애니메 스타일

**AN-01: 비치 에피소드**
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
- **모델**: Pony Diffusion V6 XL 또는 Flux Dev LoRA (애니메 LoRA)
- **네거티브**: `worst quality, low quality, normal quality, bad anatomy, bad hands, extra fingers, fewer fingers, extra limbs, bad proportions, watermark, text, signature, 3d, photorealistic`
- **CFG**: 7.0 | **스텝**: 28 | **크기**: 832×1216

**AN-02: 온천**
```
score_9, score_8_up, 1girl, solo, anime style, short blue hair,
red eyes, medium breasts, nude, sitting in outdoor hot spring,
water up to chest level, steam rising, towel on head, wooden fence
background, autumn maple leaves falling, rocks around the onsen,
evening sky with orange gradient, relaxed expression, slight blush,
detailed water reflections, beautiful lighting, anime coloring,
cel shading, masterpiece, best quality, absurdres
```
- **모델**: Pony V6 XL
- **네거티브**: `worst quality, low quality, bad anatomy, extra fingers, 3d, photorealistic, western`
- **CFG**: 7.0 | **스텝**: 28 | **크기**: 832×1216

**AN-03: 방과 후**
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
- **모델**: Flux Dev LoRA (애니메 LoRA)
- **네거티브**: `worst quality, low quality, bad anatomy, extra fingers, deformed, ugly, blurry`
- **CFG**: 7.0 | **스텝**: 30 | **크기**: 832×1216

**AN-04: 메이드 복장**
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
- **모델**: Pony V6 XL
- **네거티브**: `worst quality, low quality, bad anatomy, extra fingers, realistic, 3d`
- **CFG**: 7.0 | **스텝**: 28 | **크기**: 832×1216

**AN-05: 판타지 전사**
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
- **모델**: Flux Dev LoRA (애니메 LoRA)
- **네거티브**: `worst quality, low quality, bad anatomy, extra limbs, realistic, simple background`
- **CFG**: 7.0 | **스텝**: 30 | **크기**: 832×1216

### 5.2 ~ 5.3 추가 애니메 프롬프트 (AN-06 ~ AN-25)

| ID | 테마 | 설명 | 스타일 태그 |
|----|------|------|-----------|
| AN-06 | 90년대 레트로 | EVA풍, 셀 애니메이션 | `Gainax, CRT, VHS, plugsuit` |
| AN-07 | 만화 패널 | 흑백, 집중선 | `screentone, ink, speed lines` |
| AN-08 | 치비 에치 | SD, 귀엽고 섹시 | `chibi, big head, kawaii, blush` |
| AN-09 | 성인 화풍 | 상세한 성인 일러스트 | `ahegao, explicit, detailed shading` |
| AN-10 | 원신 스타일 | 게임 CG, 엘리먼트 | `Genshin Impact, vision, cel shading` |
| AN-11 | 서큐버스 | 악마 소녀, 뿔, 꼬리, 날개 | `demon, fantasy, dark, bat wings` |
| AN-12 | 간호사 | 섹시 애니메 간호사 | `hospital, white outfit, stethoscope` |
| AN-13 | 버니걸 | 버니 수트, 망사 스타킹 | `bunny ears, bowtie, cocktail, bar` |
| AN-14 | 마녀 | 누드 마녀, 모자, 빗자루 | `halloween, magic, cauldron, moon` |
| AN-15 | 고양이 귀 소녀 | 네코미미, 꼬리, 란제리 | `cat ears, paws, collar, bell` |
| AN-16 | 무녀 | 무녀복, 반탈의 | `torii gate, shrine, sacred, kimono` |
| AN-17 | 사이버펑크 | 네온 의체, 노출 의상 | `circuits, hologram, rain, neon` |
| AN-18 | 엘프 공주 | 뾰족한 귀, 숲, 노출 드레스 | `fantasy, crown, magic, nature` |
| AN-19 | 헬스 트레이너 | 스포츠 브라, 레깅스, 땀 | `gym, weights, mirror, athletic` |
| AN-20 | 아이돌 | 무대 의상, 반짝임 | `concert, microphone, spotlight` |
| AN-21 | 뱀파이어 | 고딕 드레스, 피, 송곳니 | `castle, moon, bats, pale skin` |
| AN-22 | 인어 | 바다, 조개 브라, 물고기 꼬리 | `underwater, coral, bubbles, scales` |
| AN-23 | 안드로이드 | 로봇 소녀, 노출된 회로 | `mechanical, chrome, blue glow` |
| AN-24 | 쿠노이치 | 닌자 소녀, 찢어진 의상 | `shuriken, smoke, bamboo forest` |
| AN-25 | 신부 | 웨딩드레스, 홍조 | `church, veil, flowers, white lace` |

---

## 6. 판타지/SF 프롬프트 (20개)

### 6.1 판타지

**FAN-01: 다크 엘프 소서러스**
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
- **모델**: Flux Dev LoRA (판타지 아트 LoRA)
- **네거티브**: `deformed, bad anatomy, bright cheerful, modern, photo, anime`
- **CFG**: 6.0 | **스텝**: 40 | **크기**: 832×1216

**FAN-02: 드래곤 라이더**
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
- **모델**: Flux Dev LoRA
- **네거티브**: `deformed, bad anatomy, cute, kawaii, modern, simple, boring`
- **CFG**: 6.5 | **스텝**: 40 | **크기**: 1216×832

**FAN-03 ~ FAN-20: 빠른 참조**

| ID | 테마 | 설명 | 핵심 태그 |
|----|------|------|----------|
| FAN-03 | 숲의 요정 | 잠자리 날개, 버섯, 반딧불이 | `fairy, mushroom, fireflies, enchanted` |
| FAN-04 | 달의 여신 | 호수 위에 떠있는 은발 여신 | `moon, silver, divine, reflection` |
| FAN-05 | 뱀파이어 | 고딕 대성당, 검은 레이스 | `Gothic, moonlight, fangs, cathedral` |
| FAN-06 | 사이버펑크 의체 | 반기계 신체, 네온 골목 | `cybernetic, neon, rain, Blade Runner` |
| FAN-07 | 에일리언 퀸 | 네 팔, 생물발광 | `alien, bioluminescent, HR Giger` |
| FAN-08 | 무중력 | 우주 정거장 내부 | `zero-g, ISS, floating, Earth view` |
| FAN-09 | 아마존 전사 | 정글 왕좌의 여전사 | `tribal, spear, tiger, primal` |
| FAN-10 | 얼음의 여왕 | 얼어붙은 성, 얼음 갑옷 | `frost, crystal, winter, blue` |
| FAN-11 | 피닉스 | 불의 여인, 재탄생 | `flames, ash, wings, ember` |
| FAN-12 | 메두사 | 뱀 머리카락, 석화 희생자 | `Greek myth, scales, golden eyes` |
| FAN-13 | 발키리 | 북유럽 전사, 오로라 | `winged helmet, spear, Asgard` |
| FAN-14 | 스페이스 오페라 | 외계 공주, 우주선 | `hologram, stars, chrome, regal` |
| FAN-15 | 스팀펑크 | 빅토리아 기계, 코르셋과 기어 | `brass, steam, clockwork, goggles` |
| FAN-16 | 촉수 | 크툴루적 존재, 심해 | `Lovecraftian, deep sea, bioluminescent` |
| FAN-17 | 지니 | 램프, 연기 형태 | `Arabian nights, gold, silk, magic` |
| FAN-18 | 드라이어드 | 나무 정령 | `forest spirit, roots, flowers, green` |
| FAN-19 | 세이렌 | 바위 위에서 노래 | `ocean, waves, moonlight, deadly beauty` |
| FAN-20 | 안드로이드 | 완벽한 크롬 바디 | `factory, cables, blue eyes, synthetic` |

---

## 7. 핀업/레트로 프롬프트 (15개)

**PIN-01: 클래식 1950년대 핀업**
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
- **모델**: Flux Dev LoRA (핀업 LoRA)
- **네거티브**: `photorealistic, modern, anime, dark, gritty, monochrome`
- **CFG**: 6.0 | **스텝**: 35 | **크기**: 832×1216

**PIN-02: 바르가스 걸**
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
- **모델**: Flux Dev LoRA
- **네거티브**: `photorealistic, harsh, dark, crude, modern, digital, anime`
- **CFG**: 5.5 | **스텝**: 35 | **크기**: 832×1216

**PIN-03 ~ PIN-15: 빠른 참조**

| ID | 시대/스타일 | 설명 | 핵심 태그 |
|----|-----------|------|----------|
| PIN-03 | 로커빌리 | 핫로드, 다이너 | `Chevy Bel Air, milkshake, neon` |
| PIN-04 | 세일러 제리 | 타투 플래시 아트 | `anchor, nautical, bold outlines` |
| PIN-05 | 아르데코 | 1920년대 쇼걸 | `Ziegfeld, gold, geometric, pearls` |
| PIN-06 | 2차 세계대전 | 폭격기 노즈 아트 | `B-17, leather jacket, military` |
| PIN-07 | 60년대 고고 | 고고 부츠, 미니스커트 | `mod, geometric, white boots` |
| PIN-08 | 70년대 디스코 | 글리터, 플랫폼 | `mirror ball, gold lame, afro` |
| PIN-09 | 80년대 에어로빅 | 레오타드, 레그워머 | `neon, VHS, gym, synthwave` |
| PIN-10 | 버를레스크 | 깃털 팬, 코르셋 | `cabaret, sequins, spotlight` |
| PIN-11 | 티키 바 | 하와이안, 풀라 스커트 | `bamboo, torch, tropical, lei` |
| PIN-12 | 카우걸 | 모자, 부츠, 올가미 | `western, denim, sunset, country` |
| PIN-13 | 프렌치 메이드 | 클래식 메이드 핀업 | `feather duster, stockings, frills` |
| PIN-14 | 간호사 | 빈티지 간호사 유니폼 | `red cross, cap, thermometer` |
| PIN-15 | 캘린더 걸 | 월별 테마 | `calendar page, seasonal, posed` |

---

## 8. 커플/인터랙션 프롬프트 (15개)

**COU-01: 로맨틱 포옹**
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
- **모델**: Flux Dev (`safety_checker=false`)
- **네거티브**: `deformed, bad anatomy, extra limbs, extra fingers, merged bodies, blurry`
- **CFG**: 5.0 | **스텝**: 40 | **크기**: 832×1216

**COU-02 ~ COU-15: 빠른 참조**

| ID | 테마 | 설명 | 핵심 태그 |
|----|------|------|----------|
| COU-02 | 비치 커플 | 석양의 해변에서 | `beach, sunset, minimal swimwear` |
| COU-03 | 샤워 | 함께 샤워 | `water, steam, glass, marble` |
| COU-04 | 르네상스 연인 | 티치아노풍 유화 | `Renaissance, oil painting, velvet` |
| COU-05 | 애니메 커플 | 침대에서 친밀하게 | `anime, blush, fairy lights` |
| COU-06 | 댄스 | 탱고, 드라마틱한 딥 | `dance hall, spotlight, passion` |
| COU-07 | 마사지 | 관능적 마사지 장면 | `oil, candles, spa, hands on back` |
| COU-08 | 다음 날 아침 | 함께 일어나기 | `sunlight, messy hair, lazy morning` |
| COU-09 | 핫 터브 | 자쿠지의 커플 | `bubbles, steam, wine, night sky` |
| COU-10 | 페인트 플레이 | 서로 바디 페인팅 | `colorful, messy, playful, studio` |
| COU-11 | 판타지 엘프 | 엘프 커플, 마법의 숲 | `pointed ears, magic, moonlight` |
| COU-12 | 누아르 | 탐정과 팜므 파탈 | `1940s, shadows, venetian blinds` |
| COU-13 | 뱀파이어 | 흡혈 장면 | `gothic, castle, moonlight, blood` |
| COU-14 | 수중 | 물 속에 떠있는 커플 | `bubbles, light rays, swimming` |
| COU-15 | 애니메 목욕 | 함께 목욕, 수줍은 표정 | `onsen, blush, steam, intimate` |

---

## 9. 네거티브 프롬프트 라이브러리

### 9.1 범용 네거티브 (모든 장면 공통)

```
deformed, bad anatomy, disfigured, poorly drawn face, mutation,
mutated, extra limbs, extra legs, extra arms, malformed limbs,
missing arms, missing legs, extra fingers, too many fingers,
fewer fingers, fused fingers, long neck, bad proportions,
duplicate, morbid, mutilated, out of frame, ugly, blurry,
bad quality, low quality, worst quality, watermark, text,
signature, logo, banner, username, cropped
```

### 9.2 포토리얼리즘 전용

```
(위 범용) + illustration, cartoon, anime, drawing,
painting, sketch, 3d render, CGI, plastic skin, mannequin,
wax figure, airbrushed, overprocessed, HDR artifacts
```

### 9.3 애니메/만화 전용

```
(위 범용) + photorealistic, realistic, 3d, photograph,
western art, Disney style, Pixar, bad anime art, off-model
```

### 9.4 신체 문제별 대응

| 문제 | 네거티브 프롬프트 수정 |
|------|---------------------|
| 여분의 손가락 | `extra fingers, too many fingers, fused fingers, six fingers` |
| 손 불량 | `bad hands, poorly drawn hands, missing fingers, deformed hands` |
| 얼굴 왜곡 | `deformed face, asymmetric face, crossed eyes, bad teeth` |
| 신체 공포 | `extra limbs, conjoined, fused bodies, merged bodies, extra torso` |
| 피부 이상 | `plastic skin, waxy skin, grey skin, green skin, zombie` |
| 비율 문제 | `child proportions, dwarf, giant head, tiny head, elongated` |

### 9.5 모델별 네거티브 프롬프트

**Flux Dev 전용:**
```
worst quality, jpeg artifacts, blurry, noisy, chromatic aberration,
lens distortion, overexposed, underexposed
```

**SDXL 전용:**
```
(worst quality:1.4), (low quality:1.4), (normal quality:1.4),
lowres, bad anatomy, bad hands, text, error, missing fingers,
extra digit, fewer digits, cropped, jpeg artifacts, signature,
watermark, username, blurry, artist name
```

**Pony V6 XL 전용:**
```
score_1, score_2, score_3, score_4, worst quality, low quality,
text, censored, deformed, bad hand, blurry, (watermark),
multiple phones, extra limbs
```

---

## 10. LoRA 레퍼런스 가이드

### 10.1 LoRA란?

LoRA(Low-Rank Adaptation)는 전체 모델을 재학습시키지 않고 기본 모델의 출력 스타일을 수정할 수 있는 소형 파인튜닝 모델 가중치입니다. Atlas Cloud에서는 **Flux Dev LoRA** ($0.032/장)로 LoRA를 사용할 수 있습니다.

### 10.2 API를 통한 LoRA 사용

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

### 10.3 권장 LoRA 가중치

| LoRA 유형 | 권장 스케일 | 너무 낮을 때 | 너무 높을 때 |
|-----------|-----------|------------|------------|
| 애니메 스타일 | 0.7–0.85 | 스타일 변화 거의 안 보임 | 과포화, 아티팩트 |
| 리얼리스틱 강화 | 0.5–0.7 | 효과 미미 | 언캐니 밸리 |
| 특정 캐릭터 | 0.75–0.9 | 캐릭터 인식 불가 | 오버피팅 |
| 화풍(유화, 수채화) | 0.6–0.8 | 디지털 느낌 | 피사체 디테일 손실 |
| 의상/복장 | 0.7–0.85 | 의상 부정확 | 의상과 신체 융합 |

### 10.4 인기 NSFW 호환 LoRA

| 카테고리 | LoRA 이름 | 소스 | 최적 스케일 |
|---------|----------|------|-----------|
| 애니메 범용 | Anime Art Style | CivitAI / HuggingFace | 0.75 |
| 90년대 애니메 | Retro Anime | HuggingFace | 0.7 |
| 리얼 피부 | Detail Tweaker | CivitAI | 0.5 |
| 성인용 | 다수 아티스트 | CivitAI | 0.8 |
| 핀업 | Vintage Pin-Up | CivitAI | 0.75 |
| 판타지 | Epic Fantasy | HuggingFace | 0.7 |
| 만화 흑백 | Manga Style | HuggingFace | 0.75 |
| 르네상스 | Classical Painting | CivitAI | 0.65 |

---

## 11. API 통합 가이드

### 11.1 Python — 전체 예제

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

## 12. 모델별 최적화 기법

### 12.1 Flux Dev — 최고 가성비 ($0.012/장)

**강점:** 뛰어난 포토리얼리즘, 정확한 해부학, 복잡한 장면 처리, 초저가.

**최적화 팁:**
- `safety_checker=false` 설정 **필수** (NSFW 콘텐츠에)
- CFG 3.5–5.5로 자연스러운 피부
- 스텝 28–35가 최적, 40 이상은 개선 미미
- 세로 사진은 2:3 비율 (832×1216)
- 카메라 참조 키워드에 잘 반응 ("Canon EOS R5", "85mm f/1.4")
- 조명 키워드 효과 탁월 — 항상 포함

### 12.2 Flux Dev LoRA — 커스텀 스타일 ($0.032/장)

**강점:** 적절한 LoRA로 모든 화풍 가능, 애니메 전문가.

**최적화 팁:**
- LoRA 스케일 0.7에서 시작, 0.05씩 증가
- 애니메 LoRA에는 애니메 전용 태그 포함
- 모든 HuggingFace LoRA가 호환되지는 않음 — SDXL LoRA는 Flux에서 작동 안 함

### 12.3 Seedream v5.0 Lite — 초고해상도 ($0.032/장)

**강점:** 최고 해상도 출력 (최대 4704×4704), 경이로운 피부 디테일.

**최적화 팁:**
- 화이트리스트 필요 — Atlas Cloud 지원팀에 문의
- 클로즈업과 디테일 중심 촬영에 최적
- 스텝 40–50으로 해상도 최대 활용

### 12.4 모델 선택 의사결정 트리

```
무엇이 필요한가?
│
├─ 포토리얼 성인 콘텐츠?
│  ├─ 예산 우선 → Flux Dev ($0.012) ★ 최고 가성비
│  ├─ 최고 디테일 → Seedream v5.0 ($0.032)
│  └─ 최고 속도 → Nano Banana 2 ($0.072)
│
├─ 애니메/만화 스타일?
│  ├─ 특정 LoRA 스타일 → Flux Dev LoRA ($0.032)
│  └─ 일반 애니메 → Pony V6 XL ($0.012)
│
├─ 예술적/회화적?
│  ├─ 유화/고전 → Flux Dev LoRA ($0.032)
│  └─ 빠른 컨셉 → Flux Dev ($0.012)
│
└─ 대량 생성 (100장+)?
   ├─ 품질 우선 → Flux Dev ($0.012) — 100장 = $1.20
   └─ 최저 비용 → SDXL ($0.008) — 100장 = $0.80
```

---

## 13. 비용 비교 및 플랫폼 분석

### 13.1 Atlas Cloud vs fal.ai 가격 비교

| 모델 | Atlas Cloud | fal.ai | 더 저렴한 곳 | 차이 |
|------|-----------|--------|------------|------|
| **Flux Dev** | $0.012/장 | ~$0.025/장 | Atlas ✅ | 52% 저렴 |
| **Flux Dev LoRA** | $0.032/장 | ~$0.032/장 | 동일 | — |
| **Nano Banana 2** | $0.072/장 | $0.0398/장 | fal.ai ✅ | fal 45% 저렴 |
| **Flux Kontext Pro** | $0.05/장 | $0.04/장 | fal.ai ✅ | fal 20% 저렴 |
| **Seedream v5.0** | $0.032/장 | N/A | Atlas 독점 | — |
| **SDXL** | $0.008/장 | ~$0.01/장 | Atlas ✅ | 20% 저렴 |

### 13.2 왜 Atlas Cloud를 선택해야 하는가?

| 요소 | Atlas Cloud | fal.ai |
|------|-----------|--------|
| **통합 API** | ✅ 모든 모델 하나의 API | ❌ 모델마다 다른 엔드포인트 |
| **NSFW 정책** | ✅ safety_checker=false로 명확히 지원 | ⚠️ 모델마다 다름 |
| **모델 종류** | ✅ 50+ 모델 (이미지, 비디오, 텍스트, 오디오) | ✅ 괜찮은 선택지 |
| **비디오 모델** | ✅ Wan 2.2 Spicy, Seedance 등 | NSFW 비디오 제한적 |
| **텍스트/LLM** | ✅ DeepSeek, Llama 등 | ❌ LLM 미지원 |
| **첫 충전 보너스** | ✅ **25% 보너스 (최대 $100)** | ❌ 보너스 없음 |
| **컴플라이언스** | ✅ SOC I & II 인증, HIPAA 준수 | 불확실 |
| **회사 소재지** | 🇺🇸 미국 기업 | 🇺🇸 미국 기업 |

### 13.3 비용 계산기 — $10으로 몇 장 생성 가능?

| 모델 | 장당 비용 | $10으로 생성 | 25% 보너스 적용 ($12.50) |
|------|---------|------------|------------------------|
| SDXL Lightning | $0.004 | 2,500장 | 3,125장 |
| SDXL | $0.008 | 1,250장 | 1,562장 |
| Flux Dev | $0.012 | 833장 | 1,041장 |
| Pony V6 XL | $0.012 | 833장 | 1,041장 |
| Flux Dev LoRA | $0.032 | 312장 | 390장 |
| Seedream v5.0 | $0.032 | 312장 | 390장 |
| Flux Kontext Pro | $0.05 | 200장 | 250장 |
| Nano Banana 2 | $0.072 | 138장 | 173장 |

### 13.4 신뢰성 & 컴플라이언스

[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)는 엔터프라이즈급 보안을 갖춘 미국 기업입니다:

- **SOC I & SOC II 인증** — 독립 감사된 보안 통제
- **HIPAA 준수** — 의료급 데이터 보호 기준
- **미국 인프라** — 데이터는 미국 내에 저장
- **데이터 학습 없음** — 프롬프트와 이미지는 완전히 비공개
- **종량제** — 월정액 없음, 구독 불필요

---

## 14. 시작하기

### 1단계: 계정 생성

[Atlas Cloud](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)에서 가입 — 30초면 완료.

### 2단계: 25% 보너스 받기

첫 충전 시 자동으로 **25% 보너스** 지급 (최대 $100 보너스). $10 충전하면 $12.50 크레딧.

### 3단계: API 키 발급

대시보드 → API Keys → 새 키 생성.

### 4단계: 생성 시작

이 저장소의 아무 프롬프트와 위의 API 예제를 사용하세요. Flux Dev ($0.012/장)부터 시작하는 것을 추천합니다 — 품질, 비용, NSFW 기능의 최적 균형.

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

## 15. Star History & 기여

### Star History

[![Star History Chart](https://api.star-history.com/svg?repos=thoughtincode/nsfw-ai-image-prompts&type=Date)](https://star-history.com/#thoughtincode/nsfw-ai-image-prompts&Date)

### 기여

기여를 환영합니다! 테스트를 거쳐 일관되게 좋은 결과를 내는 프롬프트가 있다면:

1. 이 저장소를 포크
2. 기존 형식에 따라 프롬프트 추가 (모델, 네거티브, 매개변수 포함)
3. 풀 리퀘스트 제출 (가능하면 샘플 출력 첨부)

### 관련 리소스

- [NSFW AI 모델 비교 2026](https://github.com/thoughtincode/nsfw-ai-model-comparison) — 17개 AI 모델의 종합 벤치마크
- [Atlas Cloud API 문서](https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts)

---

## 라이선스

이 프로젝트는 MIT 라이선스로 라이선스됩니다 — 자세한 내용은 [LICENSE](LICENSE) 파일을 참조하세요.

---

**면책 조항:** 이 저장소는 성인 사용자(18세 이상)의 합법적 사용만을 위해 만들어졌습니다. AI 생성 콘텐츠에 관한 현지 법률을 항상 준수하세요. 이 모음의 프롬프트는 예술적, 창작 목적입니다. 사용자는 이러한 프롬프트의 사용 방법과 생성되는 콘텐츠에 대해 책임을 집니다.

---

<p align="center">
  <a href="https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts">
    <img src="https://img.shields.io/badge/Powered%20by-Atlas%20Cloud-purple?style=for-the-badge" alt="Powered by Atlas Cloud">
  </a>
</p>
<p align="center">
  <sub>모든 프롬프트는 <a href="https://www.atlascloud.ai?ref=JPM683&utm_source=github&utm_campaign=nsfw-ai-image-prompts">Atlas Cloud</a>에서 테스트 완료 — SOC I & II 인증, HIPAA 준수, 미국 기업</sub>
</p>
