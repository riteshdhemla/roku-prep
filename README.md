# Interview Stages — CTV data & AI systems

An eighteen-stage study site for Roku data/AI systems interview prep. Each stage covers one
topic grounded in Roku's CTV platform rather than generic examples, and ends in pushbacks
written the way an interviewer actually pushes.

Start at `index.html`.

## Stages

| # | Page | Topic |
|---|---|---|
| 01 | `ctv-ecosystem.html` | How a CTV ad actually gets served |
| 02 | `roku-platform.html` | What makes Roku's data different |
| 03 | `spark-execution.html` | From DAG to shuffle |
| 04 | `spark-performance.html` | Memory, executors, and the knobs that matter |
| 05 | `spark-streaming.html` | Streaming impressions without lying about time |
| 06 | `sql-at-scale.html` | SQL that survives ten billion rows |
| 07 | `sql-ctv-cookbook.html` | The CTV query cookbook |
| 08 | `query-performance.html` | Reading the plan before blaming the warehouse |
| 09 | `storage-and-modeling.html` | Files, formats, and tables at ten billion rows a day |
| 10 | `identity-graphs.html` | Resolving who is who, at a billion edges |
| 11 | `sketches.html` | Counting without counting |
| 12 | `concurrency-reliability.html` | Two kinds of concurrency, one kind of failure |
| 13 | `ml-fundamentals.html` | ML fundamentals as trade-offs, not definitions |
| 14 | `feature-pipelines.html` | From raw beacons to a served feature |
| 15 | `agentic-systems.html` | Agents that someone has to trust on Monday |
| 16 | `measurement.html` | Numbers someone will argue with |
| 17 | `coding-patterns.html` | The eight problems, in their data-shaped form |
| 18 | `design-framework.html` | Driving the room when the question is vague |

Every stage links to the next one, and stage 18 links back to the index.

## Running it

Static HTML with no build step and no dependencies — each page carries its own styles inline.
Open `index.html` directly, or serve the directory:

```
python3 -m http.server 8000
# then visit http://localhost:8000
```

The only external requests are Google Fonts stylesheets; the pages fall back to system fonts
offline.

## Deployment

`.github/workflows/pages.yml` publishes the repo root to GitHub Pages on every push to the
default branch, and can also be run manually from the Actions tab. All links are relative, so
the site works served from the `/roku-prep/` subpath.

`configure-pages` runs with `enablement: true`, so it turns Pages on by itself once the
repository is eligible — no manual Settings step.

**The repository is not eligible yet.** It is private, and Pages on a private repository
requires a paid plan, so the deploy currently fails at `configure-pages` with
`Create Pages site failed: Resource not accessible by integration`. To publish, either:

- make the repository public — **Settings → General → Danger Zone → Change visibility** — then
  re-run the workflow from the Actions tab; or
- upgrade the account to GitHub Pro and re-run.

Once it succeeds the site is served at `https://riteshdhemla.github.io/roku-prep/`.

