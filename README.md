# Patchbay

A diagram editor for mapping hardware studio rigs: synths, mixers, aux sends and returns, samplers, interfaces, and every cable in between.

**Open it:** https://kenneth-rakentine.github.io/Patchbay/
**Windows app:** [latest release](https://github.com/Kenneth-Rakentine/Patchbay/releases/latest)

![Example board: synths into a ZED-R16 mixer with aux loops, then Octatrack, compressor and interface](docs/example-board.png)

## What it does

- **Blocks** for each piece of gear: box, rounded, pill, ellipse or plain text, with any fill, outline, text colour, S/M/L text, bold, and left or centred alignment.
- **Cables** that attach to blocks and follow them when you move things. Drag one of the dots on a block's edge to start a cable and drop it on another block.
- **Exact connections.** A normal drop snaps to the middle of the nearest side. Hold **Ctrl** while dropping to attach at the exact spot on the edge.
- **Bends you control.** Select a cable and drag a **＋** handle to add a bend, drag a bend to move it, double-click a bend to remove it. Lines can be straight, elbow (right angles) or curved.
- **Named, colour-coded cables.** Give any cable a name (ch.15/16, Aux 2, thru…) in S/M/L, plus colour, thickness, dashes and arrowheads.
- **Your own cable legend.** Name each cable colour by signal type (Audio, MIDI, USB, ADAT, aux paths…). The legend block lists each name in its own cable colour and updates as you rename colours or add cables.
- **Sections.** Turn any block into a labelled background area. Cables pass over it, and moving it moves everything inside.
- **Boards you can iterate on.** Duplicate a board to start a new version of your setup. Dates in the name (like `Current Setup 10/05/26`) roll forward to today automatically.
- **Import from Whimsical.** Bring an existing Whimsical diagram in as an editable board (see below).
- **Save, open and share** boards as files that keep saving as you work, or as a link anyone can open. No account needed.
- **Export** a board as PNG or SVG, and back up or restore every board as one JSON file.

## Controls

| Action | How |
| --- | --- |
| Draw a cable | Drag a dot on a block's edge, or use the Wire tool (L) |
| Place or connect exactly | Hold Ctrl while dragging (skips the grid, attaches at the exact edge point) |
| Add / move / remove a bend | Drag ＋ on a selected cable / drag the bend / double-click it |
| Duplicate while dragging | Alt + drag |
| Edit text | Double-click a block (Ctrl+Enter or Esc to finish) |
| New block | Double-click empty space, or the Block tool (R) |
| Name a cable | Double-click the cable |
| Pan / zoom | Space + drag or middle mouse / Ctrl + scroll wheel |
| Copy, paste, duplicate | Ctrl+C, Ctrl+V, Ctrl+D |
| Undo / redo | Ctrl+Z / Ctrl+Shift+Z |
| Fit the board on screen | Shift+1 |
| Tools | V select, H pan, R block, O ellipse, T text, L wire |

## Importing from Whimsical

1. In Whimsical, select everything on the board (Ctrl+A), right-click, and choose **Copy as SVG**.
2. Click an empty spot on the Patchbay canvas and press **Ctrl+V**. (Or open **Backup & import** and paste it, or load a saved `.svg` file.)

The diagram arrives as a new board. Shapes become blocks with their colours and text. Lines become cables that are attached to the blocks they touch, with their bends, colours, dashes and arrowheads. Text sitting on a line becomes that cable's name, and cable colours close to your legend colours snap to them so legend names apply. Everything is editable afterwards.

It works with most diagram SVGs, not only Whimsical's. Text that was exported as outlines rather than real text can't be read.

## Saving and sharing

No account needed. Your boards save automatically in the browser (or desktop app) you're using, and nobody else can see them.

- **Save to file** (File menu or Ctrl+S) writes the board to a `.patchbay.json` file on your computer. In Chrome, Edge and the desktop app, every change after that saves to the same file automatically, so keeping it in a Dropbox, Google Drive or OneDrive folder gives you the board on every computer. Other browsers download a copy instead.
- **Open file** (Ctrl+O, or drag a board file onto the window) brings a board back. Reopening a board you already have replaces it, and Ctrl+Z restores the previous version.
- **Share link** packs the whole board into a link. Whoever opens it gets their own copy to edit; nothing is uploaded anywhere. Big boards make long links, so if a forum cuts one off, share the board file instead.
- **Backup & import** saves or restores every board at once.

The website, the desktop app and each browser keep separate boards, so use a board file or a backup to move between them.

## Install it

- **As a desktop app from the website:** open the site in Chrome or Edge and click the install icon at the right end of the address bar. It gets its own window and works offline after the first visit.
- **As a Windows program:** download `Patchbay-Setup-x.y.z.exe` (installer) or `Patchbay-Portable-x.y.z.exe` (runs without installing) from [Releases](https://github.com/Kenneth-Rakentine/Patchbay/releases). Windows SmartScreen may warn about an unrecognised app because it isn't code-signed; choose **More info → Run anyway**.

## Project layout

```
index.html              the whole app (HTML, CSS and JS in one file)
manifest.webmanifest    install info for browsers
sw.js                   offline cache
icons/                  app icons
desktop/                Electron wrapper for the Windows build
.github/workflows/      builds the Windows app when a version tag is pushed
```

## Making changes

Edit `index.html` and push to `main`. GitHub Pages republishes the site within a minute or two. When you change `index.html`, also bump `VERSION` in `sw.js` so installed copies pick up the update.

To publish a new Windows build, bump `"version"` in `desktop/package.json` (for example `1.0.0` → `1.0.1`) and push to `main`. The **Build desktop app** workflow sees there's no release for that version yet, builds the installer, and publishes a new release with a matching `v1.0.1` tag. Pushes that don't change the version skip the build.

To run the desktop app locally (needs Node.js 20+):

```bash
cd desktop
npm install
npm start
```

## License

MIT
