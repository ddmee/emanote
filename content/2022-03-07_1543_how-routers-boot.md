# How routers boot

Found this well explained post at [Router 101](http://ofmodemsandmen.com/router101.html) ([internet archive link](https://web.archive.org/web/20220307153530/http://ofmodemsandmen.com/router101.html)) describing how the firmware and bootloader process for routers.

Interestingly it says that most routers basically follow the same design.

Basically there's some flash (non-volatile) memory in the device. It is partitioned into different sections. One section is the bootloader which is normally small. When the router boots, it loads this into RAM. The bootloader is a little program that runs that:

> "in it's most basic form it loads the router's firmware program from the flash memory into RAM and runs that. It is just that simple. The important thing to note here is that programs stored in flash memory are not run there but are first copied to RAM and then run."

Then it describes how the firmware partition is normally quite a large section of the flash. And to save space, it's typically compressed on flash, decompressed as it's put into memory. Then there's another section which contains non-compressed user-configuration changes to the firmware.

> " because the firmware program in flash memory is compressed we can not directly change it. Instead what is done is an area is set aside that holds all of the changed files and they are marked as changed. When the router is rebooted the bootloader checks these changed files and copies them into RAM at the proper location. The actual firmware program in flash memory is never altered but any altered files are copied into RAM during decompression so they appear in the RAM version of the firmware"

There's normally another partition that holds data-storage:

> "Data Storage - this area holds data that is unique to this router such as the various MAC addresses and wifi calibration data."

![[2022-03-07_router_flash_layout.png]]

Seems to fairly well describe how #openwrt is laided out. And indeed largely describes the [[2022-03-08_1522_glinet_convexa_b1300]]

The page also describes the recovery features to #debrick the router.

#bootloader
#firmware
#router
#partition
#flashlayout
