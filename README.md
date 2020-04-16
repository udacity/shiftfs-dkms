
# shiftfs-dkms

About:
------

This repo includes scripts to install shiftfs as a (linux-)kernel module via dkms.

#### About shiftfs:

shiftfs is a kernel filesystem for the linux kernel.
It provides easier uid/gid-shifting for containers and can be used for example with [LXD](https://linuxcontainers.org/lxd/).

* Further information on shiftfs:
https://discuss.linuxcontainers.org/t/trying-out-shiftfs/5155

* The shiftfs.c file included is from the Ubuntu Kernel repo (see also Credits):
https://git.launchpad.net/~ubuntu-kernel/ubuntu/+source/linux/+git/focal/tree/fs/shiftfs.c
   
 
* **Important Note:**     
shiftfs prevents the use of overlayfs inside a (lxd) container.   
Docker for example uses overlayfs, so this can be a problem.   
If you want to use overlayfs inside a container, you should not use shiftfs for now.   
Exception: This seems to be fixed in the ubuntu kernel, see [Bugreport 1846272 at Ubuntu](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1846272).       

  See also:
  - Section "Limitations" in first post of ["Trying out shiftfs" in the official forum of  LXD](https://discuss.linuxcontainers.org/t/trying-out-shiftfs/5155)
  - [Bugreport 1846272 at Ubuntu](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1846272) (including kernel patches to solve the problem)
  - [Issue 2 of this repo](https://github.com/toby63/shiftfs-dkms/issues/2) 
   



Content:
--------

* [Status](#status)
* [Changelog](#changelog)
* [Howto](#howto)
    * [Install](#install)
    * [Uninstall/Remove](#uninstallremove)
    * [Upgrade](#upgrade)
* [Usecases](#usecases)
* [Bugreports](#reporting-bugs)
* [Credits](#credits)
* [Copyright](#copyrightlicense)

Status:
-------

Version: | OS:            | Status:    | Date:
---      | ---            | ---        | ---
1.0      | Debian Testing | Runs/Works | March 2020

_Note: Should run on other Linux Distributions as well._

### Changelog:

See: [CHANGELOG](CHANGELOG)


Howto:
------

### Install:

#### Requirements:
 * dkms
 * kernel-headers (on debian for example: linux-headers-amd64)

#### 0. Check whether your kernel already includes shiftfs:

      # modinfo shiftfs

#### 1. Download this repo:
  
 With git:

      # git clone https://github.com/toby63/shiftfs-dkms.git shiftfs-dkms


#### 2. (Optional, but recommended) Update shiftfs.c:

 The shiftfs.c included might be outdated, thus the update-script.

 Run as user:

      # ./update1


#### 3. Compile and install shiftfs with dkms:

 Run as root or with sudo:

       # make -f Makefile.dkms

 Now you can check again, whether shiftfs is activated:

       # modinfo shiftfs

### Uninstall/Remove:  

   Run as root or with sudo:

       # ./remove1
       
### Upgrade:
 
 * Uninstall/Remove the old version:

   Run as root or with sudo:

       # ./remove1

 * (Optional) Update these scripts:
   
   _Note: See [Changelog](https://github.com/toby63/shiftfs-dkms/blob/master/CHANGELOG) whether an update is necessary._
   
   Run as user (inside the scripts folder):
       
       # git pull origin master
 
 * Repeat Step 2. and 3.


Usecases:
---------

* LXD:

  How to use shiftfs with LXD is described here:
  https://discuss.linuxcontainers.org/t/trying-out-shiftfs/5155


Reporting bugs:
---------------

 Report bugs here:
 https://github.com/toby63/shiftfs-dkms/issues


Credits:
--------

* shiftfs was made by:
   * James Bottomley
   * Seth Forshee <seth.forshee@canonical.com>
   * Christian Brauner <christian.brauner@ubuntu.com>

* Some files are based on the Debian package repo of bbswitch (https://salsa.debian.org/nvidia-team/bbswitch), including:
   * dkms.conf
   * Makefile
   * Makefile.dkms


Copyright/License:
------------------

General Public License, Version 2

See: [LICENSE](LICENSE)


