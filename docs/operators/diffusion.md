# Diffusion

*TOP · v0.8.3*

<!-- screenshot: drop a PNG at docs/images/diffusion.png and rerun the generator -->

Stable Diffusion running entirely on your machine: text to image, image to image, ControlNet and inpainting. The model is a pipeline folder you point it at, so you choose the model.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

Optional: a source image (input 1), a ControlNet control image (input 2), an inpaint mask (input 3).

## Outputs

The generated image.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [apple/ml-stable-diffusion](https://github.com/apple/ml-stable-diffusion) — the Core ML Stable Diffusion pipeline this operator drives, and how to convert a model of your own (MIT)
- [ControlNet](https://github.com/lllyasviel/ControlNet) — what the control image does

Models it downloads through the Model Manager, each under its own licence:

- [Stable Diffusion 2 base](https://huggingface.co/apple/coreml-stable-diffusion-2-base) — CreativeML Open RAIL-M
- [Stable Diffusion XL base](https://huggingface.co/apple/coreml-stable-diffusion-xl-base) — CreativeML Open RAIL++-M
- [SD 1.5 + ControlNet](https://huggingface.co/coreml-community/coreml-stable-diffusion-v1-5_cn) — CreativeML Open RAIL-M
- [DreamShaper (SD 1.5)](https://huggingface.co/coreml-community/cormel-DreamShaper-v8_cn) — CreativeML Open RAIL-M
- [SD 1.5 landscape (768x512)](https://huggingface.co/coreml-community/coreml-stable-diffusion-v1-5_cn) — CreativeML Open RAIL-M
- [SD-Turbo (1–4 steps)](https://huggingface.co/keijiro-tk/coreml-sd-turbo) — Stability AI Community License
- [SDXL VAE encoder (fp16 fix)](https://huggingface.co/madebyollin/sdxl-vae-fp16-fix) — MIT

## Worth knowing

- **If a model never finishes loading, switch Compute Units to CPU+GPU.** Under All or CPU+ANE some pipelines hang in CoreML's compiler with no error — measured on sd2-base and the 768x512 landscape model, both of which load in about 15 s under CPU+GPU. Meanwhile the previous model keeps generating, so a 768x512 model that "outputs 512x512" is the old one still answering. The operator warns after 150 s of loading and says which model is really running.
- **Not realtime.** Seconds per image, Generate-driven.
- Guidance 0 is unconditional — SD-Turbo wants guidance 1.0 and 2 steps.
- ControlNet selection changes the pipeline identity, so it reloads.
- **Control Net** lists what the loaded pipeline actually carries — the sd15-controlnet pipeline ships Canny, Depth, OpenPose and Scribble. The menu reads `None` until a pipeline finishes loading, and stays that way for a pipeline built without ControlNet.

## Parameters

### Diffusion

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Enable** | toggle | False |  |
| **Model** | menu | sd_turbo | SD-Turbo (1–4 steps)  (not installed), Stable Diffusion 2 base, SD 1.5 + ControlNet, DreamShaper (SD 1.5), SD 1.5 landscape (768x512), Stable Diffusion XL base, Custom file... |
| **Model Folder** | folder |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Prompt** | text |  |  |
| **Prompt DAT** | DAT |  |  |
| **Negative Prompt** | text |  |  |
| **Generate** | button |  |  |
| **Generate On Prompt Change** | toggle | False |  |
| **Loop Generate** | toggle | False |  |
| **Generate On Input Change** | toggle | False |  |
| **Cancel** | button |  |  |
| **Clear** | button |  |  |
| **Image File Type** | menu | png | PNG, JPEG, TIFF, EXR |
| **Unique Suffix** | toggle | False |  |
| **N** | number | 0 |  |
| **Save Path** | FileSave |  |  |
| **Save** | button |  |  |
| **Steps** | number | 0 |  |
| **Guidance Scale** | number | 0.0 |  |
| **Seed (-1 = random)** | number | 0 |  |
| **Scheduler** | StrMenu |  | PNDM, DPM-Solver++, DPM-Solver++ Karras (quality at 6-8 steps) |
| **Source TOP** | TOP |  |  |
| **Control TOP** | TOP |  |  |
| **Control Net** | StrMenu |  | None |
| **Control Net Weight** | number | 1.0 |  |
| **Use Source Image (img2img)** | toggle | False |  |
| **Source Strength** | number | 0.0 |  |
| **Input Fit** | StrMenu |  | Stretch, Letterbox (pad), Crop (cover) |
| **Mask TOP** | TOP |  |  |
| **Use Inpaint Mask** | toggle | False |  |
| **Compute Units** | StrMenu |  | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reduce Memory** | toggle | False |  |
| **While Busy** | StrMenu |  | Queue One, Ignore |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Output Resolution** | menu | native | Native (Model), Custom (Scaled) |
| **Resolution** | number | 512 |  |
| **Resolution** | number | 512 |  |

## Python

Reachable on the operator via its extension:

- `Busy`
- `Cancel`
- `ControlNets`
- `DoCallback`
- `Generate`
- `LastError`
- `LastSeed`
- `Loaded`
- `SUFFIX`
- `SampleSize`
- `SaveImage`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onPipelineLoaded`
- `onNewImage`
- `onError`
- `onSaved`

