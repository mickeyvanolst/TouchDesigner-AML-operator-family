# Pose Tracker

*CHOP · v0.6.1*

<!-- screenshot: drop a PNG at docs/images/pose_tracker.png and rerun the generator -->

Tracks people in an image: body position, 19 body joints, both hands with 21 joints each, face landmarks, and hand gestures — all from one pass over the frame, with no model to download. It is the operator to reach for when you want a body to drive something.

## Inputs

An image, wired into the first input or set as **Source**.

## Outputs

Channels, one sample per person slot. Body and hand channels are prefixed `pose_`, face landmarks `face_` — so `pose*` in a Select CHOP gets you everything about bodies and `face*` everything about faces. With **Detect 3D Pose** on, the member also emits the skeleton as geometry on `out_pose3d`: a point per joint carrying `P` in metres, and one line per bone.

## Worth knowing

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
- `GetJoints`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onPeopleChange`

