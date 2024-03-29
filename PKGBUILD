# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Sébastien Luttringer <seblu@seblu.net>
# Contributor: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Contributor: Truocolo <truocolo@aol.com>

_checks="false"
pkgname=wayland-protocols
pkgver=1.32
pkgrel=1
pkgdesc='Specifications of extended Wayland protocols'
arch=('any')
url='https://wayland.freedesktop.org/'
license=('MIT')
makedepends=('wayland' 'meson' 'ninja')
validpgpkeys=('8307C0A224BABDA1BABD0EB9A6EEEC9E0136164A'  # Jonas Ådahl
              'A66D805F7C9329B4C5D82767CCC4F07FAC641EFF') # Daniel Stone
source=("https://gitlab.freedesktop.org/wayland/$pkgname/-/releases/$pkgver/downloads/$pkgname-$pkgver.tar.xz"{,.sig})
sha256sums=('7459799d340c8296b695ef857c07ddef24c5a09b09ab6a74f7b92640d2b1ba11'
            'SKIP')

prepare() {
  cd $pkgname-$pkgver
  # apply patch from the source array (should be a pacman feature)
  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    echo "Applying patch $src..."
    patch -Np1 < "../$src"
  done
}

build() {
  local \
    _meson_opts=()
  _meson_opts=(
    -D tests="${_checks}"
  )
  meson \
    build \
      $pkgname-$pkgver \
      --buildtype=release \
      --prefix=/usr \
      "${_meson_opts[@]}"
  ninja \
    -C \
      build
}

check() {
  ninja \
    -C \
      build \
    test
}

package() {
  DESTDIR="$pkgdir" \
    ninja \
    -C \
      build \
    install
  set -x
  install \
    -Dt \
    "$pkgdir/usr/share/licenses/$pkgname" \
    -m 644 \
    "$pkgname-$pkgver/COPYING"
}

# vim:set sw=2 sts=-1 et:
