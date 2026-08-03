# Contributor:  danyf90 <daniele.formichelli@gmail.com>
# Contributor: Philipp 'TamCore' B. <philipp [at] tamcore [dot] eu>
# Contributor: Jakub Schmidtke <sjakub-at-gmail-dot-com>
# Contributor: Christoph Brill <egore911-at-gmail-dot-com>
# Contributor: Lubomir 'Kuci' Kucera <kuci24-at-gmail-dot-com>
# Contributor: Tad Fisher <tadfisher at gmail dot com>
# Contributor: Philippe Hürlimann <p@hurlimann.org>
# Contributor: Julian Raufelder <aur@raufelder.com>
# Contributor: Dhina17 <dhinalogu@gmail.com>
# Maintainer: Kordian Bruck <k@bruck.me>

pkgname=android-studio
pkgver=2026.1.3.7
_vername="quail3"
_jbrpkgver="21.0.11"
_jbrvername="b1163.116"
pkgrel=1
pkgdesc="The official Android IDE (Stable branch)"
arch=('i686' 'x86_64' 'aarch64')
url="https://developer.android.com/"
license=('APACHE')
makedepends=()
depends=('alsa-lib' 'freetype2' 'libxrender' 'libxtst' 'which')
optdepends=('gtk2: GTK+ look and feel'
            'libgl: emulator support'
            'ncurses5-compat-libs: native debugger support')
options=('!strip')
source=("https://dl.google.com/dl/android/studio/ide-zips/$pkgver/android-studio-$_vername-linux.tar.gz"
        "$pkgname.desktop"
        "license.html")
sha256sums=('36832122557ab73ca68dfd9bd989ddac40103ac003ca10e04c949a1f61578a67'
            '73cd2dde1d0f99aaba5baad1e2b91c834edd5db3c817f6fb78868d102360d3c4'
            '9a7563f7fb88c9a83df6cee9731660dc73a039ab594747e9e774916275b2e23e')

source_aarch64=("https://cache-redirector.jetbrains.com/intellij-jbr/jbr_jcef-$_jbrpkgver-linux-aarch64-$_jbrvername.tar.gz")
sha512sums_aarch64=('c39251cbafdc7a8433ed4b5136500a3530845191bc5568cfc64e199b68c6e457cf973644116dc9beb172a95ef9214d3f3a19ba1bb9dd6f0af2207c2373995d0f')

if [ "$CARCH" = "i686" ]; then
    depends+=('java-environment')
fi

package() {
  cd $srcdir/$pkgname

  # Install the application
  install -d $pkgdir/{opt/$pkgname,usr/bin}
  if [ "$CARCH" = "aarch64" ]; then
    cp -a bin lib plugins license LICENSE.txt build.txt product-info.json $pkgdir/opt/$pkgname
    mv $srcdir/jbr_jcef-$_jbrpkgver-linux-aarch64-$_jbrvername $pkgdir/opt/$pkgname/jbr
    ln -s /opt/android-studio/bin/studio.sh $pkgdir/usr/bin/$pkgname
  else
    cp -a bin lib jbr plugins license LICENSE.txt build.txt product-info.json $pkgdir/opt/$pkgname
    ln -s /opt/android-studio/bin/studio $pkgdir/usr/bin/$pkgname
  fi

  # Copy licenses
  install -Dm644 LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"
  install -Dm644 $srcdir/license.html "${pkgdir}/usr/share/licenses/${pkgname}/license.html"

  # Add the icon and desktop file
  install -Dm644 bin/studio.png $pkgdir/usr/share/pixmaps/$pkgname.png
  install -Dm644 $srcdir/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop

  chmod -R ugo+rX $pkgdir/opt
}
