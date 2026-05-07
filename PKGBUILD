# Maintainer: xDarkicex <contact@darkicex.com>
# This PKGBUILD downloads the prebuilt libravdbd binary from the upstream
# release and installs it. Models and ONNX Runtime are not bundled — run
# provision.sh after install to download them.

pkgname=libravdbd-bin
pkgver=1.4.42
pkgrel=1
pkgdesc="AI-native vector database daemon with ML embeddings (prebuilt binary)"
arch=('x86_64' 'aarch64')
url="https://github.com/zephyr-systems/libravdbd"
license=('custom')
provides=('libravdbd')
conflicts=('libravdbd')

source_x86_64=("libravdbd-linux-x86_64::https://github.com/xDarkicex/homebrew-openclaw-libravdb-memory/releases/download/v${pkgver}/libravdbd-linux-amd64")
source_aarch64=("libravdbd-linux-aarch64::https://github.com/xDarkicex/homebrew-openclaw-libravdb-memory/releases/download/v${pkgver}/libravdbd-linux-arm64")
source=("provision.sh::https://github.com/xDarkicex/homebrew-openclaw-libravdb-memory/releases/download/v${pkgver}/provision.sh")

sha256sums_x86_64=('c5c2be03e6eaf03e04e589ce318614fb5d3d2471128c934a679f8c0983f4f072')
sha256sums_aarch64=('7ea62808ee11a7b835ecc9668c588e3c826f96a0acee782f0bad853dcff96005')
sha256sums=('b358bdb9dbdf28b522b49caf4bb5b8db29a792fa92e9770e179fd030d87b70a0')

package() {
    install -Dm755 "${srcdir}/libravdbd-linux-${CARCH}" "${pkgdir}/usr/bin/libravdbd"
    install -Dm755 "${srcdir}/provision.sh" "${pkgdir}/usr/lib/libravdbd/provision.sh"
    install -Dm644 "${srcdir}/../libravdbd.service" "${pkgdir}/usr/lib/systemd/user/libravdbd.service"

    # License
    mkdir -p "${pkgdir}/usr/share/licenses/${pkgname}"
    cat > "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE" <<'LICENSE'
libravdbd is distributed under a proprietary license.
See https://github.com/zephyr-systems/libravdbd for terms.
LICENSE
}
