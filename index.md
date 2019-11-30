![avatar](https://secure.gravatar.com/avatar/5f79d29ddd71d9757723cb4b51cc424e)

## Lean Introduction

LeanChess is a chess-playing program for the IBM PC AT (a 16-bit machine) and compatibles. As of this writing, it is the smallest chess program known to exist. The smallest LeanChess edition (Barebone DOS) takes up 329 bytes, 33 bytes less than the [previous record holder][chesskelet] and less than half the size of the legendary [1K ZX Chess][1kchess].

How small is 329 bytes? Following Alex Garcia's (lost) lead, we tweaked the previous paragraph to be of exactly the same size (without counting the links).

## The Book of Lean

In the beginning David Horne created [1K ZX Chess][1kchess]. And 1K Chess ran on ZX81, and it was 672 bytes long; and all saw that it was good.

And the land had rest 20H years. And Olivier Poudade begat a [program][bootchess], and he called its name BootChess. And BootChess ran on x86, and it was 468 bytes long; and all saw that it was boot.

And Óscar Toledo Gutiérrez begat a [program][atomchess], and it was a true Boot Chess. And he called its name Atomchess, saying, Atom is the smallest of particles. And it ran on x86, and all saw that it was good. And it came to pass, that men came and made Atomchess smaller; and it was 383 bytes long.

And Alex Garcia begat a [program][chesskelet], and it ran on ZX Spectrum. And he called its name ChesSkelet, saying, After all fat is trimmed, only the skeleton remains. And men came and made ChesSkelet smaller; and it was 352 bytes long.

And Dmitry Shechtman begat a [program][source], and it ran on IBM PC AT under DOS. And he called its name LeanChess, saying, The domain is available. And LeanChess had NegaMax, and no men came to make it smaller; and it was 329 bytes long.

There were giants in the earth in those days, and also before that. Óscar Toledo G. had begotten [Nanochess][nanochess], [JavaScript 1K Chess][js1k], [Atari Atomchess][atomchess], and [others][toledo]. H. G. Muller had begotten [MicroMax][micromax] and [others][hgm].

## Why the AT?

Obviously, because AT stands for Advanced Technology! On a slightly more serious note, this question is quite a complex one (to answer, at least).

Many years ago, when we had hair where it belongs and didn't where it doesn't, we taught ourself the assembly language of the 8086 processor (shared by its cripple brother, the 8088, which the original IBM PC was built around). After using it for writing a couple of (entirely harmless) viruses we moved on to other endeavours.

In late 2019, when we pondered developing an assembly-language chess game, the choice seemed obvious. After all, 8086/8088 assembly remained the only one we had experience with, and as one's hair grows farther away from where it belongs, mastering unfamiliar architectures becomes less attainable. At that juncture we presumed we wouldn't ever approach [AtomChess]'s size, much less so that of [ChesSkelet].

For the benefit of the lest technically savvy reader, a small interjection is in order. 8086, being a 16-bit processor, has a reacher instruction set than that of its typical 8-bit counterpart, which means that more bytes are required for encoding an average instruction. As a consequence, an (average) assembly language program of equivelant function would require much less storage space, unless it specifically requires 16-bit (or larger) words for computations and/or memory access. Chess, conversely, lends itself ideally to an 8-bit assembly implementation.

## How Good Is It?

LeanChess features:

* exhaustive NegaMax search
* to constant depth (the default is 3, although 4 performed acceptably in our DOSBox)
* with material-based evaluation.

Since all its (known) bugs had been fixed, LeanChess won every game it played against its author, probably a testimony to the weakness of the latter rather than to the strength of the former.

## How Lean Is It?

Since the goal is the smallest possible program size, substantial compromises are inevitable. LeanChess does not implement any of the following:

* input validation (i.e., it accepts any four characters as the coordinates of a legal move),
* pawn 2-square advance (i.e., it does not consider it, but accepts it as a legal move, see previous bullet),
* pawn promotion (to queen or otherwise),
* en passant capture,
* castling,
* checkmate/stalemate detection,
* threefold repetition rule or
* fifty-move rule.

In addition, the UX is most rudimentary, namely:

* 25x40 text (uppercase for white and lowercase for black),
* no file or rank labels,
* no prompt,
* no input indication (except for DOS editions),
* OSless Barebone edition outputs all pieces in black and the board in brown,
* Barebone editions remove the empty square markings, and
* Barebone editions replace Bs with Os,

which brings us to:

## Why the Os?

The reasons for denoting a bishop as O are many:

1. It is colloquially known as *офицер (officer)* in Russian-speaking cultures.
1. It is denoted as O in at least five different cultures, namely: Albanian, Bulgarian, Estonian, Hindi, and Marathi<sup>[1]</sup>.
1. BishOp contains an O, which brings it on par with kNight.
1. It is mostly round.
1. 7 bytes of code are removed thanks to the fact that K, N, O, P, Q and R are no farther than 7 positions apart in the ASCII table.

## Why Black on Brown?

Again, there are numerous reasons for using this particular design in OSless editions:

1. Black is the best of all colors.
1. LeanChess always plays black.
1. Black pieces look like 
1. Brown board looks like unpainted wood.
1. 1 byte of code is removed by reusing the character count value before invoking the BIOS display interrupt.

## Is It Really Chess?

H. G. Muller offers the following [definition]:

> A Chess program is a program that can finish more than 50% of the
  games it plays against an opponent that plays moves randomly chosen
  from the set of Chess moves that are legal from the current position
  according to the FIDE rules.

Since LeanChess seems to fail this test, it cannot be considered a *full chess* implementation. Yet, it is:

* recognisably chess,
* very playable,
* employs actual AI, and
* surpasses (most of) its predecessors in terms of functionality

while remaining the smallest of all. We consider this **sufficiently chess**.

Full chess (up to a point) and improved UX are planned features, albeit in neither Barebone nor Classic editions of LeanChess, naturally.

## Is It Really the Smallest?

Some people like to argue that a program that outputs `resign` and terminates should be considered the world's smallest chess program. H. G. Muller to the rescue:

> Chess is the act of moving pieces on a (real or virtual) Chess
  board, and (...) actions like resigning or negociating a draw
  are merely part of a general mechanism of organizing matches
  or tournaments, which are not part of Chess.

A question of greater interest is the possibility of creating an actual chess program that would be smaller than LeanChess.

First, the size of LeanChess itself can be marginally reduced by abusing the `pusha`/`popa` optimisation. We opted to keep the program lean in terms of stack allocations as well, and only resorted to employing it on two occasions, where we deemed it absolutely necessary.

Second, we expect a straightforward port of LeanChess to an 8-bit architecture to produce a considerably smaller binary.

Finally, LeanChess was created from scratch by a lone programmer with no outside assistance and without consulting existing assembly chess implementations (we had had a look at [MicroMax] a long time ago, and we are truly grateful to the [Chess Programming Wiki][chesspro] authors/contributors). We are eager to see how others improve on this achievement.

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
[chesspro]: https://www.chessprogramming.org/Main_Page
[source]: https://github.com/leanchess/leanchess
[contact]: mailto:contact@leanchess.com
[1]: https://en.wikipedia.org/wiki/Chess_piece
