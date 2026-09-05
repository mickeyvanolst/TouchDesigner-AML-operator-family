# Troubleshooting

The things that actually go wrong, and what to do about them.

---

## The operator says a model is not installed

Most AML operators need no download at all. The ones that do say so on the
node, naming the model and its size:

> Depth Anything V2 Small not installed (50 MB) — press Manage Models

Press **Manage Models**. The Model Manager lists every model with its size,
licence, which operators use it, and where it would go. Nothing downloads
until you say so.

The first time you add AML to a project it offers to open the Manager for
you. Declining is remembered — it is a welcome, not a nag — and the button
on the operator gets you back there.

**Models can live in three places**, searched in this order: a `models`
folder beside your project, the library folder you chose, then the default
location. Project-first is what makes a `.toe` portable: copy it with its
`models` folder and it resolves on a machine that has nothing installed.

---

## TouchDesigner asks whether to trust a plugin

Once per plugin, the first time TouchDesigner sees it. Click OK; it
remembers. With every group installed there are up to 20 of these on the
first launch after installing.

Plugins load only when TouchDesigner starts, so **restart after installing
or updating**. If operators behave like an older version, that is usually
why — AML warns you on the node when the loaded plugin is older than the
operators.

---

## An operator produces nothing

- **Check it has an input.** Most vision operators need an image, either
  wired into the first input or set as **Source**. Wiring takes precedence.
- **A POP only draws when its render flag is on.** Contours, Geo Gen and
  Object Capture output geometry; correct geometry with the render flag off
  looks identical to nothing at all.
- **Some operators need motion.** Object Tracker has nothing to track in a
  still image, and the change-event callbacks only fire when content
  actually changes *after* the first result.

---

## The YOLO operators say CPU+GPU is not used

If you set **Compute Units** to CPU+GPU on a YOLO operator, it warns and
runs on **All** instead. That is deliberate.

CPU+GPU does not produce a wrong result there — it *quits TouchDesigner*.
Apple's Metal compiler asserts while preparing a YOLO graph for the GPU,
and an assert in that layer calls `abort()`, which nothing in the operator
can catch. The process is gone in the same frame, which is why a warning on
its own was not enough: there was never a moment in which you could read
it. So the operator refuses the setting and tells you what it did instead.

CPU + Neural Engine is the fast path on Apple silicon anyway, so in
practice you lose nothing.

The same MPSGraph abort has been seen with certain quantized Core ML models
in the **CoreML Model** operator, which does *not* substitute for you. If a
model of your own takes TouchDesigner down, try a plain fp16 export and stay
off the GPU compute path.

---

## Apple Intelligence operators say they are unavailable

Local LLM, Text Tags and Translate need macOS 26 with Apple Intelligence
enabled and the model downloaded. The operator surfaces the exact reason
rather than failing silently.

They can also fail *transiently* on a machine where they normally work —
generation returning an error while availability still reports true. A
restart of the machine has resolved it here. If an operator worked
yesterday and does not today, suspect this before suspecting your project.

---

## Speech to Text asks for permission from something called a helper

That is correct and deliberate. macOS terminates any application that asks
for speech recognition without declaring it up front, and TouchDesigner
does not declare it. Patching TouchDesigner would break its signature, so
AML ships a small helper that owns the permission instead. **TouchDesigner
itself is never modified.**

On-device recognition also needs the dictation model for your language:
System Settings → Keyboard → Dictation.

---

## Images look torn, tiled, or wrong above 1280 pixels

TouchDesigner **Non-Commercial silently downscales any texture above
1280×1280**. It does not warn; the data simply arrives wrong, which looks
like a bug in the operator.

Operators that can exceed it give you a size control — Image Playground's
**Output Size**, the CoreML TOP's **Max Texture Size**, Object Capture's
**Texture Size**. On a Commercial licence there is no cap and you can raise
them.

---

## Image Playground refuses a prompt

Two different things:

- **It must be frontmost.** Apple refuses to generate for a background
  application, so leave TouchDesigner in front while it works.
- **The prompt is a short concept, not a sentence.** Brand names and real
  people are refused outright. Measured: *"a vintage computer, white
  background"* generates; *"a vintage **mac** computer, white background"*
  is refused.

---

## Diffusion

- **Guidance 0 means unconditional** — your prompt is ignored. SD-Turbo
  wants guidance 1.0, 2 steps, DPM++ (not Karras).
- **Image-to-image needs a working VAE encoder.** Apple's own SDXL encoder
  produces NaN; AML swaps in a fixed one, fetched by the Model Manager. If
  image-to-image reports itself unavailable, the operator says why.
- **A 768×512 model can hang on load** under All or CPU+ANE — the compiler
  sits idle forever. CPU+GPU loads it fine. This is the one case where the
  GPU path is the answer, and Diffusion is not affected by the YOLO crash
  above.

---

## Something else

Open an issue with the operator, your macOS and TouchDesigner versions, and
which parameters were away from their defaults. That last one matters more
than it sounds: most bugs found so far depended on a specific combination
rather than a single setting.
