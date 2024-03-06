
Excellent YouTube videos
- by DevInsideYou [here](https://www.youtube.com/watch?v=CFzEuBGPPPg). 
- [System Crafters](https://www.youtube.com/watch?v=CxAT1u8G7is) 


```bash
# create link 
# -n "don't run"
stow -nvSt ~ *


# unstow everything
stow -nvDt ~ * 
# simulation

# dotfiles for changing dot-tmux.conf -> .tmux.conf
stow --dotfiles 
```

```zsh

stowth() {
	stow --dotfiles -vSt ~ $1
}

unstow() {
	stow --dotfiles -vDt ~ $1
}
```


Possible have a file with 

.stow-local-ignore


```zsh

stowth() {
    if [ $# -eq 0 ]; then
        echo "Usage: stowth <package_name>... [--simulate]"
        return 1
    fi
    
    local opts="--dotfiles -vSt ~"
    local packages=()
    for arg in "$@"; do
        if [[ $arg == "--simulate" ]]; then
            opts="$opts -n"
            echo "Dry-run mode (simulate): showing actions without applying changes."
        else
            packages+=("$arg")
        fi
    done
    
    stow $opts "${packages[@]}"
}

unstow() {
    if [ $# -eq 0 ]; then
        echo "Usage: unstow <package_name>... [--simulate]"
        return 1
    fi
    
    local opts="--dotfiles -vDt ~"
    local packages=()
    for arg in "$@"; do
        if [[ $arg == "--simulate" ]]; then
            opts="$opts -n"
            echo "Dry-run mode (simulate): showing actions without applying changes."
        else
            packages+=("$arg")
        fi
    done
    
    stow $opts "${packages[@]}"
}

```