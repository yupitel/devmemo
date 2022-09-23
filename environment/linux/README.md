# About

 Notes to create development environment in the linux.

## tools

### git

Set git config at ~/.gitconfig folder

```
[user]
        name = "User Name"
        email = mail@domain.com
```

### docker

Set config for docker


### aws


### ssh


### python

Use pyenv to control python version for each projects.


### node.js

Use nvm to control node.js version


### vscode extensions

Vs Code is installed in the windows.  
But with Remote - WSL extension, I use vscode in the wsl linux.

* Remote - WSL
  * Used to use `code` command in the wsl.
  * With following command, you can use vs code in the wsl.
    * `code ${folder name}`
* Remote - Containers
  * Some times, I use docker container to avoid library conflict in OS.
    * e.g : create machine learning env / use specific database version etc. 
  * After start container in docker, attach vscode to running container.
* Vim
  * In the past days, I use vim editor and several plugins for long times. But after this extension is released, I use vscode to write code in the most case.


## machine learning set up

Install cuda tool kit

```
$ wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
$ sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
$ wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda-repo-wsl-ubuntu-11-7-local_11.7.1-1_amd64.deb
$ sudo dpkg -i cuda-repo-wsl-ubuntu-11-7-local_11.7.1-1_amd64.deb
$ sudo cp /var/cuda-repo-wsl-ubuntu-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/
$ sudo apt-get update
$ sudo apt-get -y install cuda
```




