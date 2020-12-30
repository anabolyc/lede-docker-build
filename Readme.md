## Build Onion LEDE project in docker container

### Why

I need to [cross compile some applications for Onion Omega](https://docs.onion.io/omega2-docs/cross-compiling.html). [Snapclient](https://github.com/badaix/snapcast) to be more specific. To obtain latest toolchain it is always nice to build it yourself.

To complete below steps vscode is used on any linux machine. Necessary scripts are added to vscode tasks file, to call them simply press F1 and type in 'Tasks'

### Steps

1. Pull [Onion repo](https://github.com/onioniot/source) from submodule using this command
```
git submodule update
``` 
2. Prepare to build: docker build image:
Run vscode task: `build: build image`
3. Prepare build inside container:
Run vscode task: `build: prepare`
4. Run config script inside container:
Run vscode task: `build: make autoconfig`
4. (optional) Run menuconfig inside container:
Run vscode task: `build: make menuconfig`
5. Run build inside container:
Run vscode task: `build: make`

Throughout all above steps local `source` folder is mounted into container and all commands are executed inside that container. Therefore after each of those steps output will be sitting plain in `source` folder.

When build completes you'll find artifacts in `./source/staging_dir` folder:
```
$ ls -al source/staging_dir/
total 28
drwxr-xr-x  7 dronische dronische 4096 Dec 30 15:30 .
drwxr-xr-x 17 dronische dronische 4096 Dec 30 13:46 ..
drwxr-xr-x 13 dronische dronische 4096 Dec 30 12:57 host
drwxr-xr-x  5 root      root      4096 Dec 30 15:19 hostpkg
drwxr-xr-x  3 root      root      4096 Dec 30 15:30 packages
drwxr-xr-x 11 root      root      4096 Dec 30 12:57 target-mipsel_24kc_musl
drwxr-xr-x 11 root      root      4096 Dec 30 12:12 toolchain-mipsel_24kc_gcc-7.3.0_musl
```  

### Notes

I didn't use [this image](https://hub.docker.com/r/onion/omega2-source) suggested by Onion team, since it has sources included already. Instead i want to mount them from work folder, hence another image to serve that purpose.

### Links
- [OnionIoT/source](https://github.com/onioniot/source)
- [Cross-Compiling for the Omega](https://docs.onion.io/omega2-docs/cross-compiling.html)