# Maintainer: Brian Bidulock <bidulock@openss7.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgname=upower-git
_pkgname=upower
pkgver=0.99.11.r1.gc742d55
pkgrel=1
pkgdesc="Abstraction for enumerating power devices, listening to device events and querying history and statistics"
arch=('i686' 'x86_64')
url="http://upower.freedesktop.org"
license=('GPL')
depends=('systemd' 'libusb' 'dbus-glib' 'libimobiledevice' 'libgudev')
makedepends=('intltool' 'docbook-xsl' 'gobject-introspection' 'python2' 'gtk-doc' 'git')
provides=("$_pkgname=${pkgver%%.r*}-${pkgrel}")
conflicts=("$_pkgname")
backup=('etc/UPower/UPower.conf')
source=("$pkgname::git://anongit.freedesktop.org/upower" ignore-BAT1.patch)
md5sums=('SKIP'
         '95991de24ba57bdb9add422a41d480a5')

pkgver() {
  cd $pkgname
  git describe --long --tags | sed -E 's/^[^0-9]*//;s/([^-]*-g)/r\1/;s/[-_]/./g'
}

prepare() {
  cd $pkgname
  patch -p1 < ../ignore-BAT1.patch
  NOCONFIGURE=true ./autogen.sh
}

build() {
  cd $pkgname

  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib/$_pkgname \
    --disable-static
  make
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}
