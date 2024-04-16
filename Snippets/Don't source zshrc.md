
Source: https://github.com/ohmyzsh/ohmyzsh/wiki/FAQ#how-do-i-reload-the-zshrc-file

```zsh
# don't source ~/.zshrc
# instead: 
exec zsh

# can also do the following to invoke as a login (-l) shell
exec -l zsh
```

