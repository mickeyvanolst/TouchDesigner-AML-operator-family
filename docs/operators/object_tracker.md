# Object Tracker

*TOP · v0.3.5*

<!-- screenshot: drop a PNG at docs/images/object_tracker.png and rerun the generator -->

Follows things across frames and gives each one a persistent ID, so you can tell that the person at the left of this frame is the same person who was in the middle of the last one.

## Inputs

A moving image. Stills give it nothing to track.

## Outputs

A passthrough image plus a table of tracks: id, label, position, size, confidence and age.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Vision framework](https://developer.apple.com/documentation/vision) — Apple's on-device image analysis
- [VNDetectHumanRectanglesRequest](https://developer.apple.com/documentation/vision/vndetecthumanrectanglesrequest) — seeds tracks from people
- [VNRecognizeAnimalsRequest](https://developer.apple.com/documentation/vision/vnrecognizeanimalsrequest) — seeds tracks from animals
- [VNTrackObjectRequest](https://developer.apple.com/documentation/vision/vntrackobjectrequest) — follows each seed across frames
- [VNSequenceRequestHandler](https://developer.apple.com/documentation/vision/vnsequencerequesthandler) — keeps the tracks between frames

## Worth knowing

- Seeds from people, animals or a table you supply.

## Parameters

### ObjectTrack

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Max Objects** | number | 5 |  |
| **Min Confidence** | number | 0.3 |  |
| **Hold Frames** | number | 30 |  |
| **Track Level** | menu | Accurate | Accurate, Fast |
| **Seed Source** | menu | Person | Person, Animal, Input DAT |
| **Seed DAT** | DAT |  |  |
| **Seed Mode** | menu | Auto | Auto (periodic), Manual (pulse) |
| **Reseed Interval** | number | 30 |  |
| **Seed Now** | button |  |  |
| **Reset Tracker** | button |  |  |
| **Source** | TOP |  |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Async Mode** | toggle | True |  |

## Python

Reachable on the operator via its extension:

- `Count`
- `DoCallback`
- `GetTracks`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onTrackNew`
- `onTrackLost`

