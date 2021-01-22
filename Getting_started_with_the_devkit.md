# Getting Started with the DevKit

## Drivers
Most of this information comes, indirectly, from [1] 

    Before connecting STM32MP157A-DK1 or STM32MP157C-DK2 to a Windows® (7, 8, or 10) PC via USB, 
    a driver for ST-LINK/V2.1 must be installed (not required for Windows® 10). It is available from 
    the www.st.com website.In case the STM32MP157A-DK1 or STM32MP157C-DK2 Discovery kit is connected
    to the PC before the driver isinstalled, some Discovery kit interfaces may be declared as 
    “Unknown” in the PC device manager. In this case,the user must install the dedicated driver 
    files, and update the driver of the connected device from the devicemanager.

    The ST-LINK/V2-1 embeds a firmware upgrade mechanism for in-situ upgrade through the USB port. 
    As firmwaremay evolve during the lifetime of the ST-LINK/V2-1 product (addition of new 
    functionalities, bug fixes, or supportof new microprocessor families), it is recommended to visit
    periodically the www.st.com website before starting touse the STM32MP157A-DK1 or STM32MP157C-DK2
    Discovery kit to stay up-to-date with the latest firmwareversion.

The driver refered to by the above paragraphs can be found at [2] the "STSW-LINK009". Once downloaded, this can be
installed via the `stlink_winusb_install.bat` in administrator mode.

## Initial Booting

Once the drivers are installed you can initially boot the board and get output. The DevKit comes with
a pre-loaded µSD card and is good to boot from it on arival. 

### Setup

The wiring setup is pretty simple. 

  1. Connect power (USB-C near Ethernet), the PC is enough to run it. 
  2. Connect µUSB (near HDMI) for serial communication. 
  3. Start terminal output (see next section)
  4. reboot the board

Step 4 isn't strictly required, but the ordering is important and that means you'll initially miss the
boot logs, just by default. 

### Getting Terminal Output

Resource [4] contains all the information for terminal interactions for both Linux and Windows both local
and remote. Specifcally I setup for local on Windows 10. Initially I attempted PuTTY for serial 
communication, however that didn't work. Not sure why. However [TeraTerm](https://tera-term.en.lo4d.com/windows)
works perfectly. 
  
  1. Download TeraTerm and install on your PC
  2. Check device manager for the STLink COM port number: `STMicroelectronics STLink Virtual COM Port (COM6)`
  3. Open TeraTerm to COMX(X=6 for me) and set to a `115200` baud rate

### Initial Output

Once the boot is successful and TeraTerm is connected and gathering data as it should, you'll see something
along the lines of the below (truncated) output:

    NOTICE:  CPU: STM32MP157AAC Rev.B
    NOTICE:  Model: STMicroelectronics STM32MP157C-DK2 Discovery Board
    NOTICE:  Board: MB1272 Var1 Rev.C-01
    INFO:    Reset reason (0x14):
    INFO:      Pad Reset from NRST
    ...
    INFO:    SP_MIN: Initializing runtime services
    INFO:    SP_MIN: Preparing exit to normal world

    U-Boot 2018.11-stm32mp-r4 (Jun 25 2020 - 12:01:15 +0000)

    CPU: STM32MP157AAC Rev.B
    Model: STMicroelectronics STM32MP157C-DK2 Discovery Board
    ...
    XIP Kernel Image ... OK
    Using Device Tree in place at c4000000, end c4014f69

    Starting kernel ...

    [    0.000000] Booting Linux on physical CPU 0x0
    [    0.000000] Linux version 4.19.94 (oe-user@oe-host) (gcc version 8.2.0 (GCC)) #1 SMP PREEMPT Thu Jun 25 11:54:35 UTC 2020
    [    0.000000] CPU: ARMv7 Processor [410fc075] revision 5 (ARMv7), cr=10c5387d    
    ...

This shows everything is booting successfully and you have a 2018.11 u-boot with a 4.19.94 kernel.

## Flashing New Images

### Default Images

ST has various ["Packages"](https://wiki.st.com/stm32mpu/wiki/Which_STM32MPU_Embedded_Software_Package_better_suits_your_needs). In a nutshell:
  * Starter - This is prebuilt binaries 
  * Developer - Gives the ability to build a STLinux based Kernel, Opp-Tee applications and u-boot binary
  * Distribution - Yocto based build, full RFS as well as low level embedded portions

### Starter Images

Initially, it's important to understand flashing new images over anything else. In that spirt, we start with the Starter Package and the 
pregenerated images[6] that ST has to offer. Once the starter images tarball are downloaded and extracted we see the following file structure:

    stm32mp1-openstlinux-5-4-dunfell-mp1-20-11-12
    └──images
       └──stm32mp1
          ├── arm-trusted-firmware //binaries for FSBL partitions and serial boot mode
          |   ├── *.optee.stm32      // optee boot chain
          |   ├── *.serialboot.stm32 // STM32CubeProgrammer
          |   └── *.trusted.stm32    // trusted boot chain (default)
          ├── bootloader  // U-Boot binaries for FSBL, SSBL partitions and supported boot chains
          ├── flashlayout_st-image-weston // Flash layout files (text description of the partitions) for the supported boot chains on supported boot devices and boards
          ├── optee // Optee binaries for TEE partitions required for optee boot chains
          ├── scripts // helper scripts
          └── other files...  // binaries for other partitions on eMMC, microSD card, and NAND devices

### Install Programming Tool

The STM32CubeProgrammer tool is used to flash the STM32MP157x-DKx Discovery kit, the µSD card is default flash device, and the trusted boot chain is the default solution for booting.
The tools[7] can be downloaded from the link [here.](https://www.st.com/en/development-tools/stm32cubeprog.html). Once the package has been downloded, it can be extracted
and (on windows) `SetupSTM32CubeProgrammer-2.5.0.exe` can be run to install the tools. Follow the wizard to install the tools on your PC in the default paths. 

### Setup the board for flashing

Let's flash the downloaded image on the microSD card:

    Set the boot switches (1) to the off position
    Connect the USB Type-C™ (OTG) port (2) to the host PC that contains the downloaded image
    Insert the delivered microSD card into the dedicated slot (3)
    Connect the delivered power supply to the USB Type-C™ port (4)
    Press the reset button (5) to reset the board
    


## Resources

1. https://www.st.com/resource/en/user_manual/dm00591354-discovery-kits-with-stm32mp157-mpus-stmicroelectronics.pdf
2. https://my.st.com/content/my_st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-utilities/stsw-link009.license=1610949972923.product=STSW-LINK009.version=2.0.1.html
3. https://wiki.st.com/stm32mpu/wiki/STM32MP15_Discovery_kits_-_Starter_Package
4. https://wiki.st.com/stm32mpu/wiki/How_to_get_Terminal
5. https://wiki.st.com/stm32mpu/wiki/STM32MP15_Discovery_kits_-_Starter_Package#Downloading_the_image_and_flashing_it_on_the_board
6. https://st.com/content/ccc/resource/technical/software/firmware/group0/e2/88/93/37/bc/48/41/cb/STM32MP15_OpenSTLinux_Starter_Package/files/FLASH-stm32mp1-openstlinux-5-4-dunfell-mp1-20-11-12.tar.xz/jcr:content/translations/en.FLASH-stm32mp1-openstlinux-5-4-dunfell-mp1-20-11-12.tar.xz
7. https://wiki.st.com/stm32mpu/wiki/STM32MP15_Discovery_kits_-_Starter_Package#Installing_the_tools
