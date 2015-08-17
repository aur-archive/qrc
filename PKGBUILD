# Maintainer: archtux <antonio dot arias99999 at gmail dot com>

pkgname=qrc
pkgver=0.6.0
pkgrel=4
pkgdesc="QR-Code generator/reader"
arch=('i686' 'x86_64')
url="http://kde-apps.org/content/show.php/qrc?content=159951"
license=('GPL2')
depends=('opencv' 'qrencode' 'qt4' 'zbar')
optdepends=('gimp')
source=(http://kde-apps.org/CONTENT/content-files/159951-qrc-$pkgver.tgz
        qrc.desktop)
md5sums=('610a4c783388f132419f9eb77afa007e'
         '47ffcbab541fa90e15c3c818551f6391')

prepare() {
  cd $srcdir/$pkgname-$pkgver

  # Fix zbar and qrencode library path
  sed -i 's|local/lib64|lib|' qrc.pro
  sed -i 's|usr/lib64|usr/lib|' qrc.pro
  
  # Fix opencv 2.4.8-1 in Arch, g++: error: /usr/lib/libopencv_ts.so: No such file or directory
  sed -i 's|ts.so|ts.a|' qrc.pro  

  qmake-qt4
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make
}

package() {
  cd $srcdir/$pkgname-$pkgver
  
  # Binary
  install -Dm755 qrc $pkgdir/usr/bin/qrc
  
  # Languages
  mkdir -p $pkgdir/usr/share/qrc
  cp translations/*qm $pkgdir/usr/share/qrc
  
  # Desktop icon
  install -Dm644 icons/qrc.png $pkgdir/usr/share/pixmaps/qrc.png
  install -Dm644 ../qrc.desktop $pkgdir/usr/share/applications/qrc.desktop
}