# Maintainer: Tyler Beatty <tjb0607 at gmail dot com>

pkgname=primecoin-mikaelh2-git
_gitname=primecoin-hp
pkgver=0.1.1hp7
pkgrel=2
epoch=1
pkgdesc="Cryptocurrency with Scientific Computing Proof-of-Work (Prime) (mikaelh2's high performance mining fork)"
arch=('x86_64' 'i686')
url="https://bitcointalk.org/index.php?topic=255782.0"
license=('MIT')
provides=('primecoin-qt' 'primecoind')
conflicts=('primecoin-qt' 'primecoind' 'primecoin-git')
depends=('qt4' 'miniupnpc' 'boost-libs')
makedepends=('git' 'boost')
source=('git+https://bitbucket.org/mikaelh/primecoin-hp.git'
        'primecoin.desktop')
install=primecoin.install
sha256sums=(SKIP 
            'd48546c4aab0a1f42fad2aa2f2069d20b4ab85782703927ca6a4bd0846d6348f')

## files & commands for building
_makefile_unix=makefile.unix
_qmake=qmake-qt4
_qt_pro=bitcoin-qt.pro

build() {
    cd ${_gitname}/src
    
    # build primecoind
    msg "Building Primecoin daemon"
    make USE_UPNP=1 USE_SSL=1 CXXFLAGS="-O3 -march=native" $MAKEFLAGS -f ${_makefile_unix} primecoind
    
    # build primecoin-qt
    msg "Building Primecoin QT GUI"
    cd ..
    ${_qmake} ${_qt_pro}
    make $MAKEFLAGS
}

package() {
    install -Dm644 primecoin.desktop ${pkgdir}/usr/share/applications/primecoin.desktop
    
    cd ${_gitname}
    install -Dm755 primecoin-qt "$pkgdir"/usr/bin/primecoin-qt
    install -Dm755 src/primecoind "$pkgdir"/usr/bin/primecoind
    install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
    install -Dm644 src/qt/res/icons/primecoin.png "$pkgdir"/usr/share/pixmaps/primecoin256.png
}
