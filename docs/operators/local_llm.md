# Local LLM

*CHOP · v0.2.6*

<!-- screenshot: drop a PNG at docs/images/local_llm.png and rerun the generator -->

Apple Intelligence's on-device language model: a prompt in, streamed text out. Supports a persistent chat session and structured output described by a table.

## Inputs

A prompt parameter or a DAT.

## Outputs

Streamed text, progress and timing channels.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [FoundationModels](https://developer.apple.com/documentation/foundationmodels) — Apple Intelligence's on-device language model (macOS 26)
- [SystemLanguageModel](https://developer.apple.com/documentation/foundationmodels/systemlanguagemodel) — availability and the reasons it is not
- [Generating with guided output](https://developer.apple.com/documentation/foundationmodels/generating-swift-data-structures-with-guided-generation) — what the Schema DAT builds on

## Worth knowing

- **Not realtime.** Generation takes seconds; the progress and timing channels are there to choreograph around it.
- Requires Apple Intelligence to be enabled; the exact reason is surfaced when it is not.

## Parameters

### LLM

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Prompt** | text |  |  |
| **Prompt DAT** | DAT |  |  |
| **Generate** | button |  |  |
| **Generate On Prompt Change** | toggle | False |  |
| **While Busy** | menu | Queue | Queue Request, Interrupt & Replace, Ignore |
| **Stop** | button |  |  |
| **Mode** | menu | Transform | Transform (stateless), Chat (keeps context) |
| **Clear Context** | button |  |  |
| **Instructions** | text |  |  |
| **Schema DAT** | DAT |  |  |
| **Temperature** | number | 1.0 |  |
| **Max Response Tokens** | number | 0 |  |
| **Permissive Guardrails** | toggle | False |  |

## Python

Reachable on the operator via its extension:

- `Ask`
- `Available`
- `ClearContext`
- `DoCallback`
- `Fields`
- `Generating`
- `LastError`
- `Partial`
- `Response`
- `Stop`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onResponse`
- `onError`

