---
type: slides
date: 2025-02-20
theme: real-black
customTheme: real-black
highlightTheme: tomorrow-night-bright
transition: fade
controls: false
progress: false
enableMenu: false
enableChalkboard: false
enableTitleFooter: false
enableZoom: false
enableSearch: false
overview: true
---

This slide intentionally left blank
<!-- element class="fragment fade-out" -->

---

# .dotfiles

---

# Why

---

## `${HOME}`-less

---

## notebook got stolen

---

## backup ?

---

```bash
$ ls -al ~
...
drwxr-xr-x 22 gbraad gbraad   4096 Feb 18 23:10 .dotfiles
-rw-------  1 gbraad gbraad  38154 Feb 23 12:00 .dotfiles.tgz
...
```

---

# How

---

## Simple

---

## Minimal

---

# I <font color="red">&lt;3</font> Shell

---

# command line interface

---

# bash

---

# zshell

---

# customization

---

# automation

---

# `.bashrc`  |  `.zshrc`

---

# Let's start with ...

---

# Aliases

---

## shorten commands

---

```bash
$ alias hello='echo Welcome"
```

---

```bash
$ hello $USER
$ hello Gerard Braad
```

---

`~/.zshrc` for `git`
```bash
alias g="git"
alias gs="g status"
alias ga="g add"
alias gad="ga ."
alias gc="g commit"
alias gcm="gc -m"
alias gca="gc --amend"
alias gpf="g push -f"
```

---

## limitations

---

# Functions

---

```bash
$ hate() {
  echo "I <3 $@. It is fun!"
}
$ hate systemd  #  really?
```

---

## arguments

---

```bash
just() {
  if [ $# -lt 1 ]; then
    echo "Usage: $0 <command> [args...]" ; return 1
  fi

  local COMMAND=$1
  shift 1

  case "$COMMAND" in
    "test")
      echo $@  # this is a testrunner invoke
      ;;
  esac
}
```

```
$ just test [testname]
```

---

# Distribute

---

## tarballs

---

## Please, don't!


---

# Git and stow

---

# `git`

---

## Do I need to explain this?!?

---

## `stow`

---

## Symlink manager

---

```bash
.dotfiles $ ls -al zsh
-rw-r--r--  1     832 Feb 18 22:07 .zshrc
.dotfiles $ stow zsh
.dotfiles $ ls -al ~
lrwxrwxrwx  1      20 Jun  1  2023 .zshrc -> 
    .dotfiles/zsh/.zshrc
```

---

## alternatives

### Chezmoi, tuckr, etc

---
# `git` does more

---

```bash
$ .dotfiles $ ls -al config/.config/dotfiles
-rw-r--r-- 1     1379 Feb 18 15:53 servers
$ .dotfiles $ stow config
$ .dotfiles $ ls -al ~/.config/
lrwxrwxrwx  1     36 Feb 19 15:00 dotfiles ->
    ../.dotfiles/config/.config/dotfiles
```

---

## ini-files

---

`~/.config/dotfiles/servers`
```ini
[servers]
        ncognito = 10.0.21.120
```

---

`~/.local/bin/isalive.zsh`
```bash
#~/bin/zsh
CONFIG="${HOME}/.config/dotfiles/servers"
alias serversini="git config -f $CONFIG"

server=$(serversini --get "servers.$1")
ping ${server}
```

---

`~/.zshrc`
```bash
if [ -d "$HOME/.local/bin" ]; then
    PATH="$HOME/.local/bin:$PATH"
fi
```

---

```bash
$ chmod +x ~/.local/bin/isalive.zsh
$ isalive.zsh ncognito
```

---

# `source`

---

`~/.zshrc`
```bash
# User specific aliases and functions
if [ -d ${HOME}/.zshrc.d ]; then
  for file in ${HOME}/.zshrc.d/*.?sh; do
    source $file
  done
fi
```

---

## `.zshrc.d/*.?sh`

---

`~/.zshrc.d/network.zsh`
```bash
CONFIG="${HOME}/.config/dotfiles/servers"
alias serversini="git config -f ${CONFIG}"

isalive() {
  server=$(serversini --get "servers.$1")
  ping ${server}
}
```

---

```bash
$ isalive
```

---

```bash
$ isalive ncognito
```

---

```bash
$ isalive ncognito
PING 10.0.21.120 (10.0.21.120) 56(84) bytes of data.
64 bytes from 10.0.21.120: icmp_seq=1 ttl=63 time=1.74 ms
...
^C
--- 10.0.21.120 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 904ms
rtt min/avg/max/mdev = 0.958/1.371/1.738/0.320 ms
```

---

# my .dotfiles

### [dotfiles.gbraad.nl](https://github.com/gbraad-dotfiles)

---

- `dotfiles|dot [install|update|restow|...]`

- `devenv|dev [create|user|root|...]`

- `machine|mcn [download|create|start|console|...]`

- `proxy|p [proxyname]` 

- `secrets|s [get|var|file|totp]`   

---

# my workflow

---

## `install.sh`

```shell
$ curl -fsSL dotfiles.gbraad.nl/install.sh | sh
```
---

# GitHub Actions

## [install-dotfiles-action](https://github.com/gbraad-dotfiles/install-dotfiles-action)

---

# devcontainers

## [github.com/gbraad-devenv](https://github.com/gbraad-devenv)

---

# ...
