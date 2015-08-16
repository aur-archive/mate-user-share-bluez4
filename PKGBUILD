# Maintainer : Martin Wimpress <code@flexion.org>
# Contributor: Giovanni "Talorno" Ricciardi <kar98k.sniper@gmail.com>

_pkgname=mate-user-share
pkgname=${_pkgname}-bluez4
pkgver=1.6.1
pkgrel=5
pkgdesc="User level public file sharing via WebDAV or ObexFTP."
url="http://mate-desktop.org"
arch=('i686' 'x86_64')
license=('GPL')
depends=('apache' 'dbus-glib' 'dconf' 'libunique' 'mate-bluetooth' 'mod_dnssd')
makedepends=('libcanberra' 'libnotify' 'mate-common' 'mate-doc-utils'
             'mate-file-manager' 'perl-xml-parser')
options=('!emptydirs')
conflicts=('mate-user-share')
provides=('mate-user-share')
groups=('mate-extra')
install=${_pkgname}.install
source=("http://pub.mate-desktop.org/releases/1.6/${_pkgname}-${pkgver}.tar.xz"
        "https://github.com/mate-desktop/mate-user-share/commit/7a0305478295e9e7c284372677a4cbc382444482.diff")
sha1sums=('83f161dee79ea0ae4345c54a5b1339f673f68e8f'
          'ffa10ae69f5edf08d605418182f3c5bc975eb3cf')

prepare() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    # do not use download dir for incoming bluetooth downloads if mate-bluetooth isn't installed
    patch -Np1 -i "${srcdir}/7a0305478295e9e7c284372677a4cbc382444482.diff"
}

build() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    PYTHON=/usr/bin/python2 ./configure \
        --prefix=/usr \
        --libexec=/usr/lib/${_pkgname} \
        --sysconfdir=/etc \
        --disable-static \
        --disable-scrollkeeper
    make
}

package() {
    cd "${srcdir}/${_pkgname}-${pkgver}"
    make  DESTDIR="${pkgdir}" install
    rm -f "${pkgdir}/usr/share/mate-user-share/dav_user_2.0.conf"
}
