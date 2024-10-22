# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: George Rawlinson <george@rawlinson.net.nz>

_git="true"
_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _git="false"
fi
_proj="jaraco"
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_proj="poetry"
_pkg="${_proj}-core"
_pkgname="${_pkg}"
pkgname="${_py}-${_pkg}"
pkgver=1.9.0
pkgrel=2
pkgdesc='Poetry PEP 517 Build Backend & Core Utilities'
arch=(
  'any'
)
url="https://github.com/python-poetry/${_pkgname}"
license=(
  'MIT'
)
_pydeps=(
  fastjsonschema
  lark-parser
  packaging
)
depends=(
  "${_py}>=${_pymajver}"
  "${_pydeps[@]/#/python-}"
)
makedepends=(
 "${_py}-"{build,installer}
)
checkdepends=(
  git
  "${_py}-pytest"
  "${_py}-pytest-mock"
  "${_py}-setuptools"
  "${_py}-tomli-w"
  "${_py}-virtualenv"
)
conflicts=(
  "${_py}-${_proj}<1.1.0"
)
_archive="${_pkg}-${pkgver}"
source=(
  "${url}/archive/${pkgver}/${_archive}.tar.gz"
)
sha256sums=(
  '642f63ec06ba4e581b720def3a162bc23d11588fef9e9c5c57ab8a1e4f36e721'
)

build() {
  cd \
    "${_archive}"
  "${_py}" \
    -m \
      build \
    -wn
}

check() {
  cd \
    "${_archive}"
  export \
    PYTHONPATH="$PWD/src"
  # only works inside git repositories
  pytest \
    -k \
      'not test_default_with_excluded_data and not test_default_src_with_excluded_data'
}

package() {
  cd \
    "${_archive}"
  "${_py}" \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm0644 \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/" \
    LICENSE
}

# vim:set sw=2 sts=-1 et:
