# Sound Classify

*CHOP · v0.1.1*

<!-- screenshot: drop a PNG at docs/images/sound_classify.png and rerun the generator -->

Recognises 303 everyday sounds — applause, laughter, sirens, glass breaking — from an audio CHOP, with no model download.

## Inputs

Audio.

## Outputs

Ranked classes as channels, plus a stable channel per sound you name in the watch list.

## Worth knowing

- A result lands roughly every window x (1 - overlap) seconds, so channels hold between results rather than flickering.

## Parameters

### Sound

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source CHOP** | CHOP |  |  |
| **Enable** | toggle | True |  |
| **Window** | number | 3.0 |  |
| **Overlap** | number | 0.5 |  |
| **Min Confidence** | number | 0.05 |  |
| **Ranked Channels** | number | 5 |  |
| **Watch List** | text |  |  |
| **List All Classes** | toggle | False |  |

## Python

Reachable on the operator via its extension:

- `Confidence`
- `DoCallback`
- `Hearing`
- `Listening`
- `Sounds`
- `Top`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onSound`

