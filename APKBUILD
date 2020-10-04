
# Kernel config based on: arch/arm64/configs/defconfig

_flavor="postmarketos-qcom-msm8976"
pkgname=linux-$_flavor
pkgver=5.4_rc3
pkgrel=1
pkgdesc="Mainline kernel fork for Qualcomm MSM8976 devices"
arch="aarch64"
url="https://github.com/msm8953-mainline/linux"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native pmb:kconfigcheck-anbox"
makedepends="bison findutils flex installkernel  openssl-dev perl"

_carch="arm64"
# Source
_commit=57158a71d51e0e72423f7c3b6b9eda0d6962a2c2
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



sha512sums="889fa7d5769949b76c8345e3dd4068024fe77f2c29ed1288abeacf996695836c42105d65e25e36613477b819500f7bdb03c163ed2b48df8bd15736b20d3b32b3  linux-postmarketos-qcom-msm8976-57158a71d51e0e72423f7c3b6b9eda0d6962a2c2.tar.gz
e49f327e29963f7a7cd9f52709624b71693ff192699f03508310edb3eddf472a9639ee8ad7a40f9d46cd391401c8095b8622a3d8bdb44f01ffeacca2f1b1512e  config-postmarketos-qcom-msm8976.aarch64"
