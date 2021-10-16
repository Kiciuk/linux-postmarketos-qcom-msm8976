
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=5.15_rc4
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8976 devices"
arch="aarch64"
url="https://github.com/Kiciuk/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel  openssl-dev perl"

_carch="arm64"
# Source
_commit=e0cddf75d1c7268021e6ebb2008ecc4c5fb1f1ce
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
1d2c58ae3475fb0f85968407dd561b2f3750f6ebe5931130efead5dba8465530c4a9f6fcf76b4edeb21bc1d01c43634ed0654cbf471a0ee4c64cc70c1fbf0f79  linux-postmarketos-qcom-msm8976-e0cddf75d1c7268021e6ebb2008ecc4c5fb1f1ce.tar.gz
ce9c0d0fe2efd030a7e34b51dc5a752bbac44bd045f5a3fe7d3a8e71b67eb6c9d1b9cb74252096066458c5c3ee57c20eed386f3ea6074ff3f7d0611e875a6672  config-postmarketos-qcom-msm8976.aarch64
"
