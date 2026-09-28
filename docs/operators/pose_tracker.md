# Pose Tracker

*CHOP · v0.8.4*

<!-- screenshot: drop a PNG at docs/images/pose_tracker.png and rerun the generator -->

Tracks people in an image: body position, 19 body joints, both hands with 21 joints each, face landmarks, and hand gestures — all from one pass over the frame, with no model to download. It is the operator to reach for when you want a body to drive something.

## Inputs

An image, wired into the first input or set as **Source**.

## Outputs

Five CHOP outputs, split by what you do with them, all in the Kinect CHOP's dialect: one channel block per person, one sample. `out_body` — `p1/tracked`, `p1/bbox:x/y/w/h`, the 19 joints as `p1/wrist_l:x`, `:y`, `:conf`, and with **Detect 3D Pose** on `p1/tracked3d`, `p1/height` and `p1/<joint>:tx/ty/tz` in metres. `out_hands` — `p1/hand_l:tracked` and the 21 joints per hand as `p1/hand_l_index_tip:x/y/conf`. `out_gestures` — per hand `:gesture`, `:fingers`, `:pinch`, `:pinch_on`, one `:is_fist` / `:is_open` / … channel per gesture, per-finger `:ext` / `:curl`, plus the pinch midpoint and `:pinch_start` / `:pinch_end` pulses. `out_faces` — the face landmarks, prefixed `face_`, one sample per landmark point, with `face_yaw/roll/pitch` and `face_body_index` (0 = person 1). `out_instances` — every body joint as one SAMPLE per point (`x y conf person joint tracked`), the layout a Geometry COMP instances from directly; **Instance Hands** adds the hand joints. `out_pose3d` is the 3D skeleton as geometry (a point per joint in metres, a line per bone) and `out_pose` an OpenPose render.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Vision framework](https://developer.apple.com/documentation/vision) — Apple's on-device image analysis
- [VNDetectHumanBodyPoseRequest](https://developer.apple.com/documentation/vision/vndetecthumanbodyposerequest) — 19 body joints
- [VNDetectHumanHandPoseRequest](https://developer.apple.com/documentation/vision/vndetecthumanhandposerequest) — 21 joints per hand
- [VNDetectFaceLandmarksRequest](https://developer.apple.com/documentation/vision/vndetectfacelandmarksrequest) — face landmarks
- [VNDetectHumanRectanglesRequest](https://developer.apple.com/documentation/vision/vndetecthumanrectanglesrequest) — body bounding boxes
- [VNDetectHumanBodyPose3DRequest](https://developer.apple.com/documentation/vision/vndetecthumanbodypose3drequest) — 3D joints in metres (macOS 14+)

## Worth knowing

- Select by pattern: `p1/*` is one person, `*wrist_l:*` one joint across everybody, `*:conf` every confidence, `*:is_fist` a fist trigger for every hand. Max People adds `p2/`, `p3/` … blocks and changes nothing else. Sides are suffixes (`shoulder_l`), and a joint that exists in 2D and 3D has one name: `p1/wrist_l:x` and `p1/wrist_l:tx` are the same wrist.
- A joint's `:conf` is 0 when it was not detected — scale or gate by it rather than testing for zero coordinates.
- Face landmarks come from the same Vision request the separate Face Landmarks operator used to run — that operator was folded into this one, and its `GetFaces()` and `FaceCount` are available here. For face work alone, turn Detect Body, Detect Pose and Detect Hands off: the pose request is then skipped entirely and the cost matches the old dedicated operator (measured 5.9 ms against 6.1 ms).
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
| **Instance Hands** | toggle | False |  |

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
- `GetBox`
- `GetFaces`
- `GetJoints`
- `IsTracked`
- `People`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onPeopleChange`

