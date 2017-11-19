# Maintainer: Benjamin Klettbach <b dot klettbach at gmail dot com >
# Contributor: Jonathan Steel <jsteel at archlinux.org>
# Contributor: ArcticVanguard <LideEmily at gmail dot com>
# Contributor: ledti <antergist at gmail dot com>

pkgname=obs-studio
pkgrel=1
pkgver=20.1.3
pkgdesc="Free and open source software for video recording and live streaming."
arch=("i686" "x86_64")
url="https://github.com/jp9000/obs-studio"
license=("GPL2")
depends=("ffmpeg" "jansson" "libxinerama" "libxkbcommon-x11"
         "qt5-x11extras" "curl" "gtk-update-icon-cache" "cef-minimal")
makedepends=("cmake" "git" "libfdk-aac" "libxcomposite" "x264" "jack" "vlc")
optdepends=("libfdk-aac: FDK AAC codec support"
            "libxcomposite: XComposite capture support"
            "jack: JACK Support"
            "vlc: VLC Media Source"
            "pepper-flash: Flash support")
provides=("obs-studio" "obs-linuxbrowser")
source=("$pkgname::git+https://github.com/jp9000/obs-studio.git"
       "git+https://github.com/Mixer/ftl-sdk.git"
       "git+https://github.com/bazukas/obs-linuxbrowser.git"
       "transparentpainting.patch"
       "ffmpeg-vaapi.patch")
md5sums=("SKIP" "SKIP" "SKIP" "SKIP" "SKIP")

pkgver() {
  cd $pkgname
  git describe --tags
}

prepare() {
  cd $pkgname
  latesttag=$(git describe --tags)
  git checkout $latesttag
  git submodule init
  git config submodule.plugins/obs-outputs/ftl-sdk.url $srcdir/ftl-sdk
  git submodule update
  cd ../obs-linuxbrowser
  latesttag2=$(git describe --tags)
  git checkout $latesttag2
}

build() {
  cd $pkgname
  patch -Np1 -i ../ffmpeg-vaapi.patch

  mkdir -p build; cd build

  cmake -DCMAKE_INSTALL_PREFIX=/usr \
	-DOBS_VERSION_OVERRIDE=$pkgver ..

  make

  cd ../../obs-linuxbrowser
  mkdir -p ./build
  cd ./build
  cmake -D CEF_DIR="/opt/cef" ..
  make clean
  make
}

package() {
  cd $pkgname/build

  make install DESTDIR="$pkgdir"
  cd ../../
  mkdir -p "$pkgdir"/usr/share/obs/obs-plugins/obs-linuxbrowser
  cp -R "$srcdir"/obs-linuxbrowser/build/build/obs-linuxbrowser/bin/64bit/* "$pkgdir"/usr/lib/obs-plugins/
  mv "$pkgdir"/usr/lib/obs-plugins/libobs-linuxbrowser.so "$pkgdir"/usr/lib/obs-plugins/obs-linuxbrowser.so
  cp -R "$srcdir"/obs-linuxbrowser/build/build/obs-linuxbrowser/data/* "$pkgdir"/usr/share/obs/obs-plugins/obs-linuxbrowser
}

# vim: ts=2:sw=2
