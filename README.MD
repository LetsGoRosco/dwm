# DWM Patches
Build a patched version of [DWM](http://dwm.suckless.org/) rather than editing source directly. Patches are applied to the master branch of DWM.

Clone this repo:
```sh
$ git clone https://github.com/LetsGoRosco/dwm.git ~/dwm-patched
```

Clone the original [DWM](git://git.suckless.org/git) repo:
```sh
$ git clone git://git.suckless.org/dwm ~/dwm-orig
$ cd ~/dwm-orig
```
Edit files as required in the `~/dwm-orig` folder then create a unified diff:
```sh
$ git diff > ~/dwm-patched/example.diff
```
Change directory to the `~/dwm-patched` folder and edit `PKGBUILD` to add a reference for the `.diff` file 
```
$ cd ~/dwm-patched
$ nano PKGBUILD
```
Update _patches and save `PKGBUILD`:
```
_patches=(basic.diff
          example.diff)
```
and then generate the new md5sums (using this method will provide the md5sums in the correct order):
```sh
$ makepkg -g
```
Add the result into `PKGBUILD` and run `makepkg' to build with the applied patches
```
$ makepkg
```