# Depth Metric

*TOP · v0.2.3*

<!-- screenshot: drop a PNG at docs/images/depth_metric.png and rerun the generator -->

Apple's Depth Pro: depth in **real metres** from one image, with no camera intrinsics, plus the estimated focal length. This is what you want for camera reprojection or anything at real-world scale.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image.

## Outputs

A metric depth map, plus `focal_px` as a channel.

## Worth knowing

- **Not a realtime operator.** It runs at roughly 3-4 s per frame on Apple silicon, against about 48 ms for Depth Map beside it. Drive it on demand, or raise Process Interval — a camera wired straight in will look broken when it is only slow.
- Result Mode is pinned to Raw Tensor on purpose: normalising the output would throw away the metres, which are the whole point.
- **Fit Mode** changes the answer — stretching matches the model's own reference behaviour; letterboxing reads a different distance because it changes the apparent field of view.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Model** | menu | depthprometric1024_mlpackage | Depth Pro (metric depth)  (not installed), Custom file... |
| **Model Path** | file |  |  |
| **Model Status** | text |  |  |
| **Fit Mode** | menu | Stretch | Stretch, Letterbox (pad), Crop (fill) |
| **Manage Models** | button |  |  |
| **Compute Units** | menu | All | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

