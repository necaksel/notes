# thinkpad setup

## Installed brew
https://docs.brew.sh/Homebrew-on-Linux
Installed with admint user.
Then ran this in the admubuntu home folder.
```shell
test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"
test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.zshrc
```
Homebrew needs to be run from the sudo user, and in the home folder
of the sudo user, and the zsh setup hasn't worked so you need
to add it to path manually
```shell
s
cd
test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"
test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
brew # now it should work
```

## Install k9s
`brew install derailed/k9s/k9s`
And added this to .zshrc
`eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)`
For it to be on the path I need to run this manually:
Now k9s works