## Setting up Visual Studio Code for ESP32 IDF (FreeRTOS)


<p align="center">
    <img src="https://atmosphereiot.com/images/Third-Party-Logos/EspressifLogoFullGlow.png" alt="Logo" height=100 ><span width=50></span>
    <img src="https://raw.githubusercontent.com/github/explore/d8ae27ae1595c46559429174e7660c80fd92a767/topics/macos/macos.png" alt="Logo" width=100 >

  <h3 align="center">ESP32 IoT IDF</h3>

  <p align="center">
    Xtensa IoT framework.
  </p>
</p>

## Steps

- [Download and install VSC](#download-and-install-vsc)
- [Install VSC Extensions](#install-vsc-extensions)
- [Setup Toolchain](#setup-toolchain)
- [Setup and verify environment variables](#setup-and-verify-environment-variables)
- [Create project](#create-project)
- [Configure ESP32](#configure-esp32)

## Download and install VSC

Below link will point to the latest version of the Microsoft code editor which is free and open source. <br/>
Go ahead and download the latest release.<br/>
<br/>
<a href="https://code.visualstudio.com/"><span>Visual Studio Code</span></a>


## Install VSC extensions

After the installation open editor and go to 'Extensions' section to browse all available vsc extensions. <br/>
You need the following:<br/>

- C++
- Native Debug
- Code Outline or AL Outline (to display and navigate properties)

<img src="vsc-guide-1.bmp" >

## Setup toolchain

Next you need tools for compilation and linking your projects
Go to below link and follow instructions
https://docs.espressif.com/projects/esp-idf/en/feature-cmake/get-started/index.html#setup-toolchain

You need to download all-in-one esp-idf tools installer
<a href="https://dl.espressif.com/dl/esp-idf-tools-setup-1.1.exe">https://dl.espressif.com/dl/esp-idf-tools-setup-1.1.exe</a>
and get the latest ESP-IDF framework

<a href="https://docs.espressif.com/projects/esp-idf/en/feature-cmake/get-started/index.html#get-started-get-esp-idf">How to get ESP-IDF</a>

## Setup and verify environment variables

Make sure all path and idf variables are present and pointing to right locations. 
IDF_PATH is cruicial. 
You can use run-command way to set them up with `setx IDF_PATH "...your path to esp-idf folder"`

Example setup:
<br/>

<img src="vsc-guide-2.bmp" >
<img src="vsc-guide-3.bmp" >

**Note:**
If you want to quickly install whole environment with esp-idf framework - I created a batch file that will pull esp-idf from github repository, download it to user profile location (C:\Users\NAME\ESP32) and set the IDF_PATH automatically.<br/>
IMPORTANT: Please run this file as administrator!!<br/>
<a href="Resources/esp32setenv.bat">esp32setenv.bat</a>

**Make sure you install Git for Windows**<br/>
<a href="https://git-scm.com/downloads">Git Client download page</a>

## Create project

To create project that can properly compile you need the following:
### .vscode folder must be present in the root project directory

### .vscode folder must have the following files:
 - <a href=".vscode/c_cpp_properties.json">c_cpp_properties.json</a>
 - <a href=".vscode/settings.json">settings.json</a>
 - <a href=".vscode/tasks.json">tasks.json</a>

### to have key shortcuts you need to modify keybindings.json file
<a href="keybindings.json">keybindings.json</a> is located in C:\Users\....your profile name.... \AppData\Roaming\Code\User
  This file will allow to run compilation etc with just pressing keyshortcut

### alternatively and what I recommend - use the command line from terminal to compile,monitor and run your app
- `idf.py -p COM3 flash` -- wil compile and flash the board on port COM3
- `idf.py -p COM3 monitor` -- will display live serial monitor in console

if you want to flash and immefiately monitor use 
- `idf.py -p COM3 flash monitor`
 
`build` will build project with changes <br/>
`fullclean` will erase old files and refresh the whole build for new compilation <br/>

Typical project file structure: <br/>

<img src="vsc-guide-5.jpg">

### Important note:
**To open your project you must choose 'Open Folder' option** <br/>

<img src="open-folder-menu.jpg">

## Configure ESP32

Before compiling your project run the command to set up all necessary settings that IDF will use for your ESP32 chip.<br/>
In Integrated Terminal window run ` idf.py menuconfig`<br/>
If you are not in Powershell but in cmd.exe - you can run `powershell idf.py menuconfig`<br/>
<br/>
Example:<br/>
<img src="vsc-guide-4.bmp" ><br/>
<img src="esp-configmenu.jpg" ><br/>

Hit ESC until menuconfig asks about saving the configuration.<br/>
Confirm save.<br/>
<img src="menu-done.jpg" ><br/>

## CMake 

To use CMake environment your project must have CMakeLists.txt (just like Make files) in project directory

It usually contains f.ex. below lines 

```
set(MAIN_SRCS
    main/spi_master_example_main.c
    main/pretty_effect.c
    main/decode_image.c)

include($ENV{IDF_PATH}/tools/cmake/project.cmake)
project(spi_master)
```

You can change them to the project files you have.
Follow the examples provided in examples folder together with idf framework that you downloaded
There are CMakeList.txt files in different folders that will help you how to add directories and component references

I will post more later on CMake... ;)






