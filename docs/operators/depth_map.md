# Depth Map

*TOP · v0.3.6*

<!-- screenshot: drop a PNG at docs/images/depth_map.png and rerun the generator -->

Estimates depth from a single ordinary image — no depth camera. Good for parallax, fog, displacement and depth-of-field.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A depth image. Values are relative, not metres — see **Depth Metric** if you need real distance.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [Depth Anything V2](https://github.com/DepthAnything/Depth-Anything-V2) — the model; its paper and the larger, non-commercial variants

Models it downloads through the Model Manager, each under its own licence:

- [Depth Anything V2 Small](https://huggingface.co/apple/coreml-depth-anything-v2-small) — Apache-2.0

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model** | menu | depthanythingv2smallf16_mlpackage | Depth Anything V2 Small, Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Fit Mode** | menu | Stretch | Stretch, Letterbox (pad), Crop (fill) |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | All | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |
| **Result Mode** | menu | Auto | Auto, Segmentation, Raw Float |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Normalize Output** | toggle | True |  |
| **Async Mode** | toggle | True |  |

