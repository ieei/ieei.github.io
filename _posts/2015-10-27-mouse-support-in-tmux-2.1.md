---
layout: post
title: Mouse support in tmux 2.1
author: Haakon Sporsheim
date:  2015-10-27 13:38:00
categories: Tools
tags: tmux
---
I'm a vim+tmux user/believer!
I recently installed OS X el capitan and updated/upgraded most of my homebrew Cellar to put it like that.
Now, by doing that I got tmux 2.1 where apparently [mouse-mode/mode-mouse is completely rewritten][tmux changes].
I don't use the mouse for much, but still nice to have when resizing panes.

So, what you need is to change your `.tmux.conf`
{% highlight vim %}
set -g mode-mouse on
set -g mouse-resize-pane on
set -g mouse-select-pane on
set -g mouse-select-window on
{% endhighlight %}
to
{% highlight vim %}
set -g mouse on
{% endhighlight %}
Short and sweet! :)
My [dotfiles github repo][dotfiles] is already updated!

[tmux changes]: https://raw.githubusercontent.com/tmux/tmux/master/CHANGES
[dotfiles]: https://github.com/haaspors/dotfiles/commit/f0a569115c5dbc734ff40b28dbd96d826024cf41
