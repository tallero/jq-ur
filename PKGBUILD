# Maintainer: Evgeniy Alekseev <arcanis at archlinux dot org>
# Contributor: Alex Chamberlain <alex at alexchamberlain dot co dot uk>
# Contributor: Kars Wang <jaklsy at gmail dot com>

pkgname=jq
pkgver=1.8.1
pkgrel=3
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
    git cherry-pick -n 3985b80ce50bd75c6eb5a97cb3348c3f835ca8e0 # Fix GHSA-gf4g-95wj-4q4r
    git cherry-pick -n e47e56d226519635768e6aab2f38f0ab037c09e5 # Fix CVE-2026-32316
    git cherry-pick -n fdf8ef0f0810e3d365cdd5160de43db46f57ed03 # Fix CVE-2026-39956
    git cherry-pick -n -Xours 6374ae0bcdfe33a18eb0ae6db28493b1f34a0a5b # Fix CVE-2026-33948
    git cherry-pick -n 0c7d133c3c7e37c00b6d46b658a02244fdd3c784 # Fix CVE-2026-40164
    git cherry-pick -n 2f09060afab23fe9390cce7cb860b10416e1bf5f # Fix CVE-2026-39979
    git cherry-pick -n -Xours fb59f1491058d58bdc3e8dd28f1773d1ac690a1f # Fix CVE-2026-33947
    autoreconf -fi
}

build() {
    cd "$pkgname"
    ./configure --prefix=/usr
    make
}

check() {
    make -C "$pkgname" check
}

package() {
    cd "$pkgname"
    make DESTDIR="${pkgdir}" prefix=/usr install
    install -Dm644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}
