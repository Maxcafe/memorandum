# memorandum
setupやshortcut keyなどを自分の備忘録としてまとめておく．

## エイリアスの作り方

`~/.bashrc`で
```
alias [エイリアス文字列]='[エイリアスしたいコマンド]'
```
と記述することでエイリアスの作成ができる．

今使っているエイリアスとしては，次のようなものがある．
```
# aliasの一覧
alias lla='ls -al'

alias sbc='source ~/.bashrc'
alias sbp='source ~/.bash_profile'

alias de='cd ~/Desktop'

```

## brew caskでインストールしたアプリをLaunchに出力させる

次のように`~/.bashrc`に記述すれば良い．

```
# brew caskでインストールしたアプリをLaunchに出力させる
export HOMEBREW_CASK_OPTS="--appdir=/Applications"
```

## sshのパスフレーズの省略

ターミナルで
```
ssh-add -K ~/.ssh/[秘密鍵]
```
と打つことで永続的に秘密鍵を登録することができる．

もしくは

`~/.ssh/config`で以下のように記述すれば良い．
```
Host *
    AddKeysToAgent yes
    UseKeychain yes
```

ただし，セキュリティ的にはあまりよろしくない．

参考サイト: [ssh agentをパスフレーズ省略に応用する方法まとめ](https://qiita.com/onokatio/items/397a5899a0ec16c7e60a)

## ghqとpecoの初期設定

`~/.bashrc`に以下のものを追加する

```
# Ctrl-gでghqで設定しているroot以下のディレクトリを検索して移動する．
function Ctrl-g-cd-ghqroot() {
  local selected_file=$(ghq list --full-path | peco --query "$LBUFFER")
  if [ -n "$selected_file" ]; then
    if [ -t 1 ]; then
      echo ${selected_file}
      cd ${selected_file}
      pwd
    fi
  fi
}

bind -x '"\201": Ctrl-g-cd-ghqroot'
bind '"\C-g":"\201\C-m"'
```
変更したら
```
source ~/.bashrc
```
を行なって，設定を反映させる．

参考サイト:[Go言語開発環境のための、ghq+pecoの設定手順(macOS, bash向け)](https://qiita.com/hidache/items/7dbf0eba2f36f5e1a447)

## ターミナル起動時に~/.bashrcを常に読み込むようにする

`~/bash_profile`に以下のものを追記する．

```
# ターミナル起動時に~/.bashrcを常に読み込むようにする
if [ -f ~/.bashrc ] ; then
. ~/.bashrc
fi
```
変更したら
```
source ~/.bashrc
```
を行なって，設定を反映させる．

参考サイト: [ターミナル起動時に.bashrcを読み込むようにする](http://blog.ruedap.com/2010/09/13/mac-bash-bashrc)
