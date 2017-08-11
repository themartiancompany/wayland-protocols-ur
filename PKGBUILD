# Maintainer: Sébastien Luttringer <seblu@seblu.net>

pkgname=wayland-protocols
pkgver=1.10
pkgrel=1
pkgdesc='Specifications of extended Wayland protocols'
arch=('any')
url='https://wayland.freedesktop.org/'
license=('MIT')
makedepends=('wayland')
validpgpkeys=('8307C0A224BABDA1BABD0EB9A6EEEC9E0136164A'  # Jonas Ådahl
              'A66D805F7C9329B4C5D82767CCC4F07FAC641EFF') # Daniel Stone
source=("https://wayland.freedesktop.org/releases/$pkgname-$pkgver.tar.xz"{,.sig})
sha1sums=('4f1322f03fa8b2e6467b8f71471f53eff82728a4'
          'SKIP')

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
