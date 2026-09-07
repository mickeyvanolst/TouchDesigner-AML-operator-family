# YOLO Segment

*TOP · v0.4.3*

<!-- screenshot: drop a PNG at docs/images/yolo_segment.png and rerun the generator -->

Instance segmentation — a mask per detected object rather than one mask per class.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

Coloured masks or an overlay, plus a detection table.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model** | menu | fastsam_s_mlpackage | FastSAM small (segment anything), Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | Cpuane | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |

### Segment

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Min Confidence** | number | 0.45 |  |
| **Max Instances** | number | 300 |  |
| **NMS IoU Threshold** | number | 0.9 |  |
| **Track IDs** | toggle | True |  |
| **Track Hold Frames** | number | 30 |  |

### Visualization

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Visualization** | menu | Instanceoverlay | Coloured Mask, Overlay, Instance Colours, Instance Overlay, Point Mask, Passthrough (Boxes Only) |
| **Select Point X** | number | 0.5 |  |
| **Select Point Y** | number | 0.5 |  |
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

