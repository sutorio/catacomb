

## Parsing a single entry

An entry is of the form "LEXEME. Definition.", where LEXEME is a capitalised collection of word/s separated by spaces and terminated with a period.
The lexeme's definition follows. Definitions are separated by a newline, then the next entry follows a similar pattern:

```txt
TIB. A young lass

TIBBY. A cat.
```

> [!note] There is the chance that that the period + space succeeding "LEXEME" and indicating the boundary between the lexeme and its definition may have been mis-entered as a comma, or is missing.

### Parsing a lexeme

#### Basic lexeme

Each entry begins with the word/phrase at the start of the line, in capital letters, followed by a period.

```txt
TIB. A young lass
```

#### Lexeme with alternatives

The entry may have alternatives, these are separated by a comma then a lowercase `or`:

```txt
TOASTING IRON, or CHEESE TOASTER. A sword.
```

**These alternatives may not appear in the dictionary**, so need to be duplicated and also stored as a reference ("see also...").

#### Lexemes that are verb phrases

The word "TO" (capitalised) may precede the word/phrase. This is **not** included in the dictionary order. The dictionary does not specify any kind of grammatical class, so this is a way to provide usage context.

```txt
TRIG. The point at which schoolboys stand to shoot their
  marbles at taw; also the spot whence bowlers deliver the
  bowl.

TO TRIG IT. To play truant. To lay a man trigging; to
  knock him down.
```

> [!note] The lexeme should be adjusted from "TO LEXEME" to "LEXEME, TO" so that alphabetic order is kept.

> [!note] Are there other prefixes, such as "AS "?

#### Lexeme alternates

The entry may be of the form "LEXEME, or ALTERNATIVE. Definition", where the lexeme is succeeded with the literal characters ", or" followed by a space and then "ALTERNATIVE". This specifies a different spelling or a direct synonym. As there is no hard-an-fast rule as to which it is, "alternative" is used to refer to this item.

```txt
TOASTING IRON, or CHEESE TOASTER. A sword.
```

> [!note] The alternative should be duplicated as a discrete entry if it is not already, and the two entries should refer to each other. The alternative should be stripped.

> [!note] There is a chance that the the comma + space after "LEXEME" is missing, and/or that "or " is mistyped as " OR".

An alternative included in the entry for a "TO"-prefixed entry does not repeat the "TO":

```txt
TO TRANSMOGRAPHY, or TRANSMIGRIFY. To patch up
  vamp, or alter.
```

#### A note on swear words

Obvious swear words of the time are redacted with hyphens and will need to be replaced from a dictionary:

```txt
T--D. There were four t--ds for dinner: stir t--d, hold
  t--d, tread t--d, and mus-t--d: to wit, a hog's face, feet
  and chitterlings, with mustard. He will never sh--e a
  seaman's t--d; i.e. he will never make a good seaman.
```

### Parsing a definition

A definition may span multiple lines. These are normally inset, so the additional spacing should be condensed.

```txt
THUMP. A blow. This is better than a thump on the back
  with a stone; said on giving any one a drink of good liquor
  on a cold morning. Thatch, thistle, thunder, and thump;
  words to the Irish, like the Shibboleth of the Hebrews.
```
The definition is then any text up until two newlines followed by a non-indented character (at which point have reached the new entry).

```txt
...the end of the last definition.

ANOTHER LEXEME. Definition for it here. 
```

#### Definition examples

The definition may have an example, which is two newlines followed by *indented* text. Due to this, can only tell if the entry is complete by stopping once the parser reaches a *non-indented* capital letter.

```txt
TOBACCO. A plant, once in great estimation as a medicine:

       Tobacco hic
  Will make you well if you be sick.
       Tobacco hic
  If you be well will make you sick.
```

#### Inline cross-references

The definition may refer to other entries within itself. By convention these are CAPITALISED to match the format of the lexeme in question.

> [!note] There is a chance that these internal references are *not* capitalised. This can only be ascertained by manual checking.

> [!note] Both implicit and explicit reference/s should be tagged for each entry. In the context of a web document, will need to provide hyperlinks to the referenced entries.

> [!note] Examples within the definition are, as was the fashion of the time, mainly provided in verse form. This structure needs to be retained.

#### Explicit cross-references

The definition may explicitly reference a related entry via the literal sentence "See LEXEME." (note I am including the period + space that precede
it).

```txt
TOOL. The instrument of any person or faction, a cat's
  paw. See CATS PAW.
```

Occasionally, the word "see" is accidentally capitalised:

```txt
TOPER. One that loves his bottle, a soaker. SEE TO SOAK.
```

So the pattern in Regex would be `/\s(See|SEE|see)\s(\w+).`, with the second capture group being the referenced word/phrase.

> [!note] Alternatives may also be referenced in the description in a more ad-hoc fashion. The patterns used need to be understood to, again, allow "see also..." references.
> ```txt
> TOM OF BEDLAM. The same as Abram man.
> ```

#### Sources

The definition may include a source tag, and the source tag is written in capital letters in its own sentence; for example ". IRISH." or ". CANT." 

Tags are used in the definitions to provide context. This conflicts with the convention for references. In this example, `CANT` is the tag:

```txt
TWITTOC. Two. CANT.
```

In this example, `IRISH` is a tag, in a specific parseable pattern, but the two capitalised words in the contextual example are references:

```txt
TWISS. (IRISH) A Jordan, or pot de chambre. A Mr. Richard
  Twiss having in his "Travels" given a very unfavourable
  description of the Irish character, the inhabitants of
  Dublin, byway of revenge, thought proper to christen this
  utensil by his name--suffice it to say that the baptismal
  rites were not wanting at the ceremony. On a nephew of
  this gentleman the following epigram was made by
  a friend of ouis:

      Perish the country, yet my name
       Shall ne'er in STORY be forgot,
      But still the more increase in fame,
       The more the country GOES TO POT.
```

> [!note] There needs to be a list of valid source tags assembled. Any source tags need to be extracted. When parsing the definition, checks for them must occur before mapping references; the syntax convention is almost identical
