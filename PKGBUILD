pkgname=dwm
pkgver=6.2
pkgrel=1
pkgdesc="A dynamic window manager for X"
arch=('i686' 'x86_64')
url="http://dwm.suckless.org"
license=('MIT')
depends=('libx11' 'libxinerama' 'libxft' 'freetype2')
provides=('dwm')
conflicts=('dwm')
options=(zipman)
install=dwm.install
source=(http://dl.suckless.org/$pkgname/$pkgname-$pkgver.tar.gz
	dwm-tilegap-6.2.diff
	dwm-notitlecolor-6.2.diff
	config.h
	dwm.desktop)
sha256sums=('97902e2e007aaeaa3c6e3bed1f81785b817b7413947f1db1d3b62b8da4cd110e'
            '3eda10df758642314881d38e9b5feb23aa58e75d64a322460529402c874d0c64'
            'cfd573e25601a91c4c44e642fd0cf24d38105bccca2b6734754b2d76713ac92d'
            '8ce16dec3f5331d9d084fe6622839d7724fe31d72e04ec7bf4419b9d534b3e3b'
            'bc36426772e1471d6dd8c8aed91f288e16949e3463a9933fee6390ee0ccd3f81')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  cp "$srcdir/config.h" config.h

  for patch in $srcdir/*.diff; do
    if [ -f $patch ];
    then
      echo "Applying $(basename $patch)"
      patch -p1 --quiet < $patch
    fi
  done
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11 FREETYPEINC=/usr/include/freetype2
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -m644 -D README "$pkgdir/usr/share/doc/$pkgname/README"
  install -m644 -D "$srcdir/dwm.desktop" "$pkgdir/usr/share/xsessions/dwm.desktop"
}
