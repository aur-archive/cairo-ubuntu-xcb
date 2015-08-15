# Maintainer: Tevin Zhang <mail2tevin {at} gmail {dot} com>
# Contributor: Paul Bredbury <brebs@sent.com>
# Contributor: Biru Ionut <biru.ionut at gmail.com>
# Contributor: Andrea Fagiani <andfagiani {at} gmail {dot} com>
# Maintainer: Rainux Luo <rainux {at} gmail {dot} com>

# Installation order:  freetype2-ubuntu fontconfig-ubuntu libxft-ubuntu cairo-ubuntu-xcb
pkgname=cairo-ubuntu-xcb
pkgver=1.12.2
_ubver=1.12.2-1ubuntu1
pkgrel=3
pkgdesc="Cairo vector graphics library, with Ubuntu's LCD rendering patches. Enabled xcb for awesome window manager."
arch=(i686 x86_64)
url="https://launchpad.net/ubuntu/precise/+source/cairo"
license=('LGPL' 'MPL')
depends=('libpng>=1.4.0' 'libxrender' 'fontconfig-ubuntu>=2.8.0' 'libxft-ubuntu' 'pixman>=0.16.6' 'xcb-util>=0.3.6')
makedepends=('pkgconfig')
provides=("cairo=$pkgver" "cairo-tee=$pkgver" "cairo-xcb=$pkgver" "cairo-ubuntu=$pkgver")
conflicts=('cairo' 'cairo-cleartype' 'cairo-lcd' 'cairo-tee' 'cairo-xeffects' 'cairo-ubuntu')
options=('!libtool')
source=(http://cairographics.org/releases/cairo-$pkgver.tar.xz
        http://archive.ubuntu.com/ubuntu/pool/main/c/cairo/cairo_$_ubver.debian.tar.gz
        cairo-respect-fontconfig.patch)

md5sums=('87649eb75789739d517c743e94879e51'
         '84c68aa3f3c7b400928e269658c06090'
         '79f7c141c49f3d65ab308cc706d50914')


build() {
  cd $srcdir/cairo-$pkgver

  for _f in $(cat $srcdir/debian/patches/series) ; do
    patch -Np1 -i $srcdir/debian/patches/$_f
  done

  patch -Np1 -i $srcdir/cairo-respect-fontconfig.patch
  
  autoreconf
  ./configure --prefix=/usr --sysconfdir=/etc \
    --localstatedir=/var --enable-xcb --disable-static \
    --enable-tee
  make
}

package() {
  cd $srcdir/cairo-$pkgver

  make DESTDIR=$pkgdir install

  # Docs
  # Excluding debian/changelog temporarily
  install -d $pkgdir/usr/share/doc/cairo/
  install -m644 -t $pkgdir/usr/share/doc/cairo/ NEWS README
}
