# CoreML Data

*CHOP · v0.1.5*

<!-- screenshot: drop a PNG at docs/images/coreml_data.png and rerun the generator -->

The same idea as CoreML Model, for models that take numbers instead of pictures — embeddings, regressors, audio models, classifiers. Recurrent state loops itself.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

Up to four CHOPs, fed to the model's inputs in alphabetical order.

## Outputs

Channels, one per output value.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [MLModel](https://developer.apple.com/documentation/coreml/mlmodel) — the model file this operator loads
- [MLMultiArray](https://developer.apple.com/documentation/coreml/mlmultiarray) — how CHOP channels reach the model

## Worth knowing

- Image-input models are refused with a pointer to CoreML Model.

## Parameters

### Model

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Model Path** | file |  |  |
| **Compute Units** | StrMenu |  | All (Auto), CPU + Neural Engine, CPU + GPU, CPU Only |
| **Reload Model** | button |  |  |
| **Output Name** | StrMenu |  | (auto) |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Async Mode** | toggle | True |  |

