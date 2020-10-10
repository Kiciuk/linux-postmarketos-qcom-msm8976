
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=5.8_rc7
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8956/76 devices"
arch="aarch64"
url="https://github.com/Kiciuk/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel openssl-dev perl"

_carch="arm64"
# Source
_commit=09da3468ecd82dac57bdec8b0e9a9e1f8b5900f2
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

sha512sums="fdd85784f95fc0d41bd03e3beca72670ea8fe89f08edb8014b21e54a349ee603e98fe28cc62aabf396d26a191db30d6e777e8e653fe0b0136825bc5f24a7f2dd  linux-postmarketos-qcom-msm8976-e79c869542a69491d43eaec84e87577eabb69956.tar.gz
0d67f8c112dc7525910446dad3edbb67d7122f95f63b6dd038cd7e0e7dd69c55c29b715fa500b3318e63e16dc46725fb61b3fb3a58c514b2507f12d40c8b1b41  config-postmarketos-qcom-msm8976.aarch64"
