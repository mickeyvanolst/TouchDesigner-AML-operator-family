# YOLO Pose

*TOP · v0.5.3*

<!-- screenshot: drop a PNG at docs/images/yolo_pose.png and rerun the generator -->

Multi-person skeletons (17 keypoints) with track IDs, and an OpenPose-style render for feeding ControlNet.

> **Needs a model.** The operator says so on the node and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A visualisation, a keypoint table, and optionally an OpenPose render.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
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

