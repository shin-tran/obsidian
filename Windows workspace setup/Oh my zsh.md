## Setup
- Download Git
- Tutorial: https://dominikrys.com/posts/zsh-in-git-bash-on-windows/#installing-zsh-in-git-bash
## Install plugins

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting

git clone https://github.com/zsh-users/zsh-completions.git $ZSH_CUSTOM/plugins/zsh-completions

git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

```
- Add this line to `.zshrc`
```bash
plugins=(git zsh-autosuggestions zsh-syntax-highlighting web-search colored-man-pages command-not-found)
```
