# Maintainer: Sébastien Luttringer <seblu@seblu.net>

pkgname=wayland-protocols
pkgver=1.8
pkgrel=1
pkgdesc='Specifications of extended Wayland protocols'
arch=('any')
url='https://wayland.freedesktop.org/'
license=('MIT')
makedepends=('wayland')
validpgpkeys=('8307C0A224BABDA1BABD0EB9A6EEEC9E0136164A'  # Jonas Ådahl
              'A66D805F7C9329B4C5D82767CCC4F07FAC641EFF') # Daniel Stone
source=("https://wayland.freedesktop.org/releases/$pkgname-$pkgver.tar.xz"{,.sig})
sha1sums=('8a0f548d85476e4b289373c3e738e3d5a97e5a8c'
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
