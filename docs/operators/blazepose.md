# BlazePose

*CHOP · v0.1.0*

<!-- screenshot: drop a PNG at docs/images/blazepose.png and rerun the generator -->

MediaPipe's pose model, natively: 33 body joints per person with 2D positions and 3D world coordinates in metres, from a Core ML conversion that runs in about 3 ms. The 3D that Apple's own body pose only gives at 300 ms a frame.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image, wired into the first input or set as **Source**.

## Outputs

`out_body` in the family's pose dialect, one channel block per person: `p1/tracked`, `p1/conf` (the pose flag), `p1/bbox:x/y/w/h` (the crop square), `p1/roi:rotation`, then each of the 33 joints as `p1/wrist_l:x/:y/:conf` and `p1/wrist_l:tx/:ty/:tz` (metres, hips at the origin, y up, z toward the viewer). Joint names are the family's where they coincide (nose, shoulder_l, wrist_r, hip_l, knee_r, ankle_l …) plus MediaPipe's own: eye_inner_l, eye_outer_l, mouth_l, pinky_l, index_l, thumb_l, heel_l, foot_index_l and their right-hand twins. `out_instances` — one sample per joint for instancing. `out_pose3d` — the 3D skeleton as geometry (a point per joint, a line per bone, `conf` on the points). `out_overlay` and `out_pose` (OpenPose render) as on Pose Tracker.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [MediaPipe Pose Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker) — Google's BlazePose GHUM model and its 33 landmarks
- [BlazePose GHUM 3D](https://arxiv.org/abs/2206.11678) — the paper behind the 3D world coordinates
- [VNDetectHumanRectanglesRequest](https://developer.apple.com/documentation/vision/vndetecthumanrectanglesrequest) — seeds the first crop of each person

Models it downloads through the Model Manager, each under its own licence:

- [BlazePose lite](https://huggingface.co/mickeyvanolst/blazepose-coreml) — Apache-2.0
- [BlazePose full](https://huggingface.co/mickeyvanolst/blazepose-coreml) — Apache-2.0
- [BlazePose heavy](https://huggingface.co/mickeyvanolst/blazepose-coreml) — Apache-2.0

## Worth knowing

- How it tracks: Vision finds people (a human rectangle) only to seed a crop; from then on every frame's crop comes from the previous landmarks, exactly as MediaPipe does. A person whose pose flag drops under Min Confidence is held for Hold Frames, then the slot is freed and Vision looks again every Detect Interval frames.
- 3D is root-relative: every person's hips sit at the origin, and scale comes from a learned body prior, not a measurement. Bone lengths are metric; absolute distance to the camera is not.
- Three models, same channels: full (default, 2.6 ms on the Neural Engine), lite (faster on weak machines), heavy (most accurate, ~4 ms on CPU + Neural Engine). Pick one in the Model menu.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Model** | menu | blazepose_coreml_poselandmarks_full_mlpa | BlazePose full, BlazePose lite, BlazePose heavy, Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | All | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload** | button |  |  |

### Pose

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Active** | toggle | True |  |
| **Max People** | number | 1 |  |
| **Min Confidence** | number | 0.5 |  |
| **Hold Frames** | number | 12 |  |
| **Detect Interval** | number | 10 |  |
| **ROI Scale** | number | 1.25 |  |
| **ROI Growth Per Frame** | number | 0.1 |  |
| **OpenPose Render Out** | toggle | False |  |
| **OpenPose Render Size** | number | 512 |  |

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
- `GetBox`
- `GetJoints`
- `IsTracked`
- `People`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onPeopleChange`

