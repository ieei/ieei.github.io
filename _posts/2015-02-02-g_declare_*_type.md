---
layout: post
title: G_DECLARE_*_TYPE
author: Haakon Sporsheim
date:  2015-02-02 12:48:00
categories: GObject
tags: glib gobject
---
Last week [Ryan Lortie][Ryan Lortie] [blogged][desrt blog] about some new macros I really have been missing for years of doing GObject development.

[This commit][commit] adds `G_DECLARE_{FINAL,DERIVABLE}_TYPE` to gtype.h so that some of the GObject boilerplate code could be omitted.
Sweet! It will be available in next version of GLib. Version 2.44.

One thing I would personally like in the macro, as I tend to add to most GStreamer classes, is `{OBJ_NAME}_CAST`!
This would do a simple cast without any run-time checks.
Also known as [type punning][type punning] according to wikipedia.
Which basically is like `reinterpret_cast` in C++.

[Ryan Lortie]: http://blogs.gnome.org/desrt/
[desrt blog]: http://blogs.gnome.org/desrt/2015/01/27/g_declare_finalderivable_type/
[commit]: https://git.gnome.org/browse/glib/commit/?id=3b4cb28e17c6a5dac64eb8afda2b1143757ad7a4
[type punning]: http://en.wikipedia.org/wiki/Type_punning
