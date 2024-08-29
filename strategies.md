# Strategies

Several strategies for declaring a CFA are standardized.

## Sidecar

One simple strategy is to name files in a way that embodies the __sidecar__ naming pattern. In this strategy, there is one pre file in the CFA, and it has any arbitrary name. Any co files are called "sidecars" because their names are dependent on the pre: a sidecar name equals the name of the pre file followed by a unique, descriptive suffix.

Referencing the [spreadsheet-digital-signature-in-email example](README.md#example) that's mentioned in the introduction, if the spreadsheet attachment is named `balance-sheet.xlsx`, and the digital signature attachment is named `balance-sheet.xlsx.sig`, an email client can know that a sidecar CFA is active; the spreadsheet is the pre file, and the digital signature is co.

![sidecar CFA](sidecar-cfa.png)

Sidecar CFAs are not always pairwise. We could add a third file in the same container and name it `balance-sheet.xlsx-audit-report.docx`; this would be an additional sidecar bound to the same CFA.

In sidecar names, the boundary between the pre name and the unique sidecar suffix must be delimited by one or more non-word characters such as a space, `.`, `-`, or `_`.

Sidecar CFAs are *directional* and *external*. Like all external strategies, they are also container-dependent; the relationship implied by the naming convention cannot be evaluated except within the context of a shared container.

Sidecar naming is easy and intuitive. In fact, this strategy is already used by many individuals and software packages; they are making CFAs even if they don't describe it in these terms. However, sidecars are not as powerful as some other strategies. They can be extended somewhat with [clarifiers](clarifiers.md).

## Shared stem

A variation on sidecars is to associate files by giving their name a common __stem__, varying only at the end. The stem of a filename is the portion before the first `.` character. Digital cameras and related software often uses this strategy &mdash; saving `.raw` + `.tiff` or `.heic` + `.jpg` versions of each photo as associated pairs.

![shared stem CFA](shared-stem-cfa.png)

Although shared stems resemble sidecars in some ways, their semantics are different. Shared stem CFAs are *common*; within the files that share a stem, there is no notion of dependency. This makes them an awkward fit for the spreadsheet-digital-signature-in-email example we used above. Naming the spreadsheet `balance-sheet.xlsx` and the signature `balance-sheet.sig` *does* connect them, but it does not convey the idea that the signature is meaningless without the spreadsheet.

Like sidecars, shared stems are easy and intuitive, but their expressiveness is limited. They can be extended somewhat with [clarifiers](clarifiers.md).

## Infix

Another simple and external CFA convention is the __infix__ pattern. In this pattern, files that bind the same CFA share a common 1-to-3-digit infix in their names. The infix cannot begin a name. It must be preceded by two hyphens and followed by a non-word character.

Suppose a police photographer is documenting an accident that involved several vehicles, and each will be photographed from multiple angles and lighting conditions. They might associate photos of vehicle 1 using a common infix: `front-bumper--01.jpg` and `drivers-door--01.jpg`, respectively.

![infix CFA](infix-cfa.png)

Infixes are compared numerically, not textually; this means an infix of `01` and an infix of `1` are equivalent.

A file may bind more than one infix in its name: `tangled-bumpers--1--3.jpg` is a member of CFAs using both the `1` and `3` infixes, and might show both vehicles 1 and 3 in our example.

Normally, infix CFAs are *common*. They can be extended somewhat with [clarifiers](clarifiers.md).

## Metadata
Many popular file formats support arbitrary metadata. HTML allows &lt;meta&gt; tags; markdown has [YAML frontmatter](https://docs.github.com/en/contributing/writing-for-github-docs/using-yaml-frontmatter); PDFs and most Adobe file formats support [XMP metadata](https://en.wikipedia.org/wiki/Extensible_Metadata_Platform); Microsoft Office formats support keyword tagging. Such files can bind CFAs internally, by declaring one or more special <var>name</var>, <var>value</var> metadata pairs in a form that we could describe with the symbolic notation `cfaid=explanation`. (The `cfaid` and `explanation` tokens in this notation are placeholders. The equals sign is not actually used in the syntax; it represents whatever mapping mechanism the metadata format uses to associate a name with a value.)

Using metadata to bind CFAs is more expressive but also more complex than external strategies.

Each CFA metadata pair conveys the idea, "This file binds a CFA identified by `cfaid`, and its type and meaning are `explanation`." Files that have CFA metadata sharing the same identifier in the `cfaid` portion bind the same CFA and are thus part of the same set. The `cfaid` part of a CFA metadata pair always starts with the namespace, `CFA:` and is followed by an arbitrary identifier. The type of identifier influences the semantics of the CFA &mdash; for example, enabling an owner to prove control cryptographically. For more information about the two metadata components, see [Identifying CFAs](identifying.md) and [Explaining CFAs](explaining.md).

Importantly, files bound to a CFA via metadata can be part of the same set *whether or not they are in the same container, and whether or not they are owned or controlled by the same party*. This can solve certain centralization problems. 

Suppose that Alice, a composer of classical music, wants to mark all her compositions as belonging to the overall corpus of compositions that she creates during her career. Alice can embed metadata in each new digital file that she authors, marking it internally as part of a CFA identified by the UUID `0bbfac55-81c9-48ab-8934-9a46c64c0703`. That UUID then binds all her creative output together, even if it's built with a variety of tools, for many clients, across decades, and stored in a hodge-podge of storage containers.

Building on this example, suppose that Alice writes a piece of music for the violin. Later, she arranges a derivative version for the clarinet. Since these two pieces of music are part of her overall corpus, they should bind the CFA mentioned previously. In addition, these two pieces of music have a more specific relation to one another. The clarinet version is co &mdash; dependent upon the original violin composition &mdash; which is pre. In such a case, and assuming the composer chooses arbitrary identifier `68d15148-a0bd-4716-9618-061a17389689` for the CFA describing the pair, she might embed metadata in her pre violin composition that says:

    CFA:68d15148-a0bd-4716-9618-061a17389689=identifier

This says that the UUID on the left is the identifier for the CFA *and* for her pre violin file, which have a 1-to-1 relationship. She would then embed metadata in her co clarinet arrangement that says:

    CFA:68d15148-a0bd-4716-9618-061a17389689=relation 

This says that the UUID on the left is the identifier for a CFA to which the clarinet file is related, directionally, as a co file.

![directed metadata CFA](directed-metadata-cfa.png)

Now suppose that Alice writes a symphony that has 4 movements. Each movement is a separate digital file emitted by her composition software. She wants them to be associated with the arbitrary identifier `972d639a-04d7-4c1e-9ea9-196e94b05eb0` to bind her symphony together, so she embeds metadata in each movement's digital file. The metadata says:

    CFA:972d639a-04d7-4c1e-9ea9-196e94b05eb0=isPartOf

The metadata in this situation also expresses a directional CFA, but all the files we've talked about so far are pre. However, the possibility of co is still useful. If three recordings of this symphony are performed, the composer can mark the recordings as co, dependent on the multi-part pre: 

![multi-part pre metadata CFA](multi-pre-metadata-cfa.png)

For metadata schemes that require a URL to define the CFA namespace, the URL to use is: https://purl.archive.org/purl/cfa.

## Inline content

The final CFA strategy that we'll cover here is to embed a __CFA statement__ directly into the searchable content of a file. A CFA statement is literal string in `cfaid=explanation` format, and expresses the same information as metadata would. Files that have no native metadata support, like text files or the body of an email, can use this strategy. The requirement that such CFAs be part of searchable content guarantees that a simple scan with features native to the format can find them.

For example, if I wanted to bind a Google Slides presentation to a CFA, I could add a CFA statement to the speaker notes on the first slide, and find it again with a simple search:

![CFA as inline content in Google Slides](slides-inline-content.png)

In some cases, CFA statements might create visual clutter that's undesirable. They could be placed in a document header or footer, and hidden by customizing the text color.

An important use for this strategy is to apply it to a [container](concepts.md#building-blocks) (folder, zip file, email), so that the container itself can bind CFAs and possibly function as a pre file. Since the content of a container is files, adding "inline" content to the container means adding a file to it. By convention, inline CFA content in containers must be in a file named `.cfas`. This file must be plain text and must consist of one or more CFA statements, one per line. Any lines that don't match the CFA statement syntax are treated as comments.

[&lt; concepts](concepts.md) | [statements &gt;](statements.md)

