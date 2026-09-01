# The Coda Zoo

Workflows for [Coda](https://github.com/navis-org/coda), deposited by the people who use it.

Open Coda and pick **Examples ▸ Browse Workflows…** to search this repository from inside the
app; clicking an entry loads it onto the canvas. Nothing here needs to be downloaded by hand.

## What belongs here

A workflow worth depositing is one that answers a question somebody else also has, and that
carries enough explanation to be adapted rather than only re-run. A three-node graph with a
good README beats a twenty-node one without.

Most entries need a token for the connectome they query — Coda keeps credentials in
Connections and none of them ever travel inside a graph. Each entry declares what it needs, and
the browser shows that on the card *before* you open it.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). The short version:

```
workflows/
  your-workflow-slug/
    graph.coda.json     what Coda's Save button writes
    meta.json           name, summary, tags, authors, requires
    README.md           what it does, why the steps are in that order
```

then open a pull request. `index.json` is generated — CI regenerates and commits it.

## How it reaches the app

`index.json` is the only file Coda downloads to build the list — one request to
`raw.githubusercontent.com`, which is CORS-open and caches for five minutes. The graph itself is
fetched when you open an entry.

It is generated, not hand-edited, and CI checks that it matches `workflows/`. The generator
lives in Coda (`scripts/zoo-index.ts`) rather than here because validating a deposited graph
means loading Coda's node registry: whether a node type still exists, whether a param survived a
rename, whether the declared requirements match the dataset nodes in the graph. A weekly
scheduled run re-validates everything against current Coda, so a workflow that Coda has drifted
away from shows up as a failed build here rather than as a broken card in somebody's browser.
