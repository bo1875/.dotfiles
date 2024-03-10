# Dotfiles

This repo is for my dotfiles. It currently contains configuration files for **tmux** and **neovim**.  
I created these files mostly following https://github.com/josean-dev/dev-environment-files.

## tumx

tmux.conf is an exact copy from Josean's setup. More details can be refered to his blog post: https://www.josean.com/posts/tmux-setup

## neovim

The neovim setup is also mostly following Josean:

- lazy.nvim for plugins management.
- mason.nvim for lsp management.

# Install

## Clone the repo

Clone into a bare repository:

```bash
git clone --bare https://github.com/bo1875/.dotfiles.git
```

Define an alias so the rest of the git commands will always use the bare repository.

```bash
alias config='git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
```

_Note the above alias is also in the .zshrc file in the repo. In the future if you want to run git command on .dotfiles, you can always use **config** command._

Checkout the actual content from the bare repository to your $HOME.

```bash
config checkout
```

The step above might fail because you've already got some files with the same name. For example usually you might already got a .zshrc file. The follow command is a possible rough shortcut to move all the offending files automatically to a backup folder:

```bash
mkdir -p .config-backup && \
config checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | \
xargs -I{} mv {} .config-backup/{}
```

and then rerun the checkout if there were problems.

Next step is to set the flag _showUntrackedFiles_ to no on this specific (local) repository:

```bash
config config --local status.showUntrackedFiles no
```

## Installation steps for tmux

### Install tmux

```bash
brew install tmux
```

### Install tpm

```bash
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm
```

### Initialize plugins

A few plugins need to be initialized inside tumx. To do that, run tmux, then type the prefix (_ctrl + a_), and then _shift I_.

## Installation steps for neovim

Install requirement:
iTerm2

```bash
brew install --cask iterm2
```

Neovim (Version 0.9 or Later)

```bash
brew install neovim
```

Ripgrep - For Telescope Fuzzy Finder

```bash
brew install ripgrep
```

XCode Command Line Tools

```bash
xcode-select --install
```
