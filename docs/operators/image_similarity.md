# Image Similarity

*CHOP · v0.3.4*

<!-- screenshot: drop a PNG at docs/images/image_similarity.png and rerun the generator -->

How alike two images are, using Vision's feature prints — a perceptual distance rather than a pixel difference.

## Inputs

Two images.

## Outputs

A distance value as a channel.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Vision framework](https://developer.apple.com/documentation/vision) — Apple's on-device image analysis
- [VNGenerateImageFeaturePrintRequest](https://developer.apple.com/documentation/vision/vngenerateimagefeatureprintrequest) — the feature print two images are compared by
- [VNDetectFaceCaptureQualityRequest](https://developer.apple.com/documentation/vision/vndetectfacecapturequalityrequest) — face capture quality

## Parameters

### Similarity

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Reference TOP** | TOP |  |  |
| **Reference Index** | number | 0 |  |
| **Manual Array Size** | number | 0 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Async Mode** | toggle | True |  |
| **Realtime Update** | toggle | True |  |
| **Manual Update** | button |  |  |

## Python

Reachable on the operator via its extension:

- `FaceQuality`
- `Similarity`

