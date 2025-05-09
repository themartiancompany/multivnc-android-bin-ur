# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Truocolo <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer: Pellegrino Prevete (dvorak) <pellegrinoprevete@gmail.com>
# Maintainer: Pellegrino Prevete (dvorak) <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

_fdroid="true"
_github="false"
_system_install="false"
_user_install="true"
if [[ "${_system_install}" == "true" ]]; then
  _install_type="system"
elif [[ "${_user_install}" == "true" ]]; then
  _install_type="user"
fi
_offline="false"
_git="false"
_proj="hip"
_pkg=multivnc
_variant="android"
_pkgbase="${_pkg}-android"
_pkgname="${_pkgbase}"
_app_domain="coboltforge"
_app_subdomain="dontmind"
_app_id="com.${_app_domain}.${_app_subdomain}.${_pkg}"
_Pkg="MultiVNC"
pkgname=(
  "${_pkgname}-bin"
)
pkgver=2.1.8
# _commit="e117ccae32d5a7d75479b61f034000122fe9fa24"
_fdroid_pkgrel=101
pkgrel=1
if [[ "${_fdroid}" == "true" ]]; then
  pkgrel="${_fdroid_pkgrel}"
fi
_pkgdesc=(
  "Open-source VNC viewer that aims"
  "to be easy to use and fast."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'arm'
  'aarch64'
  'x86_64'
  'i686'
)
_arch="$( \
  uname \
    -m)"
_aarch="${_arch}"
if [[ "${_arch}" == "armv7l" ]]; then
  _aarch="armeabi-v7a"
elif [[ "${_arch}" == "aarch64" ]]; then
  _aarch="arm64-v8a"
fi
url="${_pkgname}.dev"
license=(
  'GPL3'
)
depends=(
  # "${_pkg}"
)
_os="$( \
  uname \
    -o)"
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  depends+=(
    'inteppacman'
  )
optdepends=(
)
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  optdepends+=(
  )
makedepends=(
  'coreutils'
)
checkdepends=(
)
provides=(
  "${_pkgname}=${pkgver}"
  "${_pkg}=${pkgver}"
)
conflicts=(
  "${_pkgname}"
)
source=()
sha256sums=()
_fdroid_url="https://f-droid.org/repo"
_http="https://github.com"
_ns="${_pkg}"
_github_url="${_http}/${_ns}/${_pkgname}"
# _tag="${pkgrel}"
_tag="${pkgver}"
_tag_name="pkgrel"
# _tag_name="pkgver"
_tarname="${_pkgname}-${pkgver}-${pkgrel}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
source=()
sha256sums=()
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}"
  _sum="SKIP"
elif [[ "${_git}" == false ]]; then
  if [[ "${_fdroid}" == "true" ]]; then
    _url="${_fdroid_url}"
    if [[ "${_tag_name}" == 'pkgrel' ]]; then
      _src="${_tarname}.apk::${_url}/${_app_id}_${pkgrel}.apk"
      _sig="${_tarname}.apk.sig::${_url}/${_app_id}_${pkgrel}.apk.asc"
      source+=(
        "${_sig}"
      )
      sha256sums+=(
        "SKIP"
      )
      _sum="6c3fb340740c9b3443b190770615feea6e97e9f52b83f64ab770f4becf0d228f"
    fi
  elif [[ "${_github}" == "true" ]]; then
    _url="${_github_url}"
    if [[ "${_tag_name}" == "pkgver" ]]; then
      _dl_name="${_pkgname}-app_v${pkgver}+github.debug.apk"
      _src="${_tarname}.apk::${_url}/releases/download/v${_tag}/${_dl_name}"
      _sum="72c8d3cf7cb12d8c550a6b2750bd00bc99ad084c70f8ff0d2ffa9189e685ce4f"
    elif [[ "${_tag_name}" == "commit" ]]; then
      _src="${_tarname}.zip::${_url}/archive/${_commit}.zip"
      _sum="dacf4a05e8dab38c49034e5d58deb477c36d005fe81324cf7973ba5487d87eb7"
    fi
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
noextract=(
  "${_src}"
)
validgpgkeys=(
  # F-droid binary releases
  "37D2C98789D8311948394E3E41E7044E1DBA2E89"
)

package() {
  local \
    _dest_dir \
    _dest \
    _extra_libs=() \
    _manifest \
    _manifests=() \
    _lib
  _dest_dir="/usr/bin"
  _dest="${_pkgname}.apk"
  if [[ "${_os}" == "Android" ]]; then
    if [[ "${_install_type}" == "system" ]]; then
      _dest_dir="/system/app/${_Pkg}"
    elif [[ "${_install_type}" == "user" ]]; then
      _dest_dir="/data/app/${_app_id}"
    fi
    _dest="base.apk"
  fi
  install \
    -dm755 \
    "${pkgdir}${_dest_dir}"
  install \
    -Dm644 \
    "${srcdir}/${_tarname}.apk" \
    "${pkgdir}${_dest_dir}/${_dest}"
}

# vim: ft=sh syn=sh et
