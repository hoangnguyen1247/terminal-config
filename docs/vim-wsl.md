# Vim-wsl

```
syntax on
set hidden
set encoding=utf-8
set nobackup
set nowritebackup
" hightlight syntax
set re=0
" using unanamed for clipboard
set clipboard^=unnamed,unnamedplus
" show line number
set number
" allow place mouse pointer
set mouse=a

filetype plugin indent on
" show existing tab with 4 spaces width
set tabstop=4
" when indenting with '>', use 4 spaces width
set shiftwidth=4
" On pressing tab, insert 4 spaces
set expandtab

call plug#begin('~/.vim/plugged')

" search files
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'

Plug 'neoclide/coc.nvim', {'branch': 'release'}
let g:coc_global_extensions = [ 'coc-json', 
	\ 'coc-html',
	\ 'coc-go',
	\ 'coc-tsserver']

Plug 'leafgarland/typescript-vim'
Plug 'peitalin/vim-jsx-typescript'

" theme
Plug 'tomasiser/vim-code-dark'

" comment code
Plug 'joom/vim-commentary'

call plug#end()

" WSL yank support
let s:clip = '/mnt/c/Windows/System32/clip.exe'  " change this path according to your mount point
if executable(s:clip)
    augroup WSLYank
        autocmd!
        autocmd TextYankPost * if v:event.operator ==# 'y' | call system(s:clip, @0) | endif
    augroup END
endif

nmap <silent> gd <Plug>(coc-definition)
nmap <silent> gy <Plug>(coc-type-definition)
nmap <silent> gi <Plug>(coc-implementation)
nmap <silent> gr <Plug>(coc-references)

nmap <leader>rn <Plug>(coc-rename)

set t_Co=256
set t_ut=
colorscheme codedar
```