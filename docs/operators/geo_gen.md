# Geo Gen

*POP · v0.5.1*

<!-- screenshot: drop a PNG at docs/images/geo_gen.png and rerun the generator -->

One image of an object becomes a coloured, UV-unwrapped 3D mesh, in a couple of seconds. The picture is reprojected onto the mesh, so the result looks like the thing you photographed.

> **Needs a model.** Pick one from the **Model** menu: it lists the models this operator can use and marks the ones you have not downloaded, and **Custom file…** frees **Model Path** for a model of your own. The node says when a model is missing and offers a **Manage Models** button; the Model Manager shows each model's size and licence and asks before downloading anything.

## Inputs

An image, set as **Source**.

## Outputs

Geometry with `P`, `Color`, `N` and `Tex`, plus baked albedo, UV-layout, position and normal maps on separate outputs.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Core ML](https://developer.apple.com/documentation/coreml) — runs the model on the CPU, GPU and Neural Engine
- [TripoSR](https://github.com/VAST-AI-Research/TripoSR) — the image-to-3D model (MIT)
- [Stable Fast 3D](https://github.com/Stability-AI/stable-fast-3d) — Stability AI's successor: the delit albedo and what it does well
- [xatlas](https://github.com/jpcy/xatlas) — the UV atlas (MIT)

Models it downloads through the Model Manager, each under its own licence:

- [TripoSR triplane (image to 3D)](https://huggingface.co/stabilityai/TripoSR) — MIT
- [TripoSR NeRF query head](https://huggingface.co/stabilityai/TripoSR) — MIT
- [Stable Fast 3D triplane (image to 3D)](https://huggingface.co/stabilityai/stable-fast-3d) — Stability AI Community License
- [Stable Fast 3D query head](https://huggingface.co/stabilityai/stable-fast-3d) — Stability AI Community License

## Worth knowing

- **Export** writes `.obj` (with MTL and the baked maps as PNG), or TouchDesigner's own `.pop` / `.tog` with the albedo beside it as PNG and the position and normal maps as EXR — data OBJ cannot carry. From Python: `Export(path)`; the `onExported` callback lists what was written.
- **Generate-driven, not per frame.** A mesh takes a few seconds, and longer at higher Grid Res with UV unwrap.
- Needs a clear subject on a clean background; a busy photo gives a confused mesh.

## Parameters

### Geo Gen

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Enable** | toggle | True |  |
| **Model** | menu | triposr_coreml | TripoSR (image to 3D), Stable Fast 3D (image to 3D) — Powered by Stability AI, Custom file... |
| **Model Folder** | folder |  |  |
| **Model Status** | text |  |  |
| **Manage Models** | button |  |  |
| **Source TOP** | TOP |  |  |
| **Generate** | button |  |  |
| **Clear** | button |  |  |
| **Generate On Source Change** | toggle | False |  |
| **Grid Resolution** | menu | G128 | 64, 96, 128, 160, 192, 256 |
| **Compute Units** | menu | All | All, CPU + Neural Engine, CPU + GPU, CPU only |
| **Density Threshold** | number | 25.0 |  |
| **Smoothing** | number | 4 |  |
| **Unwrap UVs** | toggle | True |  |
| **Bake Texture** | menu | R1024 | Off, 512 x 512, 1024 x 1024, 2048 x 2048 |
| **Project Source Image** | toggle | True |  |
| **Object File Type** | menu | obj | OBJ, POP |
| **Export File** | FileSave |  |  |
| **Export** | button |  |  |

## Python

Reachable on the operator via its extension:

- `Busy`
- `DoCallback`
- `Export`
- `Generate`
- `LastError`
- `LastMs`
- `Loaded`
- `MAPS`
- `MapPath`
- `NumPoints`
- `NumTriangles`
- `Progress`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onNewMesh`
- `onError`
- `onExported`

