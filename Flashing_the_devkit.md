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



### Resources

1. https://www.st.com/resource/en/user_manual/dm00591354-discovery-kits-with-stm32mp157-mpus-stmicroelectronics.pdf
2. https://my.st.com/content/my_st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-utilities/stsw-link009.license=1610949972923.product=STSW-LINK009.version=2.0.1.html
3. https://wiki.st.com/stm32mpu/wiki/STM32MP15_Discovery_kits_-_Starter_Package
