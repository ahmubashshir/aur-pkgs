# Maintainer: Ahmad Hasan Mubashshir <ahmubashshir@gmail.com>
# from: github
# what: openresty/lua-resty-lrucache
# match! rc[0-9]*$

pkgname=lua-resty-lrucache
pkgver=0.15
pkgrel=1

pkgdesc='Lua lrucache for nginx lua module'
arch=('any')
depends=('luajit')
url="https://github.com/openresty/lua-resty-lrucache"
license=('BSD')

source=("$pkgname-$pkgver.tar.gz::https://github.com/openresty/$pkgname/archive/v$pkgver.tar.gz")

sha256sums=('8cf1a22e0d5b8f35cb0b2e14c58fcb3aa505a8fb6e956817f0cdb1f06593f072')

build() {
	cd "$pkgname-$pkgver"
	make
}

package() {
	cd "$pkgname-$pkgver"
	make DESTDIR="$pkgdir" PREFIX=/usr LUA_LIB_DIR='$(PREFIX)/share/lua/$(LUA_VERSION)' LUA_VERSION=5.1 install
}
