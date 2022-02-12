# $Id$
# Maintainer : Bhushan shah <bshah@kde.org>
# Contributor : Antonio Rojas <arojas@archlinux.org>

pkgname=plasma-sdk-git
pkgver=5.79.0
pkgrel=1
pkgdesc="Applications useful for Plasma development"
arch=(i686 x86_64)
url='https://projects.kde.org/plasma-sdk'
license=(LGPL)
depends=(plasma-framework-git perl)
makedepends=(extra-cmake-modules-git kdoctools-git ktexteditor-git)
source=("git+https://invent.kde.org/plasma/${pkgname%-git}.git")
md5sums=('SKIP')

pkgver() {
  cd plasma-sdk
  _ver="$(cat CMakeLists.txt | grep -m1 'set(PROJECT_VERSION' | cut -d '"' -f2 | tr - .)"
  echo "${_ver}.r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../plasma-sdk \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DLIB_INSTALL_DIR=lib \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
    -DCMAKE_BUILD_TYPE=Release \
    -DBUILD_TESTING=OFF
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
}
