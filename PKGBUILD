# Maintainer: Daniel Biehl <dbiehl@live.de>
_realname=xqilla
pkgbase=mingw-w64-${_realname}
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}"
pkgver=2.3.4
pkgrel=1
pkgdesc="An XQuery and XPath 2.0 library, written in C++ and built on top of Xerces-C."
arch=("any")
url="http://xqilla.sourceforge.net/"

license=("Apache")

makedepends=("${MINGW_PACKAGE_PREFIX}-gcc" "${MINGW_PACKAGE_PREFIX}-pkg-config" "bison")
depends=("${MINGW_PACKAGE_PREFIX}-xerces-c" "${MINGW_PACKAGE_PREFIX}-icu")

source=("https://downloads.sourceforge.net/project/xqilla/XQilla-${pkgver}.tar.gz"
        "mingw64.patch")

sha256sums=('292631791631fe2e7eb9727377335063a48f12611d641d0296697e0c075902eb'
            'ec029903926ec802c11194bc83001862c1ca499c8d2df6a4af743d60541fbfaf')            
prepare() {
    cd "XQilla-${pkgver}"

    # Apply for mingw64
    patch -p1 < "${srcdir}/mingw64.patch"
}

build() {
    mkdir -p "${srcdir}/build-${MINGW_CHOST}"
    cd "${srcdir}"/build-${MINGW_CHOST}
    
    "${srcdir}"/"XQilla-${pkgver}"/configure --prefix=${MINGW_PREFIX} --with-xerces=${MINGW_PREFIX} --build=${MINGW_CHOST} --host=${MINGW_CHOST} --target=${MINGW_CHOST}
    make
}

package() {
    cd "${srcdir}"/build-${MINGW_CHOST}
    make DESTDIR="${pkgdir}/" install
}