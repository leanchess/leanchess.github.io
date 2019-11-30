![avatar](https://secure.gravatar.com/avatar/5f79d29ddd71d9757723cb4b51cc424e)

## Lean Introduction

LeanChess is a chess-playing program for the IBM PC AT (a 16-bit machine) and compatibles. As of this writing, it is the smallest known chess program in the world. The minimal LeanChess edition (Barebone DOS) takes 329 bytes, 33 bytes less than the [previous record holder][chesskelet] and less than half the size of the legendary [1K ZX Chess][1kchess].

How little is 329 bytes? Following Alex Garcia's lead, the previous paragraph (not counting the links) was tweaked to be of this exact size.

## The Book of Lean

In the beginning David Horne created [1K ZX Chess][1kchess]. And 1K Chess ran on ZX81, and it was 672 bytes long; and all saw that it was good.

And the land had rest 20H years. And Olivier Poudade begat a [program][bootchess], and he called its name BootChess. And BootChess ran on x86, and it was 468 bytes long; and all saw that it was boot.

And Óscar Toledo Gutiérrez begat a [program][atomchess], and it was a true Boot Chess. And he called its name Atomchess, saying, Atom is the smallest of particles. And it ran on x86, and all saw that it was good. And it came to pass, that men came and made Atomchess smaller; and it was 383 bytes long.

And Alex Garcia begat a [program][chesskelet], and it ran on ZX Spectrum. And he called its name ChesSkelet, saying, After all fat is trimmed, only the skeleton remains. And men came and made ChesSkelet smaller; and it was 352 bytes long.

And Dmitry Shechtman begat a [program][source], and it ran on IBM PC AT under DOS. And he called its name LeanChess, saying, The domain is available. And LeanChess had 
Max, and no men came to make it smaller; and it was 329 bytes long.

There were giants in the earth in those days, and also before that. Óscar Toledo G. had begotten [Nanochess][nanochess], [JavaScript 1K Chess][js1k], [Atari Atomchess][atomchess], and [others][toledo]. H. G. Muller had begotten [MicroMax][micromax] and [others][hgm].

## Is It Really Chess?

H. G. Muller offers the following [definition]:

> A Chess program is a program that can finish more than 50% of the
  games it plays against an opponent that plays moves randomly chosen
  from the set of Chess moves that are legal from the current position
  according to the FIDE rules.

Therefore, LeanChess cannot be considered a *full chess* implementation, but it is still:

* recognisably chess
* playable
* employs actual AI, and
* surpasses its predecessors in function

## Is It Really the Smallest?

Some people like to argue that a program that outputs `resign` is technically the world's smallest chess program. H. G. Muller to the rescue:

> Chess is the act of moving pieces on a (real or virtual) Chess
  board, and (...) actions like resigning or negociating a draw
  are merely part of a general mechanism of organizing matches
  or tournaments, which are not part of Chess.

A question of greater interest is the possibility of creating an actual chess program that would be smaller than LeanChess.

First, the size of LeanChess itself can be marginally reduced by abusing the pair of `pusha`/`popa`. Instead, we chose to leave the program lean in terms of stack allocation, and only used two on two occasions, where we deemed it absolutely necessary.

Second, a straightforward port of LeanChess to an 8-bit architecture will probably produce an even smaller chess program.

## Who
© 2019 [Dmitry Shechtman][contact]

## License
[MIT License](license.md)

[definition]: http://home.hccnet.nl/h.g.muller/definition.txt
[1kchess]: http://users.ox.ac.uk/~uzdm0006/scans/1kchess
[bootchess]: http://olivier.poudade.free.fr/src/BootChess.asm
[toledo]: https://nanochess.org/chess.html
[atomchess]: https://nanochess.org/chess6.html
[js1k]: https://nanochess.org/chess4.html#js1k
[nanochess]: https://nanochess.org/chess3.html
[hgm]: http://home.hccnet.nl/h.g.muller/chess.html
[micromax]: http://home.hccnet.nl/h.g.muller/max-src2.html
[chesskelet]: http://chesskelet.x10host.com
[source]: https://github.com/leanchess/leanchess
[contact]: mailto:contact@leanchess.com
