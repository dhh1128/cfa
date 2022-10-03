# Cross-File Associations

Cross-File Associations (CFAs) are conventions that reveal connections among files and file-like objects. They can be used to make software and humans smarter about grouping things together.

CFAs are simple enough that a human can learn them in a couple minutes, but robust enough to provide a foundation for sophisticated software.

Consider an email that includes as attachments a slide deck, photos, a spreadsheet, and a digital signature. A CFA can make it obvious that the digital signature is bound to the spreadsheet. Noticing the CFA, email client can encourage uploading or downloading the two associated files as a unit, and warn if they become separated.

## Basic Concepts

The theory behind CFAs is described in an academic paper, and the specification for CFAs is published as an RFC. We'll skip most of the details in this tutorial, but we still need to define a few terms.

With CFAs, a __file__ is anything that has a name/identifier and content -- the familiar artifact in a file system, but also a web page, a tweet, a piece of data, etc.

When a file is party to a CFA, we say that the file __binds__ the CFA. A given file may bind zero or more CFAs.

CFAs can be either __directional__ or __directionless__. A directional CFA confers special status on a subset of its bound files that are essential; these are known as __core files__. Files that don't have core status are known as __aux files__. A directionless CFA creates a simple set in which all bound files are peer, aux files.

There are different ways to declare a CFA. We call them __strategies__.

When the strategy that binds a file to a CFA requires changes to the content of the file, we say that the strategy is __internal__, or that the file is __internally bound__. When the binding convention manifests outside the content of the file, we say that the strategy is __external__, or that the file is __externally bound__. External and internal strategies are not mutually exclusive.

## Strategies

There are three strategies for declaring a CFA. Each has pros and cons.

### Sidecar

One strategy is to name files in a way that embodies the __sidecar__ naming pattern. In this strategy, there is one core file in the set of associated files, and it has any arbitrary name. Aux files are called "sidecars" because their names are dependent on the core: a sidecar name equals the name of the core file followed by a unique, descriptive suffix.

Returning to the spreadsheet-digital-signature-in-email example that we mentioned above, if the spreadsheet attachment is named `balance-sheet-23q3.xlsx`, and the digital signature attachment is named `balance-sheet-23q3.xlsx.sig`, an email client can know that a sidecar CFA is active; the spreadsheet is the core file, and the digital signature is aux.

![sidecar CFA](sidecar-cfa.png)

Sidecar CFAs are not always pairwise. We could add a third file in the same container and name it `bal-sheet-23q3.xlsx-audit-report.docx`; this would be an additional sidecar bound to the same CFA.

In sidecar names, the boundary between the core name and the unique sidecar suffix must be delimited by a non-word character such as `.`, `-`, or `_`.

Sidecar CFAs are directional and external. They are not as expressive as some other strategies, but they are easy and intuitive.

### Infix

Another simple CFA convention is the __infix__ pattern. In this pattern, files that bind the same CFA share a common 1- or 2-digit infix in their names. The infix cannot begin a name. It must be preceded by two hyphens and followed by a non-word character.

For example, in our spreadsheet-digital-signature-in-email example, we could bind the spreadsheet to its signature by naming the two files `balance-sheet-23q3--01.xlsx` and `sig--01.txt`, respectively. The common `--01` infix is what binds them together.

![infix CFA](infix-cfa.png)

Infixes are compared numerically, not textually; this means an infix of `01` and an infix of `1` are equivalent. Normally, infixes are directionless; however, there are advanced options that can change this.

A file may bind more than one infix in its name: `cozumel-kitesurf--01--04.jpg` is a member of groups using both the `01` and `04` infixes.

### Metadata

Files that are capable of holding metadata may declare CFAs using whatever metadata features their format allows. Metadata-based CFA annotations are essentially `name`=`value` pairs, where `name` categorizes the CFA, and `value` is an identifier. Three categories of `name` are possible:

* __identifier__: A file that carries this type of annotation declares itself to be the one and only core file in a CFA that's uniquely  matches this identifier.