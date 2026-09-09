# YOLO Detect

*TOP · v0.5.4*

<!-- screenshot: drop a PNG at docs/images/yolo_detect.png and rerun the generator -->

Object detection with boxes, labels and persistent track IDs, using Ultralytics YOLO models.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A visualisation plus a table of detections.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [Ultralytics YOLO26](https://docs.ultralytics.com/models/yolo26/) — the detector and its 80 COCO classes
- [Ultralytics export to Core ML](https://docs.ultralytics.com/integrations/coreml/) — how custom-trained models are exported

Models it downloads through the Model Manager, each under its own licence:

- [YOLO26 nano (detect + segment)](https://github.com/ultralytics/ultralytics) — AGPL-3.0

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model** | menu | yolo26n_seg_mlpackage | YOLO26 nano (detect + segment), Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | Cpuane | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |

### Detection

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Min Confidence** | number | 0.25 |  |
| **Max Detections** | number | 100 |  |
| **NMS IoU Threshold** | number | 0.45 |  |
| **Track IDs** | toggle | True |  |
| **Track Hold Frames** | number | 30 |  |
| **Class Filter** | text |  |  |

### Visualization

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Overlay Alpha** | number | 0.5 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

## Python

Reachable on the operator via its extension:

- `Count`
- `DoCallback`
- `GetDetections`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onCountChange`

