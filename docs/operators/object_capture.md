# Object Capture

*POP · v0.1.3*

<!-- screenshot: drop a PNG at docs/images/object_capture.png and rerun the generator -->

Apple's photogrammetry: a folder of photographs of one object becomes a real textured mesh. Slower than Geo Gen and far more accurate, because it is measuring rather than imagining.

## Inputs

A folder of photographs (a parameter, not a wire).

## Outputs

Mesh geometry plus baked albedo, normal and occlusion maps.

## Worth knowing

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
| **Save Model** | file |  |  |
| **Choose…** | button |  |  |
| **Load Model** | file |  |  |
| **Load** | button |  |  |
| **Export File** | file |  |  |
| **Choose…** | button |  |  |
| **Export** | button |  |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Scale** | number | 1.0 |  |
| **Center** | menu | Ground | As Captured, Bounds Centre, On The Ground |

## Python

Reachable on the operator via its extension:

- `Busy`
- `Cancel`
- `ChooseExportFile`
- `ChooseSaveModel`
- `DoCallback`
- `Eta`
- `Generate`
- `LastError`
- `LastMs`
- `ModelFile`
- `NumPoints`
- `NumTriangles`
- `Photos`
- `Progress`
- `Stage`
- `Supported`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onNewMesh`
- `onError`

