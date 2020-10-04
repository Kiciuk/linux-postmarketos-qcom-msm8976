
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=5.3_rc2
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8976 devices"
arch="aarch64"
url="https://github.com/msm8953-mainline/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel  openssl-dev perl"

_carch="arm64"
# Source
_commit=cdf0bd75763c2ffd0bd61d787c0ea667b3e7fe45
source="
	$pkgname-$_commit.tar.gz::https://github.com/Kiciuk/kernel-upstream/archive/$_commit.tar.gz
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



sha512sums="935085133c3eca14cbbe48c04235da90fd7ec6fef0ad0fd89df11163635ad9801b16482aa4f88b1811af68826a55881c6ca344c684faa36f7daeddf09d8fce71  linux-postmarketos-qcom-msm8976-cdf0bd75763c2ffd0bd61d787c0ea667b3e7fe45.tar.gz
620a06f1526f981375bd7b45ea2d40346a5eb333946e5070da98c06b2139fdebece405c309d82633906d92e0f2839f0f960264cb63ace7dc3cdd005dc9dfdd89  config-postmarketos-qcom-msm8976.aarch64"
