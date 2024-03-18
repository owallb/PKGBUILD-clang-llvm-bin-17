# Maintainer: Oscar Wallberg <oscar.wallberg@pm.me>

pkgname='clang+llvm-bin-17'
pkgver=17.0.6
pkgrel=1
arch=('x86_64')
url="https://llvm.org/"
license=('custom:Apache 2.0 with LLVM Exception')
pkgdesc="Clang+LLVM 17"
depends=('llvm-libs' 'gcc' 'compiler-rt' 'gcc-libs' 'zlib' 'libffi' 'libedit' 'ncurses' 'libxml2' 'perl')
provides=("clang-analyzer-17=$pkgver" "clang-tools-extra-17=$pkgver")
source=(https://github.com/llvm/llvm-project/releases/download/llvmorg-${pkgver}/clang+llvm-${pkgver}-x86_64-linux-gnu-ubuntu-22.04.tar.xz)
sha256sums=('884ee67d647d77e58740c1e645649e29ae9e8a6fe87c1376be0f3a30f3cc9ab3')

package() {
    local _dir="${srcdir}/clang+llvm-${pkgver}-x86_64-linux-gnu-ubuntu-22.04" 
    find "${_dir}" -type f | while read -r file; do
        local rel_file=$(realpath --relative-to="${_dir}" "$file")
        
        install -D "${file}" "${pkgdir}/opt/clang+llvm-17/${rel_file}"
    done

    install -d "${pkgdir}/usr/bin"
    find "${pkgdir}/opt/clang+llvm-17/bin" -type f | while read -r file; do
        local _basename="$(basename "${file}")"
        local _basename_ver
        if [[ "${_basename}" != *-17 ]]; then
            _basename_ver="${_basename}-17"
        else
            _basename_ver="${_basename}"
        fi
        ln -s "../../opt/clang+llvm-17/bin/${_basename}" "${pkgdir}/usr/bin/${_basename_ver}"
    done

    install -Dm644 ../LLVM_LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}

