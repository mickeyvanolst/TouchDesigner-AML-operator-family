# Translate

*CHOP · v0.1.5*

<!-- screenshot: drop a PNG at docs/images/translate.png and rerun the generator -->

On-device translation between 22 languages, with automatic detection of the source language.

## Inputs

Text as a parameter, or a DAT of text.

## Outputs

The translation, plus status and timing channels.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Translation framework](https://developer.apple.com/documentation/translation) — Apple's on-device translation (macOS 26)
- [TranslationSession](https://developer.apple.com/documentation/translation/translationsession) — the languages and the installed-pack rule
- [NLLanguageRecognizer](https://developer.apple.com/documentation/naturallanguage/nllanguagerecognizer) — detects the source language

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

