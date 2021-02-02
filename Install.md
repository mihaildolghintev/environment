## How I install my system


### System Update

Remove unnecessary packages:

```sh
sudo dnf remove cheese gnome-boxesd orca gnome-contacts samba-client gnome-getting-started-docs nautilus-sendto gnome-characters gnome-maps gnome-photos simple-scan virtualbox-guest-additions gedit gnome-boxes
```

Add RPM Fusion:

```sh
sudo dnf install --nogpgcheck http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

Update system:

```sh
sudo dnf update --refresh
```


### Base Settings

Install VS Code:

```sh
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo dnf install code
```

Add to `/etc/sysctl.conf`:

```
fs.inotify.max_user_watches=524288
```

Install GNOME Tweaks:

```sh
sudo dnf install gnome-tweak-tool
```

### Additional Software

Install codecs:

```sh
sudo dnf install amrnb amrwb faac faad2 flac gstreamer1-libav gstreamer1-plugins-bad-freeworld gstreamer-ffmpeg gstreamer-plugins-bad-nonfree gstreamer-plugins-espeak gstreamer-plugins-ugly lame libdca libmad libmatroska x264 x265 xvidcore gstreamer1-plugins-bad-free gstreamer1-plugins-base gstreamer1-plugins-good gstreamer-plugins-bad gstreamer1-plugins-ugly-free
```

Install tools:

```sh
sudo dnf install celluloid unrar p7zip p7zip-plugins
```

Install Microsoft fonts:

```sh
sudo dnf install https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```

Install Chrome:

```sh
sudo dnf install fedora-workstation-repositories
sudo dnf config-manager --set-enabled google-chrome
sudo dnf install google-chrome-stable
```

### Development Tools

Install tools:

```sh
sudo dnf install git tig ripgrep exa
```

Install `node` and `yarn`:

```sh
sudo wget https://dl.yarnpkg.com/rpm/yarn.repo -O /etc/yum.repos.d/yarn.repo
sudo dnf install yarn nodejs
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/latest/install.sh | bash
~/Dev/environment/bin/copy-env system
```

Restart terminal

```
nvm install node
```

Install Ruby:

```sh
sudo dnf install rubygems
```

Install containers:

```sh
sudo dnf install podman buildah
```

```sh
sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
sudo dnf install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
sudo curl -L "https://github.com/docker/compose/releases/download/1.25.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

Fix [Docker bug](https://github.com/docker/for-linux/issues/665):

```sh
sudo dnf install grubby
sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"
sudo firewall-cmd --permanent --zone=trusted --add-interface=docker0
```

Install Keybase:

```sh
sudo dnf install https://prerelease.keybase.io/keybase_amd64.rpm
run_keybase
```

Remove Keybase from Autostart.

Install [Projecteur](https://github.com/jahnf/Projecteur#download).
