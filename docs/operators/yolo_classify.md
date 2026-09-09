# YOLO Classify

*TOP · v0.4.5*

<!-- screenshot: drop a PNG at docs/images/yolo_classify.png and rerun the generator -->

Whole-image classification with a YOLO classifier.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A ranked label table.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [Ultralytics YOLO11 classify](https://docs.ultralytics.com/tasks/classify/) — the ImageNet-1k classifier and custom training

Models it downloads through the Model Manager, each under its own licence:

- [YOLO11 nano (classify)](https://github.com/ultralytics/ultralytics) — AGPL-3.0

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model** | menu | yolo11n_cls_mlpackage | YOLO11 nano (classify), Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | Cpuane | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |

### Classify

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Min Confidence** | number | 0.02 |  |
| **Max Results** | number | 100 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

## Python

Reachable on the operator via its extension:

- `DoCallback`
- `GetClasses`
- `TopClass`
- `TopConfidence`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onClassChange`

