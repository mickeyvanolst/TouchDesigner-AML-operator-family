# CoreML Model

*TOP · v0.4.3*

<!-- screenshot: drop a PNG at docs/images/coreml_model.png and rerun the generator -->

Runs any image-in Core ML model you point it at. This is the escape hatch: if a model loads, this operator will run it, including models nobody wrote an operator for.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image, and optionally a second image for two-image models.

## Outputs

Depends on **Result Mode** — a picture, a segmentation map, normalised floats, or exact tensor values for decoding downstream.

## Worth knowing

- Raw Tensor gives exact values with the shape published alongside, which is how you decode a model TouchDesigner-side.
- TouchDesigner silently downscales textures above 1280 on a Non-Commercial licence; **Max Texture Size** is there for commercial licences with bigger outputs.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model Path** | file |  |  |
| **Compute Units** | menu | All | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |
| **Result Mode** | menu | Auto | Auto, Segmentation, Raw Float, Raw Tensor |
| **Output Name** | StrMenu |  | (auto), semanticPredictions |

### Input

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Fit Mode** | StrMenu |  | Stretch, Letterbox (pad), Crop (fill) |
| **Pixel Range** | StrMenu |  | 0 to 1, -1 to 1, 0 to 255, Custom (Mean/Std) |
| **Mean (RGB)** | RGBA | 0.485 |  |
| **Mean (RGB)** | RGBA | 0.456 |  |
| **Mean (RGB)** | RGBA | 0.406 |  |
| **Std (RGB)** | RGBA | 0.229 |  |
| **Std (RGB)** | RGBA | 0.224 |  |
| **Std (RGB)** | RGBA | 0.225 |  |
| **Channel Order** | StrMenu |  | RGB, BGR |
| **Vector CHOP** | CHOP |  |  |
| **Vector Input Name** | StrMenu |  | (auto) |

### Segmentation

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Visualization** | menu | Coloured | Coloured, Overlay, Single Class Mask |
| **Overlay Alpha** | number | 0.6 |  |
| **Palette** | StrMenu |  | Auto (DAT > known sets > generated), PASCAL VOC (21 cls), Face Parsing (19 cls), From Palette DAT, Generated (any class count) |
| **Palette DAT** | DAT |  |  |
| **Selected Class** | StrMenu |  | (no model loaded) |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Normalize Output** | toggle | True |  |
| **Async Mode** | toggle | True |  |

## Python

Reachable on the operator via its extension:

- `GetClasses`
- `Loaded`

