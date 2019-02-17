# memorandum
setupやshortcut keyなどを自分の備忘録としてまとめておく．

## MacBookに導入しているもの

- Xcode
- homebrew
- peco
- ghq
- iTerm2
- Alfred3
- InosomniaX
- Popcorn-time
- AppCleaner
- Atom
  - texの設定をすること
- Emacs
- Evernote
- Thunderbird
- bash-completion
- Simple Comic
- µTorrent
- Clipy
- Vim
- Cafeine
- HyperSwitch
- Virtual Box
- Flux
- Firefox
- Google chrome
- VMware Horizon Client
- Eclipse
- Java
- Memory Cleaner
- VLC
- Texshop
- Stufflt Expander
- Toy Viewer
- Tunnelblick
- LINE
- Slack
- Telegram
- Wireshark
- Burp Suite Community Edition
- Cheat sheet
- Crash Plan

## brewでinstallするもの

```
brew install tree
brew install git
brew install ghq
brew install peco
brew install go
brew install nmap
brew install pyenv
brew install python3
brew install tmux
```

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
Host [ホスト] [ホスト名]
    User git
    Port 22
    HostName [ホスト名]
    identityFile ~/.ssh/[秘密鍵]
    TCPKeepAlive yes
    IdentitiesOnly yes
    AddKeysToAgent yes
    UseKeychain yes
```

ただし，セキュリティ的にはあまりよろしくない．

参考サイト:
- [ssh agentをパスフレーズ省略に応用する方法まとめ](https://qiita.com/onokatio/items/397a5899a0ec16c7e60a)

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

参考サイト:
- [Go言語開発環境のための、ghq+pecoの設定手順(macOS, bash向け)](https://qiita.com/hidache/items/7dbf0eba2f36f5e1a447)
- [pecoの基礎の基礎](https://qiita.com/xtetsuji/items/05f6f4c1b17854cdd75b)

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

## Vimの設定

```
"#####表示設定#####
set number "行番号を表示する
set title "編集中のファイル名を表示
set showmatch "括弧入力時の対応する括弧を表示
syntax on "コードの色分け
set expandtab
set tabstop=2 "インデントをスペース2つ分に設定
set shiftwidth=2 "tabを半角スペースで挿入する
set smartindent "オートインデント
set list "空白文字の可視化
set listchars=tab:»-,trail:-,eol:↲,extends:»,precedes:«,nbsp:% "可視化した空白文字の表示形式について
set nrformats-=octal ""0"で始まる数値を，8進数として扱わないようにする
set hidden "ファイルの保存をしていなくても，べつのファイルを開けるようにする
set history=50
set virtualedit=block "文字のないところにカーソル移動できるようにする
set whichwrap=b,s,[,],<,> "カーソルの回り込みができるようになる(行末で→を押すと、次の行へ)
set backspace=indent,eol,start "バックスペースを，空白，行末，行頭でも使えるようにする
set wildmenu

"#####検索設定#####
set ignorecase "大文字/小文字の区別なく検索する
set smartcase "検索文字列に大文字が含まれている場合は区別して検索する
set wrapscan "検索時に最後まで行ったら最初に戻る
```
