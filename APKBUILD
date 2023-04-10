
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=6.3
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8976 devices"
arch="aarch64"
url="https://github.com/Kiciuk/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel  openssl-dev perl"

_carch="arm64"
# Source
_commit=942ed4a124eaf5e42f0976babfdb8b0b8a2a3f6f
source="
	$pkgname-$_commit.tar.gz::https://github.com/Kiciuk/linux/archive/$_commit.tar.gz
	config-$_flavor.$arch
"
builddir="$srcdir/linux-$_commit"

prepare() {
	default_prepare
	cp "$srcdir/config-$_flavor.$arch" .config
}

build() {
	unset LDFLAGS
	make ARCH="$_carch" CC="${CC:-gcc}" \
		KBUILD_BUILD_VERSION=$((pkgrel + 1 ))
}

package() {
	mkdir -p "$pkgdir"/boot
	make zinstall modules_install dtbs_install \
		ARCH="$_carch" \
		INSTALL_PATH="$pkgdir"/boot \
		INSTALL_MOD_PATH="$pkgdir" \
		INSTALL_DTBS_PATH="$pkgdir"/usr/share/dtb
	rm -f "$pkgdir"/lib/modules/*/build "$pkgdir"/lib/modules/*/source

	install -D "$builddir"/include/config/kernel.release \
		"$pkgdir"/usr/share/kernel/$_flavor/kernel.release
}





sha512sums="
941a955ddffc9c6d28de1313ed8d93ce5c98645b073122581a88a759f2f30dee8527e4ad11ed0d838941f3361166ddf78a2ecbf1e8bf0e174b905f7c77dd9cbd  linux-postmarketos-qcom-msm8976-942ed4a124eaf5e42f0976babfdb8b0b8a2a3f6f.tar.gz
602ce4412aa72514f40145afe6ff6005673a7c47b9f669ed1c6e9d71a0dd7e30d8ba43b972488fd4f3bc7d7ae5779553e773524f5a88beb701cdc0efca2d3a8c  config-postmarketos-qcom-msm8976.aarch64
"
