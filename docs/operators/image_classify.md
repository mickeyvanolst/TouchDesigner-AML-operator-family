# Image Classify

*TOP · v0.3.2*

<!-- screenshot: drop a PNG at docs/images/image_classify.png and rerun the generator -->

Names what is in a picture, using Apple's built-in classifier — no model download.

## Inputs

An image.

## Outputs

A ranked table of labels with confidences.

## Parameters

### Recognize

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Mode** | menu | Classify | Image Classification, Text Recognition |
| **Max Results** | number | 10 |  |
| **Min Confidence** | number | 0.01 |  |
| **Recognition Level** | menu | Accurate | Accurate, Fast |
| **Language** | menu | EnUs | English, French, German, Spanish, Italian, Portuguese, Chinese (Simplified), Chinese (Traditional), … |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 15 |  |
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

