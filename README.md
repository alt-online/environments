# Windows/WSL2 local development environment

This repository provides recommendations for local setups needed to develop ML app, especially:

- Data analysis and modeling
- Frontend
- Backend
- IaC - Infra
- CI/CD - MLOps
- Other tools for development

## How to build dev environment

### 1. WSL setting best practice: https://learn.microsoft.com/ja-jp/windows/wsl/setup/environment

Note #1: You can install docker directly in WSL2 Ubuntu without Docker Desktop on Windows. https://docs.docker.com/engine/install/ubuntu/

- Run docker without sudo

```bash
cat /etc/group | grep docker
# add docker group if not exists
sudo groupadd docker
sudo gpasswd -a $USER docker
sudo systemctl restart docker
# reboot terminal
exit
```

Note #2: [DB installation](https://learn.microsoft.com/ja-jp/windows/wsl/setup/environment#set-up-a-database) is optional. You can install it when you need.

Note #3: [GPU acceleration](https://learn.microsoft.com/ja-jp/windows/wsl/setup/environment#set-up-gpu-acceleration-for-faster-performance) settings are optional. It depends on the specs of your PC.

Note #4: Set Ubuntu as default for Windows terminal.　https://www.howtogeek.com/720524/how-to-change-the-default-shell-in-windows-terminal/


### 2. Clone this repository and download extensions from `.vscode/extensions.json`

```bash
git clone https://github.com/alt-online/Local_Development_Environments.git
cd Local_Development_Environments
code .
```

Install the recommended extensions from the pop-up window in the lower right corner.

### 3. Please setup lastpass for security purpose: https://chrome.google.com/webstore/detail/lastpass-free-password-ma/hdokiejnpimakedhajhdlcegeplioahd?hl=ja

Credentials should be passed via lastpass.

### 4. Install asdf https://asdf-vm.com/guide/getting-started.html#_1-install-dependencies

Please install dependencies before installation by asdf. asdf internally uses pyenv for python version management. https://github.com/pyenv/pyenv/wiki#suggested-build-environment

```bash
sudo apt update; sudo apt install build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev
```

Install python/Rust/nodejs by asdf.


```bash
# list all plugins you can install
asdf plugin list all

# Add plugins
asdf plugin add python
asdf plugin add rust
asdf plugin add nodejs

# List all versions
asdf list all python
asdf list all rust
asdf list all nodejs

# Install each environment
asdf install python latest  # 3.11.4 as of now
asdf install rust latest    # 1.70.0 as of now
asdf install nodejs latest  # 20.3.1 as of now

# Set global versions
asdf global python latest
asdf global rust latest
asdf global nodejs latest

# Check versions
python -V
rustc -V
node --version
```
