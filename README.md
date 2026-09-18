# 45-Day Prep Plan — with the Roku CTV study site

The 45-day senior MLE prep plan is the site root. The eighteen-stage Roku study site it was
built around now lives under `backup/`, unchanged and still published.

```
index.html          the prep plan, with progress tracking
backup/index.html   the Roku study site index
backup/*.html       18 stages + 2 primers
```

Start at `index.html`. It links into `backup/index.html`, and that page links back.

## Prep plan

`index.html` carries the full schedule — seven components, 45 days, the sixteen designs, the
sixteen LLM topics, the twelve behavioral stories, the simulations and mock loops — and renders
every one of them as a checkbox. 286 in total, grouped into ten progress meters plus a running
total in the top bar.

Ticks are written to `localStorage` under the key `roku-prep.plan45.v1`, so progress is
**per-browser and per-device**: it survives reloads and redeploys, but does not sync between
machines and is lost if site data is cleared. There is no account and nothing leaves the
browser. Every storage access is wrapped in `try`/`catch`, so the page still renders in private
mode or with storage blocked — it simply stops remembering. The `Reset` button in the top bar
clears every tick after a confirmation.

## Primers

Two optional on-ramps for the Spark and SQL tracks, written intuition-first for readers who
find those stages assume too much. Each builds the mental model from scratch with small
concrete numbers, then ends in three self-check questions.

| # | Page | Topic |
|---|---|---|
| P1 | `backup/spark-foundations.html` | Spark, from one machine to many — read before stage 03 |
| P2 | `backup/sql-foundations.html` | SQL, in the order the engine runs it — read before stage 06 |

## Stages

| # | Page | Topic |
|---|---|---|
| 01 | `backup/ctv-ecosystem.html` | How a CTV ad actually gets served |
| 02 | `backup/roku-platform.html` | What makes Roku's data different |
| 03 | `backup/spark-execution.html` | From DAG to shuffle |
| 04 | `backup/spark-performance.html` | Memory, executors, and the knobs that matter |
| 05 | `backup/spark-streaming.html` | Streaming impressions without lying about time |
| 06 | `backup/sql-at-scale.html` | SQL that survives ten billion rows |
| 07 | `backup/sql-ctv-cookbook.html` | The CTV query cookbook |
| 08 | `backup/query-performance.html` | Reading the plan before blaming the warehouse |
| 09 | `backup/storage-and-modeling.html` | Files, formats, and tables at ten billion rows a day |
| 10 | `backup/identity-graphs.html` | Resolving who is who, at a billion edges |
| 11 | `backup/sketches.html` | Counting without counting |
| 12 | `backup/concurrency-reliability.html` | Two kinds of concurrency, one kind of failure |
| 13 | `backup/ml-fundamentals.html` | ML fundamentals as trade-offs, not definitions |
| 14 | `backup/feature-pipelines.html` | From raw beacons to a served feature |
| 15 | `backup/agentic-systems.html` | Agents that someone has to trust on Monday |
| 16 | `backup/measurement.html` | Numbers someone will argue with |
| 17 | `backup/coding-patterns.html` | The eight problems, in their data-shaped form |
| 18 | `backup/design-framework.html` | Driving the room when the question is vague |

Every stage links to the next one, and stage 18 links back to the index.

## Running it

Static HTML with no build step and no dependencies — each page carries its own styles inline.
Open `index.html` directly, or serve the repository root (not `backup/`, so the links between
the two levels resolve):

```
python3 -m http.server 8000
# then visit http://localhost:8000
```

The only external requests are Google Fonts stylesheets; the pages fall back to system fonts
offline.

## Deployment

`.github/workflows/pages.yml` publishes the repo root to GitHub Pages on every push to `main`
or `claude/web-pages-repo-push-cby8qx`, and can also be run manually from the Actions tab. All
links are relative, so the site works served from the `/roku-prep/` subpath.

The whole repo root is the artifact, so the prep plan and everything under `backup/` publish
together — nothing is built, filtered or transformed on the way out. The published URLs are
`/roku-prep/` for the plan and `/roku-prep/backup/` for the study site.

`configure-pages` runs with `enablement: true`, so it turns Pages on by itself — no manual
Settings step. That part now works: the repository became eligible and run #5 deployed
successfully on 2026-08-12.

The site is served at `https://riteshdhemla.github.io/roku-prep/`.

### Which branches may actually deploy

Listing a branch under `on.push.branches` is necessary but not sufficient. The job targets the
`github-pages` environment, and that environment carries its own **deployment branch policy**.
A push from a branch outside that policy starts the run, holds it at `waiting`, then fails it
in a couple of seconds with no step logs — the job never begins, so there is nothing to debug
in the log output.

Only `claude/web-pages-repo-push-cby8qx` is currently allowed, which is why it is the only
working branch in the trigger list. Adding a branch to `on.push.branches` without also adding
it to the environment does nothing useful: it just produces a red run on every push. To let
another branch publish, add it under **Settings → Environments → github-pages → Deployment
branches** *and* to the trigger list. Otherwise, merge into a branch that is already allowed —
that is the normal path, and it is how work reaches the published site.

