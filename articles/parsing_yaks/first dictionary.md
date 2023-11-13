
## Overview

The first dictionary is "1811 Dictionary of the Vulgar Tongue".

> **The dictionary contains both words and phrases; as such I will use "lexeme" to refer to the dictionary entry rather than "word".**

The dictionary does not specify pronunciations or grammatical classes.

## Overall Structure

A UTF-8 encoded `.txt` file. The raw file is structured thusly:

```
PROJECT GUTENBERG META INFORMATION
LITERAL TEXT: "*** START OF THE PROJECT GUTENBERG EBOOK 1811 DICTIONARY OF THE VULGAR TONGUE ***"
PROJECT GUTENBERG EDITORS
MULTIPLE NEWLINES
TITLE PAGE TEXT
MULTIPLE NEWLINES
LITERAL TEXT: "PREFACE."
PREFACE
MULTIPLE NEWLINES
LITERAL TEXT: "DICTIONARY OF THE VULGAR TONGUE."
(CONTENT)
MULTIPLE NEWLINES
LITERAL TEXT: "*** END OF THE PROJECT GUTENBERG EBOOK 1811 DICTIONARY OF THE VULGAR TONGUE ***"
MULTIPLE NEWLINES
PROJECT GUTENBERG LICENCE INFO
```

However, the initial step is to parse a single entry.

## Context-free grammar for a single entry

See [[notes_on_grammar_rules]]. 

## Writing the parser using Nom

