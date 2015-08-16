# $Id$
# Maintainer: Allan McRae <allan@archlinux.org>

pkgname=libmpc09
pkgver=0.9
pkgrel=1
pkgdesc="Library for the arithmetic of complex numbers with arbitrarily high precision"
arch=('i686' 'x86_64')
url="http://www.multiprecision.org/"
license=('LGPL')
depends=('mpfr>=3.0.0')
provides=( 'libmpc=0.9' )
conflicts=( 'libmpc<1.0' )
options=('!libtool')

source=(http://www.multiprecision.org/mpc/download/mpc-${pkgver/_/-}.tar.gz
        libmpc-0.9-configure_cflags_egrep_issue.patch
        automake-1.12.patch)
md5sums=('0d6acab8d214bd7d1fbbc593e83dd00d'
         '35d5bb02dc6c1153e581b7c34a738a08'
         'd010b28146aa2f457df6ce528b2d711b')

build() {
  cd "${srcdir}/mpc-${pkgver}"

  # http://lists.gforge.inria.fr/pipermail/mpc-discuss/2011-February/000805.html
  patch -Np1 -i $srcdir/libmpc-0.9-configure_cflags_egrep_issue.patch
  # 83eae7337dc46e3c89ec815f44620b9bc028fc8a
  patch -Np1 -i $srcdir/automake-1.12.patch
  autoreconf --install
  
  ./configure --prefix=/usr
  make
}

check() {
  cd "${srcdir}/mpc-${pkgver}"
  make check
}

package() {
  cd "${srcdir}/mpc-${pkgver}"
  make DESTDIR="${pkgdir}" install
  rm -rf ${pkgdir}/usr/{share,include} ${pkgdir}/usr/lib/libmpc.{a,so}
}

