# Specification Toolchain for STM32

## 1 GNU Arm Embedded Toolchain - [Link](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm)
	This contains intagrated and validated package for GCC compiler, libraries and other tools for necessary for bare metal software development.
	arm-none-eabi-gcc --version
	
	Download Zip Package

## 2 Build System - [Link](http://gnuwin32.sourceforge.net/packages/make.htm)
	This is MAKE build system for windows. 
	Test make -version
	
	Download binaries and dependencies for windows.
## 3 Open On-Chip Debugger - [Link](https://gnutoolchains.com/arm-eabi/openocd/)
	Tool for communicate jtags and StLinks and similar flash devieces.
	openocd --version
	
	Download latest.

## 4 git - [Link](https://git-scm.com/download/win)
	Download portable one.
	
## 5 dev Environment
	The name is just my call. Simply create directory with following order.
	Export the files that just downloaded.
	
	dev-{envName}
	|_tools
		|_gcc-arm-none-eabi-10-2020-q4-major
		|_git
		|_make-3.81
			|_bin
			|_contrib
			|_man
			|_manifest
			|_share
		|_OpenOCD-20210407-0.10.0
	|_{projectName}
	
## 6 Configure Windows Path
	Add to path so we can call from commend line without giving full authorized path.
	
### To add gcc to path;
	- Copy bin folders path.
	- Environment Variables->User Variable for {name}->New->Variable name: ARMGCC_DIR Variable Value: gcc path
	- Environment Variables->User Variable->Path->New->%ARMGCC_DIR%
	
### To add MAKE to path;
	- Copy bin folder 
	- Environment Variables->User Variable->Path->New->bin folder path

### To add OpenOCD to path;
	- Copy bin folder path
	- Environment Variables->User Variable->Path->New->bin folder path

### To add git to path;
	- copy git bin folder path
	- Environment Variables->User Variable->Path->New->bin folder path
	- copy git->usr->bin
    - Environment Variables->User Variable->Path->New->bin folder path

## 7 Edit makefile
        **Generate project with CubeMX with selection of makefile as a deployment env.
    	To flash with openOCD need to add command to makefile. 
        interfaces and targets can find openocd->share->scripts folder.
#### Overall commands look like this;
```cmake
#######################################
# clean up
#######################################
clean:
	-rm -fR $(BUILD_DIR)

#######################################
# openocd
#######################################
flash: all
	openocd -f interface/stlink.cfg -f target/stm32f4x.cfg -c "program $(BUILD_DIR)/$(TARGET).elf verify reset exit"
```
## 8 VSCode
	- Install C/C++
	- Install Cortex Debug
	- Click win32 from bottom right corner modify;
### c_cpp_properties configs
```json
		{
		    "configurations": [
		        {
		            "name": "STM32F4",
		            "includePath": [
		                "${workspaceFolder}/**"
		            ],
		            "defines": [
		                "_DEBUG",
		                "UNICODE",
		                "_UNICODE",
		                "USE_HAL_DRIVER",
		                "STM32F429xx"
		            ],
		            "windowsSdkVersion": "10.0.18362.0",
		            "compilerPath": "${env:ARMGCC_DIR}/arm-none-eabi-gcc.exe",
		            "cStandard": "c11",
		            "cppStandard": "c++17",
		            "intelliSenseMode": "gcc-arm",
		            "compilerArgs": [
		                "-mcpu=cortex-m4",
		                "-mthumb"
		            ]
		        }
		    ],
		    "version": 4
}
```

## 9 Citiations
Most configs from this videos [YT-Link](https://www.youtube.com/channel/UCuigr_BEzX1g3Qvwq5QjPXg)
