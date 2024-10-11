# meta-swid-5
PHYTEC BSP-Yocto-NXP-I.MX93-PD24.2.0 adapation project for  GORGY/BODET

Introduction
------------
This is a short description of the steps to take to build the BSP

Build
-----
Follow the steps bellow to build the BSP with ADIN1300 support.

1. Create an empty folder to build the BSP in.
   host$ mkdir ~/yocto
   host$ cd ~/yocto

2. Get our phyLinux script to check out the BSP-Yocto-NXP-i.MX93-PD24.2.0
   BSP.
   host$ wget https://download.phytec.de/Software/Linux/Yocto/Tools/phyLinux
   host$ chmod +x phyLinux
   host$ ./phyLinux init -p imx93 -r BSP-Yocto-NXP-i.MX93-PD24.2.0

3. Clone the meta-swid-5 layer into your sources directory.
   host$ git clone git@github.com:phytec/meta-swid-5.git sources/meta-swid-5 --branch scarthgap

4. Source the environment.
   host$ source sources/poky/oe-init-build-env

5. Enable the newly added layer in your bblayers.conf by adding following line
   to conf/bblayers.conf:
   BBLAYERS += " ${OEROOT}/../meta-swid-5"

6. Build one of the available machines and images.
   host$ bitbake phytec-qt5demo-image


After that the build image can be found under
deploy-ampliphy-vendor-wayland/images/<machine-name>/ .

WARNING : devtool modify u-boot-imx doesn't work for BSP-Yocto-NXP-i.MX93-PD24.2.0. 
To modify u-boot you have to proceed by patch. 

1. Clone the repository on a workspace : host$ git clone git://git.phytec.de/u-boot-imx

2. Apply the patch : host$ cd u-boot-imx host$ git am ~/yocto/sources/meta-swid-5/recipes-bsp/u-boot/u-boot-imx/0001-Adaptation-for-KSP-0741.patch

3. Modify and commit your changes

4. Create patches : host$ git format-patch -X where X is the number of commit you did

5. Put the patches on ~/yocto/sources/meta-swid-5/recipes-bsp/u-boot/u-boot-imx/

6. Add them on ~/yocto/sources/meta-swid-5/recipes-bsp/u-boot/u-boot-imx/u-boot-imx_%.bbappend : SRC_URI += "file://PatchName.patch"


