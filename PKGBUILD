# Maintainer: Ahmad Hasan Mubashshir <ahmubashshir@gmail.com>
# from: git

pkgname=(
   zapret-{nfqws,tpws,common}-git
)
pkgbase=zapret-git
pkgver=r499.ba5bde8
pkgrel=1
pkgdesc="Bypass deep packet inspection."
arch=('x86_64')
url="https://github.com/bol-van/zapret"
license=('GPL')
depends=('systemd' 'ipset' 'curl' 'iptables')
makedepends=('libnetfilter_queue' 'git')
provides=('zapret' 'zapret-git')
conflicts=('zapret')
source=(
   "zapret::git+https://github.com/bol-van/zapret.git"
   "sysusers.conf"
)
sha256sums=('SKIP'
            '25c309e2ec545c9ee53759e23961c8a3f02708a7ba8dcbabab6eb681a36c03c0')
pkgver()
{
   cd "$srcdir/${pkgbase%-git}"
   (  set -o pipefail
      git describe --tags --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
      printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
   )
   pkgrel=$(git diff --shortstat|cut -d' ' -f2)
}
build()
{
    cd "$srcdir/${pkgbase%-git}"
    make
}
_symlink() {
   mkdir -pm755 "$pkgdir/usr/bin"
   ln -s "/opt/zapret/$1" "$pkgdir/usr/bin/${1##*/}"
}

_set_config() {
   local _cfg="$pkgdir/opt/zapret/config"
   if grep -q "^#$1=" "$_cfg";then
      sed -i "/^#$1/s/#//" "$_cfg"
   fi
   sed -i "/^$1=/c\\$1=$(printf '%q' "$2")" "$_cfg"
}

package_zapret-common-git()
{
   depends=('systemd' 'ipset' 'curl' 'iptables' 'zapret-git')
   provides=('zapret-common')
   conflicts=('zapret-common')

   cd "$srcdir/${pkgbase%-git}"

   for n in ip2net mdig;do
      install -Dm755 "binaries/my/$n" "$pkgdir/opt/zapret/$n/$n"
   done
   install -Dm644 init.d/systemd/*  -t "$pkgdir/usr/lib/systemd/system"
   install -Dm755 init.d/sysv/*     -t "$pkgdir/opt/zapret/init.d/sysv"
   install -Dm755 ipset/*           -t "$pkgdir/opt/zapret/ipset"
   install -Dm644 common/*          -t "$pkgdir/opt/zapret/common"
   install -Dm644 "$srcdir/sysusers.conf" "$pkgdir/usr/lib/sysusers.d/zapret.conf"
   sed -i '1s/$/\n\nWS_USER=zapret/' "$pkgdir/opt/zapret/init.d/sysv/functions"
   _symlink init.d/sysv/zapret
}

package_zapret-nfqws-git() {

   depends=('libnetfilter_queue' 'zapret-common-git')
   provides+=('zapret-nfqws')
   conflicts+=('zapret-nfqws')
   backup=('opt/zapret/config.nfqws')

   cd "$srcdir/${pkgbase%-git}"

   install -Dm644 config               "$pkgdir/opt/zapret/config.nfqws"
   install -Dm755 "binaries/my/nfqws" "$pkgdir/opt/zapret/nfq/nfqws"
   ln -s config.nfqws "$pkgdir/opt/zapret/config"

   _symlink nfq/nfqws

   _set_config FWTYPE iptables
   _set_config MODE nfqws
   _set_config MODE_HTTP_KEEPALIVE 1
   _set_config MODE_HTTPS 1
   _set_config MODE_HTTP 1
}

package_zapret-tpws-git() {
   depends=('zapret-common-git')
   provides+=('zapret-tpws')
   conflicts+=('zapret-tpws')
   backup=('opt/zapret/config.tpws')

   cd "$srcdir/${pkgbase%-git}"

   install -Dm644 config               "$pkgdir/opt/zapret/config.tpws"
   install -Dm755 "binaries/my/tpws" "$pkgdir/opt/zapret/tpws/tpws"
   ln -s config.tpws "$pkgdir/opt/zapret/config"

   _symlink tpws/tpws

   _set_config FWTYPE iptables
   _set_config MODE tpws
   _set_config MODE_HTTP_KEEPALIVE 1
   _set_config MODE_HTTPS 1
   _set_config MODE_HTTP 1
}
