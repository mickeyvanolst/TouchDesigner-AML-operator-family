# CoreML Data

*CHOP · v0.1.0*

<!-- screenshot: drop a PNG at docs/images/coreml_data.png and rerun the generator -->

The same idea as CoreML Model, for models that take numbers instead of pictures — embeddings, regressors, audio models, classifiers. Recurrent state loops itself.

> **Needs a model.** The operator says so on the node and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

Up to four CHOPs, fed to the model's inputs in alphabetical order.

## Outputs

Channels, one per output value.

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

