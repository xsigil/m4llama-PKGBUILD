# Maintainer: MASAHIRO SUGAYA <xsigil@section-9.sh>
pkgname=m4llama-bin
_pkgname=m4llama
pkgver=0.2.2
pkgrel=1
pkgdesc="Terminal cockpit and CLI for templated local LLM inference via pure-Go M4 engine and llama-server"
arch=('x86_64' 'aarch64')
url="https://github.com/xsigil/m4llama"
license=('MIT')
depends=('glibc')
makedepends=('go' 'git')
optdepends=(
    'wl-clipboard: Wayland clipboard support (wl-copy/wl-paste)'
    'xclip: X11 clipboard fallback support'
    'neovim: Preferred prompt editor integration'
)
source=("git+https://github.com/xsigil/${_pkgname}.git#tag=v${pkgver}")
sha256sums=('SKIP')

prepare() {
    cd "${_pkgname}"
    git submodule update --init --recursive
}

build() {
    cd "${_pkgname}"
    export CGO_ENABLED=0
    export GOFLAGS="-trimpath -modcacherw"
    go build -ldflags="-s -w" -o "${_pkgname}" ./cmd/m4llama
}

check() {
    cd "${_pkgname}"
    go test ./...
}

package() {
    cd "${_pkgname}"
    install -Dm755 "${_pkgname}" "${pkgdir}/usr/bin/${_pkgname}"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE" 2>/dev/null || true
    install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
