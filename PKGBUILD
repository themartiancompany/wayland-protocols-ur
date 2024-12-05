# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Sébastien Luttringer <seblu@seblu.net>
# Contributor: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Contributor: Truocolo <truocolo@aol.com>

_checks="false"
_proj="wayland"
_pkg="${_proj}-protocols"
pkgname="${_pkg}"
pkgver=1.38
pkgrel=1
pkgdesc='Specifications of extended Wayland protocols'
arch=(
  'any'
)
url="https://${_proj}.freedesktop.org"
license=(
  'MIT'
)
makedepends=(
  "${_proj}"
  'meson'
  'ninja'
)
provides=(
  "lib${_pkg}=${pkgver}"
)
conflicts=(
  "lib${_pkg}"
)
validpgpkeys=(
  '8307C0A224BABDA1BABD0EB9A6EEEC9E0136164A'  # Jonas Ådahl
  'A66D805F7C9329B4C5D82767CCC4F07FAC641EFF') # Daniel Stone
_freedesktop="https://gitlab.freedesktop.org"
_http="${_freedesktop}"
_ns="${_proj}"
_url="${_http}/${_ns}/${_pkg}"
source=(
  "${_url}/-/releases/${pkgver}/downloads/${_pkg}-${pkgver}.tar.xz"{,.sig}
)
sha256sums=(
  'ff17292c05159d2b20ce6cacfe42d7e31a28198fa1429a769b03af7c38581dbe'
  'SKIP'
)

prepare() {
  local \
    _src
  cd \
    "${_pkg}-${pkgver}"
  # apply patch from the source array (should be a pacman feature)
  for _src in "${source[@]}"; do
    _src="${_src%%::*}"
    _src="${_src##*/}"
    [[ "${src}" = *.patch ]] || continue
    echo "Applying patch $src..."
    patch \
      -Np1 < \
      "../${src}"
  done
}

build() {
  local \
    _meson_opts=()
  _meson_opts+=(
    -D tests="${_checks}"
  )
  meson \
    build \
      "${_pkg}-${pkgver}" \
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
    "${pkgdir}/usr/share/licenses/${_pkg}" \
    -m 644 \
    "${_pkg}-${pkgver}/COPYING"
}

# vim:set sw=2 sts=-1 et:
