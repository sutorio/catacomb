
## Overview

[[test]]

I'm interested in parsers, in particular automating processing of large text files whose individual entries can be describe using a [[context-free grammar]], but use natural language within them.

So dictionaries are a good place to start, if nothing else because I'm interested in creating a quite specific [[anagram generator]].

The dictionaries I'm personally interested in are dictionaries of dialect and slang.

To start, I'm going to pull a few from [Gutenberg](https://gutenberg.org). Starting with the simplest, build parsers to process these to a structured format.

Work up to a point where I have a general program for parsers that requires only writing the rules for an entry. Parse the dictionary, flagging and possible human transcription errors. Push that amended version back to Gutenberg in the same format it came in.

Push the parsed dictionary to a database.

Repeat.

## Technologies

This is going to use Rust initially. I am interested in [[parser_combinators]], so [Nom](https://github.com/rust-bakery/nom) would seem to be the obvious choice.

However there are reasons *not* to use a parser combinator approach. The libraries seem to be rarely comprehensively documented, and often lack a wealth of examples. There seems to be a symptom prevalent in functional languages present here: they are "easy" or "simple", and therefore don't need much documentation. Small self explanatory functions! No need for piles of examples! Once you know how to use them, this may well be true, but getting to a point where a given library can be wielded with confidence is a different matter.

So I also want to look at several approaches:

1. The [[PEG]] parser framework [Pest](https://github.com/pest-parser/pest)
2. The lexer [Logos](https://www.github.com/maciejhirsz/logos). This I suspect is going to be the easiest to use and the most obvious in terms of code, but need to see. 
3. The [unicode-segmentation](https://github.com/unicode-rs/unicode-segmentation) crate, which (unsurprisingly) provides iterators for processing Unicode text strings.

Aim is also to make a try with Elixir: Dashbit maintain [Nimble Parsec](https://github.com/dashbitco/nimble_parsec), and that combined with  Phoenix Liveview app is tempting. Note that Rust code can just be compiled down to a (safe) [NIF](https://www.erlang.org/doc/tutorial/nif.html) using the [Rustler](https://github.com/rusterlium/rustler) library. So parsers (be they combinator-based or not) can be _relatively_ easily integrated into an Elixir codebase regardless.
