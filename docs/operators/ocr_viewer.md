# OCR / Text Recognition

*TOP · v0.3.0*

<!-- screenshot: drop a PNG at docs/images/ocr_viewer.png and rerun the generator -->

Reads text in an image, with position for each piece of text so you can draw over it or track it.

## Inputs

An image.

## Outputs

A table of recognised strings with confidence and bounds.

## Worth knowing

- **Recognition Level** trades speed against accuracy; the language list matters for accented text.

## Parameters

### Recognize

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Max Results** | number | 10 |  |
| **Min Confidence** | number | 0.01 |  |
| **Recognition Level** | menu | Accurate | Accurate, Fast |
| **Language** | menu | EnUs | English, French, German, Spanish, Italian, Portuguese, Chinese (Simplified), Chinese (Traditional), … |
| **Source TOP** | TOP |  |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

## Python

Reachable on the operator via its extension:

- `DoCallback`
- `GetLines`
- `GetText`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onTextChange`

