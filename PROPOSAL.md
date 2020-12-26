
## irregular x regular

### e.g. cells x genomic profiles

Suppose:
- genomic profiles have a starting resolution of 200 bp
- resolution is denoted as a tuple `(cell hierarchy level, genomic hierarchy level)`
- cell hierarchy levels include bottom (leaves), top (full summary), and some number of cuts of the dendrogram regularly spaced in between

At resolution `(0, 0)`:
- each cell-axis observation has 1 child (each observation is a leaf node), representing the lowest level of the dendrogram
- each genome-axis observation summarizes 200 bp (200 * 2^0)

At resolution `(1, 0)`:
- each cell-axis observation has 1+ children (internal node), representing the first cut of the dendrogram
- each genome-axis observation summarizes 200 bp (200 * 2^0)

At resolution `(0, 1)`:
- each cell-axis observation has 1 child (each observation is a leaf node)
- each genome-axis observation summarizes 400 bp (200 * 2^1)

At resolution `(1, 1)`:
- each cell-axis observation has 1+ children (internal node), representing the first cut of the dendrogram
- each genome-axis observation summarizes 400 bp (200 * 2^1)

For the irregular cell hierarchy axis, we must store the number of children that each node summarizes. This way we know how tall or wide to make the heatmap cells of the visualization.

- at resolution `(0, _)`: all cell-axis observations are leaf nodes representing single cells, so the counts for a dendrogram with 10 cells would look like `[1, 1, 1, 1, 1, 1, 1, 1, 1, 1]`
- at resolution `(1, _)`: the counts for the first cut may look like `[2, 2, 4, 1, 1]`
- at resolution `(2, _)`: the counts for the second cut may look like `[4, 5, 1]`
- at resolution `(3, _)`: the counts for the third cut may look like `[9, 1]`
- at resolution `(4, _)`: the counts for the lowest resolution may look like `[10]`



root .zattrs

TODO

```js
{
    assembly: 'hg38',
    multiscales: [
        {
            version: '0.1',
            type: 'hierzarrchy',
            name: 'chr1',
            metadata: {
                chromoffset: 0,
                chromsize: 248956422
            },
            datasets: [
                {
                    path: 'chromosomes/chr1/200'
                },
                {
                    path: 'chromosomes/chr1/400'
                },
                {
                    path: 'chromosomes/chr1/800'
                },
                {
                    path: 'chromosomes/chr1/1600'
                }
            ]
        },
        {
            version: '0.1',
            type: 'hierzarrchy',
            name: 'chr2',
            metadata: {
                chromoffset: 248956422,
                chromsize: 491149951
            },
            datasets: [
                {
                    path: 'chromosomes/chr2/200'
                },
                {
                    path: 'chromosomes/chr2/400'
                },
                {
                    path: 'chromosomes/chr2/800'
                },
                {
                    path: 'chromosomes/chr2/1600'
                }
            ]
        },
        ...
    ]
}
```