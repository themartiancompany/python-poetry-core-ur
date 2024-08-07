# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Caleb Maclennan <caleb@alerque.com>
# Contributor: Eli Schwartz <eschwartz@archlinux.org>
# Contributor: George Rawlinson <george@rawlinson.net.nz>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_pkgname=poetry-core
pkgname=python-poetry-core
pkgver=1.9.0
pkgrel=2
pkgdesc='Poetry PEP 517 Build Backend & Core Utilities'
arch=('any')
url="https://github.com/python-poetry/${_pkgname}"
license=('MIT')
_pydeps=(fastjsonschema
         lark-parser
         packaging)
depends=(
  "${_pydeps[@]/#/python-}"
)
makedepends=(
 "python-"{build,installer}
)
checkdepends=(
  git
  python-pytest
  python-pytest-mock
  python-setuptools
  python-tomli-w
  python-virtualenv
)
conflicts=(
  'python-poetry<1.1.0'
)
_archive="$_pkgname-$pkgver"
source=(
  "$url/archive/$pkgver/$_archive.tar.gz"
)
sha256sums=(
  '642f63ec06ba4e581b720def3a162bc23d11588fef9e9c5c57ab8a1e4f36e721'
)

build() {
  cd "$_archive"
  python -m build -wn
}

check() {
  cd \
    "$_archive"
  export \
    PYTHONPATH="$PWD/src"
  # only works inside git repositories
  pytest \
    -k \
      'not test_default_with_excluded_data and not test_default_src_with_excluded_data'
}

package() {
  cd \
    "$_archive"
  python \
    -m \
      installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -Dm0644 \
    -t "$pkgdir/usr/share/licenses/$pkgname/" \
    LICENSE
}

# vim:set sw=2 sts=-1 et:
