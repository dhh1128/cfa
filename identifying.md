# Identifying CFAs

All identifiers for CFAs are interpreted according to the ambient text encoding. They may or may not be case-sensitive, depending on the semantics of their corresponding identifier scheme, as noted below. 

## Names
The simplest way to identify a CFA is to give it a human-friendly name. This approach can be used with [metadata](strategies.md#metadata) and [inline content](strategies.md#inline-content). It is required for [sidecars](strategies.md#sidecar), where the identifier for the CFA is simply the name of the [pre](concepts.md#pre-and-co) file, and for [infixes](strategies.md#infix), where the CFA is identified by a 1-to-3-digit number. The virtue of names is that they're easy and intuitive. Their drawback is that their meaning and uniqueness are container-dependent.

If a name contains spaces, begin and end the name component of the [explanation](explaining.md) with double quote characters (`"`, U+0022); these quotes are considered delimiters, not part of the name value itself. Quotes inside a quoted name must be escaped with a backslash. No other escape sequences are supported. Tabs, carriage returns, line feeds, any zero-width or invisible characters are illegal.

Names as CFA identifiers are case-preserving, but not case-sensitive. That is, the name "my corpus" and the name "My Corpus" must be treated as equivalent, for matching purposes, but software must not normalize the case.

## UUIDs
UUIDs are another convenient form of identifier for CFAs. They have the advantage of being globally unique, and therefore container-independent. UUID form 4 carries the additional semantic that all UUIDs created by the same hardware will have something in common, which asserts something about common origin for many CFAs.

Per [RFC 4122](https://www.rfc-editor.org/rfc/rfc4122), UUIDs MUST be compared in a case-insensitive way. They should also be compared without regard to whether they are written with enclosing braces or with internal hyphens. However, as CFA identifiers, it is important to distinguish UUIDs from arbitrary string names. Therefore, in CFA metadata explanations, UUIDs MUST be written with hyphens; they SHOULD be written in lower-case form without enclosing braces. Any CFA implementation that detects a UUID MUST compare it to other UUID values per RFC 4122 rules.

A variation on UUIDs as CFA identifiers that adds some sorting features is [ULIDs](https://www.baeldung.com/cs/ulid-vs-uuid).

## URLs
URLs are another possible identifier type. These have the advantage that the CFA can be described at the URL in question. For example, the musician who wants to unify all works in their career corpus, and who uses the URL `https://mymusicalcareer.com/corpus` as the identifier for this CFA, can publish a catalog or similar information about the corpus at that URL. However, URLs are notoriously unstable; using a [PURL](https://purl.archive.org/) may be advisable.

Some systems that process URLs may be insensitive to case differences in parts of some URLs, but as CFA identifiers, URLs must be treated as case-sensitive.

## DIDs
A [decentralized identifier (DID)](https://www.w3.org/TR/did-core/) adds the notion of cryptographically provable control to the CFA. With such identifiers, the owner of the identifier can prove they control the identifier, and by implication, the CFA. The composer who identifies her corpus with a CFA identified by a DID can thus set herself up as the indisputable authority on the question of whether any particular file deserves to be part of the CFA, *in her opinion as the CFA owner*. This does not mean the file's authorship can be proved &mdash; the CFA owner might have stolen it &mdash; but the identity of the CFA's controller becomes verifiable. Further, it becomes possible to carry out a secure communication with the author using a communications technique like [DIDComm](https://identity.foundation/didcomm-messaging/spec/) or the [Trust Spanning Protocol](https://trustoverip.github.io/tswg-tsp-specification/).

Although the [DID spec](https://www.w3.org/TR/did-core/#method-syntax) allows DID methods to define their own case-sensitivity rules, CFA implementations MAY assume that all DIDs are case-sensitive.

## AIDs
An [autonomic identifier (AID)](https://trustoverip.github.io/tswg-keri-specification/#autonomic-identifier-aid) is a form of decentralized identifier that further enhances security and decentralization. Most DID methods depend on the availability of a blockchain for resolution, and do not guard against the possibility that someone other than the creator of the DID registered it. In contrast, AIDs are self-certifying &mdash; meaning they guarantee a perfect chain of custody from inception; blockchain-independent &mdash; allowing their use with any or no blockchain at all; and use a sophisticated key pre-rotation technique to maximize key hygeine and provide post-quantum safety.

AID values are case-sensitive.

## SAIDs
A [self-addressing identifier (SAID)](https://www.youtube.com/watch?v=n7tBOPHdtdw) binds an identifier to the content of the file itself. This makes the combination of identifier and content tamper-evident, because cannot be changed without also changing the identifier. A SAID thus constitutes a proof of existence for its content, and a digital signature can assert authorship over that content.

SAIDs are normally calculated by inserting a placeholder in a file, calculating a hash, and then replacing the placeholder with the SAID. This works well when file content is oriented toward serialized data structures (e.g., JSON, CBOR, MsgPack). However, it is not possible with many common file types that compress and encrypt, such as .docx, .pdf, and .zip. [Externalized SAIDs](https://dhh1128.github.io/papers/bes.pdf) address this challenge. An externalized SAID requires an internal declaration of a SAID regex, with the SAID value itself appearing in the filename. It is thus has both internal and external characteristics. For example, suppose that the XMP metadata of a PDF contained this metadata pair:

    CFA1=identifier,1v1,XSAID:".*-E###########################################\.pdf"

This would mean, "This file binds a SAID as its one and only *pre* file, and it is accompanied by a *co* file that verifies it (e.g., a digital signature). The SAID that identifies the CFA is a CESR-encoded Blake3 hash that appears as the last token in the filename, before the `.pdf` extension."

The quoted XSAID expression uses python raw string (`r"..."`) syntax, and it must match the entire filename. However, the literal character sequence `E###########################################` is matched to a valid SAID sequence instead of being interpreted by regex rules.

SAIDs are case-sensitive.

## Namespaced SAIDs
An AID (or a DID) can be combined with a SAID to get the benefits of both: cryptographic control plus tamper-evident content addressing. Whoever controls the AID or DID is the controller of the namespace, and the SAID references content under their control. In such cases, the identexpr component of the explanation begins with a cryptographic identifier that constitutes the namespace, and is followed by a dot, then a SAID or externalized SAID. For example:

    CFA1=identifier,1v1,EcGraT4XWiPBnyV7IcSklDxXOF-xfoyOz0WURwoHW14y.".*-E###########################################\.pdf"

## Other identifier types
The foregoing list is not exhaustive. It is entirely possible to use other well-known identifier types as well: DOI numbers, LEIs, ISBNs, Bitcoin addresses, etc. The common constraint is that these identifier types 