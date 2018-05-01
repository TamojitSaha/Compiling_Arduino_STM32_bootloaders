# Introduction
This repo is a result of painstaking quest to find answer for **How to compile STM32duino bootloaders ?**
Here I walk you through some steps so that you can compile the [bootloaders](https://github.com/rogerclarkmelbourne/STM32duino-bootloader) provided by [Roger Clark](https://github.com/rogerclarkmelbourne). The steps shown here are for compiling in Windows platform.

# Procedure:
Follow the step carefully, so that you don't land up in soup.

Install [7z](https://www.7-zip.org/download.html) if you dont have.
If you already have WinAVR installed jump to [STEP 3](#step_3)

## STEP_1
Install WinAVR to get `make` command in Windows commandline from [here](http://winavr.sourceforge.net/download.html).

Download [this](https://github.com/TamojitSaha/Compiling_Arduino_STM32_bootloaders/raw/master/msys-1.0.dll) **DLL** file and keep the file in your WinAVR installation directory under *utils/bin/*. If you have installed in *C:/* directory then drop the file inside *C:\WinAVR-20100110\utils\bin*.

## STEP_2
Now download [this](https://drive.google.com/open?id=1UwgdbDHb4tuEc8PhKtAlPxB9ZGHike-d) zip, extract it, copy and paste the folders in the WinAVR installation directory. Yes! just replace the folders.

## STEP_3
In *System Variables* and *User Variables* under *Environment variables* click on *NEW* and add the following directory to the **PATH** variable:
* C:\WinAVR-20100110\utils\bin
* C:\WinAVR-20100110\bin

If it is already present skip this step.

## STEP_4(Optional)
Open command window and type `avr-gcc -v` and hit enter. 
The command prompt window should show `gcc version 4.8.0 20130306 (experimental) (GCC)` in the last line. 
If you see this you are good to go, else go through the previous steps once more.

## STEP_5
This step is the most essential to successfully compile bootloaders.
Download [this](https://drive.google.com/open?id=1CXIdgZg0YR4yTiWd5X4JvsHldB1uhKta) ARM GCC Toolchain and extract(just *extract here* wil do) it in your desired location. 
You should see a folder named **GNU Tools ARM Embedded**. Inside the subfolder named **4.8.3-2014q1**  you will find a folder named **arm-none-eabi**. Again moving inside you will find **bin** folder. 

For example:

If you have extracted the folder inside *C:\Program Files (x86)* then the directory address should read *C:\Program Files (x86)\GNU Tools ARM Embedded\4.8.3-2014q1\arm-none-eabi\bin\*

Copy the directory of this *bin* folder and add it to the **PATH** variable of *System Variables* and *User Variables*

## STEP_6(Optional)
Open command window and type `arm-none-eabi-gcc` and hit enter. If you see the following:

```shell
arm-none-eabi-gcc: fatal error: no input files

compilation terminated.
```

then, you have successfully completed [STEP 5](#step_5).

## STEP_7
Download the bootloaders from [here](https://github.com/rogerclarkmelbourne/STM32duino-bootloader). Extract it and open command window in the same directory. If you are unable to open the command window in the extracted **STM32duino-bootloader** folder run the [registry file](Add_Open_Command_Window_Here_as_Administrator.reg) provided in this repo. This will edit your registry, so that you can open command window in any of your desired directory. **It makes your life a lot easier!!**.

Right click on the bootloader directory and you show see *Open Command Window here as Administrator* option. Clicking on it will open a command window after a prompt. 

If you want to compile bootloader for **STM32F103C** variant then refer to the **make all.bat** file in the **STM32duino-bootloader** folder. In this case I am using the popular [BluePill](http://wiki.stm32duino.com/index.php?title=Blue_Pill) board where the LED is connected to *PC13* pin.

So in the command window run `make generic-pc13`. If everything goes good then you should see the following at the end of the process:

```shell
Copying to binaries folder

cp build/maple_boot.bin bootloader_only_binaries/generic_boot20_pc13.bin
```

Viola, you have successfully compiled bootloader in Windows !!!
Go and get two beers :beers:, will have it together. Cheers!!

N.B Your compiled binary file is stored in *bootloader_only_binaries* folder.
