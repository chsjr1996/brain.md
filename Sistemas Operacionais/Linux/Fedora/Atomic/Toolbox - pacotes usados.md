#fedora #revisar 

## Oficiais

```
sudo dnf5 install node npm nvim zsh tmux php composer
```

## Externos

**Lazygit**
```shell
sudo dnf copr enable atim/lazygit -y
```
---
```shell
sudo dnf install lazygit
```

**NVM**
```shell
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```
---
```shell
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```
