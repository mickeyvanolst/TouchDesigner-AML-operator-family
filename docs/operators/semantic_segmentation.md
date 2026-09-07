# Semantic Segmentation

*TOP · v0.4.1*

<!-- screenshot: drop a PNG at docs/images/semantic_segmentation.png and rerun the generator -->

Labels every pixel with a class — person, car, road, and so on — as a coloured map, an overlay or a single-class matte.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A class map, overlay or binary mask, and **out_segnames** — the classes actually present in the frame as a table of class id, name, pixel count and coverage.

## Worth knowing

- **Selected Class** with the single-class visualisation is how you get a matte for one thing.
- Three models, three vocabularies: **DeepLab V3** (21 PASCAL VOC classes), **DETR ResNet-50** (133 COCO-panoptic classes, including sky, road and grass) and **Face Parsing** (19 facial classes). Class names come from the model itself where it ships them, which is why DETR reports `sky (other)` rather than `class 119`.
- **Face Parsing wants a face, not a scene.** It is trained on tight portrait crops, so a wide camera frame with a small head in it comes back as noise rather than facial features. Crop to the face first — the bounding box from Face Detect is a good source — and keep that crop square: the input is scaled to the model's square input, so a 16:9 crop reaches the model squashed.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model** | menu | deeplabv3fp16_mlmodel | DeepLab V3 (segmentation), DETR ResNet-50 (segmentation), Face parsing (19 classes), Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | All | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |
| **Result Mode** | menu | Segmentation | Auto, Segmentation, Raw Float |

### Segmentation

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Visualization** | menu | Coloured | Coloured, Overlay, Single Class Mask |
| **Palette** | menu | Auto | Auto (match the model), PASCAL VOC (21 classes), Face Parsing (19 classes), From Palette DAT, Generated colours |
| **Palette DAT** | DAT |  |  |
| **Selected Class** | StrMenu | 15 | aeroplane, background, bicycle, bird, boat, bottle, bus, car, … |
| **Overlay Alpha** | number | 0.6 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 2 |  |
| **Async Mode** | toggle | True |  |

