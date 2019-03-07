_runtime_commit='03af0a80dbcbcfa09a828cde46151749bee2480e'
_runc_commit='6635b4f0c6af3810594d2770f662f34ddc15b40d'
_runc_path='gopath/src/github.com/opencontainers/runc'
pkgname=nvidia-container-runtime
pkgver=2.0.0
pkgrel=2
pkgdesc='NVIDIA container runtime'
arch=('x86_64')
url='https://github.com/NVIDIA/nvidia-container-runtime'
license=('custom')
depends=('libseccomp' 'nvidia-container-runtime-hook')
makedepends=('go' 'git')
source_x86_64=("git+https://github.com/NVIDIA/nvidia-container-runtime.git#commit=${_runtime_commit}"
               "git+https://github.com/opencontainers/runc.git#commit=${_runc_commit}")
sha256sums_x86_64=('SKIP'
                   'SKIP')

prepare() {
  cd runc
  git apply $srcdir/nvidia-container-runtime/runtime/runc/${_runc_commit}/*
  mkdir -p $srcdir/gopath/src/github.com/opencontainers
  ln -rTsf "$srcdir/runc" "$srcdir/${_runc_path}"
}

build() {
  cd $srcdir/${_runc_path}
  GOPATH="$srcdir/gopath" make
}

package() {
  install -D -m755 "$srcdir/${_runc_path}/runc" "$pkgdir/usr/bin/nvidia-container-runtime"
  install -D -m644 "$srcdir/nvidia-container-runtime/LICENSE" "$pkgdir/usr/share/$pkgname/licenses/LICENSE"
}
