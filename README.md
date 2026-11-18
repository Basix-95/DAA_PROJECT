# Financial Maximum Gain Window Visualizer

Open `index.html` in any modern browser. No server, installation, or internet connection is needed.

## Inputs
- CSV with `day` in the first column and one column per asset.
- Each cell is an additive gain in consistent units; `NA` or blank means unavailable.
- K is the maximum number of switches; cost is a uniform nonnegative cost per switch.

## Algorithm
Layered-DAG dynamic programming using states `(time, asset, switches_used)`. At each state, the algorithm considers starting a new contiguous window (only with zero switches), holding the current asset, or switching from a different asset at the preceding period. A predecessor chain reconstructs the optimal path. Ties favor fewer switches, earlier start, then shorter window.

Time complexity: O(N M^2 (K+1)). Memory: O(N M (K+1)) for reconstruction.

## Samples
- `sample-paper.csv`: matches the four-day example in the project document. With K=1 and cost=2, the optimum is day 2-4: A -> A -> B, net gain 18.
- `sample-extended.csv`: 8 days and 3 assets. Try K=2 and cost=2.
- `sample-no-profit.csv`: all nonpositive outcomes and missing states.

The DAG view collapses the switch-count dimension for clarity, while the actual solver tracks it. This is an educational historical optimizer, not investment advice.
