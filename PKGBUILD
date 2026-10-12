# Maintainer: arto <alessio@artoni.org>
pkgname=minilarbs-dwmblocks
_commit=8cedd220684064f1433749ed2a19a6184c22cf07
pkgver=0.r72.8cedd22
pkgrel=1
pkgdesc="minilarbs build of dwmblocks"
arch=(x86_64)
url=https://github.com/aartoni/dwmblocks
license=(ISC)
depends=(glibc libx11)
provides=(dwmblocks)
conflicts=(dwmblocks)
_patches=(
  dwmblocks-statuscmd-20210402-96cbb45.patch
  minilarbs-block-button.patch
  minilarbs-full-sleep.patch
  minilarbs-defer-signals.patch
)
source=("dwmblocks-$_commit.tar.gz::https://github.com/torrinfail/dwmblocks/archive/$_commit.tar.gz"
        blocks.h
        "${_patches[@]}")
b2sums=('65b4bdc04ce3d4e5b7c13145389fd46088f257c9a55bcb79a057877b72a1f3d8c16209ebd0595dae1f7ac15fab29b87375ed5d976995e241f4f4a114fe3d53bd'
        'dd19d7fd70f7a77e9fa7df170b2f4d644a874da98c332f2c93d8ca716d47ff35600923765070ab328e9e7c77a2ac2bb42aab1f270d54057b0a2742713dad0695'
        '91f9bebf7865f024a7f53fe49767e67baf4dfbe65537f743b56b20b4608bac2ebabec4cec9533eb0590c608022b4d8861118ce3f1ea7c16eb152d94b68fe974d'
        'a9401eef8c625ebd73619d5acb7d303a486ed0a8220d87d53ce435336988a0f304b5db755925dc521809dd3d75c8be6a0c477d05234a18738cc5faed46dfe6bd'
        '69be684142539f170f84bdc2946b247c1ceb726a1bea8c907dbbbba582df47c536a9eb22ffdc7a02eb307abf5729e0bd85ae38a6d16e9efbda9e6ea8decc4807'
        'aa4c4b6feb8cd42b5d40f259495a7599f7fb3f036153e17866bd11e0022a916fb71808c67940245d31bfebb75bd3468077eddd9db287a3561f7514ea5fdeae40')

prepare() {
  cd "dwmblocks-$_commit"
  local p
  for p in "${_patches[@]}"; do
    patch -Np1 -i "$srcdir/${p##*/}"
  done
  cp "$srcdir/blocks.h" .
  printf '%s\n' \
    'CFLAGS += -std=gnu99 $(PKG_CPPFLAGS) $(PKG_CFLAGS)' \
    'LDFLAGS := $(PKG_LDFLAGS) $(LDFLAGS)' >> Makefile
}

build() {
  make -C "dwmblocks-$_commit" \
    PKG_CPPFLAGS="$CPPFLAGS" PKG_CFLAGS="$CFLAGS" PKG_LDFLAGS="$LDFLAGS"
}

package() {
  make -C "dwmblocks-$_commit" PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 "dwmblocks-$_commit/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
