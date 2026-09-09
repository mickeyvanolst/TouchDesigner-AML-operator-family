# Speech Synth

*CHOP · v0.2.6*

<!-- screenshot: drop a PNG at docs/images/speech_synth.png and rerun the generator -->

Text to speech, rendered faster than realtime, with per-word timing you can animate to.

## Inputs

A DAT (optional): its text is spoken instead of the Text parameter, rows joined with newlines. Text DAT does the same by reference.

## Outputs

48 kHz mono audio plus word-timing channels.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [AVSpeechSynthesizer](https://developer.apple.com/documentation/avfaudio/avspeechsynthesizer) — the synthesizer
- [AVSpeechSynthesisVoice](https://developer.apple.com/documentation/avfaudio/avspeechsynthesisvoice) — the voices, and where the better ones are downloaded

## Worth knowing

- The Voice menu lists the voices macOS has installed for the chosen language. Enhanced and premium voices are downloaded in System Settings > Accessibility > Spoken Content > System Voice > Manage Voices and appear here marked (enhanced) or (premium); Siri voices are not available to apps.

## Parameters

### Synth

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Text** | text |  |  |
| **Text DAT** | DAT |  |  |
| **Speak** | button |  |  |
| **Speak On Text Change** | toggle | False |  |
| **While Speaking** | menu | Queue | Queue Utterance, Interrupt & Replace |
| **Stop** | button |  |  |
| **Voice** | StrMenu |  | Default, Samantha, Ava (Premium), Eddy, Flo, Grandma, Grandpa, Reed, … |
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

