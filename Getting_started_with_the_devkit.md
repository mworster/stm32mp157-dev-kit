# Getting Started with the DevKit

## Drivers
Most of this information comes, indirectly, from [1] 

    Before connecting STM32MP157A-DK1 or STM32MP157C-DK2 to a Windows® (7, 8, or 10) PC via USB, 
    a driver for ST-LINK/V2.1 must be installed (not required for Windows® 10). It is available from 
    the www.st.com website.In case the STM32MP157A-DK1 or STM32MP157C-DK2 Discovery kit is connected
    to the PC before the driver isinstalled, some Discovery kit interfaces may be declared as 
    “Unknown” in the PC device manager. In this case,the user must install the dedicated driver 
    files, and update the driver of the connected device from the devicemanager.

The driver refered to by the above paragraph can be found at [2] the "STSW-LINK009". Once downloaded, this can be
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

## Resources

1. https://www.st.com/resource/en/user_manual/dm00591354-discovery-kits-with-stm32mp157-mpus-stmicroelectronics.pdf
2. https://my.st.com/content/my_st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-utilities/stsw-link009.license=1610949972923.product=STSW-LINK009.version=2.0.1.html
3. https://wiki.st.com/stm32mpu/wiki/STM32MP15_Discovery_kits_-_Starter_Package
4. https://wiki.st.com/stm32mpu/wiki/How_to_get_Terminal
