# Depth Map

*TOP · v0.2.3*

<!-- screenshot: drop a PNG at docs/images/depth_map.png and rerun the generator -->

Estimates depth from a single ordinary image — no depth camera. Good for parallax, fog, displacement and depth-of-field.

> **Needs a model.** The operator says so on the node and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A depth image. Values are relative, not metres — see **Depth Metric** if you need real distance.

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
| **Result Mode** | menu | Auto | Auto, Segmentation, Raw Float |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Normalize Output** | toggle | True |  |
| **Async Mode** | toggle | True |  |

