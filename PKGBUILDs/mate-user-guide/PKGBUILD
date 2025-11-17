# Maintainer: Alexander Epaneshnikov <alex19ep@archlinux.org>
# Contributor: Brad Fanella <cesura@archlinux.org>
# Contributor: Martin Wimpress <code@flexion.org>

pkgname=mate-user-guide
pkgver=1.28.0
pkgrel=2
pkgdesc="MATE User Guide"
groups=('mate')
url="https://mate-desktop.org"
arch=('any')
license=('GFDL-1.1-or-later')
depends=('yelp')
makedepends=('autoconf-archive' 'itstool' 'mate-common' 'yelp-tools')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/mate-desktop/mate-user-guide/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('bedce24a8f11eaeb929fa5ccf5d682160c28d6436097c710341eb4152b11b784')

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
