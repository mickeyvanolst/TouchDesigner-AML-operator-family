# Person Mask

*TOP · v0.2.4*

<!-- screenshot: drop a PNG at docs/images/person_mask.png and rerun the generator -->

Separates people from the background. Apple's person segmentation, with a quality setting, plus a mode that returns up to four people as separate masks rather than one combined matte.

## Inputs

An image.

## Outputs

A mask, heatmap or overlay, depending on **Visualization**.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Vision framework](https://developer.apple.com/documentation/vision) — Apple's on-device image analysis
- [VNGeneratePersonSegmentationRequest](https://developer.apple.com/documentation/vision/vngeneratepersonsegmentationrequest) — the person mask
- [VNGeneratePersonInstanceMaskRequest](https://developer.apple.com/documentation/vision/vngeneratepersoninstancemaskrequest) — one mask per person (macOS 14+)

## Worth knowing

- **Separate People** gives each person their own mask; `Instance` 0 is everyone, N is the Nth person.

## Parameters

### Mask

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Instance** | number | 0 |  |
| **Quality** | menu | Balanced | Fast, Balanced, Accurate |
| **Visualization** | menu | Mask | Mask, Heatmap, Overlay |
| **Threshold** | number | 0.5 |  |
| **Overlay Alpha** | number | 0.7 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

