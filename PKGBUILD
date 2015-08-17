# Maintainer: Splex
# Contributor: Slash <demodevil5[at]yahoo[dot]com>
pkgname=secondlife-oculus-rift-bin
pkgver=3.7.12.292141
_relname=Second_Life_Project_OculusRift_3_7_12_292141_i686
_pngver=1.5.1
pkgrel=1
pkgdesc="Second Life is a 3-D virtual world entirely built and owned by its residents (Binary version.) (OculusRift Channel)"
url="http://wiki.secondlife.com/wiki/Linden_Lab_Official:Alternate_Viewers#Second_Life_Project_OculusRift_Channel"
license=('GPL')
[ "$CARCH" = "i686" ] && depends=('freealut' 'gtk2' 'libgl' 'libidn' 'mesa' 'sdl' 'libxml2' 'glu' 'pangox-compat')
[ "$CARCH" = "i686" ] && optdepends=('libpulse: for PulseAudio support' 'alsa-lib: for ALSA support' 'nvidia-utils: for NVIDIA support' 'nvidia-libgl: for NVIDIA support' 'flashplugin: for inworld Flash support')
[ "$CARCH" = "x86_64" ] && depends=('lib32-freealut' 'lib32-gtk2' 'lib32-libgl' 'lib32-libidn' 'lib32-mesa' 'lib32-sdl' 'lib32-libxml2' 'lib32-glu' 'lib32-pangox-compat')
[ "$CARCH" = "x86_64" ] && optdepends=('lib32-libpulse: for PulseAudio support' 'lib32-alsa-lib: for ALSA support' 'lib32-nvidia-utils: for NVIDIA support' 'lib32-nvidia-libgl: for NVIDIA support' 'lib32-flashplugin: for inworld Flash support')
arch=('i686' 'x86_64')
conflicts=('secondlife' 'secondlife-svn' 'secondlife-bin')
install=secondlife.install
            #http://download.cloud.secondlife.com/Viewer_3/Second_Life_Project_OculusRift_3_7_8_289834_i686.tar.bz2
source=('secondlife.desktop'
        'secondlife.launcher'
        "http://download.cloud.secondlife.com/Viewer_3/${_relname}.tar.bz2"
        "http://downloads.sourceforge.net/sourceforge/libpng/libpng-${_pngver}.tar.xz")

build() {
  # build compatible lib32-libpng
  msg "Building libpng..."

  if [ "$CARCH" = "x86_64" ] ; then
    export CC="gcc -m32"
    export CXX="g++ -m32"
    export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"
  fi

  cd "${srcdir}/libpng-${_pngver}"

  ./configure
  make
}

package() {
  cd $srcdir
  
  # Rename Data Directory
  mv ${_relname} secondlife
  
  # Install Desktop File
  install -D -m644 $srcdir/secondlife.desktop \
    $pkgdir/usr/share/applications/secondlife.desktop
  
  # Install Icon File
  install -D -m644 $srcdir/secondlife/secondlife_icon.png \
    $pkgdir/usr/share/pixmaps/secondlife.png
  
  # Install Launcher
  install -D -m755 $srcdir/secondlife.launcher \
    $pkgdir/usr/bin/secondlife

  # Move Data to Destination Directory
  install -d $pkgdir/opt
  mv secondlife $pkgdir/opt/
  
  # Change Permissions of files to root:games
  chown -R root:games $pkgdir/opt/secondlife
  chmod -R g+rw $pkgdir/opt/secondlife
  
  # Make Binary Group-Executable
  chmod g+x $pkgdir/opt/secondlife/secondlife

  # Install libpng we built
  install -D -m755 $srcdir/libpng-${_pngver}/.libs/libpng15.so.15.1.0 \
    $pkgdir/opt/secondlife/lib

  cd $pkgdir/opt/secondlife/lib
  ln -s libpng15.so.15.1.0 libpng15.so.15
  ln -s libpng15.so.15.1.0 libpng15.so
  ln -s libfontconfig.so.1.4.4 libfontconfig.so.1
}

# vim:set ts=2 sw=2 et:
md5sums=('382de210a260ca1445cf5c0dbed1a9ec'
         'ae369202ee997c53926cb998f471093a'
         '45b7677b057a494a58b4909dce9d8f26'
         '35455234375f1adff8083f408a099e3a')
