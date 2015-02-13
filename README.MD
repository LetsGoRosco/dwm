# DWM Patches
Clone the original repo:
```sh
$ git clone git://git.suckless.org/dwm/ dwm-orig
```
Edit files as required then create a unified diff:
```sh
$ git diff > example.diff
```
Copy the `.diff` file to the patch repo folder and add a reference to `PKBGUILD`
```
_patches=(basic.diff
          example.diff)
```
and then generate the new md5sums:
```sh
$ makepkg -g
```
Add the result into `PKGBUILD` and run `makepkg' to build with the applied patches
```
$ makepkg
```
