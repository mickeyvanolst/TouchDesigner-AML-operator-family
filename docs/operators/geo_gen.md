# Geo Gen

*POP · v0.2.6*

<!-- screenshot: drop a PNG at docs/images/geo_gen.png and rerun the generator -->

One image of an object becomes a coloured, UV-unwrapped 3D mesh, in a couple of seconds. The picture is reprojected onto the mesh, so the result looks like the thing you photographed.

> **Needs a model.** The operator says so on the node and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image, set as **Source**.

## Outputs

Geometry with `P`, `Color`, `N` and `Tex`, plus baked albedo, UV-layout, position and normal maps on separate outputs.

## Worth knowing

- **Generate-driven, not per frame.** A mesh takes a few seconds, and longer at higher Grid Res with UV unwrap.
- Needs a clear subject on a clean background; a busy photo gives a confused mesh.

## Parameters

### Geo Gen

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Enable** | toggle | True |  |
| **Model Folder** | folder |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Source TOP** | TOP |  |  |
| **Generate** | button |  |  |
| **Generate On Source Change** | toggle | False |  |
| **Grid Resolution** | menu | G128 | 64, 96, 128, 160, 192, 256 |
| **Compute Units** | menu | All | All, CPU + Neural Engine, CPU + GPU, CPU only |
| **Density Threshold** | number | 25.0 |  |
| **Smoothing** | number | 4 |  |
| **Unwrap UVs** | toggle | True |  |
| **Bake Texture** | menu | R1024 | Off, 512 x 512, 1024 x 1024, 2048 x 2048 |
| **Project Source Image** | toggle | True |  |
| **Export File** | file |  |  |
| **Choose…** | button |  |  |
| **Export** | button |  |  |

## Python

Reachable on the operator via its extension:

- `Busy`
- `ChooseExportFile`
- `DoCallback`
- `Generate`
- `LastError`
- `LastMs`
- `Loaded`
- `NumPoints`
- `NumTriangles`
- `Progress`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onNewMesh`
- `onError`

