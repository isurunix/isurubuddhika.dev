---
title: "Setting up NeoVim and NVChad in WSL"
date: 2023-11-11T18:35:48+05:30
draft: false
tags:
- WSL
- Neovim
- NvChad
description: "Guide to setting up neovim and NVchad in WSL and the pain points I experienced during the setup"
---

I usually use vim as my text editor of choice when I'm working with different text files like configurations,
build scripts, docker compose files and etc. Some time ago I started using NeoVim on my personal laptop outof curiosity
and at the end I fell in love with it. So natuarally I wanted to use the same in my work setup as well.
Although Fedora is my goto distro nowadays for work I have to use Windows as per company policy.
However I ended up using WSL/Ubuntu for all my development work since I couldn't live without all the nicities of Linux.
This is just a casual article expalining all the unexpected errors I came across when I'm setting up NeoVim and NVChad on WSL/Ubuntu

## Installation Steps

1. Install latest Neovim version.  
   ```bash
   # Download and extract neovim latest
   wget https://github.com/neovim/neovim/releases/latest/download/nvim-linux64.tar.gz 
   tar -xzvf nvim-linux.tar.gz
   sudo mv nvim-linux /opt/nvim
   sudo ln -s /usr/bin/nvim /opt/nvim/bin/nvim

   # Edit .bashrc or .zshrc based on your shell to replace vi/vim with nvim
   alias vi=nvim
   alias vim=nvim
   ```
2. Install NvChad  
   ```bash
   # Backup existing config
   mkdir ~/backup_nvim
   cp -r ~/.config/nvim ~/backup_nvim
   cp -r ~/.local/share/nvim ~/backup_nvim
   cp -r ~/.cache/nvim ~/backup_nvim

   # Remove old configs
   rm -rf ~/.config/nvim
   rm -rf ~/.local/share/nvim
   rm -rf ~/.cache/nvim

   # Install NvChad
   git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim
   ```
## Post Install Experience

### First Hurdle

Well the very first issue I ran into was getting the correct NeoVim version. 
I'm running Ubuntu 20.04 on WSL and it appears that neither the official ubuntu repos or the official PPA for NVChad
on LaunchPad has the latest version. So I had to resort to manually downloading the binaries from the GitHub releases 
and setup the symlinks and all to get NeoVim working.
I know this is pretty trivial work in the world of Linux but still I got suprised when it didn't worked because 
I was so used working in Fedora and I totally forgot that I'm running a bit old distro on WSL.

**TLDR:**
>If you are running a older distro and want to use NeoVim and NvChad better to install the latest version of NeoVim 
using the GitHub releases instead of using your OS package manager and repositories.

### Second Hurdle

So with installing the correct version completed I was looking at using nvim as my daily editor. But then only I noticed
that I have a very strange issue. *Nvim wasn't allowing me to press even a single key*. Pressing a single key would
through a error in nvim mentioning that plugin files could not be parsed due to incorrect line endings. The error was 
due to plugin Lua files containing ^M for line endings rather than /n line endings expected in Linux.
This was strange because I was running all the installation commands from within WSL terminal. Anyway I decided to fix
the line endings with `dos2linux` tool and it seems to fix the problem.

## The End

So with line endings issue with plugins resolved I was finally able to get nvim and NvChad up and running successfully
in WSL/Ubuntu. So far I haven't seen any other issues with the setup and I'm happily using it for most of my text editing
work. 
