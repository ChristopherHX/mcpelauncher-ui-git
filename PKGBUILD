# Maintainer: Paul <paul@mrarm.io>
pkgname=mcpelauncher-ui-git
pkgver=v0.1.beta.1.r1.gb3f9c5a
pkgrel=1
pkgdesc="Minecraft: PE Linux launcher UI"
arch=('x86_64' 'i686')
url="https://github.com/ChristopherHX/mcpelauncher-ui-manifest"
license=('GPL3', 'MIT')
makedepends=('git' 'cmake')
depends=('qt5-base' 'qt5-webengine' 'qt5-declarative' 'qt5-quickcontrols' 'qt5-quickcontrols2' 'qt5-svg' 'libzip' 'protobuf' 'libuv' 'mcpelauncher-client')
provides=('mcpelauncher-ui')
conflicts=('mcpelauncher-ui')
source=(
  'git://github.com/ChristopherHX/mcpelauncher-ui-manifest.git'
  'nlohmann_json_license.txt::https://raw.githubusercontent.com/nlohmann/json/develop/LICENSE.MIT'
)
md5sums=(
  'SKIP'
  'SKIP'
)

pkgver() {
  cd "mcpelauncher-ui-manifest"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
prepare() {
  cd mcpelauncher-ui-manifest
  git remote set-url origin https://github.com/ChristopherHX/mcpelauncher-ui-manifest
  git submodule update --init --recursive
}
build() {
  cd mcpelauncher-ui-manifest
  mkdir -p build
  cd build
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release ..
  make
}
package() {
  cd mcpelauncher-ui-manifest/build
  make DESTDIR="$pkgdir" install
  install -Dm644 ../mcpelauncher-ui-qt/LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 ../../nlohmann_json_license.txt "$pkgdir/usr/share/licenses/$pkgname/nlohmann_json_license.txt"
}
