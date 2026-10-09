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
_patches=()
source=("dwmblocks-$_commit.tar.gz::https://github.com/torrinfail/dwmblocks/archive/$_commit.tar.gz"
        blocks.h
        "${_patches[@]}")
b2sums=('65b4bdc04ce3d4e5b7c13145389fd46088f257c9a55bcb79a057877b72a1f3d8c16209ebd0595dae1f7ac15fab29b87375ed5d976995e241f4f4a114fe3d53bd'
        '932dba9a7a94c02c0d6c19c96efae3b04da9266559254b10dc1117470c2df65cabb83a4e3e35cd42909c26cb0e31e63fb1c37b43b7c9e74470d5aeb6330f097a')

prepare() {
  cd "dwmblocks-$_commit"
  local p
  for p in "${_patches[@]}"; do
    patch -Np1 -i "$srcdir/${p##*/}"
  done
  cp "$srcdir/blocks.h" .
  printf '%s\n' 'CFLAGS += -std=gnu99 $(PKG_CPPFLAGS) $(PKG_CFLAGS)' 'LDFLAGS += $(PKG_LDFLAGS)' >> Makefile
}

build() {
  make -C "dwmblocks-$_commit" \
    PKG_CPPFLAGS="$CPPFLAGS" PKG_CFLAGS="$CFLAGS" PKG_LDFLAGS="$LDFLAGS"
}

package() {
  make -C "dwmblocks-$_commit" PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 "dwmblocks-$_commit/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
