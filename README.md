# Dollar Darwin

**Evolution on a budget: Muse Ember breeds a Snake-playing program for under one dollar.**

Built at the OpenRouter x Meta Build Day (The $1 Challenge).

## What it does

Instead of asking a large model once, Dollar Darwin asks a small, cheap model about a hundred times and lets the answers compete.

1. Muse Ember writes 10 different `move(state)` functions for a Snake game.
2. The browser runs every program on 3 fixed boards and scores it. This step uses no model and costs nothing.
3. The best 2 programs survive.
4. Muse Ember gets each survivor back, together with its score and the reason it died on each board, and writes improved versions.
5. Repeat for several generations.

The page shows the current champion playing, the score per generation, the champion's source code, and a live counter of what the run has cost so far. The cost is the real amount reported by OpenRouter for each call, not an estimate.

## Where Muse Ember and OpenRouter are used

Every program in the population is written by `meta/muse-ember`, called through the OpenRouter chat completions API. There is no other model and no backend. The evolutionary loop, the game, the sandboxed evaluation (Web Workers with a timeout) and the UI are a single HTML file.

## Run it

1. Open `index.html` in a browser.
2. Paste an OpenRouter API key. It stays in the page and is never stored.
3. Model: `meta/muse-ember`.
4. Press **Start evolution**.

The run stops on its own when the budget field (default $1) is reached.

## Game rules given to the model

12x12 grid, 8 obstacles, the snake dies on walls, obstacles, its own body, or after 200 steps without food. Fitness is the average number of food items eaten across 3 fixed boards.
