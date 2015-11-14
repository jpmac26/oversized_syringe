# oversized_syringe
Modding tool for the Hyperdimension Neptunia series games; enable packing/unpacking of resources from the games' custom archive format

** under active developement and still experimental **

# Abstract

The games themselves run pretty well under wine, the existing modding tools, however, do not
(neither kitserver nor the packer created by anon).

Since I wanted to try the new translation for ReBirth;2, I had to borrow a friend's PC in order
to statically patch my game files.

However, since being dependant on that kind of sucks, I decided to make my own packing/unpacking tool,
by reverse-engineering the game's archive format.

I was able to un-compress the files by using QuickBMS (which you should also check out), then it was just
a matter of discovering the compression algorithm, comparing "before" and "after"

# Usage

    ./oversized_syringe.py -h

# Roadmap

1. Directory import/merge feature
2. Extensive testing
3. GUI
4. Better compression algorithm
5. Support for other OSes

# Thanks to

[Luigi Auriemma](aluigi.altervista.org)

[Idea Factory International](http://www.ideafintl.com/)