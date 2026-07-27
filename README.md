# Малка Трапеза (Baby Table) — 11-month, egg-free, seasonal meal picker

A single-file, self-hosted web app. No backend, no database, no external
calls except the Google Fonts CSS (remove that `<link>` in `index.html`
if you need it fully offline — it'll fall back to system fonts).

## Run it

Any of these work:

- **Just open it.** Double-click `index.html` — it works straight from
  disk in any modern browser.
- **Serve it locally** (nicer for phones on the same wifi):
  ```
  cd babyapp
  python3 -m http.server 8080
  ```
  then visit `http://<your-computer-ip>:8080` from another device.
- **Self-host properly**: copy `index.html` to any static hosting —
  nginx, Caddy, Apache, a Raspberry Pi, a NAS's web share, GitHub Pages
  (private repo), etc. It's one file, so deployment is just "put the
  file somewhere a browser can reach."

## What's inside

- **Seasonal picks tab** — pick a month (defaults to the current one)
  and see egg-free, age-appropriate recipes built around what's
  actually in season in Bulgaria that month (root veg and stored fruit
  in winter, stone fruit and tomatoes/peppers in summer, etc.).
- **Build from my fridge tab** — tick what you have at home; it shows
  full-match recipes first, then near-matches with what's missing.
- All recipes are hard-coded with no egg in any ingredient list, and
  textures are labelled (smooth purée / soft mash / finger food) for
  an 11-month-old. Grapes and corn kernels are always specified
  peeled/mashed rather than served whole, since they're common
  choking hazards at this age.

## Extending it

Everything lives in the `RECIPES`, `SEASON`, and `FRIDGE_GROUPS`
JavaScript objects near the top of the `<script>` block in
`index.html` — no build step, just edit and refresh. To add a recipe:

```js
{
  name: "…",
  season: ["June","July"],       // months it fits, or MONTHS.slice() for year-round
  texture: "Soft mash",
  ingredients: ["zucchini","rice","olive oil"],
  steps: "…"
}
```

## What this app deliberately does *not* do

It has no medical logic. It won't account for:
- calorie/protein targets during post-surgical recovery,
- neutropenic food-safety precautions if immune status is still
  recovering from treatment,
- reintroducing textures/volumes after a hospital stay,
- allergies beyond egg (add exclusions manually if there are others).

Those should come from the child's oncology dietitian or paediatrician
— treat this as a seasonal/logistics tool on top of whatever plan
they set, not a replacement for it.
