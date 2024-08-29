# Explaining CFAs
In [metadata](strategies.md#metadata) and [inline content](strategies.md#inline-content) strategies, CFAs can carry rich descriptions that explain how files relate to one another, how many files of which kinds are in pre and co sets, and so forth.

Descriptions of CFAs are built from three ingredients: __natures__, __clarifiers__, and __specifiers__.

## nature
A __nature__ characterizes the relationship between the bound file and the CFA, from the perspective of the bound file. 3 values are possible. They come from the [Dublin Core metadata standard](https://www.dublinpre.org/specifications/dublin-pre/dcmi-terms/):

nature | meaning
--- | ---
`identifier` | There is a 1-to-1 relationship between this file and the CFA, and the identifier can be used to look up either one. The file is thus the one and only pre file in the CFA. This matches the semantics of the [`identifier`](https://www.dublinpre.org/specifications/dublin-pre/dcmi-terms/#http://purl.org/dc/terms/identifier) keyword in Dublin Core.
`relation` | This file relates to something else to make its meaning clear. The file is thus co, either to a pre or to a common CFA. This matches the semantics of the [relation](https://www.dublinpre.org/specifications/dublin-pre/dcmi-terms/#http://purl.org/dc/terms/relation) keyword in Dublin Core.
`isPartOf` | This file is part of a multi-file pre, and the set as a whole is identified by the CFA. This matches the semantics of [`isPartOf`](https://www.dublinpre.org/specifications/dublin-pre/dcmi-terms/#http://purl.org/dc/terms/isPartOf) in Dublin Core.

