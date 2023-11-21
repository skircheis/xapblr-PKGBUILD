# Maintainer: Siegfried Kircheis < kircheis [dot] siegfried [at] proton [dot] me >

_pkgname=xapblr
pkgname="${_pkgname}"-git
pkgver=0.5.0.r3.gc2b67e8
pkgrel=1
pkgdesc="Locally index Tumblr blogs in a xapian database for advanced searching"
url='http://github.com/skircheis/xapblr.git'
arch=('any')
license=('MIT')
depends=(
    'python>=3.8'
    'python-pytumblr2'
    'python-xapian'
    'python-flask'
    'python-flask-assets'
    'python-dateparser'
    'python-sqlalchemy>=2.0'
    'systemd'
    'uwsgi'
    'uwsgi-plugin-python'
    'dart-sass'
)
makedepends=(
    'python-setuptools'
    'python-versioningit'
    'python-setuptools-git'
    'python-wheel'
)
optdepends=(
    'python-open-clip-torch'
    'python-humanfriendly'
)
conflicts=('xapblr')
source=('git+https://github.com/skircheis/xapblr.git')
sha256sums=('SKIP')

provides=("${_pkgname}=${pkgver}")

pkgver() {
  cd "$srcdir/$_pkgname"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
    cd "${_pkgname}"
    python -m build --wheel --no-isolation
}

prepare() {
    # Clean out old wheels etc.
    git -C "${pkgname%-git}" clean -dfx
}

package() {
    cd "${_pkgname}"
    python -m installer --destdir="$pkgdir" dist/*.whl

    mkdir -p "$pkgdir/usr/lib/systemd/user"
    install -Dm644 systemd/user/* \
        "$pkgdir/usr/lib/systemd/user"
    mkdir -p "$pkgdir/etc/uwsgi"
    install -Dm644 config/uwsgi/xapblr.ini \
        "$pkgdir/etc/uwsgi"
}
