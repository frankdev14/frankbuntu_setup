# sudo apt update && sudo apt upgrade && sudo reboot now
# sudo apt install curl
# curl -fsS https://dl.brave.com/install.sh | sh
# Setting up brave browser
# Remove snapd:
## https://ubuntuhandbook.org/index.php/2024/03/install-thunderbird-deb-ubuntu-2404/
## https://kskroyal.com/remove-snap-packages-from-ubuntu/ or https://www.omgubuntu.co.uk/2024/08/install-thunderbird-deb-not-snap-in-ubuntu-24-04
# sudo snap remove --purge firefox && sudo apt remove *firefox* && sudo apt remove *libreoffice* && sudo apt remove *remmina* && sudo apt remove *transmission* && sudo snap remove --purge thunderbird && sudo apt remove thunderbird
# sudo snap remove gtk-common-themes
# sudo snap remove gnome-42-2204
# sudo snap remove snapd-desktop-integration
# sudo snap remove desktop-security-center
# sudo snap remove prompting-client
# sudo snap remove snap-store
# sudo snap remove firmware-updater
# sudo snap remove bare
# sudo snap remove core22
# sudo snap remove snapd
sudo systemctl stop snapd
sudo systemctl disable snapd
sudo systemctl mask snapd
sudo apt purge snapd -y
sudo apt-mark hold snapd
sudo rm -rf ~/snap
sudo rm -rf /snap
sudo rm -rf /var/snap
sudo rm -rf /var/lib/snapd
sudo nano /etc/apt/preferences.d/nosnap.pref
Package: snapd
Pin: release a=*
Pin-Priority: -10

sudo install -d -m 0755 /etc/apt/keyrings
wget -q https://packages.mozilla.org/apt/repo-signing-key.gpg -O- | sudo tee /etc/apt/keyrings/packages.mozilla.org.asc > /dev/null

echo "deb [signed-by=/etc/apt/keyrings/packages.mozilla.org.asc] https://packages.mozilla.org/apt mozilla main" | sudo tee -a /etc/apt/sources.list.d/mozilla.list > /dev/null

echo '
Package: *
Pin: origin packages.mozilla.org
Pin-Priority: 1000
' | sudo tee /etc/apt/preferences.d/mozilla

sudo add-apt-repository ppa:mozillateam/ppa
sudo gnome-text-editor /etc/apt/preferences.d/mozillateamppa

Package: thunderbird*
Pin: release o=LP-PPA-mozillateam
Pin-Priority: 1000

Package: thunderbird*
Pin: release o=Ubuntu
Pin-Priority: -10

echo 'Unattended-Upgrade::Allowed-Origins:: "LP-PPA-mozillateam:${distro_codename}";' | sudo tee /etc/apt/apt.conf.d/51unattended-upgrades-thunderbird

# Install nvidia driver from aditional drivers

# setting up my screens and hz
# disable mouse acceleration

# sudo apt install gdebi
# https://github.com/ilya-zlobintsev/LACT
# Open software and install this software: refine, gnome extensions, bitwarden, protontricks, protonplus, adwsteamgtk, zen browser, spotify, discord, obsidian

sudo apt install dconf-editor gnome-tweaks pavucontrol

Open refine and enable vrr support



Open pavucontrol and change my audio settings and enable pro audio for jbl quantum

check devices with: pw-cli ls Node | less
mkdir -p ~/.config/wireplumber/wireplumber.conf.d
nano ~/.config/wireplumber/wireplumber.conf.d/55-audio-rename.conf

monitor.alsa.rules = [
  {
    matches = [
      {
        node.name = "alsa_output.usb-Harman_International_Inc_JBL_Quantum810_Wireless-00.pro-output-0"
      }
    ]
    actions = {
      update-props = {
        node.description = "JBL Quantum 810 Wireless Game"
      }
    }
  }
  {
    matches = [
      {
        node.name = "alsa_output.usb-Harman_International_Inc_JBL_Quantum810_Wireless-00.pro-output-1"
      }
    ]
    actions = {
      update-props = {
        node.description = "JBL Quantum 810 Wireless Chat"
      }
    }
  }
]

systemctl --user restart wireplumber.service

sudo apt install vlc steam ufw gufw

sudo systemctl enable ufw
sudo systemctl start ufw
sudo ufw deny 22/tcp


sudo apt install ubuntu-restricted-extras
sudo apt install build-essential checkinstall
sudo apt install libfuse2t64 unzip p7zip p7zip-full unrar

# Install spanish lang and setting up on format and keyboard, setting up

sudo mkdir -p '/etc/systemd/resolved.conf.d' && sudo -e '/etc/systemd/resolved.conf.d/99-dns-over-tls.conf'

