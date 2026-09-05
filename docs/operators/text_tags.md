# Text Tags

*CHOP · v0.2.1*

<!-- screenshot: drop a PNG at docs/images/text_tags.png and rerun the generator -->

Turns a piece of text into tags, using the on-device language model.

## Inputs

Text.

## Outputs

The tags, as a table.

## Worth knowing

- **Not realtime.** A second or two per request.

## Parameters

### Tags

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Text** | text |  |  |
| **Text DAT** | DAT |  |  |
| **Tag** | button |  |  |
| **Tag On Text Change** | toggle | False |  |
| **While Busy** | menu | Interrupt | Queue Request, Interrupt & Replace, Ignore |
| **Stop** | button |  |  |

## Python

Reachable on the operator via its extension:

- `DoCallback`
- `GetTags`
- `Sentiment`
- `Tag`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onTags`

