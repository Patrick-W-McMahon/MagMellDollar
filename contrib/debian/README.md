
Debian
====================
This directory contains files used to package magmelldollard/magmelldollar-qt
for Debian-based Linux systems. If you compile magmelldollard/magmelldollar-qt yourself, there are some useful files here.

## magmelldollar: URI support ##


magmelldollar-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install magmelldollar-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your magmelldollar-qt binary to `/usr/bin`
and the `../../share/pixmaps/magmelldollar128.png` to `/usr/share/pixmaps`

magmelldollar-qt.protocol (KDE)

