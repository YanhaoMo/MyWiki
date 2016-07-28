# .zshrc
```zsh
export ZSH=/opt/oh-my-zsh
ZSH_THEME="robbyrussell"
plugins=(git sudo docker)
source $ZSH/oh-my-zsh.sh
COMPLETION_WAITING_DOTS="true"
# ENABLE_CORRECTION="true"
# DISABLE_UNTRACKED_FILES_DIRTY="true"

CONF_DIR=~/.shell
for i in {alias,functions,variables} ; do
  if [ -f $CONF_DIR/$i ] ; then
    source $CONF_DIR/$i
  fi
done
```
# .shell/alias
```zsh
alias es='emacs --daemon'
alias e='env TERM=xterm-256color emacsclient -t'
alias ec='emacsclient -c'
alias emacs='env TERM=xterm-256color emacs -nw'
alias tm='tmux -2'
alias minicom='minicom -c on'
alias ff='fcitx-fbterm-helper -l'
alias baise='echo -en "\e]P7ffffff"'
alias discon_sm="smbcontrol nmbd shutdown && smbcontrol smbd shutdown"
```
# .shell/variables
```zsh
export LANGUAGE="en_US.UTF-8"
```
# .shell/functions
```zsh
function update() {
  if [[ $# > 1 ]]; then
    echo Only support one parament !
    return -1
  fi
# 检查是否为git目录
  if [[ -d .git ]]; then
    if [[ $# = 1 ]]; then
        git add --all && git ct -m $1 && git push
    else
        git add --all && git ct -m "update" && git push
    fi
  else
    echo Have no git repository! Or you are in a wrong directory.
    return -1
  fi
}
function upload() {
# 必须要有一个参数
  if [[ $# != 1 ]]; then
    echo Usage: upload path/to/image
    return -1
  fi
# 上传图片
  curl -F "name=@$1" http://img.vim-cn.com/
}
```