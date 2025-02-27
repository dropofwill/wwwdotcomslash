+++
title = "My Vim Config Part 1: The Basics"
date = 2014-11-02T03:23:00Z
weight = 100

[taxonomies]
tags = ["Vim", "Config"]

+++

As someone that came to Vim from Sublime Text (through the excellent Vi-ntage mode), one thing that held me back was just how annoying the default Vim settings are. In a way looking back at it that wasn't a bad thing, it let me really craft my own configuration that I'm pretty happy with, but always looking for ways to improve. In order to help someone else a who is headed down that path find a config that works for them a little quicker.

<!-- more -->

To start off I just want to look at the basic stuff, how do we get rid of all that annoying old Vi stuff and get some useful defaults?

First, the most important thing to do is turn off Vi-compatibility, unless you plan on using this config on really old computers you shouldn't have any need for this compatibility.

~~~
" Use Vim settings that are not compatible with legacy Vi
set nocompatible
~~~

By default backspace in Vim's insert mode behaves a little weirdly. It works as you expect on a single line, but doesn't allow you to delete over new lines, automatically indented text, or beyond the point where you entered insert mode. You can change that by adding that to the backspace setting. I also like to set utf-8 to handle odd characters without trouble (I use √ all the time in todo lists for example).

~~~
" Backspace anything in insert mode
set backspace=indent,eol,start

" Set the text encoding to handle utf-8
set encoding=utf-8
~~~

Next we want to make things start to look a little better (more on that in a later post). Most of this is pretty self explanatory. One cool thing is relativenumber/number this sets it so the current line give you the actual line number with all the other lines relative to that. This makes it so it's easy to run commands like 10j or 5dd without having to count the lines.

Scroll off makes sure the current line always has n lines above or below visible. Some people like to set this to 4000 or some other high number to always keep the cursor in the center of the screen, personally I like to just leave it at 4 or 5.

~~~
syntax on           " Syntax highlighting
set relativenumber	" Line numbers relative to cursor
set number          " But ignore the current line
set numberwidth=4   " How wide the line number column should be by default
set showcmd         " Show incomplete commands
set noerrorbells    " No dinging!
set scrolloff=4     " Pad lines vertically by 4
set hidden          " Hide buffers instead of yelling at me about it
set ruler           " Tells you the coords of the cursor in the status line
set wildmenu        " Tab complete vim commands
set wildmode=longest,list,full
set laststatus=2    " Always show status line
~~~

Tabs are something that everyone complains about with Vim and they are a little bit confusing at first. Basically the width of what your tab key creates and what the shift keys (`<<`, `>>`, `<`, and `>`) create are two separate settings, even though you would very rarely actually want them different. Here I'm just showing how I like to indent my code in a perfect world (2 spaces, autoindented nicely), later when we talk about plugins I'll show you how to do this on a per file-type basis.

Breakindent is a bleeding edge feature added to Vim 7.4, which makes words wrap such that they respect the indent level. This makes word wrap with long-lined and heavily indented code (cough html cough) actually alright to look at.

~~~
" Nice, compact default tab settings
set tabstop=2
set shiftwidth=2
set expandtab
set autoindent
" set nowrap
set breakindent
~~~

If you still want to be able to use the mouse and your terminal allows it, you can enable it with this function. I used to, but I find it gets more in the way than I actually use it, but it's nice to know how to enable it if you want it sometime.

~~~
" In many terminal emulators the mouse works just fine, so you can enable it.
if has('mouse')
  set mouse=a
endif
~~~

One thing you'll notice when working with Vim is all these dotfiles it litters all over your working directory. These are how maintains undo state across sessions as one example. A lot of people just disable this because they don't like the clutter and use version control (which everyone should of course). But instead of just getting rid of it I like to throw it in a tmp directory somewhere so if some catastrophic does happen I have a backup plan.

Also copy and paste isn't great out of the box, setting copyindent makes things a lot more bearable.

~~~
" File management
set undolevels=1000
set backupdir=~/.vim/tmp
set directory=~/.vim/tmp
set undodir=~/.vim/tmp
set noswapfile

" Copy/Paste settings
set copyindent
~~~

Finally some more personal choices that I've found useful. Colorcolumn just draws a vertical sstripe at 80 characters wide to show when my code is getting to wide. Incsearch and hlsearch make regex-ing a nicer visual experience. Set spell is awesome, it highlights your mistakes, and gives you a list of suggestions when you run `za=`. Run `:help spell` for more details.

~~~
set incsearch   " Show matches as you type
set hlsearch    " Highlight all search matches not just the current one
set showmatch   " Visually flash matching brackets when typing
set spell       " Spell checker for Vim!
set colorcolumn=80 " Let me know when my lines are too damn long
~~~

That's it for now, next time we'll talk about the adventure that is key remapping.
