# Maintainer: Mubashshir <ahmubashshir@gmail.com>
# pkg: github alexhuntley/Plots
pkgname=plots
_gitname=Plots

pkgver=0.6.0
pkgrel=2
pkgdesc="A graph plotting app for GNOME"

arch=(any)
url="https://github.com/alexhuntley/Plots"
license=('GPL')
depends=(
    'gtk3'
    'python-gobject'
    'python-opengl'
    'python-jinja'
    'python-numpy'
    'python-lark-parser'
    'python-freetype-py'
    'python-pyglm'
    'otf-latinmodern-math'
)

makedepends=('python-setuptools')
checkdepends=('python-pytest')

source=(
    "$pkgname-$pkgver.tar.gz::https://github.com/alexhuntley/$_gitname/archive/v$pkgver.tar.gz"
)
sha256sums=('cfc918dc68cf0e1a19494a23c4df9d8cc048b229717dfdc533922367c9e0c20a')

build() {
    cd "$_gitname-$pkgver"
    python setup.py build
}
check() {
    cd "$_gitname-$pkgver"
    python setup.py test
}

package() {
    cd "$_gitname-$pkgver"
    rm -rf build/lib/tests
    python setup.py install --root="$pkgdir" --optimize=1 --skip-build
    install -D -t "$pkgdir/usr/share/help/C/plots/" help/C/*
    install -Dm644 res/com.github.alexhuntley.Plots.svg "$pkgdir/usr/share/icons/hicolor/scalable/apps/plots.svg"
    install -Dm644 res/com.github.alexhuntley.Plots-symbolic.svg "$pkgdir/usr/share/icons/hicolor/symbolic/apps/plots-symbolic.svg"
    install -Dm644 res/com.github.alexhuntley.Plots.desktop "$pkgdir/usr/share/applications/plots.desktop"
    sed -Ei 's/^(Icon=).*$/\1plots/' "$pkgdir/usr/share/applications/plots.desktop"
}
