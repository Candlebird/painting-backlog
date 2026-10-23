# Painting Backlog

Paint progress, model by model, for every unit in the group's [Crusade Dataslate](https://candlebird.github.io/crusade-dataslate/) forces. Live at https://candlebird.github.io/painting-backlog/.

- A single `index.html` with no build step. GitHub Pages serves `main` as-is.
- Uses the Dataslate's Firebase project and Google sign-in. It **reads** `forces/*` live (new units and model counts show up as soon as they change in the Dataslate) and **writes** only `paint/*` and `paintPhotos/*`. The Dataslate never reads those.
- Access rules for `paint/*` and `paintPhotos/*` are in the Dataslate repo's `firestore.rules`.

## Data

`paint/{unitId}` (or `paint/x-{uuid}` for models not in a force):
`{ owner, unitId?, forceId?, name, unitType?, size, n: [built, primed, painted, based], recipe?, notes?, photo?, updatedAt }`.
Unbuilt is whatever is left of the unit's size. If a unit shrinks in the Dataslate, the least-finished models are dropped first.

`paintPhotos/{id}`: `{ owner, data }`, a JPEG data URL shrunk to fit under 600 KB.
