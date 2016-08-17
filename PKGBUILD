# Maintainer: Sébastien Luttringer <seblu@seblu.net>

pkgname=wayland-protocols
pkgver=1.7
pkgrel=1
pkgdesc='Specifications of extended Wayland protocols'
arch=('any')
url='http://wayland.freedesktop.org'
license=('MIT')
makedepends=('wayland')
source=("http://wayland.freedesktop.org/releases/$pkgname-$pkgver.tar.xz")
sha1sums=('c4726694daf5feb1437f5f4f13c3b2a9b94b8118')

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
