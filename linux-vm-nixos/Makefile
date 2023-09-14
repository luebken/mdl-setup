# Bootstrap the filesystems
bootstrap-fs:
	ssh root@$(NIXADDR) " \
		parted /dev/vda -- mklabel gpt; \
		parted /dev/vda -- mkpart primary 512MB -8GB; \
		parted /dev/vda -- mkpart primary linux-swap -8GB 100\%; \
		parted /dev/vda -- mkpart ESP fat32 1MB 512MB; \
		parted /dev/vda -- set 3 esp on; \
		sleep 1; \
		mkfs.ext4 -L nixos /dev/vda1; \
		mkswap -L swap /dev/vda2; \
		mkfs.fat -F 32 -n boot /dev/vda3; \
		sleep 1; \
		mount /dev/disk/by-label/nixos /mnt; \
		mkdir -p /mnt/boot; \
		mount /dev/disk/by-label/boot /mnt/boot; \
	"

# Bootstrap with basic config to setup SSH
# TODO split
bootstrap-ssh:
	ssh root@$(NIXADDR) " \
		nixos-generate-config --root /mnt; \
		sed --in-place '/system\.stateVersion = .*/a \
  			services.openssh.enable = true;\n \
			services.openssh.settings.PasswordAuthentication = true;\n \
			services.openssh.settings.PermitRootLogin = \"yes\";\n \
			users.users.root.initialPassword = \"password\";\n \
		' /mnt/etc/nixos/configuration.nix; \
		nixos-install --no-root-passwd \
	"