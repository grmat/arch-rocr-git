# Maintainer: grmat <grmat@sub.red>

pkgname=roc-rocr-git
_pkgname=ROCR-Runtime
pkgdesc='ROCm Platform Runtime: ROCr a HPC market enhanced HSA based runtime'
pkgver=1.1.0.r13.g8dc021c
pkgrel=1
arch=('x86_64')
license=('MIT')
makedepends=('git libelf')
depends=('')

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
  cmake -D CMAKE_PREFIX_PATH=/usr \
        ..
  make ${MAKEFLAGS}
}

package() {
  mkdir -p "${pkgdir}/usr/include"
  cp -r "${srcdir}/${_pkgname}/src/inc" "${pkgdir}/usr/include/hsa"

#? amd_hsa_tools_interfaces.h
#? hsa_ext_debugger.h
#? hsa_ext_profiler.h

  cd ${srcdir}/${_pkgname}/src/build
  mkdir -p "${pkgdir}/usr/lib"
  mv "libhsa-runtime64.so.1.0.0" "${pkgdir}/usr/lib/"
  mv "libhsa-runtime64.so.1" "${pkgdir}/usr/lib/"

  mkdir -p "${pkgdir}/usr/share/licenses/${pkgname}"
  install -D -m644 "${srcdir}/${_pkgname}/LICENSE.txt" "${pkgdir}/usr/share/licenses/${pkgname}/"

  rm -rf "${srcdir}/${_pkgname}/src/build"
}
