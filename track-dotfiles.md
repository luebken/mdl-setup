# Tracking dotfiles

The idea is to use to Git to understand of what's happening in my home folder with all the configurations that are changed from the various developer tools.

## Configure
Create a `.gitignore` to your home directory and add all the Mac folders like "Desktop", "Document" etc. to it. Choose a folder that is unique and recognizable, mine is `.mdl-cfg`.

Next create a [bare Git repository](https://www.saintsjd.com/2011/01/what-is-a-bare-git-repository/) and configure the git command to interact with it:

```sh
git init --bare $HOME/.mdl-cfg
```
```sh
# Add the alias to .bash_profile:
alias mdl-cfg='git --git-dir=$HOME/.mdl-cfg/ --work-tree=$HOME'
echo "$ mdl-cfg status -s:"
mdl-cfg status -s
echo "to clean run: $ mdl-cfg clean -fd"
```

Afterwards use your new command just like git:
```sh
mdl-cfg status
mdl-cfg add .
mdl-cfg commit -m "inital commit"
```

Note: I explicitly want so show untracked files. Other tutorials suggest to unset it via: `status.showUntrackedFiles no`.

