vim-emoji
=========

Emoji in Vim. Emojis are only available on terminal Vim on Mac.

Extracted from
[vim-github-dashboard](https://github.com/junegunn/vim-github-dashboard).

![](https://raw.github.com/junegunn/vim-emoji/png/emoji-sign.png)

Installation
------------

[Use](https://github.com/tpope/vim-pathogen)
[your](https://github.com/gmarik/vundle)
[favorite](https://github.com/junegunn/vim-plug)
[plugin](https://github.com/Shougo/neobundle.vim)
[manager](https://github.com/MarcWeber/vim-addon-manager).

- [Pathogen](https://github.com/tpope/vim-pathogen)
  - `git clone https://github.com/junegunn/vim-emoji.git ~/.vim/bundle/vim-emoji`
- [Vundle](https://github.com/gmarik/vundle)
  1. Add `Bundle 'junegunn/vim-emoji'` to .vimrc
  2. Run `:BundleInstall`
- [NeoBundle](https://github.com/Shougo/neobundle.vim)
  1. Add `NeoBundle 'junegunn/vim-emoji'` to .vimrc
  2. Run `:NeoBundleInstall`
- [vim-plug](https://github.com/junegunn/vim-plug)
  1. Add `Plug 'junegunn/vim-emoji'` to .vimrc
  2. Run `:PlugInstall`

List of functions
-----------------

- `emoji#available()`
- `emoji#for(name[, default = '', pad = 1])`
  - Refer to [Emoji cheat sheet](http://www.emoji-cheat-sheet.com)
- `emoji#list()`

Examples
--------

### Using Emojis as [Git Gutter](https://github.com/airblade/vim-gitgutter) symbols

```vim
" In .vimrc
silent! if emoji#available()
  let g:gitgutter_sign_added = emoji#for('small_blue_diamond')
  let g:gitgutter_sign_modified = emoji#for('small_orange_diamond')
  let g:gitgutter_sign_removed = emoji#for('small_red_triangle')
  let g:gitgutter_sign_modified_removed = emoji#for('collision')
endif
```

### Append Emoji list to current buffer

```vim
for e in emoji#list()
  call append(line('$'), printf('%s (%s)', emoji#for(e), e))
endfor
```

### Replace `:emoji_name:` into Emojis

```vim
function! s:replace_emojis() range
  for lnum in range(a:firstline, a:lastline)
    let line = getline(lnum)
    let subs = substitute(line,
          \ '\(:\([^:]\+\):\)', '\=emoji#for(submatch(2), submatch(1))', 'g')
    if line != subs
      call setline(lnum, subs)
    endif
  endfor
endfunction
command! -range ReplaceEmojis <line1>,<line2>call s:replace_emojis()
```
