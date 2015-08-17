# Maintainer: Daenyth <Daenyth+Arch [AT] gmail [DOT] com>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: rabyte <rabyte__gmail>
# Contributor to alpha version: Wiz <wiz@haxx.es>
# Contributor since 0.7.3: MCMic <mcmic@free.fr>

pkgname=supertuxkart-alpha
pkgver=0.7.3
pkgrel=2
pkgdesc="A new and improved version of TuxKart, a kart racing game featuring Tux and his friends"
arch=('i686' 'x86_64')
url="http://supertuxkart.sourceforge.net/"
license=('GPL2')
depends=('sdl>=1.2' 'libvorbis' 'freealut' 'libgl' 'freeglut')
makedepends=('cmake' 'svn')
conflicts=('supertuxkart')
source=(http://downloads.sourceforge.net/project/supertuxkart/SuperTuxKart/$pkgver/supertuxkart-$pkgver-src.tar.bz2)
md5sums=('502664b2ec9ad5ab88b1882fef4c074d')

build() {
  cd ${srcdir}/

  svn checkout https://irrlicht.svn.sourceforge.net/svnroot/irrlicht/trunk@3843 irrlicht
  
  cd irrlicht/source/Irrlicht/
  make STATIC=yes NDEBUG=1
  cd ${srcdir}/supertuxkart-${pkgver}
  
  echo ${srcdir}/irrlicht/

  cmake -DIRRLICHT_DIR=${srcdir}/irrlicht -DCMAKE_INSTALL_PREFIX=/usr .
  #~ ./configure --prefix=/usr --datadir=/usr/share || return 1

  # Fix compilation failure: http://bugs.gentoo.org/283490
  #~ sed -i 's/-lGL/-lGL -lGLU/' config.status

  # those configure flags really mean nothing...
  #~ sed -i "s#/usr/local#/usr#" src/file_manager.cpp
  #~ sed -i "s#/games##" $(grep -Rl "/games" *)

  make
  make DESTDIR=${pkgdir} install

  # fix executable location...
  #~ install -dm755 ${pkgdir}/usr/bin
  #~ mv ${pkgdir}/usr/supertuxkart ${pkgdir}/usr/bin/supertuxkart
  #~ sed -i "s#usr/supertuxkart#usr/bin/supertuxkart#" \
    #~ ${pkgdir}/usr/share/applications/supertuxkart.desktop
}

# vim:set ts=2 sw=2 et:
