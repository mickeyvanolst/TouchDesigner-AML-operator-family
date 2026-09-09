# Saliency

*TOP · v0.2.6*

<!-- screenshot: drop a PNG at docs/images/saliency.png and rerun the generator -->

Where a viewer would look. Attention saliency predicts gaze; objectness saliency highlights whole objects. Useful for automatic cropping, framing and attention-driven effects.

## Inputs

An image.

## Outputs

A heatmap, mask or overlay.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Vision framework](https://developer.apple.com/documentation/vision) — Apple's on-device image analysis
- [VNGenerateAttentionBasedSaliencyImageRequest](https://developer.apple.com/documentation/vision/vngenerateattentionbasedsaliencyimagerequest) — where the eye goes
- [VNGenerateObjectnessBasedSaliencyImageRequest](https://developer.apple.com/documentation/vision/vngenerateobjectnessbasedsaliencyimagerequest) — where the objects are

## Parameters

### Mask

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Mode** | menu | Attention | Attention (where the eye goes), Objectness (where things are) |
| **Visualization** | menu | Heatmap | Mask, Heatmap, Overlay |
| **Threshold** | number | 0.5 |  |
| **Overlay Alpha** | number | 0.7 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 2 |  |
| **Async Mode** | toggle | True |  |

