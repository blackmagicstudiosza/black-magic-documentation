# Black Magik — Documentation

AI image generation inside Aseprite, powered by ComfyUI.

![Black Magik Overview](images/home_overview.png)

---

## Generation

| Page | Description |
|---|---|
| [Text to Image](Text-to-Image) | Generate images from a text prompt |
| [Image to Image](Image-To-Image) | Transform your existing canvas using a prompt |
| [Inpaint / Outpaint](Inpainting-And-Outpainting) | Regenerate a selected region or extend the canvas |
| [IPAdapter](IPAdapter) | Guide generation using a reference image |
| [ControlNet](Controlnet) | Guide generation using pose, depth, edges, and more |
| [Pixel Art](pixelartdetector) | Palette reduction and conversion using PixelArt Detector nodes |

---

## Reference

| Page | Description |
|---|---|
| [Tools](Tools) | Wang tilesets, pixelation, background removal, ControlNet reference generator |
| [API Providers](API) | Cloud generation via PixelLab, Nano Banana, OpenAI, Grok, and RetroDiffusion |
| [Settings](Settings) | Server management, model installation, plugin preferences |
| [Custom LoRAs](Black-Magic-LoRAs) | Trained LoRAs — settings, trigger words, and recommended parameters |

---

## Quick Start

1. Go to the **Settings** tab and click **Start Servers**.
2. Wait for both servers to show as running.
3. Open the **Text to Image** tab, pick a model, write a prompt, and click **Generate**.

New to diffusion models? Start with the [Text to Image](Text-to-Image) page — it explains checkpoints, LoRAs, and all KSampler settings from scratch.
