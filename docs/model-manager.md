# Model Manager

Most AML operators need no download at all. The ones that do — depth,
segmentation, YOLO, Geo Gen, Depth Metric, Diffusion — use a model that is
not part of macOS, and the Model Manager is where those live.

It is a window, not an operator. It does not go in your network and it does
not get saved into your project.

<!-- screenshot: drop a PNG at docs/images/model-manager.png -->

---

## Opening it

Press **Manage Models** on any operator that uses a model. The window opens
focused on that operator's model, so you land on the row you came for.

The first time AML is added to a project it also offers to open the Manager
for you. Declining is remembered — it asks once per machine, not once per
project.

---

## What each row tells you

| Column | Meaning |
|---|---|
| **Model** | The model's name |
| **Size** | How much you are about to download |
| **Used by** | Which operators can use it — some are shared |
| **Licence** | The model's own licence, which is **not** AML's licence |
| **Where** | Which folder it is installed in, or `—` if it is not |
| **State** | `installed`, `not installed`, or live download progress |
| **Action** | What the button will do |
| **Source** | Opens the model's own page in your browser |

## The action button

- **Download** — fetches it. You are always asked first, and the
  confirmation says what, from where, to where, how big, and under which
  licence.
- **Delete** — removes that copy from disk. You are asked first.
- **Cancel** — stops a download in progress.
- **Convert…** — the YOLO weights are converted on your machine rather than
  redistributed, because their licence is AGPL-3.0. Run
  `get_models.command`, which needs `python3` and a few minutes.
- **Terminal…** — the Stable Diffusion pipelines arrive as archives that
  have to be unpacked, and for ControlNet merged. The guided downloader
  does that; this window does not. Run `get_models.command`.

---

## Where models are stored

Three locations, searched in this order:

1. a `models` folder **beside your project**
2. the **library folder** — set it to anywhere you like, including an
   external drive
3. the default, in Application Support

Project-first is what makes a project portable: copy the `.toe` together
with its `models` folder and every operator resolves on a machine that has
nothing installed.

**Download To** chooses between the library folder and the project folder
for the next download.

---

## Worth knowing

- **Downloads do not resume.** A failure or a cancel deletes the partial
  download and the next attempt starts over. That keeps the whole thing
  simple and leaves nothing half-written on disk; the cost is that a large
  pipeline dying near the end starts again.
- **The licence shown is the model's own.** AML's licence does not cover
  the models, and some of them carry real restrictions — the YOLO weights
  are AGPL-3.0, and commercial use needs a licence from Ultralytics. The
  confirmation dialog names the licence before anything downloads.
- **An operator will not overwrite a model path you chose.** If you point
  an operator at your own file, the Manager leaves it alone and the
  operator says `Custom model`.
- **Deleting a model updates every operator** that used it, within a
  second — they check continuously rather than only when they cook.
