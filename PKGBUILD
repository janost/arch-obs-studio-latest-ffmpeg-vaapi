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
         "qt5-x11extras" "curl" "gtk-update-icon-cache")
makedepends=("cmake" "git" "libfdk-aac" "libxcomposite" "x264" "jack" "vlc")
optdepends=("libfdk-aac: FDK AAC codec support"
            "libxcomposite: XComposite capture support"
            "jack: JACK Support"
            "vlc: VLC Media Source")
provides=("obs-studio")
conflicts=("obs-studio-git" "obs-linuxbrowser")
source=("$pkgname::git+https://github.com/jp9000/obs-studio.git"
       "git+https://github.com/Mixer/ftl-sdk.git"
       "ffmpeg-vaapi.patch")
md5sums=("SKIP" "SKIP" "SKIP")

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
}

build() {
  cd $pkgname
  patch -Np1 -i ../ffmpeg-vaapi.patch

  mkdir -p build; cd build

  cmake -DCMAKE_INSTALL_PREFIX=/usr \
	-DOBS_VERSION_OVERRIDE=$pkgver ..

  make
}

package() {
  cd $pkgname/build

  make install DESTDIR="$pkgdir"
}

# vim: ts=2:sw=2
