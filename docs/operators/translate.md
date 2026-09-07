# Translate

*CHOP · v0.1.3*

<!-- screenshot: drop a PNG at docs/images/translate.png and rerun the generator -->

On-device translation between 22 languages, with automatic detection of the source language.

## Inputs

Text as a parameter, or a DAT of text.

## Outputs

The translation, plus status and timing channels.

## Worth knowing

- **Not realtime.** About a second per translation.
- Language packs are the ones macOS has installed — a missing pair is reported rather than failing quietly.

## Parameters

### Translate

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Enable** | toggle | True |  |
| **Text** | text |  |  |
| **Text DAT** | DAT |  |  |
| **Source Language** | StrMenu | auto | Detect the language, Arabic  (ar), Chinese  (zh), Danish  (da), Dutch  (nl), English  (en), French  (fr), German  (de), … |
| **Target Language** | StrMenu | es | Arabic  (ar), Chinese  (zh), Danish  (da), Dutch  (nl), English  (en), French  (fr), German  (de), Hindi  (hi), … |
| **Translate** | button |  |  |
| **Translate On Text Change** | toggle | True |  |
| **List Languages** | toggle | False |  |

## Python

Reachable on the operator via its extension:

- `Available`
- `Busy`
- `DoCallback`
- `Languages`
- `LastError`
- `LastMs`
- `Pair`
- `Text`
- `Translate`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onTranslated`

