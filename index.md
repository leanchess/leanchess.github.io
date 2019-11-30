![avatar](https://secure.gravatar.com/avatar/5f79d29ddd71d9757723cb4b51cc424e)

## Lean Introduction

LeanChess is a chess-playing program for the IBM PC AT (a 16-bit machine) and compatibles. As of this writing, it is the smallest chess program known to exist. The smallest LeanChess edition (Barebone DOS) is 329 bytes small; 33 bytes less than the [previous record holder][chesskelet] and less than half the size of the legendary [1K ZX Chess][1kchess].

How small is 329 bytes? Following Alex Garcia's (lost) lead, we tweaked the previous paragraph to be of exactly the same size (without counting the links).

## The Book of Lean

In the beginning David Horne created [1K ZX Chess][1kchess]. And 1K Chess ran on ZX81, and it was 672 bytes long; and all saw that it was good.

And the land had rest 20H years. And Olivier Poudade begat a [program][bootchess], and he called its name BootChess. And BootChess ran on x86, and it was 468 bytes long; and all saw that it was boot.

And Óscar Toledo Gutiérrez begat a [program][atomchess], and it was a true Boot Chess. And he called its name Atomchess, saying, Atom is the smallest of particles. And it ran on x86, and all saw that it was good. And it came to pass, that men came and made Atomchess smaller; and it was 383 bytes long.

And Alex Garcia begat a [program][chesskelet], and it ran on ZX Spectrum. And he called its name ChesSkelet, saying, After all fat is trimmed, only the skeleton remains. And men came and made ChesSkelet smaller; and it was 352 bytes long.

And Dmitry Shechtman begat a [program][source], and it ran on IBM PC AT under DOS. And he called its name LeanChess, saying, The domain is available. And LeanChess had NegaMax, and no men came to make it smaller; and it was 329 bytes long.

There were giants in the earth in those days, and also before that. Óscar Toledo G. had begotten [Nanochess][nanochess], [JavaScript 1K Chess][js1k], [Atari Atomchess][atomchess], and [others][toledo]. H. G. Muller had begotten [MicroMax][micromax] and [others][hgm].

<a name="AT"></a>
## Why the AT?

Obviously, because AT stands for Advanced Technology! On a slightly more serious note, this question is quite a complex one (to answer, at least).

Many years ago, when we had hair where it belongs and didn't where it doesn't, we taught ourself the assembly language of the 8086 processor (shared by its cripple brother, the 8088, which the original IBM PC was built around). After using it for writing a couple of (entirely harmless) viruses we moved on to other endeavours.

In late 2019, when we pondered developing an assembly-language chess game, the choice of platform seemed obvious to us. 8086/8088 assembly was still the only one we had had experience with, and as one's hair grows farther away from where it belongs, mastering unfamiliar architectures becomes less attainable. At that juncture we presumed we wouldn't ever approach [AtomChess]'s size, much less so that of [ChesSkelet].

To benefit the less technically savvy reader, an oversimplified interjection is in order. 8086, being a 16-bit processor, offers a reacher instruction set than does its typical 8-bit counterpart, which means that more bytes are required for encoding an average instruction. As a consequence, an (average) machine language program of equivelant function would require much less storage space, unless it specifically requires 16-bit (or larger) words for computations and/or memory access. Chess, conversely, lends itself ideally to eight bits. This explains the little hope that we had of beating [ChesSkelet] at its game (sizecoding, not chess).

On to the reason from switching from the PC to the AT. As we were browsing through the x86 documentation, we stumbled upon an unfamiliar instruction: `pusha`. The description read:

> Note: this instruction works only on 80186 CPU and later!

As it turned out, `pusha` replaces eight consecutive `push` instructions, whereas its counterpart `popa` replaces seven (the recovered SP value is discarded), meaning that the two, when used in conjunction, could bring up to 12 bytes worth of savings. We were naturally eager to try this, and they did just that for LeanChess. We then repeated the procedure, for a somewhat humbler profit (the exact byte count is lost to the ages). It was either between or immediately after these two instances that LeanChess became smaller than Atomchess.

No computer series (to speak of) were based on 80186, making IBM PC AT the earliest platform to support this extension and, coincidentally, the minimum requirement for LeanChess.

## How Good Is It?

LeanChess features:

* exhaustive NegaMax search
* to constant depth (the default is 3, although 4 performed acceptably in our DOSBox)
* with material-based evaluation.

Since all its (known) bugs had been fixed, LeanChess won every game it played against its creator, a fact that probably testifies to the weakness of the latter rather than to the strength of the former.

## How Lean is It?

Since the goal is the smallest possible program size, substantial compromises are inevitable. LeanChess does not implement

* input validation (i.e., it accepts any four characters as the coordinates of a legal move),
* pawn 2-square advance (i.e., it does not consider it, but accepts it as a legal move, see previous bullet),
* pawn promotion (to queen or otherwise),
* en passant capture,
* castling,
* checkmate/stalemate detection,
* threefold repetition or fifty-move rule.

Furthermore, the UX is fairly rudimentary, offering

* 25x40 text display (uppercase for white and lowercase for black)
* with no file or rank labels,
* no prompt and
* no input indication (except for DOS editions), with
* OSless Barebone edition displaying black pieces on brown board,
* Barebone editions removing the empty square markings, and
* Barebone editions replacing Bs with Os,

which brings us to:

## Why Os for Bishops?

Reasons for denoting a bishop as O are many:

1. It is colloquially known as *офицер (officer)* in Russian-speaking cultures.
1. It is denoted as O in at least five different languages, namely: Albanian, Bulgarian, Estonian, Hindi, and Marathi<sup>[1]</sup>.
1. BishOp contains an O, which brings it on par with kNight.
1. It is mostly round.
1. 7 bytes of code are removed thanks to the fact that K, N, O, P, Q and R are no farther than 7 positions apart in the ASCII table.

## Why Black on Brown?

Again, there are numerous reasons for applying this particular design to OSless editions:

1. Black is the leanest of all colors.
1. LeanChess always plays black.
1. Black lends the pieces the color of upscale marble.
1. Brown lends the board the color of unpainted wood.
1. 1 byte of code is removed by using the same value for character count and character attributes.

## Is It Really Chess?

H. G. Muller offers the following [definition]:

> A Chess program is a program that can finish more than 50% of the
  games it plays against an opponent that plays moves randomly chosen
  from the set of Chess moves that are legal from the current position
  according to the FIDE rules.

Since LeanChess seems to fail this test, it cannot be considered a **full chess** implementation. Yet, it is:

* recognisably chess,
* very playable,
* employs actual AI, and
* surpasses (most of) its predecessors in terms of functionality

while remaining the smallest. We dub it **sufficiently chess**.

Full chess (up to a point) and improved UX are planned future additions to LeanChess, albeit in neither of its currently published editions.

## Is It Really the Smallest?

Some people like to argue that a program that outputs `resign` and terminates should be considered the world's smallest chess program. H. G. Muller to the rescue once more:

> Chess is the act of moving pieces on a (real or virtual) Chess
  board, and (...) actions like resigning or negociating a draw
  are merely part of a general mechanism of organizing matches
  or tournaments, which are not part of Chess.

A question of greater interest to us is the possibility of an actual chess program breaking the record currently held by LeanChess.

First, the size of LeanChess itself could be further reduced (albeit marginally) by abusing the `pusha`/`popa` [optimisation](#AT). We opted to keep the program lean in terms of stack allocations as well, and only resorted to employing it in the two instances we deemed absolutely necessary.

Second, we expect a straightforward port of LeanChess to an [8-bit architecture](#AT) to produce a considerably smaller binary.

Finally, LeanChess was created from scratch by a lone programmer with no outside assistance and without consulting existing assembly chess implementations (we had had a look at [MicroMax] a long time ago, and we are truly grateful to the [Chess Programming Wiki][chesspro] authors/contributors). We are eager to see how others improve on our accomplishment.

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
