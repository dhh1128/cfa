# Identifying CFAs

## Names
The simplest way to identify a CFA is to give it a human-friendly name. This approach can be used with [metadata](strategies.md#metadata) and [inline content](strategies.md#inline-content). It is required for [sidecars](strategies.md#sidecar), where the identifier for the CFA is simply the name of the [pre](concepts.md#pre-and-co) file, and for [infixes](strategies.md#infix), where the CFA is identified by a 1-to-3-digit number. The virtue of names is that they're easy and intuitive. Their drawback is that their meaning and uniqueness are container-dependent.

## UUIDs
UUIDs are another convenient form of identifier for CFAs. They have the advantage of being globally unique, and therefore container-independent. UUID form 4 carries the additional semantic that all UUIDs created by the same hardware will have something in common, which asserts something about common origin for many CFAs.

## URLs
URLs are another possible identifier type. These have the advantage that the CFA can be described at the URL in question. For example, the musician who wants to unify all works in their career corpus, and who uses the URL `https://mymusicalcareer.com/corpus` as the identifier for this CFA, can publish a catalog or similar information about the corpus at that URL. However, URLs are notoriously unstable; using a PURL may be advisable.

## DIDs
A [decentralized identifier (DID)](https://www.w3.org/TR/did-core/) adds the notion of cryptographically provable control to the CFA. With such identifiers, the owner of the identifier can prove they control the identifier, and by implication, the CFA. The composer who identifies her corpus with a CFA identified by a DID can thus set herself up as the indisputable authority on the question of whether any particular file deserves to be part of the CFA, *in her opinion as the CFA owner*. This does not mean the file's authorship can be proved &mdash; the CFA owner might have stolen it &mdash; but the identity of the CFA's controller becomes verifiable. Further, it becomes possible to carry out a secure communication with the author using a communications technique like [DIDComm](https://identity.foundation/didcomm-messaging/spec/) or the [Trust Spanning Protocol](https://trustoverip.github.io/tswg-tsp-specification/).

## AIDs
An [autonomic identifier (AID)](https://trustoverip.github.io/tswg-keri-specification/#autonomic-identifier-aid) is a form of decentralized identifier that further enhances security and decentralization. Most DID methods depend on the availability of a blockchain for resolution, and do not guard against the possibility that someone other than the creator of the DID registered it. In contrast, AIDs are self-certifying &mdash; meaning they guarantee a perfect chain of custody from inception &mdash; blockchain-independent &mdash; allowing their use with any or no blockchain at all &mdash; and use a sophisticated key pre-rotation technique to maximize key hygeine and provide post-quantum safety.

## SAIDs
A [self-addressing identifier (SAID)](https://www.youtube.com/watch?v=n7tBOPHdtdw) goes one step further still, by binding an identifier to the content of the file itself. This makes the combination of identifier and content tamper-evident, because cannot be changed without also changing the identifier. A SAID thus constitutes a proof of existence for its content, and a digital signature can assert authorship over that content.

SAIDs are normally calculated by inserting a placeholder in a file, calculating a hash, and then replacing the placeholder with the SAID. This works well when file content is oriented toward serialized data structures (e.g., JSON, CBOR, MsgPack). However, it is not possible with many common file types that compress and encrypt, such as .docx, .pdf, and .zip. [Externalized SAIDs](https://dhh1128.github.io/papers/bes.pdf) address this challenge.

## Other identifier types
The foregoing list is not exhaustive. It is entirely possible to use other well-known identifier types as well: DOI numbers, LEIs, ISBNs, Bitcoin addresses, etc.