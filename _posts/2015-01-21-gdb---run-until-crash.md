---
layout: post
title: GDB - run until crash
author: Haakon Sporsheim
date:  2015-01-21 12:58:00
categories: Tools
tags: gdb tools
---
When you write code you most likely want to add test coverage for it by adding a unit test, module test or whatever you want to call it.
Personally I mainly work on highly threaded C/C++ code, where there inevitably will be bugs.
Either in the form of non-deterministic tests or in the code it self as deadlocks or data races.
In my current position we have an extensive CI system which from time to time report that there is such a test.
Even though the test runs millions of times each day, it could be months or years between runs that would make the test fail.

I find it very useful to isolate the test and run it through GDB with or without extra debug to find and squash the bug.
Since most of my tests run very fast and then exit, it is nice to run the test over and over again until it either crashes or deadlocks.
This is how I do it:

    GNU gdb (GDB) 7.6.1-ubuntu
    Copyright (C) 2013 Free Software Foundation, Inc.
    License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
    This is free software: you are free to change and redistribute it.
    There is NO WARRANTY, to the extent permitted by law. Type "show copying"
    and "show warranty" for details.
    This GDB was configured as "x86_64-linux-gnu".
    For bug reporting instructions, please see:
    <http://www.gnu.org/software/gdb/bugs/>...

    (gdb) set pagination off
    (gdb) break exit
    Breakpoint 1 at 0xcafef00dbeef: file exit.c, line 99.
    (gdb) commands
    Type commands for breakpoint(s) 1, one per line.
    End with a line saying just "end".
    >run
    >end
    (gdb) run

As you see, the point is to rerun the program when the breakpoint on `exit()` occurs.
Also note how I disable pagination, as this will stop the debugged program when output accumulates.

