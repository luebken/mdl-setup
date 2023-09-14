# Nix projects

To install project specific packages I'm leveraging "nix-shell" which uses a per directory file.

e.g. for a NodeJS project create a `shell.nix` file:

```sh
{ pkgs ? import <nixpkgs> {} }:

pkgs.mkShell {
  packages = [
    pkgs.nodejs_20
  ];
}
```

In the project you can now enable it via `nix-shell` from the Mac host or from the Linux VM.