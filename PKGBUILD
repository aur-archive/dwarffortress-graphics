# Maintainer: gazj <garyjames82 [AT] gmail [DOT] com>
# Taken from original df PKGBUILD credit to below
# Daenyth <Daenyth+Arch [AT] gmail [DOT] com>
# djnm <nmihalich [at} gmail dott com>
pkgname=dwarffortress-graphics
pkgver=0.31.21
pkgrel=1
pkgdesc="A single-player fantasy game. You control a dwarven outpost or an adventurer in a randomly generated persistent world. Mike Mayday's graphical version"
arch=(i686 x86_64)
# WIP Thread: http://www.bay12forums.com/smf/index.php?topic=57492.0
url="http://mayday.w.staszic.waw.pl/df.php"
install="$pkgname.install"
license=('custom:dwarffortress')
conflicts="dwarffortress"
depends=(gtk2 mesa sdl_image sdl_ttf libsndfile openal)
if [[ $CARCH == 'x86_64' ]]; then
  depends=(lib32-gtk2 lib32-mesa lib32-sdl_image lib32-libsndfile lib32-openal lib32-libxdamage lib32-ncurses lib32-sdl_ttf)
  optdepends=('lib32-nvidia-utils: If you have nvidia graphics'
              'lib32-catalyst-utils: If you have ATI graphics')
fi
source=(http://www.foxjames.co.uk/linux/dfg/dfg_31_21_linux.tar.bz2
        dwarffortress dwarffortress.desktop dwarffortress.png)
md5sums=('3ffed409a12c96096839c02f1efc0ff6'
         'c19aacc31e8df354827db352fecfd200'
         'c8984d1eea6e409ecf339d6ee9e91e42'
         'b1d51f82400073af9bb179e34a9209d0')

build() {
  cd $srcdir/df_linux
  install -dm755 $pkgdir/opt/
  cp -r $srcdir/df_linux/ $pkgdir/opt/

  # Yay for precompiled stuff with junk permissions! :D
  find $pkgdir/opt/df_linux -type d -exec chmod 755 {} +
  find $pkgdir/opt/df_linux -type f -exec chmod 644 {} +

  install -Dm755 $srcdir/dwarffortress $pkgdir/usr/bin/dwarffortress

  chmod 755 $pkgdir/opt/df_linux/libs/Dwarf_Fortress

  install -d -m775 -o root -g games $pkgdir/opt/df_linux/data/save

  # This probably is overkill, but I don't know what specific files df needs permission for in here.
  chown -R root:games $pkgdir/opt/df_linux/data
  find $pkgdir/opt/df_linux/data -type d -exec chmod 775 {} +
  find $pkgdir/opt/df_linux/data -type f -exec chmod 664 {} +

  # Desktop launcher with icon
  install -Dm644 $srcdir/dwarffortress.desktop $pkgdir/usr/share/applications/dwarffortress.desktop
  install -Dm644 $srcdir/dwarffortress.png     $pkgdir/usr/share/pixmaps/dwarffortress.png

  install -Dm644 $srcdir/df_linux/readme.txt $pkgdir/usr/share/licenses/dwarffortress/readme.txt
}
# vim:set ts=2 sw=2 et:
