# Getting started

AML is a family of TouchDesigner operators that wrap Apple's own machine
learning — Vision, Core ML, Speech, Apple Intelligence — as operators you
drag into a network. Everything runs on your Mac. No Python environment, no
cloud service, no API keys.

**Requirements:** an Apple Silicon Mac, macOS 12 or newer, TouchDesigner
2023.12000 or newer. A few operators need a newer macOS and say so.

---

## Install

Run the installer, or drag the `.tox` from the release zip into a project —
either way it installs for your user only and needs no admin password.

Then **restart TouchDesigner**. Plugins load at startup, so this is not
optional. On that first launch TouchDesigner asks once per plugin whether
to trust it; click OK for each and it remembers.

---

## Your first operator

1. Open the **Palette** and find **AML**, or press Tab in a network and look
   for the AML operators in the OP Create dialog.
2. Drop in **Pose Tracker** and wire a Video Device In or a Movie File In
   into it.
3. Add a Select CHOP and set its channel names to `pose*`.

You are now tracking a body. No download happened, because Pose Tracker
uses Apple's own frameworks.

---

## Operators that need a model

Some operators use a model that is not part of macOS — depth, segmentation,
YOLO, Geo Gen, Diffusion. Those say so on the node, naming the model and its
size, and carry a **Manage Models** button.

Each of them has a **Model** menu listing the models it can use, with the
ones you have not downloaded marked as such. Choosing a model is normally
all you do — the operator finds it wherever it is installed. The last entry,
**Custom file…**, frees the **Model Path** field for a converted model of
your own.

The Model Manager lists every model AML knows about: size, licence, which
operators use it, whether it is on this machine, and a link to where it
comes from. Nothing downloads until you ask.

**No model is bundled in the installer.** It is under 2 MB to download and
about 5 MB installed — every operator, no weights — so you only ever fetch
the models you actually use.

---

## Where models live

Searched in this order:

1. a `models` folder **beside your project**
2. the **library folder** you choose in the Model Manager
3. the default location in Application Support

Project-first is what makes a project portable: copy the `.toe` together
with its `models` folder and every operator resolves on a machine that has
nothing installed.

---

## What to read next

- **[Operator reference](README.md)** — one page per operator: what it does,
  what to wire in, what comes out, and every parameter.
- **[Model Manager](model-manager.md)** — where models come from, where
  they are stored, and what each licence means.
- **[Troubleshooting](troubleshooting.md)** — the things that actually go
  wrong, and what to do about them.

---

## A few things worth knowing early

- **Wiring beats the Source parameter.** Operators that take an image accept
  it either way; a wired input wins.
- **POPs need their render flag on.** Contours, Geo Gen and Object Capture
  output geometry, and geometry you cannot see looks exactly like no
  geometry at all.
- **TouchDesigner Non-Commercial silently downscales textures above 1280.**
  It does not warn. Operators that can exceed that give you a size control.
- **Callbacks are opt-in.** Press **Create Callbacks** on an operator and it
  writes an editable DAT beside it, already hooked up.
