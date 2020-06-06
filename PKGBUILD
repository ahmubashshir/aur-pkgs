# Maintainer: Ahmad Hasan Mubashshir <ahmubashshir@gmail.com>
pkgname=update-notifier-service
pkgver=1
pkgrel=1
pkgdesc="Update notifier systemd user service and timer"
arch=('any')
license=('GPL')
install=update-notifier.install
depends=('update-notifier')
source=(
	'update-notifier.service'
	'update-notifier.timer'
	'update-notifier.hook'
)
sha256sums=('77860876f3dd1de8da0db947e10c0caa868bad1de487b2c06d13a7fcfd446b93'
            'eab72cc565c6bb1a594256c9efa6debe2551a03965be989108f950bde83158e4'
            '911fbad2abaeda9b20508a155404b240cef9fda6db06f8523da5ddf7c520adf2')
validpgpkeys=('916961EE198832DD70B628B356DB0538F60D951C')

package() {
	install -Dm 644 update-notifier.service "$pkgdir/usr/lib/systemd/user/update-notifier.service"
	install -Dm 644 update-notifier.timer "$pkgdir/usr/lib/systemd/user/update-notifier.timer"
	install -Dm 644 update-notifier.hook "$pkgdir/usr/share/libalpm/hooks/update-notifier.hook"
}
