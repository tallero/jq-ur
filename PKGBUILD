# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Evgeniy Alekseev
#     <arcanis at archlinux dot org>
#   Alex Chamberlain
#     <alex at alexchamberlain dot co dot uk>
#   Kars Wang
#     <jaklsy at gmail dot com>

_os="$(
  uname \
    -o)"
_arch="$(
  uname \
    -m)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot"
  _compiler="clang"
  _libcompiler="llvm-libs"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
fi
_py="python"
_pkg=jq
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=1.8.2
pkgrel=2
pkgdesc='Command-line JSON processor'
arch=(
  "aarch64"
  "arm"
  "armv6h"
  "armv7l"
  "armv8l"
  "i686"
  "mips"
  "pentium4"
  "powerpc"
  "sparc"
  'x86_64'
)
url="https://${_pkg}lang.github.io/${_pkg}"
license=('MIT')
depends=(
  "${_libc}"
  'oniguruma'
)
makedepends=(
  'autoconf'
  'automake'
  'bison'
  "${_compiler}"
  'flex'
  "${_py}"
)
_git="true"
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
_512_sum='370dfd2fffe2515f52a7c5335555a15820cf8a4906395889bf474864197705705066cc32df689272b414448b8090db3c59c3a8eb18a6bc1c7f0f036b47463d51'
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_http" ]]; then
  _http="https://${_git_service}.com"
fi
if [[ ! -v "_ns" ]]; then
  _ns="jqlang"
  _ns="themartiancompany"
fi
_url="${_http}/${_ns}/${_pkg}"
if [[ ! -v "_tag_name" ]]; then
  _tag_name="tag"
fi
if [[ ! -v "_tag" ]]; then
  if [[ "${_tag_name}" == "tag" ]]; then
    _tag="${_pkg}-${pkgver}"
  fi
fi
if [[ "${_git}" == "true" ]]; then
  _uri="git+${_url}.git#${_tag_name}=${_tag}"
fi
_tarname="${_pkg}-${pkgver}"
_src="${_tarname}::${_uri}"
source=(
  "${_src}"
)
sha512sums=(
  "${_512_sum}"
)

prepare() {
  cd \
    "${_tarname}"
  autoreconf \
    -fi
}

build() {
  local \
    _configure_opts=()
  _configure_opts+=(
    --prefix="/usr"
  )
  cd \
    "${_tarname}"
  "./configure" \
    "${_configure_opts[@]}"
  make
}

check() {
  make \
    -C \
      "${_tarname}" \
    check
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
    prefix="/usr"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install
  install \
    -vDm644 \
    "COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
