# Speech to Text

*CHOP · v0.2.6*

<!-- screenshot: drop a PNG at docs/images/speech_text.png and rerun the generator -->

Live speech recognition from an audio CHOP, on-device.

## Inputs

Audio, wired in.

## Outputs

Channels for activity and counts, and a table of utterances with the live partial hypothesis.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Speech framework](https://developer.apple.com/documentation/speech) — Apple's speech recognition
- [SFSpeechRecognizer](https://developer.apple.com/documentation/speech/sfspeechrecognizer) — locales, on-device support, the server task limit
- [requiresOnDeviceRecognition](https://developer.apple.com/documentation/speech/sfspeechrecognitionrequest/requiresondevicerecognition) — what On-Device Only switches

## Worth knowing

- The first use asks permission once, attributed to a bundled helper — TouchDesigner itself is never modified.
- On-device recognition needs the dictation model for your language to be downloaded in System Settings.

## Parameters

### Speech

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Audio CHOP** | CHOP |  |  |
| **Enable** | toggle | False |  |
| **Language** | StrMenu |  | ar-SA, ca-ES, cs-CZ, da-DK, de-AT, de-CH, de-DE, el-GR, … |
| **On-Device Only** | toggle | True |  |
| **Add Punctuation** | toggle | True |  |
| **Task Hint** | menu | Unspecified | Unspecified, Dictation, Search, Confirmation |
| **Context Strings** | text |  |  |
| **Utterance Hold (s)** | number | 1.5 |  |
| **Max Utterances** | number | 20 |  |
| **Clear Transcript** | button |  |  |
| **Restart Session** | button |  |  |

## Python

Reachable on the operator via its extension:

- `Active`
- `Clear`
- `DoCallback`
- `Partial`
- `Restart`
- `Transcript`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onUtterance`

