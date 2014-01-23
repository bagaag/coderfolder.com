---
layout: default
title:  "My .vimrc File"
categories: ubuntu
---

    colorscheme slate

    syntax on

    nmap <C-V> "+gp
    imap <C-V> <ESC><C-V>a
    vmap <C-C> "+y

    set backspace=2
    set backspace=indent,eol,start

    set tabstop=4

    nnoremap <F5> "=strftime("%Y-%m-%d %H:%M ")<CR>P
    inoremap <F5> <C-R>=strftime("%Y-%m-%d %H:%M ")<CR>
    nnoremap <silent> <C-S> :if expand("%") == ""<CR>browse confirm w<CR>else<CR>confirm w<CR>endif<CR>
    inoremap <silent> <C-S> <ESC>:w<CR>a

    if has("gui_running")
      set guioptions-=T  "remove toolbar
      set lines=34 columns=100
      if has("gui_gtk2")
    	set guifont=Inconsolata\ 11
      elseif has("gui_win32")
    	set guifont=Consolas:h10:cANSI:b
      endif
    endif

    au BufRead,BufNewFile *.md set filetype=markdown
