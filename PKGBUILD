pkgname=openconnect-multiplecerts
_pkgname=openconnect
pkgver=8.10.r753.gb0e53bfa
pkgrel=1
pkgdesc="Open client for Cisco AnyConnect VPN"
arch=('i686' 'x86_64')
license=('GPL')
url="http://www.infradead.org/openconnect.html"
depends=('libproxy' 'vpnc' 'pcsclite' 'trousers' 'stoken' 'oath-toolkit')
makedepends=('intltool' 'python' 'git')
options=('!emptydirs')
provides=($_pkgname 'libopenconnect.so')
conflicts=($_pkgname)
source=("$pkgname::git+https://github.com/Aerion/openconnect-wip.git")
md5sums=('SKIP')

build() {
  cd $pkgname
  ./autogen.sh
  PYTHON=/usr/bin/python ./configure --prefix=/usr \
      --sbindir=/usr/bin \
      --libexecdir=/usr/lib \
      --disable-static \
      --without-gnutls \
      --with-vpnc-script=/etc/vpnc/vpnc-script
  # Fight unused direct deps
  sed -i -e "s/ -shared / $LDFLAGS\0 /g" libtool
  make V=0
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}
