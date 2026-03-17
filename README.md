# COS314 Study Pack

Self-contained HTML study notes for COS314 (Artificial Intelligence) at UP. Open `index.html` in a browser — no build step, no server needed.

## Structure

```
index.html              ← topic index / home page
styles.css              ← shared base styles
01_problem_representation.html
02_heuristics.html
03_dfs_dfid_bfs.html
04_hill_climbing_astar.html
05_minimax_alphabeta.html
06_sa_tabu_ils.html
07_genetic_algorithms.html
demos/                  ← standalone interactive visualisations (embedded via <iframe>)
  sa_8x8.html           ← SA Metropolis step-through on an 8×8 grid
  tabu_grid.html        ← Tabu Search on a 7×5 cost grid
  tabu_continuous.html  ← Tabu Search on a continuous landscape
  ils.html              ← Iterated Local Search on a continuous landscape
```

## Adding a new interactive demo

Demos come from Claude as HTML fragments. To embed one:

**1. Wrap it** — create `demos/your_demo.html` using `demos/sa_8x8.html` as the shell template. The key parts to keep from the template are the `<!DOCTYPE>`, the base reset CSS, and the `:root` block that bridges Claude's CSS variables to this dark theme:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body { font-family: 'Segoe UI', Arial, sans-serif; background: #0f1117; color: #d4d0c8; }
:root {
  --color-border-secondary:    #252830;
  --color-border-tertiary:     #1e2028;
  --color-background-secondary:#1c1f2b;
  --color-background-primary:  #0f1117;
  --color-text-primary:        #e0d8c8;
  --color-text-secondary:      #a0988a;
  --color-text-tertiary:       #605850;
  --border-radius-md:          6px;
  --font-mono: 'Cascadia Code','Fira Mono','Consolas',monospace;
}
</style>
</head>
<body>
  <!-- paste the Claude fragment here -->
</body>
</html>
```

**2. Embed it** — in the relevant topic file, add:

```html
<h3>Interactive Demo: Your Title</h3>
<p>One sentence describing what to look for.</p>
<iframe class="demo-frame" src="demos/your_demo.html" title="Your Title" style="height:500px"></iframe>
```

The `.demo-frame` class (defined in each topic file's `<style>`) handles the border and border-radius. The auto-resize script at the bottom of each topic file will adjust the height automatically on load — the `style="height:500px"` is just the initial fallback.
