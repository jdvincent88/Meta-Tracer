# Meta-Tracer

**Drawing/tracing projector in Augmented Reality (Passthrough) for Meta Quest 2**

Meta-Tracer is a [WebXR](https://immersiveweb.dev) app built with [three.js](https://threejs.org) and [three-mesh-ui](https://felixmariotto.github.io/three-mesh-ui/) that projects a virtual image on top of a sheet of paper in passthrough so you can trace it. It is plain HTML and JavaScript with no build step: the whole app is [`index.html`](index.html), and it can be served straight from GitHub Pages.

It is based on [Passtracing](https://github.com/fabio914/passtracing) by Fabio Dela Antonio (MIT), tuned for the Quest 2's grayscale passthrough, and adds three features:

| Feature | What it does | Controller | Panel | Keyboard |
|---------|--------------|------------|-------|----------|
| **Lock** | Freezes the image in place. While locked, the trigger no longer repositions the image and the thumbstick no longer resizes it. Opacity and invert still work. | Grip (squeeze) | "Position" button | `L` |
| **Opacity slider** | Sets the image opacity from 0% to 100%. Below about 30% the image fades into an edge-detected line drawing. | Thumbstick left/right | Slider, and the − / + buttons | `[` and `]` |
| **Color invert** | Inverts the image colors in the shader. On grayscale passthrough this turns dark line art into light lines that stand out against dark paper or a desk. | Click the thumbstick | "Colors" button | `I` |

The control panel is a WebXR DOM overlay, so it floats in front of you inside the AR session. Point a controller at it and pull the trigger to press a button or drag the slider. Pressing the trigger while pointing at the panel never moves the image, even when it is unlocked.

## Instructions

1. Open the GitHub Pages URL for this repository on your PC (or directly in the Quest browser).

2. Copy an image URL and paste it in the text field. For example, a public domain image from [rawpixel](https://www.rawpixel.com/public-domain).

   *Some [CORS policies](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) might prevent the app from loading images from certain websites. You'll want to use URLs from websites that allow their content to be loaded from any origin* (`Access-Control-Allow-Origin: *`).

3. Click on "Load image" to reload the page with this image, or click on "Send link to Meta Quest" to send it to your headset.

4. After opening the link on your Meta Quest 2, click on "Start AR".

5. Hold the trigger to position the image on top of a sheet of paper, use the thumbstick to adjust size and opacity, then press the grip button (or the "Position" button on the panel) to lock it.

6. Draw/Trace. Use "Exit AR" on the panel to leave the session.

### All controls

| Input | Action |
|-------|--------|
| Thumbstick left / right | Decrease / increase opacity |
| Thumbstick up / down | Increase / decrease size (disabled while locked) |
| Hold trigger | Reposition image (disabled while locked) |
| Grip | Lock / unlock position |
| Click thumbstick | Invert colors |
| A or X | Show / hide image |
| B or Y | Show / hide instructions |

## Running locally

There is nothing to build. Serve the repository root over HTTPS (WebXR requires a secure context; `localhost` also counts) and open `index.html`. For example:

```
npx http-server -p 8080
```

Then open `http://localhost:8080/` on your PC to preview, or expose it over HTTPS (for example with [localtunnel](https://github.com/localtunnel/localtunnel)) to open it on the headset.

three.js, three-mesh-ui and the import-map polyfill are loaded from [unpkg](https://unpkg.com), so the device needs internet access.

## Deploying to GitHub Pages

Enable GitHub Pages for the repository (Settings → Pages) with the source set to the `main` branch and the root folder. The app will be available at `https://<user>.github.io/<repository>/`.

## Requirements

Meta Quest 2 (also works on Meta Quest Pro and Quest 3).

## Credits and license

- [Passtracing](https://github.com/fabio914/passtracing) by Fabio Dela Antonio, MIT License. Meta-Tracer's `index.html` and the sample image are derived from it.
- The sample image (`Images/discovery.jpg`) is NASA's photo of Space Shuttle Discovery lifting off on STS-133, sourced via rawpixel (public domain).
- This repository was forked from [reality-mixer-js](https://github.com/fabio914/reality-mixer-js) (also by Fabio Dela Antonio, MIT). Its files are still present under `src/`, `examples/` and `schemas/`; see [README-reality-mixer.md](README-reality-mixer.md). They are not used by Meta-Tracer.

Licensed under the MIT License, see [LICENSE](LICENSE).
