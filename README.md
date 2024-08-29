<!-- Ideas:

* what relationships does this file have to other files (and to its container)
* what kind of relationship is it?
* how many in the relationship?
* what are the types of the files?
* 
* CFA statements in form: s i identifier clarifier
* some statements can be about container (first letter is 'c'...)
* embed a filename regex in SAID placeholder
* declare that a file must have a sidecar named .cfas?
    s i {fname} 1c1 -->

# Cross-File Associations

Cross-File Associations (CFAs) are a way to declare relationships among files and file-like objects. They help software and humans to be smarter about grouping things together.

CFAs aren't for expressing every nuance of relationships; rather, they make it easy to say the basics. They're simple enough for anybody to use without special tools, but sophisticated enough to enable powerful features in software that wants to be helpful.

## Example

Consider an email that includes as attachments a slide deck, photos, a spreadsheet, and a digital signature. A CFA can make it obvious that the digital signature is bound to the spreadsheet. Noticing the CFA, email clients can encourage uploading or downloading the two associated files as a unit, and warn if they become separated.

![CFA example](cfa-example.png)

<hr>

Continue the tutorial at: [concepts &gt;](concepts.md)
