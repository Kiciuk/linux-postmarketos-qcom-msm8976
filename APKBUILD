
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=5.10_25
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8976 devices"
arch="aarch64"
url="https://github.com/msm8953-mainline/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel  openssl-dev perl"

_carch="arm64"
# Source
_commit=986e6d44b89c573c3aa98b12f7f4bec4e9138588
source="
	$pkgname-$_commit.tar.gz::https://github.com/Kiciuk/linux/archive/$_commit.tar.gz
	config-$_flavor.$arch
"
builddir="$srcdir/kernel-upstream-$_commit"

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




