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

alias gia='git add .'
alias gic='git commit -m'
alias gip='git push'
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

はじめにghqのルートにしたいディレクトリをルートに以下のコマンドで設定する．
```
git config --global ghq.root [ghqのルートにしたいディレクトリのパス] 
```

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

bind -x '"\C-g": Ctrl-g-cd-ghqroot'
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
set listchars=tab:»-,trail:-,eol:↲,ex"dein Scripts-----------------------------
if &compatible
  set nocompatible               " Be iMproved
endif

" Required:
set runtimepath+=/Users/Ryota.K/.cache/repos/github.com/Shougo/dein.vim

" Required:
if dein#load_state('/Users/Ryota.K/.cache')
  call dein#begin('/Users/Ryota.K/.cache')

  " Let dein manage dein
  " Required:
  call dein#add('/Users/Ryota.K/.cache/repos/github.com/Shougo/dein.vim')

  " Add or remove your plugins here like this:
  "call dein#add('Shougo/neosnippet.vim')
  "call dein#add('Shougo/neosnippet-snippets')
  call dein#add('davidhalter/jedi-vim')
  call dein#add('scrooloose/nerdtree')

  " Required:
  call dein#end()
  call dein#save_state()
endif

" Required:
filetype plugin indent on
syntax enable

" If you want to install not installed plugins on startup.
if dein#check_install()
  call dein#install()
endif

"End dein Scripts-------------------------

"#####表示設定#####
set number "行番号を表示する
set title "編集中のファイル名を表示
set showmatch "括弧入力時の対応する括弧を表示
syntax on "コードの色分け
set expandtab "タブ入力を複数の空白入力に置き換える
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
set wildmenu " コマンドモードの補完
set ruler

"#####検索設定#####
set ignorecase "大文字/小文字の区別なく検索する
set smartcase "検索文字列に大文字が含まれている場合は区別して検索する
set wrapscan "検索時に最後まで行ったら最初に戻る
set incsearch " インクリメンタルサーチ. １文字入力毎に検索を行う
set hlsearch " 検索結果をハイライト

"#####カーソル#####
set whichwrap=b,s,h,l,<,>,[,],~ " カーソルの左右移動で行末から次の行の行頭への移動が可能になる
set cursorline " カーソルラインをハイライト
source $VIMRUNTIME/macros/matchit.vim " Vimの「%」を拡張する

"#####マウスの有効化#####
if has('mouse')
    set mouse=a
    if has('mouse_sgr')
        set ttymouse=sgr
    elseif v:version > 703 || v:version is 703 && has('patch632')
        set ttymouse=sgr
    else
        set ttymouse=xterm2
    endif
endif

"#####ペースト設定#####
"クリップボードから普通にペーストすると自動インデントが効いて下に行くほど右にずれていきますが，以下の設定をすることで，クリップボードからペーストする時だけインデントしないようにしてくれる．
if &term =~ "xterm"
    let &t_SI .= "\e[?2004h"
    let &t_EI .= "\e[?2004l"
    let &pastetoggle = "\e[201~"

    function XTermPasteBegin(ret)
        set paste
        return a:ret
    endfunction

    inoremap <special> <expr> <Esc>[200~ XTermPasteBegin("")
endif

"#####自動補完#####
set completeopt=menuone
for k in split("abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ_",'\zs')
  exec "imap " . k . " " . k . "<C-N><C-P>"
endfor

"imap <expr> <TAB> pumvisible() ? "\<Down>" : "\<Tab>"
tends:»,precedes:«,nbsp:% "可視化した空白文字の表示形式について
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
