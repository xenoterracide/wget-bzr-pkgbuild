# AUR Maintainer: Caleb Cushing <xenoterracide@gmail.com>
# Arch Maintainer: Allan McRae <allan@archlinux.org>
# Contributor: Judd Vinet <jvinet@zeroflux.org>

pkgname='wget-bzr'
pkgver='20100611'
pkgrel=1
pkgdesc="A network utility to retrieve files from the Web"
arch=('i686' 'x86_64')
url="http://www.gnu.org/software/wget/wget.html"
license=('GPL3')
groups=('base')
depends=('glibc' 'openssl')
provides='wget'
optdepends=('ca-certificates: HTTPS downloads')
backup=('etc/wgetrc')
install=wget.install
source=()
md5sums=()

build() {
  if [ -d ${srcdir}/${pkgname} ]; then
    cd ${srcdir}/${pkgname}
	make clean
	bzr update
  else
    cd ${srcdir}
    bzr branch http://bzr.savannah.gnu.org/r/wget/trunk $pkgname
    cd ${srcdir}/${pkgname}
    ./bootstrap
  fi

  ./configure --prefix=/usr --sysconfdir=/etc
  make || return 1
}

package() {
  cd ${srcdir}/$pkgname-$pkgver
  make DESTDIR=${pkgdir} install || return 1
  make check || return 1
}
