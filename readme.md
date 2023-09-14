# My Setup

## Intro
This is a brief description of my Mac M1 developer setup, which is currently based on Nix for Darwin and Linux. The core idea is to have a few tools like `make` or `git` available on both systems and have the rest available on a per-project basis. That way I switch language or database versions per project without influencing the rest of the system.

Note: The following docs contain automation, but they are not fully automated. This is on purpose. I like it more descriptive, so it's comprehensible and adaptable for other future setups.

## Building blocks
My setup currently consists of 4 building blocks: 

1. Nix on Mac: [nix-mac/](nix-mac/)
2. Tracking dotfiles with git: [track-dotfiles.md](track-dotfiles.md)
3. Linux VM with UTM and NixOS: [linux-vm-nixos](linux-vm-nixos/) 
4. Project specific Nix configuration: [nix-projects](nix-projects.md)