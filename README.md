# mint-backgrounds

![AUR version](https://img.shields.io/aur/version/mint-backgrounds?label=AUR)
![AUR votes](https://img.shields.io/aur/votes/mint-backgrounds)

This repository contains build files to build the Arch Linux package `mint-backgrounds`. Instead of building the
package yourself, it can also be obtained from the following private repository. More detailed are described
[here](#obtaining-pre-built-packages-from-a-repository).

## Build

Clone this repository and use `makepkg` to build the package by yourself. For example:

```bash
git clone https://aur.archlinux.org/mint-backgrounds.git
cd mint-backgrounds
makepkg
```

## Yay

The build files are also available via AUR and can be installed via an AUR helper like `yay`.

```bash
yay --sync --aur mint-backgrounds
```

## Obtaining pre-built packages from a repository

Instead of building the packages locally, it is also possible to configure an additional repository to install the
package directly via `pacman`. The following commands are used to create the repository, configure the GPG key to verify
the packages and install the package:

```bash
# Create drop-in directory
sudo mkdir --parents /etc/pacman.d/repos

# Create configuration of the repository 'volker.raschek'
sudo tee /etc/pacman.d/repos/volker.raschek.conf > /dev/null <<'EOF'
[volker.raschek]
SigLevel = PackageRequired TrustedOnly
Include = /etc/pacman.d/repos/volker.raschek.list
EOF

# Create mirror list of the repository 'volker.raschek'
sudo tee /etc/pacman.d/repos/volker.raschek.list > /dev/null <<'EOF'
Server = https://aur.cryptic.systems/$repo/$arch
EOF

# Import gpg key of the repository 'volker.raschek'
sudo pacman-key --keyserver hkps://keys.openpgp.org --recv-keys 9B146D11A9ED6CA7E279EB1A852BCC170D81A982

# Extend existing pacman configuration of the repository 'volker.raschek'
sudo echo "Include = /etc/pacman.d/repos/*.conf" >> /etc/pacman.conf

# Update pacman cache
sudo pacman --sync --refresh

# Install the package and receive updates directly via pacman :)
sudo pacman --sync mint-backgrounds
```
