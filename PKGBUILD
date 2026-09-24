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
# Contributors:
#   Gore Liu
#     <goreliu@126.com>

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
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_docs" ]]; then
  _docs="true"
  if [[ "${_os}" == "Msys" ]]; then
    _docs="false"
  fi
fi
_py="python"
_pkg=jq
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=1.8.2
_commit="34f7186b86743a083a589741b6cea95293524108"
pkgrel=26
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
license=(
  'MIT'
)
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
if [[ "${_os}" == "Msys" ]]; then
  makedepends+=(
    "libtool"
  )
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ "${_os}" == "Msys" ]]; then
  _git="false"
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
_github_release_sum='71b8d6e8f5fe81f6c6d0d110e3892251f6ce76ed095abd315e26e6e1193af3af'
_github_gz_sum="860f5609e96149f21371dd3317764a2b792dee9b6eddb0e5c8efce8fa0f9a9fd"
_github_zip_sum="6d76dfe18b1ff4de14dcffb5e5dde1ba9aca3e58c126dd9e590fe48831839dcb"
_512_sum='370dfd2fffe2515f52a7c5335555a15820cf8a4906395889bf474864197705705066cc32df689272b414448b8090db3c59c3a8eb18a6bc1c7f0f036b47463d51'
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_http" ]]; then
  _http="https://${_git_service}.com"
fi
if [[ ! -v "_ns" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _ns="jqlang"
  elif [[ "${_git}" == "false" ]]; then
    _ns="themartiancompany"
    _ns="jqlang"
  fi
fi
_url="${_http}/${_ns}/${_pkg}"
if [[ ! -v "_tag_name" ]]; then
  if [[ "${_ns}" == "jqlang" ]]; then
    _tag_name="tag"
  elif [[ "${_ns}" == "themartiancompany" ]]; then
    _tag_name="commit"
  fi
fi
if [[ ! -v "_tag" ]]; then
  if [[ "${_tag_name}" == "tag" ]]; then
    _tag="${_pkg}-${pkgver}"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _tag="${_commit}"
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      _archive_format="zip"
      _archive_format="tar.gz"
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_tarname="${_pkg}-${_tag}"
if [[ "${_tag_name}" == "tag" ]]; then
  _tarname="${_pkg}-${pkgver}"
fi
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_git}" == "true" ]]; then
  _uri="git+${_url}#${_tag_name}=${_tag}"
  _src="${_tarname}::${_uri}"
  if [[ "${_tag_name}" == "commit" ]]; then
    _sum="SKIP"
  elif [[ "${_tag_name}" == "tag" ]]; then
    _sum="SKIP"
  fi
elif [[ "${_git}" == "false" ]]; then
  if [[ "${_ns}" == "jqlang" ]]; then
    _sum="${_github_release_sum}"
    _uri="${_url}/releases/download/${_tarname}/${_tarname}.${_archive_format}"
  else
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        if [[ "${_archive_format}" == "zip" ]]; then
          _sum="${_github_zip_sum}"
        elif [[ "${_archive_format}" == "tar.gz" ]]; then
          _sum="${_github_gz_sum}"
        fi
      fi
    fi
  fi
  _src="${_tarfile}::${_uri}"
fi

source=(
  "${_src}"
)
if [[ "${_ns}" == "jqlang" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_tag_name}" == "tag" ]]; then
      sha512sums=(
        "${_512_sum}"
      )
    fi
  fi
fi
sha256sums=(
  "${_sum}"
)

_usr_get() {
  local \
    _bin
  _bin="$(
    dirname \
      "$(command \
           -v \
           "env")")"
  dirname \
    "${_bin}"
}

prepare() {
  local \
    _index \
    _pattern \
    _patterns=() \
    _repl \
    _replacements=() \
    _usr
  _patterns+=(
    "/bin/sh"
    "^#!/bin/sh$"
    "^#! /bin/sh$"
  )
  _replacements+=(
    "${_usr}/bin/sh"
    "#!${_usr}/bin/sh"
    "#! ${_usr}/bin/sh"
  )
  _usr="$(
    _usr_get)"
  cd \
    "${_tarname}"
  if [[ "${_os}" == "Android" ]]; then
    export \
      CONFIG_SHELL="${_usr}/bin/bash"
  fi
  if [[ "${_os}" == "Msys" ]]; then
    echo \
      "echo ${pkgver}" > \
      "scripts/version"
    autoreconf \
      -fiv || \
    true
    _msg=(
      "Running autoreconf a second time."
    )
    echo \
      "${_msg[*]}"
    autoreconf \
      -fiv
  else
    autoreconf \
      -fiv 
  fi
  if [[ "${_os}" == "Android" ]]; then
    _index=0
    for _pattern in "${_patterns[@]}"; do
      _repl="${_replacements["${_index}"]}"
      sed \
        "s%${_pattern}%${_repl}%g" \
        -i \
        "${PWD}/configure"
      _index="$((
        _index + 1))"
    done
  fi
}

build() {
  local \
    _configure_opts=() \
    _usr
  _usr="$(
    _usr_get)"
  _configure_opts+=(
    --prefix="/usr"
  )
  if [[ "${_docs}" == "false" ]]; then
    _configure_opts+=(
      --disable-docs
    )
  fi
  if [[ "${_os}" == "Msys" ]]; then
    _configure_opts+=(
      # --prefix="${MINGW_PREFIX}"
      --build="${MINGW_CHOST}"
      --host="${MINGW_CHOST}"
      --target="${MINGW_CHOST}"
      --enable-static
      --enable-shared
    )
  fi
  if [[ "${_os}" == "Android" ]]; then
    _configure_opts+=(
      CONFIG_SHELL="${_usr}/bin/bash"
    )
  fi
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
