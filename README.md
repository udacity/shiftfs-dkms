
# shiftfs-dkms

Content:
--------
* [About](#about)
* [Important Note](#important-note)
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


About:
------

This repo provides scripts to install (linux-)kernel module **shiftfs** via dkms.   

_Note: shiftfs will maybe be included in the mainline kernel in the future.   
At this point (to my knowledge) only ubuntu included it in their kernel (see also: [check whether shiftfs is already included](#0-check-whether-your-kernel-already-includes-shiftfs))._

#### About shiftfs:

shiftfs is a kernel filesystem for the linux kernel.   
It provides easier uid/gid-shifting for containers and can be used for example with [LXD](https://linuxcontainers.org/lxd/) (see also: [Usecases](#usecases)).

* Further information on shiftfs:
https://discuss.linuxcontainers.org/t/trying-out-shiftfs/5155

* The shiftfs.c file included is from the Ubuntu Kernel repo:
https://git.launchpad.net/~ubuntu-kernel/ubuntu/+source/linux/+git/focal/tree/fs/shiftfs.c

* [Credits/Authors of shiftfs](#credits)
   
 
Important Note:
---------------

shiftfs can prevent the use of overlayfs **inside a container**.      
A usecase for this is running Docker with the overlayfs-storage driver **inside a lxd container**.   
Kernelpatches that solve this problem are available, but not included in the mainline kernel (and most distros kernels) (yet).   
For **workarounds and more information** see:
  - [Issue 2 of this repo](https://github.com/toby63/shiftfs-dkms/issues/2#issuecomment-614688392) 
  - [Bugreport 1846272 at Ubuntu](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1846272) 
  - [Ubuntu kernel commit](https://git.launchpad.net/~ubuntu-kernel/ubuntu/+source/linux/+git/focal/commit/fs/overlayfs?id=d24b8a547be1578cb5a200ad9ac57a258f0a9de1) (including kernel patches to solve the problem)
  - Section "Limitations" in first post of ["Trying out shiftfs" in the official forum of  LXD](https://discuss.linuxcontainers.org/t/trying-out-shiftfs/5155)
  

Status:
-------

Repo: | 
------- |
active | 

Version: | OS:            | Status:    | Date of last test:
---      | ---            | ---        | ---
1.0      | Debian Testing | Runs/Works | March 2020

_Note: Should run on other Linux Distributions as well._

### Changelog:

See: [CHANGELOG](CHANGELOG)


Howto:
------

### Install:

#### Requirements:
 * (Recommended) Recent Linux Kernel (>5.0)
 * dkms
 * kernel-headers (e.g. debian package (for 64-bit): linux-headers-amd64)

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
   
   (recent info in the shiftfs.c file (footer, tag: MODULE_AUTHOR))

* Some files are based on the Debian package repo of bbswitch (https://salsa.debian.org/nvidia-team/bbswitch), including:
   * dkms.conf
   * Makefile
   * Makefile.dkms
   
* Special thanks to:
   * Stéphane Graber @stgraber
   * Christian Brauner @brauner   
   
  for the helpful advice.


Copyright/License:
------------------

General Public License, Version 2

See: [LICENSE](LICENSE)
