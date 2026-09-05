# Diffusion

*TOP · v0.6.6*

<!-- screenshot: drop a PNG at docs/images/diffusion.png and rerun the generator -->

Stable Diffusion running entirely on your machine: text to image, image to image, ControlNet and inpainting. The model is a pipeline folder you point it at, so you choose the model.

> **Needs a model.** The operator says so on the node and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

Optional: a source image (input 1), a ControlNet control image (input 2), an inpaint mask (input 3).

## Outputs

The generated image.

## Worth knowing

- **Not realtime.** Seconds per image, Generate-driven.
- Guidance 0 is unconditional — SD-Turbo wants guidance 1.0 and 2 steps.
- ControlNet selection changes the pipeline identity, so it reloads.

## Parameters

### Diffusion

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Enable** | toggle | False |  |
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
| **Save Path** | file |  |  |
| **Choose…** | button |  |  |
| **Save** | button |  |  |
| **Steps** | number | 0 |  |
| **Guidance Scale** | number | 0.0 |  |
| **Seed (-1 = random)** | number | 0 |  |
| **Scheduler** | StrMenu |  | PNDM, DPM-Solver++, DPM-Solver++ Karras (quality at 6-8 steps) |
| **Source TOP** | TOP |  |  |
| **Control TOP** | TOP |  |  |
| **Control Net** | StrMenu |  | None, Canny, Depth, OpenPose, Scribble |
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
- `ChooseSavePath`
- `ControlNets`
- `DoCallback`
- `Generate`
- `LastError`
- `LastSeed`
- `Loaded`
- `SampleSize`
- `SaveImage`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onPipelineLoaded`
- `onNewImage`
- `onError`
- `onSaved`

