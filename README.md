# QEMU SETUP AND KERNEL HACKING

### Installing Git 
```
sudo apt-get install git
git clone https://github.com/SudarsunKannan/AdvOS
cd AdvOS
```

### Set environmental variables
```
$BASE/source scripts/setvars.sh "trusty"
```

### Getting Kernel Source
We will be using linux-4.17 kernel this semester
```
cd $BASE
wget https://cdn.kernel.org/pub/linux/kernel/v4.x/linux-4.17.tar.xz
tar xf linux-4.17.tar.xz
```

### Instal required libraries
```
sudo apt-get install -y build-essential cmake libssl-dev bison flex
```

### Compiling and launching QEMU 
From the source directory set the environment variables.
trusty specifies the host systems linux version/codename; pass your own OS version name.
```
source scripts/setvars.sh "trusty"   
$BASE/scripts/compile_kern.sh
```

### Create the QEMU IMAGE  

Create the QEMU IMAGE only for the first time. You should
not create an image (which is your disk now) every time you will be
compiling and testing your kernel.

During installation, if prompted (y,n), enter yes
```
$BASE/scripts/qemu_create.sh  
```

### Setting your QEMU image 

Next, we will have to set password for the VM, and install required packages 
for the QEMU
```
cd $BASE 
source scripts/setvars.sh "trusty"
$BASE/scripts/mount_qemu.sh
cd $MOUNT_DIR   //Go to where the QEMU disk is mounted
sudo chroot .  //Set the disk as your root file system
passwd         //Add new password for the root user in the virtual machine
sudo apt-get install -y build-essential cmake libssl-dev  //Install packages
exit           //Unmount the QEMU disk
cd $BASE       
$BASE/scripts/umount_qemu.sh  //Unmount the QEMU disk
```

### Now launch the QEMU
This script will use the compiled 4.17 kernel to run the QEMU
```
$BASE/scripts/run_qemu.sh
```


### Copying data from your host to QEMU
If you want to copy some data between your machine and QEMU disk image, then use the following script for convenience
This scripts copies directories/files from your host machine to QEMU's root folder
```
$BASE/scripts/copy_data_to_qemu.sh FULL_PATH_OF_DIRECTORY_TO_COPY
```

### Killing the QEMU process
```
$BASE/scripts/killqemu.sh
```




