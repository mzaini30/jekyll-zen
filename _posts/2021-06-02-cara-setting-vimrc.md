---
layout: post
title: Cara Setting .vimrc untuk Setting Neovim
image: https://1.bp.blogspot.com/-Q1joKqelonw/XTmdJb1U6GI/AAAAAAAACh8/xqKkg7Vq43wAuNIZRhwaEkyihrx40tHKACLcBGAs/s1600/Neovim%2BScreenshots%2B1.jpg  
category: linux
---

Mungkin ini menjadi artikel pertama aku bahas Neovim di sini. Ya karena capek juga sih belajar text editor yang berbeda dengan yang biasanya digunakan. Kan kalau biasanya itu, kayak Sublime, kita ngetiknya ya di Sublime. Nah, kalau Neovim, kita mengetiknya di Terminal. Mantap dah. Jadinya sih lebih ringan ya. Cuma, aku masih bingung aja sih cara makainya. Oh iya, postingan ini aku ngetiknya juga di Neovim.

Pastikan dulu kamu sudah install Neovim dengan perintah:

```bash
sudo apt install neovim
```

Kalau di Termux:

```bash
pkg install neovim
```

Kemudian, buat `~/.config/nvim/init.vim` yang isinya:

```vim
set runtimepath+=~/.vim,~/.vim/after
set packpath+=~/.vim
source ~/.vimrc
```

Sekarang, kita bisa membuat settingan kita di `~/.vimrc`

Contohnya aja:

```vim
set tabstop=2       " The width of a TAB is set to 4.
                    " Still it is a \t. It is just that
                    " Vim will interpret it to be having
                    " a width of 4.
set shiftwidth=2    " Indents will have a width of 4
set softtabstop=2   " Sets the number of columns for a TAB
set expandtab       " Expand TABs to spaces
set nocompatible              " be iMproved, required
filetype plugin indent on                  " required
syntax on
```
