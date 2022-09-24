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
#### pyenv

install
```
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```

set variable and initialize command to .bashrc
```
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
``` 

check current version
```
pyenv versions
```

install specific version
```
pyenv install <version>
```

set specific version as default
```
pyenv global <version>
```

show list of avairable versions
```
pyenv install -l
```



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

Before this step, if you use ml on wsl, you need to install nvidia geforce driver for windows.

Install cuda tool kit
Before install, check software requirements for ml library.

If you have previous installation, remove it first. 
```
$ sudo apt --purge remove "cuda*"
$ sudo apt --purge remove "nvidia*"
$ sudo rm /etc/apt/sources.list.d/cuda*
$ sudo rm -rf /usr/local/cuda*
$ sudo apt-get autoremove && sudo apt-get autoclean
```

Install

```
$ wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
$ sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
$ wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda-repo-wsl-ubuntu-11-7-local_11.7.1-1_amd64.deb
$ sudo dpkg -i cuda-repo-wsl-ubuntu-11-7-local_11.7.1-1_amd64.deb
$ sudo cp /var/cuda-repo-wsl-ubuntu-11-7-local/cuda-*-keyring.gpg /usr/share/keyrings/
$ sudo apt-get update
$ sudo apt-get -y install cuda
```

Check the result with nvidia-smi command  
If successfully installed, nvidia video-card is shown in the result.

```
$ nvidia-smi
```

Result sample
* Driver and CUDA Version are refered on the windows side driver.
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.65.01    Driver Version: 516.94       CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:01:00.0  On |                  N/A |
|  0%   46C    P8    12W / 290W |    476MiB /  8192MiB |      3%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```


Install cuDNN (nvidia account is required to download files)

uninstall existing library
```
$ dpkg -l | grep cudnn
$ sudo dpkg --remove libcudnn8
```


get library from archive site  
https://developer.nvidia.com/rdp/cudnn-archive

cuDNN Runtime Library for Ubuntu20.04 x86_64 (Deb)

```
$ sudo dpkg -i cudnn-local-repo-ubuntu2004-8.5.0.96_1.0-1_amd64.deb
$ sudo cp /var/cudnn-local-repo-ubuntu2004-8.5.0.96/cudnn-local-0579404E-keyring.gpg /usr/share/keyrings/

```

Add path description in .bashrc
```
LD_LIBRARY_PATH="$LD_LIBRARY_PATH":/usr/local/cuda-11/lib64
PATH="$PATH":/usr/local/cuda/bin
```

reload setting
```
source ~/.bashrc
```


Install miniconda with pyenv and set as global

```
$ pyenv install miniconda3-latest
$ pyenv global miniconda3-latest
$ conda init bash <- set your shell script type
```

### tensorflow setup

#### Before start

create tf environment.  
deactivate and activate commands are as followings.

```
$ conda create --name tf python=3.9
$ conda deactivate
$ conda activate tf
```

Install CUDA and cuDNN with conda.
```
$ conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0
```

For your convenience, set following file. If tf environment is activated, the following files is automatically activated.
```
$ mkdir -p $CONDA_PREFIX/etc/conda/activate.d
$ echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/' > $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
```

#### Install tf

upgrade pip
```
pip install --upgrade pip
```

install tf
```
pip install tensorflow
```







