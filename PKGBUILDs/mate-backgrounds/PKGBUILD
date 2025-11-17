# Maintainer: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>

pkgname=mate-backgrounds
pkgver=1.28.0
pkgrel=2
pkgdesc="Background images and data for MATE"
url="https://mate-desktop.org"
arch=('any')
license=('GPL-2.0-or-later')
groups=('mate')
makedepends=('mate-common')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/mate-desktop/mate-backgrounds/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('a2240af029707b7149b5b9ce67160025a408049b1af6dbb5cd85418511585fa7')

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
