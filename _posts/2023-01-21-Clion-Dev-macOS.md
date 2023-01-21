# Setup CLion with STM32CubeMX project for STM32 Developement on macOS

Arduino IDE is very easy to handle but might not have some functionalities such as debugging, code completion and inlay hint. This would trouble you especially when you want to conduct a large project.

IDEs by Jetbrains like Intellij and Pycharm are very popular in the market. They have many advantages including charming UIs, good usability, safe refactoring. Doubtlessly, their IDEs could greatly assist our coding works. CLion is a cross-platform IDE for C/C++ development by Jetbrains, and I will guide you how to setup a basic development environment for STM32 in this tutorial.

## Tools

### Software

- A computer with macOS(for sure)
- CLion
- STM32CubeMX
- Homebrew
- MacPorts
  
### Hardware

- STM32 MCU
- ST-Link/J-Link

## Installations

### Prerequisites

You should have installed these tools before you continue the next step.

#### [CLion](https://www.jetbrains.com/clion/download/#section=mac)

> The version should be higher than 2019.2.

#### [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html#get-software)

>Downloading requires email verification.

- After you unzip the downloaded file, right-click the STM32CubeMX package and click ``Show Package Contents`` and right click to open the executable file inside the package.

#### [Homebrew](https://brew.sh/)

#### [MacPorts](https://www.macports.org/install.php)

#### ARM Toolchain

Run ``brew tap ArmMbed/homebrew-formulae`` and ``brew install arm-none-eabi-gcc`` in the terminal.

>Validate the installation: ``arm-none-eabi-gcc -v``.

#### OpenOCD

``brew install open-ocd``
