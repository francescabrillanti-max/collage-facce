# Collage Facce — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Single `index.html` that loads face assets and composes a random face every 3 seconds using p5.js.

**Architecture:** Single HTML file with embedded CSS and p5.js sketch. Assets are preloaded in `preload()`, face parts tracked as arrays of p5.Image objects. A `drawFace()` function picks one random image per category and draws them layered in order.

**Tech Stack:** p5.js (CDN), vanilla HTML/CSS

---

### Task 1: Create index.html with p5.js setup

**Files:**
- Create: `index.html`

- [ ] **Step 1: Write the HTML scaffold with p5.js CDN**

```html
<!DOCTYPE html>
<html lang="it">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Collage Facce</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.11.0/p5.min.js"></script>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      overflow: hidden;
      background: #000;
    }
    canvas {
      display: block;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  </style>
</head>
<body>
<script>
// sketch here
</script>
</body>
</html>
```

- [ ] **Step 2: Add p5.js global variables and preload**

```js
let sfondo;
let occhiSx = [], occhiDx = [], nasi = [], bocche = [], capelli = [], orecchie = [];

function preload() {
  sfondo = loadImage('assets/sfondo.png');
  for (let i = 1; i <= 5; i++) {
    occhiSx.push(loadImage(`assets/occhio-sx${i}.png`));
    occhiDx.push(loadImage(`assets/occhio-dx${i}.png`));
    nasi.push(loadImage(`assets/naso${i}.png`));
    bocche.push(loadImage(`assets/bocca${i}.png`));
    capelli.push(loadImage(`assets/capelli${i}.png`));
    orecchie.push(loadImage(`assets/orecchie${i}.png`));
  }
}
```

- [ ] **Step 3: Add setup() and drawFace()**

```js
let lastChange = 0;
const INTERVAL = 3000;

// current face parts indices
let current = { occhioSx: 0, occhioDx: 0, naso: 0, bocca: 0, capelli: 0, orecchie: 0 };

function setup() {
  createCanvas(736, 1104);
  randomFace();
  lastChange = millis();
}

function draw() {
  if (millis() - lastChange > INTERVAL) {
    randomFace();
    lastChange = millis();
  }
  drawFace();
}

function randomFace() {
  current.occhioSx = floor(random(occhiSx.length));
  current.occhioDx = floor(random(occhiDx.length));
  current.naso = floor(random(nasi.length));
  current.bocca = floor(random(bocche.length));
  current.capelli = floor(random(capelli.length));
  current.orecchie = floor(random(orecchie.length));
}

function drawFace() {
  image(sfondo, 0, 0);
  image(orecchie[current.orecchie], 0, 0);
  image(occhiSx[current.occhioSx], 0, 0);
  image(occhiDx[current.occhioDx], 0, 0);
  image(nasi[current.naso], 0, 0);
  image(bocche[current.bocca], 0, 0);
  image(capelli[current.capelli], 0, 0);
}
```

- [ ] **Step 4: Verify locally**

Open `index.html` in browser. Expected: face appears, changes to a new random face every 3 seconds.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add p5js collage-facce poster"
```
