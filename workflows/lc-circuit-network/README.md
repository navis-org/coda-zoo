## What it does

Finds every `LC*` cell type in the synthetic optic-lobe dataset, pulls their downstream
partners, folds the result to one row per **type pair**, and draws it as a node-link diagram
with a feed-forward layout.

## Why the steps are where they are

The **Group By** before **Build Network** is the load-bearing one. Connectivity comes back one
row per *neuron* pair; a network built straight off that has a node per neuron and is a hairball
at the scale of an optic lobe. Grouping to type pairs first is what makes the picture readable,
and it is the step people leave out.

The weight threshold on the network node is set low deliberately — raise it until the diagram
says something, rather than picking a number first.

## Adapting it

Swap `dataset.mock.opticlobe` for a real dataset node and the rest of the chain is unchanged;
the type pattern in **Find Neurons** is anchored, so `LC.*` matches `LC4` but not `LPLC1`.
