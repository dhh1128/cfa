# CFA statements

A CFA statement is structured a bit like a sentence in natural language: it consists of a sequence of space-separated tokens, on a single line. When multiple CFA statements appear together, they may be separated by a `.` character. An example of a CFA statement is:

```
is 68d15148-a0bd-4716-9618-061a17389689 1 v 1 (n /{stem}\.sig$/).
```

In plain English, this statement says: "*This file has a pre role in a CFA identified by the string `68d15148-a0bd-4716-9618-061a17389689`. Exactly 1 pre and 1 co file are known to bind this CFA, and the co file provides cryptographic verification of the pre file. The co file should have a filename that is the same as the pre file, but with an extra `.sig` as a suffix.*"

Statements follow this token sequence, where tokens are space-separated like words in a sentence:

```
nature identifier [clarifier [descriptors]]
```





