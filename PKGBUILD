# Maintainer: MASAHIRO SUGAYA <xsigil@section-9.sh>
pkgname=m4llama-bin
_pkgname=m4llama
pkgver=0.2.0
pkgrel=1
pkgdesc="Terminal cockpit and CLI for templated local LLM inference via pure-Go M4 engine and llama-server"
arch=('x86_64' 'aarch64')
url="https://github.com/xsigil/m4llama"
license=('MIT')
depends=('glibc')
makedepends=('go')
optdepends=(
    'wl-clipboard: Wayland clipboard support (wl-copy/wl-paste)'
    'xclip: X11 clipboard fallback support'
    'neovim: Preferred prompt editor integration'
)
source=("${_pkgname}-${pkgver}.tar.gz::https://github.com/xsigil/${_pkgname}/archive/refs/tags/v${pkgver}.tar.gz")
sha256sums=('SKIP') # updpkgsums で自動計算します

build() {
    cd "${_pkgname}-${pkgver}"
    export CGO_ENABLED=0
    export GOFLAGS="-trimpath -modcacherw"
    go build -ldflags="-s -w" -o "${_pkgname}" ./cmd/m4llama
}

check() {
    cd "${_pkgname}-${pkgver}"
    go test ./...
}

package() {
    cd "${_pkgname}-${pkgver}"
    install -Dm755 "${_pkgname}" "${pkgdir}/usr/bin/${_pkgname}"
    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE" 2>/dev/null || true
    install -Dm644 README.md "${pkgdir}/usr/share/doc/${pkgname}/README.md"
}
