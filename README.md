# meta-swid-5
PHYTEC BSP-Yocto-NXP-I.MX93-PD24.1.1 adapation project for  GORGY/BODET

Introduction
------------
This is a short description of the steps to take to build the BSP

Build
-----
Follow the steps bellow to build the BSP.

1. Create an empty folder to build the BSP in.
   host$ mkdir ~/yocto
   host$ cd ~/yocto

2. Get our phyLinux script to check out the BSP-Yocto-Ampliphy-i.MX6-PD21.1.0
   BSP.
   host$ wget https://download.phytec.de/Software/Linux/Yocto/Tools/phyLinux
   host$ chmod +x phyLinux
   host$ ./phyLinux init -p imx93 -r BSP-Yocto-NXP-i.MX93-PD24.1.1

3. Clone the meta-swid-5 layer into your sources directory.
   host$ git clone git@github.com:phytec/meta-swid-5.git sources/meta-swid-5

4. Source the environment.
   host$ source sources/poky/oe-init-build-env

5. Enable the newly added layer in your bblayers.conf by adding following line
   to conf/bblayers.conf:
   BBLAYERS += " ${OEROOT}/../meta-swid-5"

6. Build one of the available machines and images.
   host$ bitbake phytec-qt5demo-image


After that the build image can be found under
deploy/images/<machine-name>/ .
