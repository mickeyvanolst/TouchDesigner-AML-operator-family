# YOLO Pose

*TOP · v0.6.6*

<!-- screenshot: drop a PNG at docs/images/yolo_pose.png and rerun the generator -->

Multi-person skeletons (17 keypoints) with track IDs, and an OpenPose-style render for feeding ControlNet.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A visualisation, a keypoint table, and optionally an OpenPose render.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [Ultralytics YOLO11 pose](https://docs.ultralytics.com/tasks/pose/) — the 17 COCO keypoints

Models it downloads through the Model Manager, each under its own licence:

- [YOLO11 nano (pose)](https://github.com/ultralytics/ultralytics) — AGPL-3.0

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model** | menu | yolo11n_pose_mlpackage | YOLO11 nano (pose), Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | Cpuane | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |
| **Use Keypoint Map** | toggle | False |  |

### Detection

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Min Confidence** | number | 0.25 |  |
| **Max Detections** | number | 100 |  |
| **NMS IoU Threshold** | number | 0.45 |  |
| **Track IDs** | toggle | True |  |
| **Track Hold Frames** | number | 30 |  |
| **OpenPose Render Out** | toggle | False |  |
| **OpenPose Render Size** | number | 512 |  |

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

- `ActivePeople`
- `DoCallback`
- `GetJoints`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onPeopleChange`

