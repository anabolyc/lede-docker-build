## Build Onion LEDE project in docker container

Steps are

1. Pull Onion repo from submodule
```
git submodule update
``` 
2. Prepare to build: docker build image
Run vscode task: `build: build image`
3. Prepare build inside container
Run vscode task: `build: prepare`
4. Run config script inside container
Run vscode task: `build: make autoconfig`
4. (optional) Run menuconfig inside container
Run vscode task: `build: make menuconfig`
5. Run build inside container
Run vscode task: `build: make`