

Automatic listing of files after a cd

```z
function cs () {
  if [ -n "$1" ]; then
    z "$@" && eza --color=auto --icons --group-directories-first -a
  else
    z ~ && eza --color=auto --icons --group-directories-first -a
  fi
}

```


