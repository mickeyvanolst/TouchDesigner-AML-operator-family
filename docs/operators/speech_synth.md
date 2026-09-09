# Speech Synth

*CHOP · v0.2.3*

<!-- screenshot: drop a PNG at docs/images/speech_synth.png and rerun the generator -->

Text to speech, rendered faster than realtime, with per-word timing you can animate to.

## Inputs

None — the text is a parameter.

## Outputs

48 kHz mono audio plus word-timing channels.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [AVSpeechSynthesizer](https://developer.apple.com/documentation/avfaudio/avspeechsynthesizer) — the synthesizer
- [AVSpeechSynthesisVoice](https://developer.apple.com/documentation/avfaudio/avspeechsynthesisvoice) — the voices, and where the better ones are downloaded

## Parameters

### Synth

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Text** | text |  |  |
| **Speak** | button |  |  |
| **Speak On Text Change** | toggle | False |  |
| **While Speaking** | menu | Queue | Queue Utterance, Interrupt & Replace |
| **Stop** | button |  |  |
| **Voice** | StrMenu |  | Default, Samantha, Eddy, Flo, Grandma, Grandpa, Reed, Rocko, … |
| **Language** | StrMenu |  | ar-001, bg-BG, bn-IN, ca-ES, cs-CZ, da-DK, de-DE, el-GR, … |
| **Rate** | number | 0.5 |  |
| **Pitch** | number | 1.0 |  |
| **Volume** | number | 1.0 |  |

## Python

Reachable on the operator via its extension:

- `DoCallback`
- `Queue`
- `Say`
- `Speaking`
- `Stop`
- `Words`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onWord`
- `onDone`

