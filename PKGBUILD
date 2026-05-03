# Maintainer: xDarkicex <contact@darkicex.com>
# This PKGBUILD downloads the prebuilt libravdbd binary from the upstream
# release and installs it. Models and ONNX Runtime are not bundled — run
# provision.sh after install to download them.

pkgname=libravdbd-bin
pkgver=1.4.28
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

sha256sums_x86_64=('b5c3758010e98dcb4d5ab877a4e744158175fd98d603ef0679bd8bf03d77d0ff')
sha256sums_aarch64=('f8fb08dbaafaa85efab4b64e7c26cdd3d2007f89af9bec76b05a3cbd5101ab89')
sha256sums=('f145f78feaeeae2be62fbc3e01a3ce16d214bc815b5238405330927fe27303da')

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
