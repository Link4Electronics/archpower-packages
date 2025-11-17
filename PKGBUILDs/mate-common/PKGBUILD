# Maintainer: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>

pkgname=mate-common
pkgver=1.28.0
pkgrel=2
pkgdesc="Common development macros for MATE"
arch=('any')
license=('GPL-3.0-or-later')
depends=('autoconf' 'automake' 'gettext' 'gtk-doc' 'libtool'
         'pkg-config')
url="https://mate-desktop.org"
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/mate-desktop/mate-common/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('7100ecd60a9b5f398b9c3508eb17bca657bb748a74fc9f277b1e5ba1e022b701')

prepare() {
	cd "${pkgname}-${pkgver}"
	./autogen.sh
}

build() {
	cd "${pkgname}-${pkgver}"
    	./configure \
        	--prefix=/usr
    	make
}

package() {
    	cd "${pkgname}-${pkgver}"
    	make DESTDIR="${pkgdir}" install
}
