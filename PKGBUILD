# Maintainer: grmat <grmat@sub.red>

pkgname=roc-rocr-git
_pkgname=ROCR-Runtime
pkgdesc='ROCm Platform Runtime: ROCr a HPC market enhanced HSA based runtime'
pkgver=1.1.0.r13.g8dc021c
pkgrel=1
arch=('x86_64')
license=('MIT')
makedepends=('git libelf')
depends=('roc-roct-git')

source=("git+https://github.com/RadeonOpenCompute/${_pkgname}.git")
sha256sums=('SKIP')

pkgver() {
  cd $srcdir/${_pkgname}
  git describe --long | sed 's/^roc-//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${srcdir}/${_pkgname}/src"
  mkdir build
  cd build
  cmake -D CMAKE_PREFIX_PATH=/opt/rocm/libhsakmt \
        -D CMAKE_INSTALL_PREFIX="${pkgdir}/opt/rocm" \
        ..
  make ${MAKEFLAGS}
}

package() {
  mkdir -p ${pkgdir}/opt/rocm
  cd "${srcdir}/${_pkgname}/src/build"
  make install

  mkdir -p "${pkgdir}/usr/share/licenses/${pkgname}"
  install -D -m644 "${srcdir}/${_pkgname}/LICENSE.txt" "${pkgdir}/usr/share/licenses/${pkgname}/"

  make clean
  rm -rf "${srcdir}/${_pkgname}/src/build"
}
