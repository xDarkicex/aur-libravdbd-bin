# Maintainer: xDarkicex <contact@darkicex.com>
# This PKGBUILD downloads the prebuilt libravdbd binary from the upstream
# release and installs it. Models and ONNX Runtime are not bundled — run
# provision.sh after install to download them.

pkgname=libravdbd-bin
pkgver=1.5.0
pkgrel=1
pkgdesc="AI-native vector database daemon with ML embeddings (prebuilt binary)"
arch=('x86_64' 'aarch64')
url="https://github.com/zephyr-systems/libravdbd"
license=('custom')
provides=('libravdbd')
conflicts=('libravdbd')

source_x86_64=("libravdbd-linux-x86_64::https://github.com/xDarkicex/homebrew-openclaw-libravdb-memory/releases/download/v${pkgver}/libravdbd-linux-amd64")
source_aarch64=("libravdbd-linux-aarch64::https://github.com/xDarkicex/homebrew-openclaw-libravdb-memory/releases/download/v${pkgver}/libravdbd-linux-arm64")
source=("provision.sh::https://github.com/xDarkicex/homebrew-openclaw-libravdb-memory/releases/download/v${pkgver}/provision.sh"
        "nomic-embed-text-v1.5.Q8_0.gguf::https://huggingface.co/nomic-ai/nomic-embed-text-v1.5-GGUF/resolve/main/nomic-embed-text-v1.5.Q8_0.gguf")

sha256sums_x86_64=('be5be7e85c1ec3572207cb5676182164abc437841260070fd4fed451757b1032')
sha256sums_aarch64=('bc59ac1f0244122f1c439fbc6d620f93c3347ce5f8f1131f9f9860002ea8e15f')
sha256sums=('9775a425df4592b8962a044b802781db2b3691022e38eb88f9e16ac24ef98333'
            '3e24342164b3d94991ba9692fdc0dd08e3fd7362e0aacc396a9a5c54a544c3b7')

package() {
    install -Dm755 "${srcdir}/libravdbd-linux-${CARCH}" "${pkgdir}/usr/bin/libravdbd"
    install -Dm755 "${srcdir}/provision.sh" "${pkgdir}/usr/lib/libravdbd/provision.sh"
    install -Dm644 "${srcdir}/../libravdbd.service" "${pkgdir}/usr/lib/systemd/user/libravdbd.service"

    # Install GGUF model — searched in <exe>/models/<profile>/ by resolveGGUFModelPath
    install -Dm644 "${srcdir}/nomic-embed-text-v1.5.Q8_0.gguf" \
        "${pkgdir}/usr/lib/libravdbd/models/nomic-embed-text-v1.5/nomic-embed-text-v1.5.Q8_0.gguf"

    # License
    mkdir -p "${pkgdir}/usr/share/licenses/${pkgname}"
    cat > "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE" <<'LICENSE'
libravdbd is distributed under a proprietary license.
See https://github.com/zephyr-systems/libravdbd for terms.
LICENSE
}
