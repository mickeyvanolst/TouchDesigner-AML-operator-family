# Object Capture

*POP · v0.2.2*

<!-- screenshot: drop a PNG at docs/images/object_capture.png and rerun the generator -->

Apple's photogrammetry: a folder of photographs of one object becomes a real textured mesh. Slower than Geo Gen and far more accurate, because it is measuring rather than imagining.

## Inputs

A folder of photographs (a parameter, not a wire).

## Outputs

Mesh geometry plus baked albedo, normal and occlusion maps.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [RealityKit Object Capture](https://developer.apple.com/documentation/realitykit/realitykit-object-capture) — Apple's photogrammetry, and how to shoot for it
- [PhotogrammetrySession](https://developer.apple.com/documentation/realitykit/photogrammetrysession) — the session behind Generate: detail levels, ordering, sensitivity
- [Model I/O](https://developer.apple.com/documentation/modelio) — reads the USDZ back into geometry

## Worth knowing

- **Photos from a DAT.** Wire a table of image paths into the DAT input — a list you curated, or a Folder DAT pointed at the shots — and it is used instead of Photo Folder, which greys out while the input is wired.
- **Status** is a read-only parameter: the stage and progress while capturing, `done 255.3 s` after, `idle` before — no DAT needed to watch it.
- **Export** writes `.obj` (with MTL and maps as PNG), `.usdz` (Apple's own file), or TouchDesigner's `.pop` / `.tog` with albedo, normal and occlusion maps as PNG beside it. From Python: `Export(path)`; `onExported` lists what was written.
- **Not realtime.** A capture runs for tens of seconds to minutes, dominated by aligning the photographs rather than by the detail setting.
- Timing is dominated by alignment, not by the detail setting.
- Captures arrive in real-world metres; scale and centre are applied on the way out so they stay adjustable.

## Parameters

### Object Capture

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Enable** | toggle | True |  |
| **Photo Folder** | folder |  |  |
| **Detail** | menu | Reduced | Preview (fastest), Reduced, Medium, Full, Raw (no decimation) |
| **Max Polygons** | number | 50000 |  |
| **Texture Size** | menu | S1024 | 1024, 2048, 4096, 8192 |
| **Photos In Order** | toggle | False |  |
| **High Feature Sensitivity** | toggle | False |  |
| **Generate** | button |  |  |
| **Cancel** | button |  |  |
| **Model File** | FileSave |  |  |
| **Reload** | button |  |  |
| **Object File Type** | menu | obj | OBJ, POP |
| **Export File** | FileSave |  |  |
| **Export** | button |  |  |
| **Status** | text |  |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Scale** | number | 1.0 |  |
| **Center** | menu | Ground | As Captured, Bounds Centre, On The Ground |

## Python

Reachable on the operator via its extension:

- `Busy`
- `Cancel`
- `DoCallback`
- `Eta`
- `Export`
- `Generate`
- `LastError`
- `LastMs`
- `MAPS`
- `MapPath`
- `ModelFile`
- `ModelPath`
- `NumPoints`
- `NumTriangles`
- `PhotoList`
- `PhotoSource`
- `Photos`
- `Progress`
- `Reload`
- `Stage`
- `Supported`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onNewMesh`
- `onError`
- `onExported`

