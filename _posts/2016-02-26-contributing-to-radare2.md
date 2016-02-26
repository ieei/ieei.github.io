---
layout: post
title: Contributing to Radare2
author: Haakon Sporsheim
date:  2016-02-26 12:00:00
categories: dev
tags: re radare xtensa
---
You might wonder; What's Radare or Radare2?
Well, head over to [rada.re][rada.re]/[radare.org][radare.org] and check it out.
Basically it is a reverse engineering tool for static software anlysis.
You can also use it for debugging I guess, but my main use of it will be
reverse engineering binary blobs by disassembling machine code to understand
how it works.

Recently I've been playing with Tensilica Xtensa processors, and been looking
at a SoC I'll probably write something about later.
Anyhow; I got hold of the bootloader as a binary blob for this SoC/platform
which I wanted to know how works.
This bootloader is located in the ROM of the device and includes a lot of board
functionality I wanted to understand more about.
So I figured that this was a good time to try out Radare2 finally.
I was a bit worried that Radare2 didn't support the architecture, but indeed
did it have support for Xtensa ISA using GNU binutils (I think).
Yay!

After using Radare2 for a couple of hours I had found `Visual mode` which is a
very interactive way of looking at a binary, but I also discovered that that
some rendering sometimes looked ... funny!?
There were some instructions that didn't have the right color.
Also, I realized that jump/branch instructions didn't render all lines correctly.
As I was new to Radare at the time it took some time before I got the whole picture.
Radare2 disassembled instructions correctly, but the interpretation was sometimes wrong.
The reason is that the module responsible for analysis (anal) was
very much a [proof of concept implementation][anal_xtensa.c-old].

The first thing I noticed was that the implementation didn't take care about
signedness of the jump address.
Hence it would in most cases add to the relative address.
Since the jump addresses mostly are signed extended, short jumps backwards
would be interpreted as big jumps forward.
E.g. the 8bit immediate `0xfe` would be interpreted as `254` instead of `-2`.

After some initial hacking I decided to rewrite the Xtensa analysis backend/plugin.
And so I did: [github.com/radare/radare2@4d4ab622][commit].
The patch(set) got merged today after I finished it last night. Cool!
I had to read most of the Tensilica Xtensa Instruction Set Architecture (ISA) Reference Manual.
Use your friend Google to find it if you are interested.
The instruction set is quite nice, although I found the opcodes somewhat messy
scattered around in terms of functionality grouping.
I mean, probably not horrendous, but identifying all the different branch/conditional jumps
must be done in several steps.
Oh well, it's not that bad.
I guess, I would be surprised if I only could check a specific bit in the
opcode to figure out that it was a jump.

Here is an asciicast of how it looks right now using git HEAD:
[![asciicast](https://asciinema.org/a/00p5h37dadkauem09wybp0txz.png)](https://asciinema.org/a/00p5h37dadkauem09wybp0txz)


[rada.re]: //rada.re
[radare.org]: //radare.org
[anal_xtensa.c-old]: https://github.com/radare/radare2/blob/d17cbff22cee717959b15040bf04f383fca4f1bf/libr/anal/p/anal_xtensa.c
[commit]: https://github.com/radare/radare2/commit/4d4ab62211d8f84e6b90ae22d099a4186ca5fe46
