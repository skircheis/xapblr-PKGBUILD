# Maintainer: Siegfried Kircheis < kircheis [dot] siegfried [at] proton [dot] me >

_pkgname=xapblr
pkgname="${_pkgname}"-git
pkgver=0.1.1.r6.g547252b
pkgrel=1
pkgdesc="Locally index Tumblr blogs in a xapian database for advanced searching"
url='http://github.com/skircheis/xapblr.git'
arch=('any')
license=('MIT')
depends=(
    'python>=3.8'
    'python-pytumblr'
    'python-xapian'
    'python-flask'
    'python-flask-assets'
    'python-dateparser'
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
