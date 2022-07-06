# dotfiles

## Install on a new computer

````
//make a alias for git that uses .cfg directory 
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

//gitignore the config repo itself
echo ".cfg" >> .gitignore
git clone --bare git@github.com:EsaNuurtamo/dotfiles.git $HOME/.cfg

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
