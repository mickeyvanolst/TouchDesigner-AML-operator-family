# Semantic Segmentation

*TOP · v0.2.4*

<!-- screenshot: drop a PNG at docs/images/semantic_segmentation.png and rerun the generator -->

Labels every pixel with a class — person, car, road, and so on — as a coloured map, an overlay or a single-class matte.

> **Needs a model.** The operator says so on the node and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A class map, overlay or binary mask.

## Worth knowing

- **Selected Class** with the single-class visualisation is how you get a matte for one thing.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
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
| **Selected Class** | StrMenu | 15 | background  (100.0%) |
| **Overlay Alpha** | number | 0.6 |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 2 |  |
| **Async Mode** | toggle | True |  |

