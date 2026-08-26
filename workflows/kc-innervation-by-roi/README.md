## What it does

Counts postsynapses per ROI for each Kenyon cell subtype and stacks them into a bar chart, so
the calyx-dominated subtypes separate from the lobe-dominated ones at a glance.

## Why Group By comes after ROI Counts

**ROI Counts** returns one row per neuron per ROI. Grouping *after* it aggregates across the
neurons of a type while keeping the ROI split, which is what makes a stacked bar meaningful —
group first and the ROI dimension is already gone.

## Adapting it

Point it at a real hemibrain dataset node and add a token in Connections. The ROI names differ
between connectomes, so the chart's category order is worth revisiting after a swap.
