# about

 Notes to create development environment from scratch.


## tools

* vscode
  * editor to write software etc.
* wsl
  * Base development environment.
  * Linux on wsl can be used for development in mose case. So I create most of the development environment in the linux on wsl.
  * install
    * check distribution
      * wsl --list --online
    * install
      * wsl --install -d ${DistroName}


## settings

### wsl

Create setting file at `C:\Users\<yourUserName>\.wslconfig` 

Setting smaple  
Wsl set 50% of the total memory as default.

```
[wsl2]
memory=32GB 
```
