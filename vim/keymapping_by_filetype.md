# different key mapping for different filetype

vim already support autocmd which can be set to excutes on certain file types

so for simple use, you can write this in your vimrc:

```
autocmd FileType c,cpp nmap <buffer> <leader>ss ma:%!astyle --pad-oper --pad-header --unpad-paren<CR>`a
autocmd FileType rust nmap <buffer> <leader>ss ma:RustFmt<CR>`a
```

the lines above make `<leader>ss` use 
* astyle to reformat c and c++ code 
* rustfmt to reformat rust code

To avoid ReSource the vimrc cause problems you should put these in a group like below

This way augroup will get cleared and then set when ReSourced.

```
augroup reformat_key
    autocmd!
    autocmd FileType c,cpp nmap <buffer> <leader>ss ma:%!astyle --pad-oper --pad-header --unpad-paren<CR>`a
    autocmd FileType rust nmap <buffer> <leader>ss ma:RustFmt<CR>`a
augroup END
```

The approch above is for small changes. 

If you have more command like this, please consider move to `~/.vim/after/ftplugin/<filetype>.vim` for easier management.

`<filetype>` in this example is the `c,cpp,rust` part

If you choose to move, then in ~/.vim/after/ftplugin/c.vim would be this:

```
nmap <buffer> <leader>ss ma:%!astyle --pad-oper --pad-header --unpad-paren<CR>`a
```

# references

Just two answers:
1. [filetype dependent keymapping](https://vi.stackexchange.com/questions/10664/file-type-dependent-key-mapping)
1. [multi filetype in one autocmd](https://stackoverflow.com/questions/28310094/is-it-possible-to-include-multiple-file-types-when-using-the-filetype-event)
