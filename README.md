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

The workflow enables Pages itself on its first successful run, so no manual Settings step is
needed. Pages on a private repository requires a paid plan, though — on a free account, make
the repo public first (**Settings → General → Change visibility**), then re-run the workflow.

