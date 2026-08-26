## What it does

Fetches LC4 skeletons and their synapse locations from the synthetic optic-lobe dataset and
draws both in one 3D viewer — skeletons coloured by type, synapses by polarity.

## Why two branches into one viewer

Skeletons and synapses are separate fetches with separate schemas, and the 3D viewer takes
several geometry inputs precisely so they can be overlaid without being joined into one table
first. Joining them would force a single colour encoding on both.

## Adapting it

The neuron count is where this one gets expensive against a real backend. Narrow **Find
Neurons** before you widen the pattern.
