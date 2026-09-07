# Face Landmarks

*CHOP · v0.3.1*

<!-- screenshot: drop a PNG at docs/images/face_landmarks.png and rerun the generator -->

Face detection with per-region landmark points — eyes, pupils, brows, nose, lips and the face contour — as channels you can drive geometry or parameters with.

## Inputs

An image, wired in or set as **Source**.

## Outputs

Channels prefixed `face_`, one sample per landmark point.

## Worth knowing

- Each region has its own toggle; turning regions off reduces the sample count, so downstream indices move.

## Parameters

### Face

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Max Faces** | number | 3 |  |
| **Body Pose CHOP** | CHOP |  |  |
| **Track Eyes** | toggle | True |  |
| **Track Brows** | toggle | True |  |
| **Track Nose** | toggle | True |  |
| **Track Lips** | toggle | True |  |
| **Track Contour** | toggle | False |  |
| **Pitch Bias (°)** | number | 0.0 |  |
| **Hold Frames** | number | 12 |  |
| **Min Confidence** | number | 0.1 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

## Python

Reachable on the operator via its extension:

- `FaceCount`
- `GetFaces`

