# Maintainer: Jguer <joaogg3@gmail.com>
pkgname=yay
pkgver=2.219
pkgrel=1
pkgdesc="Yet another yogurt. Pacman wrapper and AUR helper written in go."
arch=('i686' 'x86_64' 'armv7h' 'aarch64')
url="https://github.com/Jguer/yay"
license=('GPL')
options=('!strip' '!emptydirs')
depends=(
  'sudo'
)
makedepends=(
  'git'
  'go'
)
conflicts=('yay-bin')
source=("https://github.com/Jguer/yay/archive/v${pkgver}.tar.gz")
sha1sums=('674392963a80093d04c7a8ed0aea0adc541dc003')

prepare() {
  export GOPATH="${srcdir}/.go"
  export GOBIN="$GOPATH/bin"
  mkdir -p "$GOPATH"
  rm -rf "$GOPATH/src"
  ln -sf "$srcdir/$pkgname-$pkgver/vendor" "$GOPATH/src"
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  git submodule update --init
  go build -v -o ${pkgname} -ldflags "-s -w -X main.version=${pkgver}"
}

package() {
  _output="${srcdir}/$pkgname-$pkgver"
  install -Dm755 "${_output}/${pkgname}" "${pkgdir}/usr/bin/${pkgname}"

  # Install GLP v3
  # install -Dm644 "${_output}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname/-bin/}/LICENSE"

  # Install manpage
  install -Dm644 "${_output}/yay.8" "${pkgdir}/usr/share/man/man8/yay.8"

  # Install bash completion
  install -Dm644 "${_output}/bash-completion" "${pkgdir}/usr/share/bash-completion/completions/yay"

  # Install zsh completion
  install -Dm644 "${_output}/zsh-completion" "${pkgdir}/usr/share/zsh/site-functions/_yay"

  # Install fish completion
  install -Dm644 "${_output}/yay.fish" "${pkgdir}/usr/share/fish/vendor_completions.d/yay.fish"
}
