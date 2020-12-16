# wsl-dotfiles

Dotfiles for my [Arch Linux](https://www.archlinux.org/) installation on WSL 2.

Note: Arch Linux is **not offically supported on WSL 2**.

## Software used

- [Git](https://git-scm.com)
- [GitHub CLI](https://github.com/cli/cli)
- [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh)
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k)
- [Vim](https://www.vim.org)
- [ZSH](http://zsh.sourceforge.net/)

## Setup

- Create a non-root user with sudo privileges, and switch to that user
- Clone this repository
- Symlink dotfiles in the repository to the appropriate location
- Run the following commands

```bash
# Install Oh My Zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "$ZSH_CUSTOM/themes/powerlevel10k"

# Install packages from repo
sudo pacman -Sy --needed `cat packages.txt`

# Install yay
git clone --depth 1 https://aur.archlinux.org/yay-bin.git
cd yay-bin
makepkg -sir
cd ..
rm -r yay-bin

# Install packages from AUR
yay --aur -S `cat packages_aur.txt`

# Set up Github CLI
gh auth login
mkdir "$ZSH_CUSTOM/plugins/gh"
gh completion -s zsh > "$ZSH_CUSTOM/plugins/gh/_gh"

# Configure WSL
cat > /tmp/wsl.conf <<EOF
[user]
default = $USER
EOF
sudo mv /tmp/wsl.conf /etc/wsl.conf
```
