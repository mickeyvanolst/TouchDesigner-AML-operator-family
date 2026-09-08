# Subject Mask

*TOP · v0.2.0*

<!-- screenshot: drop a PNG at docs/images/subject_mask.png and rerun the generator -->

Apple's lift-the-subject segmentation: every salient object, not just people, cut from the background. The same thing the Photos app does when you long-press a subject.

## Inputs

An image.

## Outputs

A soft mask at the input resolution. Or a **cut-out**: the source with the subject kept and everything else transparent, premultiplied, ready for an Over TOP with no extra operators.

## Worth knowing

- With no subject in frame the mask is entirely black — that is the honest answer, not a failure.

## Parameters

### Mask

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Instance** | number | 0 |  |
| **Visualization** | menu | Mask | Mask, Heatmap, Overlay, Cut-out |
| **Threshold** | number | 0.5 |  |
| **Overlay Alpha** | number | 0.7 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

