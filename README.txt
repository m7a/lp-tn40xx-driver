Ma_Sys.ma Build Instructions for tn40xx driver to run on Debian 12 Bookworm
===========================================================================

Contact: <info@masysma.net>

I am using the EDIMAX EN-9320TX-E 10 Gigabit Ethernet PCI Express Server
Adapter. It requires the `tn40xx` driver which is not upstream.

There are multiple repositories which collect relevant files and commits to
make use of this driver on modern Linux distributions.

 * <https://github.com/acooks/tn40xx-driver> -- this seems to be the initial
   one. Some useful pull requests are attached but the repository has not seen
   updates since quite some time.

 * <https://github.com/danbarke/tn40xx-driver> -- this repository contains the
   necessary header file with the firmware blob. If you have used the card
   previously already, you may already have this blob. If not, you can get it
   from here: <https://github.com/danbarke/tn40xx-driver/blob/release/tn40xx-004/MV88X3310_phy.h>
   with SHA256 of the header file being
   bcd4767fdde0ad31050d821ca05370266218792b892a2c7439a97b4c6ff1c89d.

 * <https://github.com/cahz/tn40xx-driver> -- This repository has almost all of
   the patches applied which you need to build this on a recent Linux.
   The missing patches are specific to the use of the MV88X3310 blob and
   are supplied by this repository.

This repository contains build instructions to create a Debian package for DKMS
installation of the driver when using MV88X3310. Add the blob header file
(see .gitignore for the expected file name), install the necessary dependencies
(`debuild`, `ant`, `config-package-dev`) and then build the package as follows:

	ant package

If everything works out, a `.deb` file is created that you can add to your own
local repository or directly install via `apt install ./*.deb` or something to
install the driver managed by DKMS.
