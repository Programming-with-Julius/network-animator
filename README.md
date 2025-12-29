[Fully vibe-coded, does not reflect me as a developer]

# network-animator

Live demo: https://programming-with-julius.github.io/network-animator/

`network-animator` is a single-file HTML tool that renders a fully-connected neural network on a canvas, with a “clean stage” area at the top for easy screen recording. You configure the amount of layers and the number of nodes per layer (e.g. `6, 8, 8, 4`), and the visualizer draws nodes + edges with a dark background, glowy outlines, and a set of styling + animation controls.

## Features

- Fully connected network rendering (layer sizes like `4,6,6,3`)
- Reserved top stage area for clean screen recordings
- Dark background with white node outlines and grey edges (customizable)
- Glow controls
  - independent node glow + edge glow
  - configurable colors for node/edge outlines and node fill
- Edge animation options
  - animated dashed edges (speed/length/gap)
  - optional curved edges
- “Weight-based” styling
  - seeded random weights (stable across redraws)
  - weight-based edge opacity
  - quick “randomize weights” action
- Performance / style knobs
  - edge dropout (show only a subset of edges)
  - adjustable FPS
- Interaction
  - hover highlight for a node + its incident edges
  - optional hover labels `(layer, node)`
- Export
  - export current frame as PNG

## Usage

1. Open the live demo link above, or open `index.html` locally in a browser.
2. Enter your network shape in **Layers (nodes per layer)** (comma-separated).
3. Tweak styling/animation controls below the canvas.
4. Record only the top stage area for clean captures.

### Shortcuts

- `R` — randomize weights
- `Space` — toggle dashed-edge animation

## How it works (high level)

- The network is laid out in layers across the canvas:
  - layer `x` positions are spaced horizontally between left/right padding
  - node `y` positions are evenly distributed vertically per layer
- Edges are drawn between every node in layer `L` and every node in layer `L+1`:
  - optional dropout hides a fraction of edges for performance / aesthetics
  - optional curves draw cubic Bézier connections for a “flowy” look
- A seeded pseudo-random generator produces stable per-edge weights:
  - the absolute weight controls edge opacity (when enabled)
  - changing the seed or pressing “Randomize weights” regenerates weights
- The render loop uses `requestAnimationFrame`, while honoring a target FPS:
  - edge dashes animate via `lineDashOffset` when enabled
- Hover detection picks the nearest node under the cursor and highlights it:
  - incident edges (prev/next layer connections) are re-drawn on top

## License

MIT. See `LICENSE`.
