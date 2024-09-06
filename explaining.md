# Explaining CFAs
In [metadata](strategies.md#metadata) and [inline content](strategies.md#inline-content) strategies, CFAs can carry rich descriptions that explain how files relate to one another, how many files of which kinds are in *pre* and *co* sets, and so forth.

A __CFA explanation__ is a comma-separated string with no extra spaces, consisting of 3 tokens:

    nature,[clarifier],identexpr

This string is terminated by whitespace, unless <var>identexpr</var> contains a quoted expression (in which case, it is terminated by the close quote).

## nature
A __nature__ characterizes the relationship between the bound file and the CFA, from the perspective of the bound file. 3 case-sensitive string values are possible. They come from the [Dublin Core metadata standard](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/):

nature | meaning
--- | ---
`identifier` | There is a 1-to-1 relationship between this file and the CFA, and the identifier can be used to look up either one. The file is thus the one and only *pre* file in the CFA. This matches the semantics of the [`identifier`](http://purl.org/dc/terms/identifier) keyword in Dublin Core.
`relation` | This file relates to something else to make its meaning clear. The file is thus co, either to a *pre* or to a common CFA. This matches the semantics of the [`relation`](http://purl.org/dc/terms/relation) keyword in Dublin Core.
`isPartOf` | This file is part of a multi-file pre, and the set as a whole is identified by the CFA. This matches the semantics of [`isPartOf`](http://purl.org/dc/terms/isPartOf) in Dublin Core.

## clarifier
Clarifiers are explained [here](clarifying.md). Clarifiers can be omitted, causing the first and the third commas in an explanation to appear with no intervening content.

## identexpr
The <var>identexpr</var> component of an explanation tells how this cross-file association can be distinguished from others. Normally, this is done by providing a literal identifier &mdash;a name, a UUID, a DID, a SAID, etc. In the the case of externalized SAIDs, the expression is more complex. See [Identifying a CFA](identifying.md).