# dotfiles

## Install on a new computer

Do the following commands in HOME -folder:
````
//gitignore the config repo itself
echo ".cfg" >> .gitignore
git clone --bare git@github.com:EsaNuurtamo/dotfiles.git $HOME/.cfg

//make a alias for git that uses .cfg directory
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

// checkout files from the remote
config checkout

//if there is conflicts backup the files you need and rerun checkout
mkdir -p .config-backup && \
config checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | \
xargs -I{} mv {} .config-backup/{}

config config --local status.showUntrackedFiles no
````

## Start commiting your dotfile changes
````
config status
config add .vimrc
config commit -m "Add vimrc"
config add .bashrc
config commit -m "Add bashrc"
config push
````

### Terminal and fish shell
- Install iTerm2
- Install fish and fisher
- Link the preferences in iterm2: General -> Preferences -> load from custom folder
- Install custom fonts

#### Copy these commands
````
brew update 
brew install cask fish fisher git node 
brew tap homebrew/cask-fonts
brew install --cask font-hack-nerd-font iterm2 karabiner-elements
````

### Install editor and plugins
- VSCode is easy to setup
- Here is neovim config that offers most things that VSCode has (linting, global search, autosuggestions, typescript checking)
````
brew install nvim 
````
Create a symbolic link from neovim to the sandard place where VIM is installed:
`ln -s (which nvim) /usr/local/bin/vim`))

## Plugin manager for Neovim:
````
sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
       https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
````
Open neovim and it will install the plugins that are defined in init.vim:
````
nvim //open editor
:PlugsInstall //in the editor
````

Check out inspiration from here:
https://github.com/craftzdog/dotfiles-public
