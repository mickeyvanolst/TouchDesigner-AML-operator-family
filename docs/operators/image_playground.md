# Image Playground

*TOP · v0.2.3*

<!-- screenshot: drop a PNG at docs/images/image_playground.png and rerun the generator -->

Apple's own image generator: a prompt becomes a picture in a few seconds, with nothing to download.

## Inputs

None — the prompt is a parameter.

## Outputs

The generated image.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [ImagePlayground](https://developer.apple.com/documentation/imageplayground) — Apple's image generator (macOS 26)
- [ImageCreator](https://developer.apple.com/documentation/imageplayground/imagecreator) — the styles, the prompt rules and why it needs the app in front

## Worth knowing

- **Not realtime.** Generate-driven, a few seconds per image.
- TouchDesigner must stay the frontmost application while it generates; Apple refuses to generate for a background app.
- Prompts are a short concept, not a sentence, and brand names and real people are refused.

## Parameters

### Playground

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Enable** | toggle | True |  |
| **Prompt** | text |  |  |
| **Style** | menu | Animation | Animation, Illustration, Sketch |
| **Output Size** | menu | S1280 | 1280 (safe on every licence), 1024, 512, Native 1536 (Commercial licence) |
| **Images Per Run** | number | 1 |  |
| **Generate** | button |  |  |
| **Clear** | button |  |  |
| **Generate On Prompt Change** | toggle | False |  |
| **Image File Type** | menu | png | PNG, JPEG, TIFF, EXR |
| **Unique Suffix** | toggle | False |  |
| **N** | number | 0 |  |
| **Save Path** | FileSave |  |  |
| **Save** | button |  |  |

