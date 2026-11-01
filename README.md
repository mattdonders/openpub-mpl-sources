# OpenPub: MPL-2.0 source code

OpenPub (Mac App Store and Microsoft Store for Windows) links these MPL-2.0 libraries statically. This repository provides their
source code, as used in the app, under the Mozilla Public License 2.0.

| Library | Version | Changes | Upstream |
|---|---|---|---|
| libmspub | 0.1.5 | `patches/libmspub-text-id.patch` applied (already applied in `libmspub-0.1.5/`) | https://dev-www.libreoffice.org/src/libmspub/libmspub-0.1.5.tar.xz |
| librevenge | 0.0.6 | Mac: none. Windows: `patches/librevenge-msvc-stat.patch` (not applied in `librevenge-0.0.6/`, which is the unmodified source the Mac app uses) | https://sourceforge.net/projects/libwpd/files/librevenge/librevenge-0.0.6/ |

librevenge is dual-licensed MPL-2.0 / LGPL-2.1+; OpenPub uses it under MPL-2.0.

## The patches

`libmspub-text-id.patch` adds a `librevenge:mspub-text-id` property to each text object, so a
renderer can tell which text frames are linked boxes sharing one story.

`librevenge-msvc-stat.patch` (Windows build only) defines the POSIX `S_ISREG`/`S_ISDIR` macros, which the Microsoft C runtime's `<sys/stat.h>` lacks, in `src/lib/RVNGDirectoryStream.cpp`. To get the exact librevenge source used in OpenPub for Windows, apply it to `librevenge-0.0.6/` with `patch -p1`. The Windows app applies the same `libmspub-text-id.patch` as the Mac app.

Each library's own license file is inside its directory. Questions: matt@mattdonders.com
