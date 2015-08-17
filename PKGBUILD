# 2013-05-30
# Maintainer: Dreieck
# Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=xaos-gtk2
_pkgname=xaos
pkgver=3.5
pkgrel=2
pkgdesc="A fast portable real-time interactive fractal zoomer. With gtk2-, X11- and aa-interfaces, and other build options also enabled."
arch=('i686' 'x86_64')
url="http://sourceforge.net/projects/xaos/"
license=('GPL')
depends=('gsl' 'libpng' 'aalib' 'gtk2')
provides=("${_pkgname}=${pkgver}")
conflicts=("${_pkgname}")
options=('!makeflags')
install=xaos.install
source=(http://downloads.sourceforge.net/sourceforge/xaos/${_pkgname}-${pkgver}.tar.gz \
        xaos-3.5-libpng15.patch xaos-3.5-build-fix-i686.patch)
sha1sums=('6d16a58187fba7276e6bd0547cc2fd6bb073b801'
          '6c51cb2ee1c5f28973680ffc3a040c2cea65fd33'
          'd2ea8f0460c79c47fb289a4c2f87fe5c44057f9d')

prepare() {
  cd ${_pkgname}-${pkgver}
  patch -p0 -i ../xaos-3.5-libpng15.patch
  if [[ $CARCH == "i686" ]]; then
    patch -p1 -i ../xaos-3.5-build-fix-i686.patch
  fi
}

build() {
  cd ${_pkgname}-${pkgver}
  ./configure \
    --prefix=/usr \
    --with-gsl \
    --with-aa-driver \
    --with-x \
    --with-gtk-driver \
    --with-x11-driver \
    --with-sffe \
    --with-png \
    --with-pthread \
    --with-mitshm \
    --with-long-double
  make || return "$?"
}

package() {
  cd ${_pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" install
}
