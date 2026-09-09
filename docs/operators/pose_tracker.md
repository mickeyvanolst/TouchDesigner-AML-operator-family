# Pose Tracker

*CHOP · v0.8.3*

<!-- screenshot: drop a PNG at docs/images/pose_tracker.png and rerun the generator -->

Tracks people in an image: body position, 19 body joints, both hands with 21 joints each, face landmarks, and hand gestures — all from one pass over the frame, with no model to download. It is the operator to reach for when you want a body to drive something.

## Inputs

An image, wired into the first input or set as **Source**.

## Outputs

Two CHOP outputs. `out_channels` carries the body and hand channels, prefixed `pose_`, one sample per person slot. `out_faces` carries the face landmarks, prefixed `face_`, one sample per landmark point — their own output because the sample count is Max Faces × 87, which would otherwise pad every body channel out to that length. With **Detect 3D Pose** on, the member also emits the skeleton as geometry on `out_pose3d`: a point per joint carrying `P` in metres, and one line per bone.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Vision framework](https://developer.apple.com/documentation/vision) — Apple's on-device image analysis
- [VNDetectHumanBodyPoseRequest](https://developer.apple.com/documentation/vision/vndetecthumanbodyposerequest) — 19 body joints
- [VNDetectHumanHandPoseRequest](https://developer.apple.com/documentation/vision/vndetecthumanhandposerequest) — 21 joints per hand
- [VNDetectFaceLandmarksRequest](https://developer.apple.com/documentation/vision/vndetectfacelandmarksrequest) — face landmarks
- [VNDetectHumanRectanglesRequest](https://developer.apple.com/documentation/vision/vndetecthumanrectanglesrequest) — body bounding boxes
- [VNDetectHumanBodyPose3DRequest](https://developer.apple.com/documentation/vision/vndetecthumanbodypose3drequest) — 3D joints in metres (macOS 14+)

## Worth knowing

- Face landmarks come from the same Vision request the separate Face Landmarks operator used to run — that operator was folded into this one, and its `GetFaces()` and `FaceCount` are available here. For face work alone, turn Detect Body, Detect Pose and Detect Hands off: the pose request is then skipped entirely and the cost matches the old dedicated operator (measured 5.9 ms against 6.1 ms).
- Face landmarks produce far more samples than people — `numSamples` is `max(Max People, Max Faces x points-per-face)`, which is 261 with faces on. Read the person count from **Max People**, never from the sample count.
- 3D pose is expensive (~300 ms against ~12 ms for everything else) so it runs on its own queue: 2D tracking stays at full rate while the skeleton refreshes a few times a second.
- A channel that is not being produced reads as `None`. Guard any expression that indexes one, or turning a toggle off will put your own nodes into error.

## Parameters

### Face

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Detect Face** | toggle | True |  |
| **Max Faces** | number | 3 |  |
| **Track Eyes** | toggle | True |  |
| **Track Brows** | toggle | True |  |
| **Track Nose** | toggle | True |  |
| **Track Lips** | toggle | True |  |
| **Track Contour** | toggle | False |  |
| **Pitch Bias (°)** | number | 0.0 |  |

### Pose

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Detect Body** | toggle | True |  |
| **Detect Pose** | toggle | True |  |
| **Detect 3D Pose** | toggle | False |  |
| **3D Compute** | menu | Auto | Auto (Vision decides), Neural Engine, GPU |
| **Detect Hands** | toggle | False |  |
| **Detect Gestures** | toggle | False |  |
| **Max People** | number | 5 |  |
| **Gesture Hold Frames** | number | 3 |  |
| **Hold Frames** | number | 12 |  |
| **Min Confidence** | number | 0.1 |  |
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
- `FaceCount`
- `GetFaces`
- `GetJoints`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onPeopleChange`

