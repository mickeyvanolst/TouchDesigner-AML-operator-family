# Barcode / QR Reader

*TOP · v0.1.4*

<!-- screenshot: drop a PNG at docs/images/code_reader.png and rerun the generator -->

Reads QR codes, barcodes and the other symbologies Vision supports, returning the payload and where it sits in frame.

## Inputs

An image.

## Outputs

A table: payload, symbology, confidence and bounds.

## Built on

This operator is a thin layer over the following; their own documentation is the reference for what it can and cannot do.

- [Vision framework](https://developer.apple.com/documentation/vision) — Apple's on-device image analysis
- [VNDetectBarcodesRequest](https://developer.apple.com/documentation/vision/vndetectbarcodesrequest) — QR and barcode detection; the symbologies it lists are the ones this operator reads

## Worth knowing

- A binary payload comes back as an empty string rather than mangled text.

## Parameters

### Recognize

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Max Results** | number | 10 |  |
| **Min Confidence** | number | 0.01 |  |
| **Source TOP** | TOP |  |  |

### Output

| Parameter | Type | Default | Options |
|---|---|---|---|
| **Process Resolution** | menu | useinput | Use Input, Limit (Longest Side) |
| **Resolution Limit** | number | 512 |  |
| **Process Interval** | number | 1 |  |
| **Async Mode** | toggle | True |  |

## Python

Reachable on the operator via its extension:

- `DoCallback`
- `GetCodes`
- `GetPayloads`
- `Payload`

## Callbacks

Press **Create Callbacks** to get an editable DAT beside the operator with these hooks:

- `onCode`

