pkgname=dwm
pkgver=6.0.r42.g35db6d8
pkgrel=1
pkgdesc="A dynamic window manager for X"
url="http://dwm.suckless.org"
arch=('i686' 'x86_64')
license=('MIT')
options=(zipman)
depends=('libx11' 'libxinerama')
install=dwm.install
source=(git://git.suckless.org/dwm#branch=master)
_patches=(00-propergaps-dwm-6.1.diff
	        01-pertag-dwm-6.1.diff
          02-attachabove-dwm-6.1.diff
          03-config-dwm-6.1.diff)
source=(${source[@]} ${_patches[@]})

build() {
  cd $srcdir/$pkgname


  for p in "${_patches[@]}"; do
    echo "=> $p"
    patch < ../$p || return 1
  done

  sed -i 's/CPPFLAGS =/CPPFLAGS +=/g' config.mk
  sed -i 's/^CFLAGS = -g/#CFLAGS += -g/g' config.mk
  sed -i 's/^#CFLAGS = -std/CFLAGS += -std/g' config.mk
  sed -i 's/^LDFLAGS = -g/#LDFLAGS += -g/g' config.mk
  sed -i 's/^#LDFLAGS = -s/LDFLAGS += -s/g' config.mk
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

pkgver() {
  cd "$srcdir/$pkgname"
  ( set -o pipefail
    git describe --long --tags 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}

package() {
  cd $srcdir/$pkgname
  make PREFIX=/usr DESTDIR=$pkgdir install
}

md5sums=('SKIP'
         '3c64aea264a013494085887dca6c79dc'
         '10a9dea769872609ed186f4f1f3869fb'
         'fbdbaefdb657d4ebb42069b7146492a6'
	       '0cf1eec0a0bb87b5984874930799cd90')
