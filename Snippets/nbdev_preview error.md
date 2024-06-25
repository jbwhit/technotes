
## The problem

```
❯ nbdev_preview
Preparing to preview
[1/2] 00_core.ipynb
Error running Lua:
error loading module 'lpeg' from file '/usr/local/lib/lua/5.4/lpeg.so':
	dlopen(/usr/local/lib/lua/5.4/lpeg.so, 0x0006): tried: '/usr/local/lib/lua/5.4/lpeg.so' (code signature in <CCEE8702-AB22-3100-BFA3-4ADBDFA3E36B> '/usr/local/Cellar/lpeg/1.1.0/lib/lua/5.4/lpeg.so' not valid for use in process: mapped file has no cdhash, completely unsigned? Code has to be at least ad-hoc signed.), '/System/Volumes/Preboot/Cryptexes/OS/usr/local/lib/lua/5.4/lpeg.so' (no such file), '/usr/local/lib/lua/5.4/lpeg.so' (code signature in <CCEE8702-AB22-3100-BFA3-4ADBDFA3E36B> '/usr/local/Cellar/lpeg/1.1.0/lib/lua/5.4/lpeg.so' not valid for use in process: mapped file has no cdhash, completely unsigned? Code has to be at least ad-hoc signed.), '/usr/local/Cellar/lpeg/1.1.0/lib/lua/5.4/lpeg.so' (code signature in <CCEE8702-AB22-3100-BFA3-4ADBDFA3E36B> '/usr/local/Cellar/lpeg/1.1.0/lib/lua/5.4/lpeg.so' not valid for use in process: mapped file has no cdhash, completely unsigned? Code has to be at least ad-hoc signed.), '/System/Volumes/Preboot/Cryptexes/OS/usr/local/Cellar/lpeg/1.1.0/lib/lua/5.4/lpeg.so' (no such file), '/usr/local/Cellar/lpeg/1.1.0/lib/lua/5.4/lpeg.so' (code signature in <CCEE8702-AB22-3100-BFA3-4ADBDFA3E36B> '/usr/local/Cellar/lpeg/1.1.0/lib/lua/5.4/lpeg.so' not valid for use in process: mapped file has no cdhash, completely unsigned? Code has to be at least ad-hoc signed.)
stack traceback:
	[C]: in upvalue 'orig_require'
	[string "..."]:1442: in function 'require'
	/Applications/quarto/share/pandoc/datadir/lpegshortcode.lua:4: in main chunk
	[C]: in upvalue 'orig_require'
	[string "..."]:1442: in function 'require'
	/Applications/quarto/share/pandoc/datadir/readqmd.lua:6: in main chunk
	[C]: in upvalue 'orig_require'
	[string "..."]:1442: in function 'require'
	/Applications/quarto/share/filters/qmd-reader.lua:6: in main chunk
```


## The fix 

This apparently was a problem in the quarto install. 

I went to this: https://quarto.org/docs/download/ to get the pre-release and installing that package (1.5.40) all the problems went away. 

## Things that didn't work:

Things that I had tried, uninstalling/reinstalling pandoc, lpeg, neovim, etc. 