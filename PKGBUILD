# Maintainer: Mubashshir <ahmubashshir@gmail.com>

_name=combomethod
pkgname=( python-$_name python2-$_name)
pkgbase=python-$_name
pkgver=1.0.12
pkgrel=1
pkgdesc='Decorator indicating a method is both a class and an instance method'

arch=(any)
url=https://bitbucket.org/jeunice/combomethod
license=(Apache)
depends=()

makedepends=(python-setuptools python2-setuptools)
source=(https://files.pythonhosted.org/packages/source/${_name::1}/$_name/$_name-$pkgver.zip)
sha256sums=(4975b436ffe3e0a2561b58e3e9d047a50f4b16c8d4956d6a3e6ce566d034dd5e)

build() {
    cd "$srcdir/$_name-$pkgver"
    python setup.py build
}
package_python-combomethod()
{
    depends=( python )
    cd "$srcdir/$_name-$pkgver"
    python setup.py install --root="$pkgdir" --optimize=1 --skip-build
}
package_python2-combomethod()
{
    depends=( python2 )
    cd "$srcdir/$_name-$pkgver"
    python setup.py install --root="$pkgdir" --optimize=1 --skip-build
}
