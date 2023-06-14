# CFA Developers Guide

Implementing support for CFAs requires you to answer the following questions:

1. Do you intend to create CFAs, recognize / enforce / react to CFAs, or both?
2. Which strategies will you support?
3. Which file and container types will you support?

## Recipes

### Enforcing a naming convention

Creating external CFAs in a specific context (e.g., binding email attachments together) is trivial. Assuming you already create data in your context, and you've read the tutorial carefully enough to identify the semantics and strategy you want, you'll just need a few lines of extra code to enforce naming conventions. Something like this:

```pseudocode
def sidecar(pre, extension):
    return pre + extension
def common(co, extension):
    return basename(co) + extension
def infix(stem, extension):
    return stem + '--' + next_infix() 
def save_file_set(container, strategy, stem, streams, extensions):
    """
    Save a set of files into the same container. Set will either have
    no pre file, 
    """
    for stream in streams:
        fname = strategy(stem, extensions[0])
        with container.open(fname, 'wb') as f:
            f.write(data)
        extensions.pop[0]

save_file_set(my_folder, sidecar, [main_file, signature], ['pdf', 'sig'], )
```

### Writing statements

If you're already writing rich file content, such that adding metadata or 

Recognizing and reacting to external CFAs is also easy. When you manipulate a file, check for files in the same container that are associated with the one you're operating on. If you see associations that use the sidecar, common stem, or suffix strategies, help the user maintain the set intelligently. You'll probably need to write a few functions, but nothing ambitious.

The most powerful CFAs use CFA statements. These can be parsed efficiently with regular expressions, but because they live inside file content, you must scan files to find them, and that means you may need support for various file formats. A library should help you with this.


## Statement Syntax
A slightly simplified ABNF for a CFA statement is:

```ABNF
statement: core [x extra] *1STOP

core: view x identifier
extra: pre [x] predicate [x] co
pre: cardinality [[x] descriptor]
co: cardinality [[x] descriptor] 
view: "is" / "depends on" / "part of"   ; compare as keyword
x: 1*WSP                                ; one or more spaces or tabs 

identifier: 1*VCHAR                     ; SAID, AID, DID, URL, UUID, etc.
cardinality: 1*DIGIT / "?"
descriptor: 1*(namer / typer)
namer: "named" [x] name_pat             ; "named" compares as keyword
name_pat: "/" 1*(placeholder / regex_fragment) "/"
regex_fragment: 1*VCHAR
placeholder: "{" pl_word "}             ; pl_word compares as keyword
pl_word: "id" / "fname" / "stem" / "said" / "xsaid"
typer: "media type" [x] type_pat        ; first token compares as keyword
type_pat: "/" regex_fragment "/"
STOP: "."
```

A regex that does good rough parsing on a CFA statement is, in Javascript syntax:

```
/([-._ a-z]+)[ \t]+([^ \r\n\t]+)(?:[ \t]*(\d+|\?)(?:[ \t]*\(([^)]*)\))?[ \t]*([-._ a-z]+?)[ \t]*(\d+|\?)(?:[ \t]*\(([^)]*)\))?)?[ \t]*(?:$|(?<!\.)[\r\n]|\.(?=[ \t\r\n]|$))/gi
```
Note the `gi` after the final slash; these are the flags for repeated matching and case insensitivity.

This regex will find all instances of a CFA statement inside some lines of text, whether the statements are on separate lines or separated by `.` on a single line. The capture groups created by this regex are:

group | mapping
--- | ---
1 | view
2 | identifier
3 | pre cardinality, if any
4 | pre descriptors, if any
5 | predicate, if any
6 | co cardinality, if any
7 | co descriptors, if any

Some symbols in the syntax are keywords (see inline comments). Keywords are matched case-insensitively, ignoring punctuation, and allowing truncation, as a non-technical human might guess. This makes the syntax easy for non-coders to get right. The spec has details; here we'll simply note that "depends-on", "dependsOn", "DEPENDS_ON", "dep", "DepOn" and "D" all match the second alternative in the `view` RULE, for example.

