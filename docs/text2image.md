## What Is This?

Text to Image generates a brand new picture entirely from your text description. There is no starting image — the model begins from pure noise and sculpts it into something matching your prompt over many small steps. Use this tab when you want to create something from scratch.

![Text to Image Example](https://github.com/blackmagicstudiosza/black-magic-documentation/blob/main/images/text2image.png)

---

## Quick Start

1. Choose a **Base Model** (checkpoint).
2. Optionally add one or more **LoRAs** for a specific art style or character.
3. Set the **Generation Size** (or click **Use Canvas Size**).
4. Write a **Positive Prompt** and optionally refine the **Negative Prompt**.
5. Leave the **KSampler** settings at their defaults to start.
6. Click **Generate**.

---

## Base Model Selector

A checkpoint is a single file containing a complete, self-contained AI model — think of it as the artist behind your generations. Each checkpoint has been trained on a specific collection of images and has developed its own visual style as a result. One checkpoint might produce photorealistic results, another painterly oil paintings, another crisp pixel art. The checkpoint you pick has the single biggest impact on what your output looks like.

**Tips:**
- Models trained on pixel art (e.g. `pixel-art-xl`, `PixelArtDiffusion`) produce pixel art output without extra effort in the prompt.
- SDXL-based models generally produce higher resolution and more coherent results than SD 1.5 models but are slower and need more VRAM.
- The model name usually gives you a hint — look for keywords like `pixel`, `anime`, `realistic`, `cartoon`, etc.
- Start with one model and learn its strengths before switching around.

---

## LoRA Selector

LoRAs (Low-Rank Adaptations) are small add-on files that nudge the model toward a specific style, character, concept, or technique without replacing the whole model.

**Controls:**

| Control | What It Does |
|---|---|
| Number of LoRAs slider | Shows 1–5 LoRA slots. Slots beyond the slider value are hidden and set to DISABLE. |
| LoRA dropdown | Pick which LoRA file to use. Set to `DISABLE` to skip that slot entirely. |
| Model Strength | Controls how strongly the LoRA pushes the visual output toward its style. At `0.0` the LoRA has no effect; at `1.0` it applies its full influence. |
| Clip Strength | Controls how much the LoRA changes what your prompt words mean to the model. For example, a pixel art LoRA with high Clip Strength might make the word "character" automatically invoke pixel art proportions and conventions even if you don't write "pixel art" in your prompt. At lower values your words keep their normal meaning while the visual style still shifts. **In almost all cases, set this to the same value as Model Strength.** |

**Recommended ranges:**
- **Model Strength:** `0.5–1.0` for most LoRAs. Start at `0.8`. Above `1.0` often causes over-saturation or artifacts.
- **Clip Strength:** Match Model Strength as your default. Only lower it independently if the LoRA seems to be overriding or confusing your prompts in unexpected ways while the image style still looks correct.
- If a LoRA is making your image look broken or overpowering the prompt, reduce both strengths to `0.4–0.6`.

---

## Generation Size (EmptyLatentImage)

Sets the pixel dimensions the model generates at internally. This is not the canvas size — it is the size the AI works at before the result is placed onto your sprite.

| Field | What It Does |
|---|---|
| Width | Generation width in pixels |
| Height | Generation height in pixels |
| Use Canvas Size | Sets width/height to match the active Aseprite sprite dimensions |

**Recommended sizes:**
- **SD 1.5 models:** 512×512 is native. 512×768 or 768×512 work well for portrait/landscape. Avoid going above 768 in either dimension.
- **SDXL models:** 1024×1024 is native. Common variants: 1152×896, 896×1152, 1216×832.
- **Pixel art models:** Often work best at lower resolutions like 128×128, 256×256, or 512×512 — check the model's documentation for guidance.
- **Rule of thumb:** Keep dimensions as multiples of 64 (e.g. 512, 576, 640, 704, 768, 832…). Odd values can produce visual artifacts.
- Larger sizes use more VRAM and take longer. Start small while dialing in your prompt, then scale up.

---

## Prompts

### Positive Prompt
Describe what you **want** in the image. Be specific — more detail generally produces better results.

**Tips:**
- Lead with the most important concept (subject first, then style, then detail).
- Include style keywords: `pixel art`, `oil painting`, `watercolor`, `anime`, `photorealistic`, etc.
- Quality boosters for non-pixel models: `masterpiece, best quality, highly detailed`.
- Comma-separate concepts. Each comma acts as a natural emphasis boundary.

**Examples:**
```
pixel art character, knight in silver armor, holding sword, blue cape, 16x16, retro game style
```
```
isometric dungeon tile, stone floor, lit torch on wall, dark fantasy, pixel art
```

### Negative Prompt
Describe what you **do not want** in the image. The pre-filled default (`blurry, cropped, ugly, text, watermark`) is a reasonable starting point.

**Common additions:**
```
blurry, low quality, extra limbs, bad anatomy, deformed, watermark, signature, text, cropped, jpeg artifacts
```

**Tips:**
- Negative prompts prevent common failure modes. If your generations have a recurring problem (extra fingers, bad backgrounds), add those words here.
- Don't go overboard — an extremely long negative prompt can sometimes compete with your positive prompt.

---

## KSampler Settings

The KSampler is the engine that actually runs the diffusion process. Understanding these settings unlocks much better results.

### Seed
A number that initializes the starting noise pattern. The same seed + same settings = the same image every time.

| Mode | Behavior |
|---|---|
| **fixed** | The same seed is reused every generation (reproducible results) |
| **increment** | Seed goes up by 1 each time |
| **decrement** | Seed goes down by 1 each time |
| **randomize** | A new random seed is picked each time |

**Tips:**
- Use `randomize` while exploring. Once you get a result you like, note the seed and switch to `fixed` to refine it further without losing that composition.
- The **seed button** manually advances the seed according to the current mode without triggering a generation.

---

### Steps
How many refinement passes the model takes. More steps = more refined result, but with diminishing returns after a point.

| Range | Effect |
|---|---|
| 10–15 | Fast, rougher results — good for quick iteration while finding the right prompt |
| 20–30 | **Recommended default.** Good balance of quality and speed. |
| 40–50 | Slower. Sometimes slightly sharper. Rarely worth the extra time. |
| 50+ | Usually wasteful — quality plateaus or can even degrade. |

**Start at 20. Increase to 28–30 for final renders.**

---

### CFG (Classifier-Free Guidance Scale)
Controls how strictly the model follows your prompt versus improvising freely.

| Value | Effect |
|---|---|
| 1–3 | Very loose — model largely ignores the prompt. Creative but unpredictable. |
| 5–7 | **Recommended range.** Balanced, natural-looking results. |
| 7–9 | Prompt-faithful but can over-saturate colors or over-sharpen details. |
| 10+ | Very rigid — often produces burnt, over-contrasted, or plastic-looking images. |

**Start at 7.0. If results look too random, go up to 7.5–8. If they look artificial or plastic, go down to 6–6.5.**

---

### Sampler
The mathematical algorithm used to run the diffusion steps. Different samplers have different speed/quality tradeoffs and aesthetic characteristics.

| Sampler | Character |
|---|---|
| **euler_ancestral** | Fast, slightly painterly, good general purpose. **Best starting point.** |
| **euler** | Clean and deterministic. Less variation between generations at the same seed. |
| **dpmpp_2m** | Efficient — often good quality at 20 steps. |
| **dpmpp_sde** | Stochastic. Can produce very detailed, slightly different results each run even with a fixed seed. |
| **ddim** | Deterministic, older algorithm. Fine for general use. |
| **lcm** | Very fast (4–8 steps), but requires an LCM-compatible model or LoRA. |

**Recommended default: `euler_ancestral`**

---

### Scheduler
Controls how the noise level changes across the steps. Works closely with the Sampler.

| Scheduler | Character |
|---|---|
| **normal** | Safe general-purpose default. **Start here.** |
| **karras** | Often improves detail and softness. Pairs well with dpmpp samplers. |
| **sgm_uniform** | Good for SDXL models. |
| **exponential** | Aggressive early denoise. Can produce very clean results. |
| **simple** | Minimal, similar to normal. |

**Recommended default: `normal`. Try `karras` with dpmpp samplers for a quality bump.**

---

### Denoise %
How much of the image to recreate from noise. In Text to Image this is always `1.00` — you are generating from pure noise, so 100% is correct and should not be changed.

- **Text to Image default: 1.00** — do not change this for text-to-image.
- Values below 1.0 in text-to-image will partially reuse undefined noise and produce inconsistent results.

---

## Workflow Tools (Top Bar)

| Tool | What It Does |
|---|---|
| **Save Workflow** | Saves the current settings to a named file so you can reload them later. |
| **Load Workflow** | Opens a saved or history workflow and restores its settings into the dialog. |
| **Generate** | Runs the generation. The workflow is also auto-saved to history. The seed updates per the Seed Generation mode. |

**Tip:** Save workflows when you find a combination you like. You can build a library of different styles and reload them instantly.
