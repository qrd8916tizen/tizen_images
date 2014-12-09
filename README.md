tizen_images
============

tizen file trees for qrd8916:
tizen/data.tgz
tizen/platform.tgz.00
tizen/platform.tgz.01
tizen/platform.tgz.02
tizen/platform.tgz.03
tizen/platform.tgz.04
tizen/platform.tgz.05
tizen/ums.tgz

kernel:
android/boot.img

How to install tizen to QRD8916

1. extract data
$sudo tar zxvf data.tgz
(Please note that you should use "sudo")

2. extract platform
$cat platform.tgz.00  platform.tgz.01  platform.tgz.02  platform.tgz.03  platform.tgz.04  platform.tgz.05 > platform.tgz
$sudo tar zxvf platform.tgz
(Please note that you should use "sudo")

3. extract ums
$sudo tar zxvf data.tgz
(Please note that you should use "sudo")

4. make tizen sparse images:
$sudo /home/user/tizen_images/tools/make_ext4fs -s -l 838860800 platform.simg platform
$sudo /home/user/tizen_images/tools/make_ext4fs -s -l 800000000 data.simg data
$sudo /home/user/tizen_images/tools/make_ext4fs -s -l 40000000 ums.simg usm
(Please use tools/make_ext4fs to make sparse image)

5. flash tizen sparse images to qrd8916
Boot qrd8916 into fastboot mode, then execute the following commands:
$sudo fastboot flash boot android/boot.img
$sudo fastboot erase system
$sudo fastboot flash system platform.simg
$sudo fastboot erase userdata
$sudo fastboot flash userdata data.simg
$sudo fastboot erase cache
$sudo fastboot flash cache ums.simg

6. Reboot the device to Tizen
$sudo fastboot reboot

