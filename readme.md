Unoficial CM-11 for Sony Xperia U

Getting Started :

    curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > /root/bin/repo
    chmod 755 /root/bin/repo
    mkdir cm-11
    cd cm-11
    repo init -u git://github.com/CyanogenMod/android.git -b cm-11.0
    repo sync
    cd device
    mkdir sony
    cd sony
    git clone https://github.com/Andrewas/android_device_sony_kumquat.git -b cm-11.0 kumquat
    cd kumquat

Now connect your phone which have runing CM11 :

    ./extract-files.sh
    cd ../../..
    cd hardware
    git clone https://github.com/munjeni/android_hardware_semc.git -b master semc
    cd ..
    mkdir -p kernel/sony
    cd kernel/sony
    git clone https://github.com/munjeni/android_kernel_xperiago.git -b cm-11
    cd ../..

Patch android source code :

    patch -p1 < hardware/semc/patches/bionic.patch
    patch -p1 < hardware/semc/patches/bootable_recovery.patch
    patch -p1 < hardware/semc/patches/external_bluetooth_bluedroid.patch
    patch -p1 < hardware/semc/patches/framework_av.patch
    patch -p1 < hardware/semc/patches/framework_base.patch
    patch -p1 < hardware/semc/patches/framework_native.patch
    patch -p1 < hardware/semc/patches/hardware_libhardware.patch
    patch -p1 < hardware/semc/patches/hardware_libhardware_legacy.patch
    patch -p1 < hardware/semc/patches/system_core.patch

Our step is optional!!! Use only if you going to sync CM 11 source code daily, than simple revert each patch before you sync CM 11 source code :

    patch -p1 -R < hardware/semc/patches/bionic.patch
    patch -p1 -R < hardware/semc/patches/bootable_recovery.patch
    patch -p1 -R < hardware/semc/patches/external_bluetooth_bluedroid.patch
    patch -p1 -R < hardware/semc/patches/framework_av.patch
    patch -p1 -R < hardware/semc/patches/framework_base.patch
    patch -p1 -R < hardware/semc/patches/framework_native.patch
    patch -p1 -R < hardware/semc/patches/hardware_libhardware.patch
    patch -p1 -R < hardware/semc/patches/hardware_libhardware_legacy.patch
    patch -p1 -R < hardware/semc/patches/system_core.patch
    repo forall -p -c 'git checkout -f'
    repo sync
    patch -p1 < hardware/semc/patches/bionic.patch
    patch -p1 < hardware/semc/patches/bootable_recovery.patch
    patch -p1 < hardware/semc/patches/external_bluetooth_bluedroid.patch
    patch -p1 < hardware/semc/patches/framework_av.patch
    patch -p1 < hardware/semc/patches/framework_base.patch
    patch -p1 < hardware/semc/patches/framework_native.patch
    patch -p1 < hardware/semc/patches/hardware_libhardware.patch
    patch -p1 < hardware/semc/patches/hardware_libhardware_legacy.patch
    patch -p1 < hardware/semc/patches/system_core.patch

Download CM prebuilts :
   cd vendor/cm
   ./get-prebuilts
   cd ../..

You are ready to build :

    . build/envsetup.sh
    lunch cm_kumquat-userdebug
    make otapackage

ENJOY!
