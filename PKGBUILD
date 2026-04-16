# Maintainer: Evgeniy Alekseev <arcanis at archlinux dot org>
# Contributor: Alex Chamberlain <alex at alexchamberlain dot co dot uk>
# Contributor: Kars Wang <jaklsy at gmail dot com>

pkgname=jq
pkgver=1.8.1
pkgrel=2
pkgdesc='Command-line JSON processor'
arch=('x86_64')
url='https://jqlang.github.io/jq/'
license=('MIT')
depends=('glibc' 'oniguruma')
makedepends=('autoconf' 'automake' 'bison' 'flex' 'git' 'python')
source=("git+https://github.com/jqlang/jq.git#tag=jq-${pkgver}")
sha512sums=('756a136b20991bbe24ab8b1b92511b877502697146dd1c492d388ee4bf3f6c968e91e6f45078519575f57407f091e171457fd16f6794002660b493766efa3725')

prepare() {
    cd "$pkgname"
    # Backport the CVE-2026-33947 fix.
    git cherry-pick -n -Xtheirs fb59f1491058d58bdc3e8dd28f1773d1ac690a1f
    autoreconf -fi
}

build() {
    cd "$pkgname"
    ./configure --prefix=/usr
    make
}

package() {
    cd "$pkgname"
    make DESTDIR="${pkgdir}" prefix=/usr install
    install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
