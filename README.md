# pico-cmake-template

A simple and clean template for creating a C/C++ project for the Raspberry Pi Pico series using modern CMake.

This template is designed to be a self-contained starting point. It includes the official Raspberry Pi Pico SDK as a Git submodule, so you don't need to set up a system-wide SDK path.

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)![License](https://img.shields.io/badge/license-MIT-blue)

## Features

*   **Self-Contained**: Includes `pico-sdk` as a Git submodule, making the project portable and easy to set up.
*   **Modern CMake**: Uses modern CMake practices for clarity and maintainability.
*   **Clear Project Structure**: Separates your application code from the SDK and build files.
*   **Ready to Build**: Includes a simple "blink" example to get you started.
*   **Easy to Customize**: Designed to be easily extended with your own source files and libraries.

## Project Structure

```
pico-cmake-template/
├── lib/
│   ├── pico-sdk/          # Git submodule for the Pico SDK
│   └── pico_sdk_import.cmake # Helper to import the SDK
├── src/                   # Your application source code
│   ├── main.c
│   └── CMakeLists.txt
├── .gitignore             # Git ignore file
├── CMakeLists.txt         # Main CMake project file
└── README.md              # This file
```

## Prerequisites

Before you begin, ensure you have the following tools installed on your system:
*   [Git](https://git-scm.com/downloads)
*   [CMake](https://cmake.org/download/) (Version 3.13 or newer)
*   [ARM GCC Compiler Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-arm-embedded-toolchain/downloads) (`arm-none-eabi-gcc`)
*   Python 3 (for some SDK tools)

## Usage

### 1. Create your project from this template

Click the "**Use this template**" button at the top of this repository's GitHub page to create your own new repository.

### 2. Clone your new repository

Clone your newly created repository to your local machine. The `--recurse-submodules` flag is essential as it will also clone the `pico-sdk`.

```bash
git clone --recurse-submodules https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git
cd YOUR-REPOSITORY-NAME
```

**If you forgot `--recurse-submodules`**, you can initialize the submodules at any time with:

```bash
git submodule update --init
```

### 3. Configure the Project with CMake

Create a `build` directory and run CMake from within it to configure the project. This will generate the necessary build files (e.g., Makefiles).

```bash
mkdir build
cd build
cmake ..
```

*On Windows, you might need to specify the generator for your build tools (e.g., MinGW Makefiles or NMake Makefiles).*

### 4. Build the Project

Run `make` (or your chosen build tool) inside the `build` directory to compile your application.

```bash
make
```

After a successful build, you will find your firmware files in the `build/src/` directory, including:
*   `application.elf`
*   `application.uf2`

The `.uf2` file is the one you will use to flash your Raspberry Pi Pico.

### 5. Flash the Firmware to your Pico

1.  Press and hold the **BOOTSEL** button on your Pico.
2.  Connect the Pico to your computer via a USB cable.
3.  It will appear as a mass storage device (like a USB drive) named `RPI-RP2`.
4.  Drag and drop the `application.uf2` file from `build/src/` into the `RPI-RP2` drive.
5.  The Pico will automatically reboot and start running your program. The on-board LED should start blinking (not on Pico W or Pico 2 W as no `PICO_DEFAULT_LED_PIN`).

## Customizing Your Project

1.  **Change Project Name**: Edit the `project(pico_cmake_template_project ...)` line in the main `CMakeLists.txt` and the `add_executable(application ...)` line in `src/CMakeLists.txt` to your desired project name.
2.  **Add Your Code**: Add new `.c` or `.cpp` files to the `src/` directory.
3.  **Update `src/CMakeLists.txt`**: Add the new source files to the `add_executable()` command in `src/CMakeLists.txt`.
4.  **Link Libraries**: If you use additional hardware features (e.g., I2C, SPI), link the necessary libraries in `src/CMakeLists.txt`.

## License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.