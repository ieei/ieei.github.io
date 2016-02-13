---
layout: post
title: Moving over to github pages
author: Haakon Sporsheim
date:  2016-02-13 22:45:00
categories: timeline
tags: github
---
It's weird. A year ago or so I thought using wordpress would be easy and simple
enough to actually write something quite often.
It turns out I was wrong.
First of all I don't like wordpress for it's technology.
It's PHP! :P And uses a database (MySQL).
Second, it is pain to use.
Log in, use a WYSIWYG editor and publish through the browser.
Changing wordpress, extending or touching it apart from installing plugins seems
tedious and waste of time.
Even just hunting for the proper plugins is waste of time if you ask me.
So...

### Welcome to [github pages][ghpages] using [jekyll][jekyll]
Now this is nice!
I write my posts using markdown in my favorite editor, `git commit` and `git push`.


The horrible comments plugin I used in wordpress is swapped out with an
incredible simple [disqus][disqus] integration.
Farewell wordpress comments spam.
You should see my wordpress comments gmail filter.
Seems like spammers are targeting wordpress sites!

I think it looks pretty good.
I'm no designer, but have been part of some UI/UX work in the past.
I've spent some time customizing it.
Too much time, but it was all fun and worth it.
It uses [bootstrap][bootstrap] and some javascript for navbar stuff.
Underneath it's jekyll obviously and bootstrap sass for styling.
Locally I serve it running `bundle exec jekyll serve` as you would find in the
github pages documentation.

I strongly recommend my setup, it's pretty easy, and I especially like the new way of posting!
[github.com/ieei/ieei.github.io][source]

[ghpages]: //pages.github.com
[jekyll]: //www.jekyllrb.com
[disqus]: //www.disqus.com
[bootstrap]: //getbootstrap.com
[source]: //github.com/ieei/ieei.github.io
