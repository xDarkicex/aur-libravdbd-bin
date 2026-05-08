# Maintainer: xDarkicex <contact@darkicex.com>
# This PKGBUILD downloads the prebuilt libravdbd binary from the upstream
# release and installs it. Models and ONNX Runtime are not bundled — run
# provision.sh after install to download them.

pkgname=libravdbd-bin
pkgver=1.4.58
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

sha256sums_x86_64=('556d382470a8a2556b1ab840ea5867ba148478146277d5b52b2d550118055e4a')
sha256sums_aarch64=('069ebe11402744cb202b3ebfea68d6c4d0126fb44f709c3749bd8ad7adb7df9d')
sha256sums=('9102a44e0f6e19928c67bcd2abffc4d16bb56d631200c8db299627e6e48ff6a7')

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
