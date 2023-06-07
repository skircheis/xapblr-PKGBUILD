# Maintainer: Siegfried Kircheis < kircheis [dot] siegfried [at] proton [dot] me >

_pkgname=xapblr
pkgname="${_pkgname}"-git
pkgver=0.1.0.r24.g737a717
pkgrel=1
pkgdesc="Locally index Tumblr blogs in a xapian database for advanced searching"
url='http://github.com/skircheis/xapblr.git'
arch=('any')
license=('MIT')
depends=(
    'python>=3.8'
    'python-pytumblr'
    'python-lark-parser'
    'python-xapian'
    'python-flask'
    'python-flask-assets'
    'systemd'
    'uwsgi'
    'uwsgi-plugin-python'
)
makedepends=(
    'python-setuptools'
    'python-wheel'
)
conflicts=('xapblr')
source=('git+https://github.com/skircheis/xapblr.git')
sha256sums=(SKIP)

provides=("${pkgname}")

pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    cd "${_pkgname}"
    python -m build --wheel --no-isolation
}

package() {
    cd "${_pkgname}"
    python -m installer --destdir="$pkgdir" dist/*.whl

    mkdir -p "$pkgdir/usr/lib/systemd/user"
    install -Dm644 systemd/user/* \
        "$pkgdir/usr/lib/systemd/user"
}
