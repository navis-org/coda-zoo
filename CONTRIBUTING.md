# Depositing a workflow

## 1. Build it in Coda and save it

Get the graph working, then **Save ▸ Download** — that writes a `.coda.json`. Before you do:

- **Take the credentials out of the picture.** They are never *in* the picture — Coda keeps
  tokens in Connections and no credential is ever written into a graph — but check that nothing
  else identifying went in, in particular a note you wrote to yourself and a Custom dataset node
  pointing at an internal server.
- **Trim the run to something reproducible.** A neuron selection of 10,000 ids is ~110 kB of
  params in one node and pins the workflow to one dataset version. A pattern that finds the same
  cells is smaller, and it is what somebody adapting the workflow actually wants.
- **Write the notes.** Text notes on the canvas are the only documentation most readers will
  see. Say why the threshold is 10, not that there is a threshold.

## 2. Make the directory

```
workflows/<slug>/
  graph.coda.json
  meta.json
  README.md
```

`<slug>` is kebab-case, is the entry's permanent identity, and should describe the *result*
rather than the method — `lc-outputs-by-partner-type`, not `groupby-demo`.

`meta.json`:

```json
{
  "name": "LC outputs by partner type",
  "summary": "Find LC neurons, pull downstream partners, aggregate synapses by partner type.",
  "tags": ["connectivity", "optic-lobe", "hemibrain"],
  "authors": [{ "name": "Your Name", "github": "your-login" }],
  "requires": ["neuprint"]
}
```

- **`summary` is one line**, under 140 characters. It is what the card shows, and a paragraph
  pasted here is not wrapped into more room — it is cut off. The long version goes in the README.
- **`tags` are lowercase** and are how anybody finds this. Name the dataset, the kind of
  analysis, and the output.
- **`requires`** lists the registered sources the graph's dataset nodes reach for: `neuprint`,
  `cave`, `catmaid`, `mock`. Use `mock` for a workflow that runs on the synthetic datasets and
  needs no token at all — those are the most useful entries here, because anybody can open one.

  You have to write it, and the generator checks it against the graph. That is deliberate: the
  point is that you notice what your workflow asks of a reader.

`README.md` is the long description, rendered in the browser's detail panel and on GitHub.
Three headings work well: *What it does*, *Why the steps are where they are*, and *Adapting it*.
The middle one is the part that is worth your time — a graph shows what it computes and says
nothing about why.

## 3. Regenerate the index

`index.json` is generated. You need a checkout of Coda beside this one:

```bash
git clone https://github.com/navis-org/coda
cd coda && pnpm install
pnpm zoo:index ../coda-zoo
```

It validates every entry against Coda's node registry and rewrites `index.json`. Errors fail the
build and have to be fixed; warnings ship. Commit the regenerated `index.json` with your entry.

If you would rather not install Coda, open the pull request without it — CI will tell you
exactly what the index should contain, and a maintainer can regenerate it.

## 4. Open a pull request

Review is about whether the workflow is useful and whether the README makes it adaptable. The
mechanical checks are CI's job.

## Changing or withdrawing an entry

Edit it in place; the slug is the identity and should not change, because it is what an entry's
URL is built from. To withdraw one, delete the directory and regenerate. There is no deprecation
mechanism — Coda fetches the current index every five minutes, so a removed entry is gone from
the browser within the hour.