[Resolve]
DNS=1.1.1.2#security.cloudflare-dns.com 1.0.0.2#security.cloudflare-dns.com 2606:4700:4700::1112#security.cloudflare-dns.com 2606:4700:4700::1002#security.cloudflare-dns.com
DNSOverTLS=yes
Domains=~.

sudo timedatectl set-local-rtc '0'

gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize-or-previews'

sudo apt install -y build-essential make curl ca-certificates libssl-dev libxmlsec1-dev libmagic-dev libmagickwand-dev zsh fzf git-lfs starship bleachbit ffmpeg geary

chsh -s $(which zsh)

sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/MichaelAquilina/zsh-you-should-use.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/you-should-use
git clone https://github.com/Aloxaf/fzf-tab ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/fzf-tab

sudo apt autoremove
sudo apt autoclean
sudo apt clean

sudo mv /etc/apt/apt.conf.d/20apt-esm-hook.conf /etc/apt/apt.conf.d/20apt-esm-hook.bak

curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.local/bin/env
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
rm -rf aws awscliv2.zip
https://github.com/frankdev14/windows_dotfiles
https://github.com/frankdev14/penguin_toolkit

sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt update
sudo apt install golang-go

Install vscode

# create an script for extensiones:
#!/bin/bash

extensions=(
    aaron-bond.better-comments
    alefragnani.project-manager
    batisteo.vscode-django
    charliermarsh.ruff
    cweijan.dbclient-jdbc
    cweijan.vscode-mysql-client2
    esbenp.prettier-vscode
    formulahendry.auto-close-tag
    formulahendry.auto-rename-tag
    github.remotehub
    graphql.vscode-graphql
    graphql.vscode-graphql-syntax
    gruntfuggly.todo-tree
    hbenl.vscode-test-explorer
    ibm.output-colorizer
    idleberg.icon-fonts
    kamikillerto.vscode-colorize
    kevinrose.vsc-python-indent
    littlefoxteam.vscode-python-test-adapter
    mhutchie.git-graph
    miguelsolorio.fluent-icons
    miguelsolorio.min-theme
    miguelsolorio.symbols
    mikestead.dotenv
    mkxml.vscode-filesize
    mrmlnc.vscode-autoprefixer
    ms-azuretools.vscode-containers
    ms-azuretools.vscode-docker
    ms-kubernetes-tools.vscode-kubernetes-tools
    ms-python.debugpy
    ms-python.isort
    ms-python.python
    ms-python.vscode-pylance
    ms-python.vscode-python-envs
    ms-vscode-remote.remote-containers
    ms-vscode-remote.remote-ssh
    ms-vscode-remote.remote-ssh-edit
    ms-vscode-remote.remote-wsl
    ms-vscode-remote.vscode-remote-extensionpack
    ms-vscode.azure-repos
    ms-vscode.remote-explorer
    ms-vscode.remote-repositories
    ms-vscode.remote-server
    ms-vscode.test-adapter-converter
    njpwerner.autodocstring
    pranaygp.vscode-css-peek
    redhat.vscode-yaml
    spywhere.guides
    wholroyd.jinja
    yzhang.markdown-all-in-one
    zhuangtongfa.material-theme
)

for ext in "${extensions[@]}"; do
  code --install-extension "$ext"
done

#exec: bash test.sh

sudo nano /etc/sysctl.conf

fs.inotify.max_user_watches = 10000000
fs.inotify.max_user_instances = 256

sudo sysctl -p

sudo apt install podman
flatpak install flathub io.podman_desktop.PodmanDesktop
# follow then podman desktop setup wizard

sudo mkdir -p /etc/systemd/system/user@.service.d/
sudo nano /etc/systemd/system/user@.service.d/delegate.conf

[Service]
Delegate=yes

sudo systemctl daemon-reload

systemctl --user restart podman

sudo nano /etc/environment
GDK_GL=gles

curl -fsSL https://ollama.com/install.sh | sh
sudo apt install nvidia-cuda-toolkit
curl -f https://zed.dev/install.sh | sh

Install nerd fonts
sudo fc-cache -f -v

Install dotfiles zsh, aws and starship dotfiles


# partition 2nd drive
sudo nano /etc/fstab

Save UUID for the next step:
sudo blkid

Add this line for every partition as you wish to automount and enable it for development, game partition, etc.

UUID=your_UUID /mnt/Games ext4 defaults,user,exec,rw 0 2

Mount the new fstab: sudo mount -a

When all is mounted, you should give the right permissions to every folder that you mount:
sudo chown user:user /mnt/Games


# Change keybinds like Alt Space into dconfeditor

https://docs.astral.sh/ruff/installation/
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash

mkdir -p ~/.themes
cp -r /usr/share/themes/Yaru-purple* ~/.themes/
flatpak override --user --env=GTK_THEME=Yaru-purple-dark
nano .profile
export GTK_THEME=Yaru-purple-dark



https://rickrainey.com/posts/ubuntu-dev-setup/
