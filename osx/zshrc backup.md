# Zshrc Backup

```bash
# pyenv
export PATH="$HOME/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"

# go
export GOPATH=$HOME/go

# npm
export PATH=~/.npm-global/bin:$PATH

# aliases - zsh
alias rmhistory='rm $HISTFILE'

# aliases - docker
alias dcbuild='docker-compose build'
alias dcup='docker-compose up'
alias dcstop='docker-compose stop'
alias dcstopall='docker stop $(docker ps -aq)'
alias dcexec='docker-compose exec'
alias dcrmc='docker container prune'
alias dcrmi='docker image prune'
alias dcrmv='docker volume prune'
alias dcrmn='docker network prune'
alias dcrmall='docker system prune'
```

