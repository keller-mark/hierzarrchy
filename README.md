# hierzarrchy
Python helpers for storing multi-scale irregular-by-regular and irregular-by-irregular hierarchies with Zarr.
JavaScript helpers for reading the stores with Zarr.js.

🚧 work in progress 🚧

Problem:
- Hierarchical clusterings of cells and genes introduce two irregularly shaped trees (one on each axis) in which two nodes at the same level in the tree may have different numbers of leaves.
- Hierarchical clusterings of cells which correspond to genome-wide profiles intoduces one irregularly shaped tree (for the cells axis) and one regularly shaped tree (for the genome axis (HiGlass)).
- Storage of multi-scale data with Zarr has primarily focused on pre-computing image pyramids, which have a regular shape.

Notes:
- Hierarchical clustering introduces a partial ordering of nodes. However, initially this repository will focus on cases in which there is an optimal ordering that has been chosen.
  - For example, the gene axis of a gene-by-cell matrix may be optimally ordered for visualization using the method proposed by Bar-Joseph et al. 2001.
- When determining the best storage layout to minimize the number of chunks requested, focus on visualization:
  - Typically looking at a single resolution at a time (along each axis), so fine to store different resolutions in different groups
  - Typically panning along a single resolution at a time, so chunks should store values contiguously within each resolution

- This feels like a problem that must have already been solved before and I just don't know its computer science terminology. Perhaps it is a [space-filling tree](https://en.wikipedia.org/wiki/List_of_data_structures#Space-partitioning_trees)? 

Resources
- [Zarr multiscale convention](https://github.com/zarr-developers/zarr-specs/issues/50)
- [HiGlass Zarr datafetchers](https://github.com/higlass/higlass-zarr-datafetchers)
- [Bar-Joseph et al. 2001](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.83.6798&rep=rep1&type=pdf)

![irregular by regular](./img/irregular-regular.png)

![irregular by irregular](./img/irregular-irregular.png)
