# Maintainer: Alexander Epaneshnikov <alex19ep@archlinux.org>
# Contributor: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>

pkgname=mate-icon-theme
pkgver=1.28.0
pkgrel=2
pkgdesc="MATE icon theme"
url="https://mate-desktop.org"
arch=('any')
license=('LGPL-3.0-only')
options=('!emptydirs')
makedepends=('mate-common' 'icon-naming-utils')
groups=('mate')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/mate-desktop/mate-icon-theme/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('6cd3e848131f3ab995bc7c6f8445157d79fcc6b172c0ad2bc0bc8d81bdc8ae0d')

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
