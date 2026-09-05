# Contours

*POP · v0.1.2*

<!-- screenshot: drop a PNG at docs/images/contours.png and rerun the generator -->

Traces the outlines in an image and hands them back as geometry — one line strip per contour, with the nesting depth of holes, so you can draw, extrude or animate real edges.

## Inputs

An image, wired in or set as **Source**.

## Outputs

Line-strip geometry. Points carry `P`, `contour` and `depth` (0 is an outline, 1 a hole in it).

## Worth knowing

- **Detail** is the biggest lever on how many contours you get.
- A POP only draws when its render flag is on.

## Parameters

### Contours

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Source TOP** | TOP |  |  |
| **Enable** | toggle | True |  |
| **Detail** | number | 512 |  |
| **Contrast** | number | 2.0 |  |
| **Contrast Pivot** | number | 0.0 |  |
| **Dark On Light** | toggle | True |  |
| **Simplify** | number | 0.002 |  |
| **Min Points** | number | 8 |  |
| **Outlines Only** | toggle | False |  |
| **Process Interval** | number | 1 |  |
| **Coordinates** | menu | Centred | 0 to 1 (image space), Centred, aspect-corrected |
| **Async** | toggle | True |  |

