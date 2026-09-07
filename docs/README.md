# AML operators

One page per operator: what it does, what to wire into it, what comes out, and every parameter.

Most operators need no download at all. The ones that use a model say so on the node and fetch it through the [Model Manager](model-manager.md), which shows the size and licence first.

See also: [getting started](getting-started.md) · [troubleshooting](troubleshooting.md)

## Vision — no download

- [Barcode / QR Reader](operators/code_reader.md) — Reads QR codes, barcodes and the other symbologies Vision supports, returning the payload and where it sits in frame.
- [Contours](operators/contours.md) — Traces the outlines in an image and hands them back as geometry — one line strip per contour, with the nesting depth of holes, so you can draw, extrude or animate real edges.
- [Image Classify](operators/image_classify.md) — Names what is in a picture, using Apple's built-in classifier — no model download.
- [Image Similarity](operators/image_similarity.md) — How alike two images are, using Vision's feature prints — a perceptual distance rather than a pixel difference.
- [Object Tracker](operators/object_tracker.md) — Follows things across frames and gives each one a persistent ID, so you can tell that the person at the left of this frame is the same person who was in the middle of the last one.
- [OCR / Text Recognition](operators/ocr_viewer.md) — Reads text in an image, with position for each piece of text so you can draw over it or track it.
- [Person Mask](operators/person_mask.md) — Separates people from the background.
- [Pose Tracker](operators/pose_tracker.md) — Tracks people in an image: body position, 19 body joints, both hands with 21 joints each, face landmarks, and hand gestures — all from one pass over the frame, with no model to download.
- [Saliency](operators/saliency.md) — Where a viewer would look.
- [Subject Mask](operators/subject_mask.md) — Apple's lift-the-subject segmentation: every salient object, not just people, cut from the background.

## Models

- [CoreML Data](operators/coreml_data.md) — The same idea as CoreML Model, for models that take numbers instead of pictures — embeddings, regressors, audio models, classifiers.
- [CoreML Model](operators/coreml_model.md) — Runs any image-in Core ML model you point it at.
- [Depth Map](operators/depth_map.md) — Estimates depth from a single ordinary image — no depth camera.
- [Depth Metric](operators/depth_metric.md) — Apple's Depth Pro: depth in **real metres** from one image, with no camera intrinsics, plus the estimated focal length.
- [Diffusion](operators/diffusion.md) — Stable Diffusion running entirely on your machine: text to image, image to image, ControlNet and inpainting.
- [Geo Gen](operators/geo_gen.md) — One image of an object becomes a coloured, UV-unwrapped 3D mesh, in a couple of seconds.
- [Semantic Segmentation](operators/semantic_segmentation.md) — Labels every pixel with a class — person, car, road, and so on — as a coloured map, an overlay or a single-class matte.
- [YOLO Classify](operators/yolo_classify.md) — Whole-image classification with a YOLO classifier.
- [YOLO Detect](operators/yolo_detect.md) — Object detection with boxes, labels and persistent track IDs, using Ultralytics YOLO models.
- [YOLO Pose](operators/yolo_pose.md) — Multi-person skeletons (17 keypoints) with track IDs, and an OpenPose-style render for feeding ControlNet.
- [YOLO Segment](operators/yolo_segment.md) — Instance segmentation — a mask per detected object rather than one mask per class.

## Language and audio

- [Local LLM](operators/local_llm.md) — Apple Intelligence's on-device language model: a prompt in, streamed text out.
- [Sound Classify](operators/sound_classify.md) — Recognises 303 everyday sounds — applause, laughter, sirens, glass breaking — from an audio CHOP, with no model download.
- [Speech Synth](operators/speech_synth.md) — Text to speech, rendered faster than realtime, with per-word timing you can animate to.
- [Speech to Text](operators/speech_text.md) — Live speech recognition from an audio CHOP, on-device.
- [Text Tags](operators/text_tags.md) — Turns a piece of text into tags, using the on-device language model.
- [Translate](operators/translate.md) — On-device translation between 22 languages, with automatic detection of the source language.

## 3D and generation

- [Image Playground](operators/image_playground.md) — Apple's own image generator: a prompt becomes a picture in a few seconds, with nothing to download.
- [Object Capture](operators/object_capture.md) — Apple's photogrammetry: a folder of photographs of one object becomes a real textured mesh.

