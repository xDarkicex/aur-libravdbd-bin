# Maintainer: xDarkicex <contact@darkicex.com>
# This PKGBUILD downloads the prebuilt libravdbd binary from the upstream
# release and installs it. Models and ONNX Runtime are not bundled — run
# provision.sh after install to download them.

pkgname=libravdbd-bin
pkgver=1.9.3
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

sha256sums_x86_64=('317a3f9df96ea4b19d2c65212e694c4f2a71bcade577c9d759676b47b2a71865')
sha256sums_aarch64=('c9cb031ddf44ffddf885013682e7beb724b125edf87e0d03f6bb5f49fed373ab')
sha256sums=('297b24e979de3fc70cda1dbdf3c47403c0ac178a7d1d1f402e8debb978b9d758'
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
LIBRAVDB END USER LICENSE AGREEMENT (EULA)
Copyright (c) 2026 Zephyr Systems. All rights reserved.

1. DEFINITIONS: "Software" refers to the compiled binary files and
   accompanying documentation distributed as libravdbd (the LibraVDB
   vector service daemon). "Source Code" refers to the underlying
   human-readable Go source files, which remain strictly proprietary
   and confidential.

2. LICENSE GRANT: Subject to the terms of this Agreement, Licensor
   grants Licensee a non-exclusive, non-transferable, revocable
   license to download, install, and execute the pre-compiled binary
   form of the Software solely for personal, educational, or internal
   evaluation purposes.

3. RESTRICTIONS: Licensee explicitly agrees NOT to, and shall not
   permit any third party or autonomous agent to:
   (a) Decompile, disassemble, reverse engineer, decrypt, or otherwise
       attempt to derive or reconstruct the Source Code or algorithmic
       logic of the Software binaries;
   (b) Modify, adapt, tamper with, or create derivative works based on
       the Software;
   (c) Redistribute, sell, rent, lease, sublicense, or publicly host
       the Software as a managed service without explicit, prior
       written commercial authorization from the Licensor;
   (d) Remove, alter, or obscure any copyright notices, trademarks, or
       proprietary legends contained within the Software.

4. INTELLECTUAL PROPERTY: Licensee acknowledges that 100% of the
   Source Code, engineering designs, mathematical scoring formulas,
   and proprietary logic are and shall remain the sole and exclusive
   intellectual property of the Licensor. No title or ownership of the
   Source Code is transferred under this Agreement.

5. TERMINATION: This license terminates automatically and instantly
   upon any violation of the restrictions outlined in Section 3.

6. DISCLAIMER OF WARRANTY: THE SOFTWARE IS PROVIDED "AS IS", WITHOUT
   WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED
   TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR
   PURPOSE, AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
   COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES, OR OTHER
   LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT, OR OTHERWISE,
   ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE
   OR OTHER DEALINGS IN THE SOFTWARE.
LICENSE
}
