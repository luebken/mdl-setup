# Linux VM with NixOS

99.9% of software will be deployed on Linux, so I'd like to get close to that by having a local VM with Linux handy. It's meant as a long running running environment. 

## Download
* Download and install [UTM](https://mac.getutm.app/)
* Download minimal [NixOS 64-bit ARM ISO](https://nixos.org/download)

## Install Boot VM
* Open UTM
* "Create a New Virtual Machine" > "Virtualize" > "Linux"
* "Boot Iso Image" Select downloaded iso: nixos-minima-...aarch64-linux.iso
* "Hardware & Storage": Use default values 
* Share a directory you want to share

## Configure SSH access for boot image
After starting up the VM set a root password with `sudo passwd` so we can ssh into it. Get the current IP with `ifconfig`. Set the IP in `.bash_profile` with `export NIXADDR=192.168.64.X`. You can now SSH into it `ssh root@$NIXADDR`.

## Bootstrap NixOS
For the actual Nix install configure the fileystem via `make bootstrap-fs`. See [Makefile](Makefile). For setting up SSH and running nix install `make bootstrap-ssh`.

Afterwards shutdown the VM from the UTM menu, clear the CD/DVD ISO and retstart the VM.

From the Mac terminal remove "known_hosts" entries and ssh into the machine:
```sh
sed -i '' '/192.168/d' ~/.ssh/known_hosts
ssh root@$NIXADDR
```

## File sharing
To enable filesharing we first need to add the 9pfs package to "/etc/nixos/configuration.nix":
```
  environment.systemPackages = with pkgs; [
    vim
    _9pfs
  ];
```
Create the mountpoint in the VM and rebuild the Nix configuration:
```sh
sudo mkdir /workspace
sudo mount -t 9p -o trans=virtio share /workspace -oversion=9p2000.L
nixos-generate-config
nixos-rebuild switch
```