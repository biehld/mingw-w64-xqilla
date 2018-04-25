# Maintainer: Daniel Biehl <dbiehl@live.de>
_realname=xqilla
pkgbase=mingw-w64-${_realname}
pkgname="${MINGW_PACKAGE_PREFIX}-${_realname}"
pkgver=2.3.3
pkgrel=1
pkgdesc="An XQuery and XPath 2.0 library, written in C++ and built on top of Xerces-C."
arch=("any")
url="http://xqilla.sourceforge.net/"

license=("GPL3")

makedepends=("${MINGW_PACKAGE_PREFIX}-gcc" "${MINGW_PACKAGE_PREFIX}-pkg-config")
depends=("${MINGW_PACKAGE_PREFIX}-xerces-c" "${MINGW_PACKAGE_PREFIX}-icu")

source=("https://downloads.sourceforge.net/project/xqilla/XQilla-${pkgver}.tar.gz"
        "xerces-containing-node.patch" "mingw64.patch")
sha256sums=('8f76b9b4f966f315acc2a8e104e426d8a76ba4ea3441b0ecfdd1e39195674fd6'
            '36ffb2dff579e5610ca3be2a962942433127b24a78ca454647059d6d54b8e014'
            'b3dd469180667d629fe44e72d6ac7ece50ae0cf63b9a6cab7228907404df2afd')
            
prepare() {
    cd "XQilla-${pkgver}"

    # Apply patch from Homebrew to make XQilla compatible with Xerces-C 3.2.
    # See: https://sourceforge.net/p/xqilla/bugs/48/
    patch -p1 < "${srcdir}/xerces-containing-node.patch"
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