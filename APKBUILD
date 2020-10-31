# Maintainer: Junak <junak.pub@gmail.com>
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=5.9_rc7
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8953 devices"
arch="aarch64"
url="https://github.com/msm8953-mainline/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel openssl-dev perl"

_carch="arm64"
# Source
_commit=313a352b8cac46ebd5821349c9aa9d556d263753
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

sha512sums="0df4264a0a5bfd9c40ff240eb6b4fc753e56fbcae34ea1d22534bedd7314b2b30b16f6f7f79cd8d6a0827a49ccb59aa73fef805188a9766c8a894f9dea42fb71  linux-postmarketos-qcom-msm8976-313a352b8cac46ebd5821349c9aa9d556d263753.tar.gz
63c9845c890e15b0c75029c314d568539c1e0542bf0df8c9f27c3e0096e1d84f5ca84bf0d526e61fba400223320f6648188627d4b1951f868085ab0956f4e91d  config-postmarketos-qcom-msm8976.aarch64"
