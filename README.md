# Dollar Darwin

**Natural selection for code, for under one dollar.**

What if you stopped asking an AI for the right answer, and let evolution find it instead?

Dollar Darwin applies natural selection to programs. Meta's Muse Ember writes a population of programs that play Snake. The browser lets them compete. The weakest die out, the best survive, and Ember breeds the next generation from the survivors. Nobody writes the winning program. It emerges.

Built at the OpenRouter x Meta Build Day (The $1 Challenge).

## Why this needs a cheap model

Evolution is wasteful by design: most offspring are worse than their parents, and progress comes from the few that are not. That only pays off when a single attempt costs almost nothing.

With an expensive model you ask once and hope. With Muse Ember you can afford to ask a hundred times and keep the best. In our runs a generation of 10 programs cost roughly 3 cents.

## The evolutionary loop

| Evolution | In Dollar Darwin |
| --- | --- |
| Population | 10 `move(state)` programs per generation, each written by Muse Ember |
| Environment | A 12x12 Snake board with 8 obstacles |
| Fitness | Average number of apples eaten across 3 fixed boards |
| Selection | The best 2 programs survive, including survivors from earlier generations |
| Mutation | Ember rewrites each survivor, knowing its score and how it died on every board |
| Variation | Each child gets a different hint, for example "check for dead ends with a flood fill" or "try a clearly different strategy" |

Scoring happens in the browser, uses no model and costs nothing. Only writing and rewriting programs costs money.

## What you see

- The current winner playing Snake
- The best score per generation, plus one dot for every program Ember wrote
- The source code of each generation's winner, selectable by generation
- The number of model calls and the money spent so far. The cost is the real amount OpenRouter reports for each call, not an estimate.

In one recorded run the winner went from 55.7 apples in generation 1 to 78.7 in generation 4.

## Where Muse Ember and OpenRouter are used

Every program in every generation is written by `meta/muse-ember`, called through the OpenRouter chat completions API. There is no other model and no backend. The loop, the game, the sandboxed evaluation (one Web Worker per program, with a timeout) and the UI are a single HTML file.

## Run it

1. Open `index.html` in a browser.
2. Paste an OpenRouter API key. It stays in the page and is never stored.
3. Model: `meta/muse-ember`.
4. Press **Start evolution**.

The run stops on its own when the budget field (default $1) is reached.

## Known limits

- Fitness is measured on the same 3 boards every generation, so programs can overfit to them.
- With only 2 survivors and 10 children, runs tend to plateau after a few generations. A larger population should go further.

## Beyond Snake

Snake is the part you can watch. The same loop works for anything that can be scored automatically: a function with tests, a prompt with an eval, a query with a runtime.
