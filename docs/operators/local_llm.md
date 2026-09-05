# Local LLM

*CHOP · v0.2.1*

<!-- screenshot: drop a PNG at docs/images/local_llm.png and rerun the generator -->

Apple Intelligence's on-device language model: a prompt in, streamed text out. Supports a persistent chat session and structured output described by a table.

## Inputs

A prompt parameter or a DAT.

## Outputs

Streamed text, progress and timing channels.

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

