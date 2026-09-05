# YOLO Classify

*TOP · v0.3.3*

<!-- screenshot: drop a PNG at docs/images/yolo_classify.png and rerun the generator -->

Whole-image classification with a YOLO classifier.

> **Needs a model.** The operator says so on the node and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A ranked label table.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | Cpuane | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |

### Classify

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Min Confidence** | number | 0.02 |  |
| **Max Results** | number | 100 |  |

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
- `GetClasses`
- `TopClass`
- `TopConfidence`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onClassChange`

