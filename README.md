# stm32mp157-dev-kit
Startup, notes, and files for playing with the STMicroelectronics 32bit Cortex A7 dev kit

ST Microelectronics website:
https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-mpu-eval-tools/stm32-mcu-mpu-eval-tools/stm32-discovery-kits/stm32mp157a-dk1.html#tools-software

The CubeIDE is the eclipse based IDE for the STM32mp157a devkit. 

Need to create an account before you can download and use any of the software. 

The serial connector comes off of ST-LINK CN11 on the devkit. This requires a driver to function:
https://www.st.com/en/development-tools/stsw-link009.html

Every download from ST requires a (free) account.	

After installing this driver instead of saying "COM6" and "stlink" is now says device unknown
procedure (plug in STLINK, then power)
If we reverse, and plug in power first, then it knows exactly what the device is.
