
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=5.3_rc2
pkgrel=0
pkgdesc="Mainline kernel fork for Qualcomm MSM8976 devices"
arch="aarch64"
url="https://github.com/msm8953-mainline/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex  openssl-dev perl"

_carch="arm64"
# Source
_commit=9d083e28e101c1f22f2e0757fdb6883a33276402
source="
	$pkgname-$_commit.tar.gz::https://github.com/Kiciuk/kernel-upstream/archive/$_commit.tar.gz
	config-$_flavor.$arch
	linux-010-fix-build-failure-against-gcc-10.patch
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



sha512sums="6abc2924d6e9e8b61a9ec7e9d70c897f509d30788ac307bbd25d86786e824787b95d5380a93a0b5f55d76e34b2a1a789b533d497a4b7f5bf62f8e9a7313f4fcb  linux-postmarketos-qcom-msm8976-9d083e28e101c1f22f2e0757fdb6883a33276402.tar.gz
714dea2b113a00117aac9444802cebc154762d0d14d34da863867544e7ebf660abca95df83dd0880e7c926138f56b52a37cde2208a196dd984f4b90b87e621e9  config-postmarketos-qcom-msm8976.aarch64
c0afed20605890284d0981af036651b48206e13dc64c4230142b6db6e75fa75947fa0fdf237259a82331ece60833d7bc9b6245dbb23c6fd2eab9795c84f54dd7  linux-010-fix-build-failure-against-gcc-10.patch"
