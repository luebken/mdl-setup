# Install Mac Nix

[Nix](https://nixos.org) is a package-manager / DSL / Linux and makes my setup reproducible by using declarative builds and deployments.

## Install Nix Package Manager
I've used the [official installation script](https://nixos.org/nix/install). The [Mac installation](https://nixos.org/manual/nix/stable/installation/installing-binary#macos-installation) is a [multi-user installation](https://nixos.org/manual/nix/stable/installation/multi-user). The nix store is stored on it's own APFS volume (see in disk utility), is owned by root and a daemon with a couple of users for the different builds (see Users & Groups in System Settings).

## Nix Darwin

Additionally you need to install [Nix Darwin](https://github.com/LnL7/nix-darwin) which is the equivalent to NixOS.

## Configure Nix
To configure the setup we need to add packages and other configurations to: `~/.nixpkgs/darwin-configuration.nix` and run `darwin-rebuild switch` afterwards. See [.nixpkgs/darwin-configuration.nix](.nixpkgs/darwin-configuration.nix) for my current configuration.