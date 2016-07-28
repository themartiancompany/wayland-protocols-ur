# Maintainer: Sébastien Luttringer <seblu@seblu.net>

pkgname=wayland-protocols
pkgver=1.5
pkgrel=1
pkgdesc='Specifications of extended Wayland protocols'
arch=('any')
url='http://wayland.freedesktop.org'
license=('MIT')
makedepends=('wayland')
source=("http://wayland.freedesktop.org/releases/$pkgname-$pkgver.tar.xz")
sha1sums=('fb1df343635407b4082ff73cca7005f2b780b518')

build() {
  cd $pkgname-$pkgver

  ./configure --prefix=/usr
  make
}

package() {
  cd $pkgname-$pkgver

  make DESTDIR="$pkgdir" install
  install -Dm 644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
}

# vim:set ts=2 sw=2 et:
