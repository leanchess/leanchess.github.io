![avatar](https://secure.gravatar.com/avatar/5f79d29ddd71d9757723cb4b51cc424e)

## Lean Introduction

LeanChess is a [free][license] chess program for the IBM PC AT (a [16-bit machine](#16-bit)) and compatibles. As of this writing, it's the world's [smallest](#smallest) [chess-playing](#chess) program. The shortest LeanChess edition ([Barebone DOS](#editions) is 328 bytes long, 24 bytes shorter than the [previous record holder][chesskelet], or less than half the size of the legendary [1K ZX Chess][1kchess].

How little is 328 bytes? Following Alex Garcia's (lost) lead, we tweaked the previous paragraph (sans links) to be of exactly this size.

## The Book of Lean

In the beginning David Horne created [1K ZX Chess][1kchess]. And 1K Chess ran on ZX81, and it was 672 bytes long; and all saw that it was good.

And the land had rest 20H years. And Olivier Poudade begat a program, and he called its name [BootChess]. And BootChess ran on x86, and it was 468 bytes long; and all saw that it was boot.

And Óscar Toledo Gutiérrez begat a program, and it was a true Boot Chess. And he called its name [Atomchess], saying, The atom is the smallest of particles. And it ran on x86, and all saw that it was good. And it came to pass, that men came and made Atomchess smaller; and it was 383 bytes long.

And Alex Garcia begat a program, and it ran on ZX Spectrum. And he called its name [ChesSkelet], saying, After all fat is trimmed, only the skeleton remains. And men came and made ChesSkelet smaller; and it was 352 bytes long.

And Dmitry Shechtman begat a [program][source], and it ran on IBM PC AT under DOS. And he called its name LeanChess, saying, The domain is available. And it was good, and no men came to make it smaller; and it was 328 bytes long.

There were giants in the earth in those days, and also [before that][story]. Jan Kuipers had begotten [Tiny Chess 86][tinychess86]. H. G. Muller had begotten [MicroMax] and [others][hgm]. Óscar Toledo G. had begotten [Nanochess], [JavaScript 1K Chess][js1k], [Atari Atomchess][atomchess], and [others][toledo].

<a name="editions"></a>
## LeanChess Editions

The following editions are currently available (all having the same AI).

&nbsp;   | DOS | BIOS
---------|-----|-----
Barebone |[COM (328b)](https://github.com/leanchess/leanchess/releases/download/v1.0/LCBD.COM)  [ASM](https://github.com/leanchess/leanchess/raw/master/LC.ASM)|[COM (333b)](https://github.com/leanchess/leanchess/releases/download/v1.0/LCBB.COM)  [ASM](https://github.com/leanchess/leanchess/raw/bios/LC.ASM)
Classic  | TBD |[COM (342b)](https://github.com/leanchess/leanchess/releases/download/v1.0/LCCB.COM)  [ASM](https://github.com/leanchess/leanchess/blob/classic-bios/LC.ASM)

Building from source:

```
tasm lc
tlink /t lc
```

<a name="tools"></a>
## Tools Used

| Function | Tool
|----------|----------
| Emulator | DOSBox
| Editor   | Notepad++
| Compiler | TASM
| Linker   | TLINK
| Debugger | `mov ax, 0924h`
|          | `stosb`
|          | `int 21h`
         
<a name="AT"></a>
## Why the AT?

Many years ago, when we had hair where it belongs and didn't where it doesn't, we taught ourselves the assembly language of the 8086 processor (shared by its cripple brother, the 8088, which the original IBM PC was built around). After using it for writing a couple of (entirely harmless) viruses we moved on to other endeavours.

In late 2019, when we pondered developing an assembly-language chess game, the choice of platform seemed obvious to us. 8086/8088 assembly was still the only one we had had experience with, and as one's hair grows farther away from where it belongs, mastering unfamiliar architectures becomes less attainable. At that juncture we presumed the resultant program wouldn't ever come close to [AtomChess], much less so to [ChesSkelet].

<a name="16-bit"></a>
To benefit the less technically savvy reader, an oversimplified interjection is in order. 8086, being a 16-bit processor, offers a reacher instruction set than does its typical 8-bit counterpart, thus more bytes are needed for encoding an average instruction. As a consequence, a (typical) 8-bit machine language program of equivalent function will consume substantially less storage space, unless it specifically requires 16-bit (or larger) words for arithmetics and/or memory accesses. Chess, conversely, lends itself ideally to the 8-bit realm. This explains the little hope we had of beating the author of [ChesSkelet] at his game (sizecoding, not chess).

<a name="pusha"></a>
On to the reason for switching from the PC to the PC AT. As we were browsing through the x86 documentation, we stumbled upon an unfamiliar instruction: `pusha`. The description read:

> Note: this instruction works only on 80186 CPU and later!

As it turned out, `pusha` replaces eight consecutive `push`es, whereas its counterpart `popa` replaces seven `pop`s (along with two `dec sp`s in lieu of `pop sp`), meaning that being used in conjunction, these two could effectively reduce code size by up to 12 bytes. Applying this twice to LeanChess made it at least 18 bytes smaller (the exact number is lost to the ages). It was either between or immediately after these two instances that it became leaner than Atomchess.

As we were initially ignorant of a method of enabling 80186 assembler support, we blatantly substituted every `pusha` and `popa` with `db 60h` and `db 61h`, respectively. Much to our surprise, adding the `.186` directive yielded a further 1-byte reduction.

No computer series (to speak of) were based on 80186, making IBM PC AT the earliest platform to support this extension and, coincidentally, the minimum requirement for LeanChess.

<a name="strength"></a>
## How Good Is It?

LeanChess features

* exhaustive NegaMax search
* to a constant depth (the default is 3, although 4 performed acceptably in our DOSBox)
* with material-only evaluation.

Since all its (known) bugs had been fixed, LeanChess won every game it played against its creator, a fact that probably testifies to the weakness of the latter rather than to the strength of the former.

## How Lean is It?

Since our objective is to make the program as small as possible, substantial compromises are inevitable. LeanChess does not implement

* input validation (i.e., it accepts any four characters as the coordinates of a legal move),
* pawn 2-square advance (i.e., it does not consider it, but accepts it as a legal move, see previous bullet),
* pawn promotion (to queen or otherwise),
* en passant capture,
* castling,
* checkmate/stalemate detection, or
* threefold repetition and fifty-move rules.

Furthermore, its UX is fairly rudimentary, offering

* 25x40 text display (uppercase for white and lowercase for black)
* with no file or rank labels,
* no prompt and
* no input indication in OSless editions, with
* black pieces on brown board in OSless Barebone,
* no empty square markings in Barebone editions, and
* Os for bishops in Barebone editions,

which brings us to the question:

## Why Os for Bishops?

Reasons for denoting a bishop as O are many:

1. It is colloquially known as *офицер (officer)* in Russian-speaking cultures.
1. It is denoted as O in at least five different languages, namely: Albanian, Bulgarian, Estonian, Hindi, and Marathi<sup>[1]</sup>.
1. BishOp contains an O, which brings it on par with kNight.
1. It is mostly round.
1. 7 bytes of code are removed thanks to the fact that K, N, O, P, Q and R are no farther than 7 positions apart in the ASCII table.

## Why Black on Brown?

Again, there are numerous reasons for applying this particular design to OSless editions:

1. Black is the leanest color.
1. LeanChess always plays black.
1. Black lends the pieces the color of upscale marble.
1. Brown lends the board the color of unpainted wood.
1. 1 byte of code is removed by using the same value for character count and character attributes.

<a name="chess"></a>
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
* surpasses (most of) its predecessors in terms of functionality,

while remaining the smallest. We dub it **sufficiently chess**.

Full chess (up to a point) and improved UX are planned future LeanChess extensions, albeit to neither of its currently published editions.

<a name="smallest"></a>
## Is It Really the Smallest?

Some argue that a program that produces `resign` as its output and terminates is the world's smallest chess program. H. G. Muller to the rescue once again:

> Chess is the act of moving pieces on a (real or virtual) Chess
  board, and (...) actions like resigning or negociating a draw
  are merely part of a general mechanism of organizing matches
  or tournaments, which are not part of Chess.

A question of greater interest to us is the possibility of an actual chess program breaking the record currently held by LeanChess.

Firstly, the size of LeanChess itself could be further reduced (albeit marginally) by abusing the `pusha`/`popa` [optimisation](#pusha). We opted to keep the program lean in terms of stack allocations as well by only employing it on two instances, where we deemed it absolutely necessary.

Secondly, we believe porting LeanChess to an [8-bit architecture](#16-bit) would yield a noticeably smaller binary. We leave that as an exercise for the reader (kindly requesting that, should they partake in it, [the original copyright notice be included][license]).

Finally, LeanChess was created from scratch by a lone programmer with no assistance and without consulting existing assembly implementations (we had had a look at [MicroMax] a long time ago, and we are truly grateful to the editors of the [Chess Programming Wiki][chesspro]). We are eager to see how others improve on our accomplishment.

[definition]: http://home.hccnet.nl/h.g.muller/definition.txt
[1kchess]: http://users.ox.ac.uk/~uzdm0006/scans/1kchess
[bootchess]: http://olivier.poudade.free.fr/src/BootChess.asm
[toledo]: https://nanochess.org/chess.html
[atomchess]: https://nanochess.org/chess6.html
[js1k]: https://nanochess.org/chess4.html#js1k
[nanochess]: https://nanochess.org/chess3.html
[hgm]: http://home.hccnet.nl/h.g.muller/chess.html
[micromax]: http://home.hccnet.nl/h.g.muller/max-src2.html
[tinychess86]: https://www.chessprogramming.org/Tiny_Chess_86
[chesskelet]: http://chesskelet.x10host.com
[story]: http://chesskelet.x10host.com/story.html
[chesspro]: https://www.chessprogramming.org/Main_Page
[source]: https://github.com/leanchess/leanchess
[contact]: mailto:contact@leanchess.com
[license]: https://github.com/leanchess/leanchess/blob/master/LICENSE
[16-bit]: #16-bit
[pusha]: #pusha
[1]: https://en.wikipedia.org/wiki/Chess_piece
