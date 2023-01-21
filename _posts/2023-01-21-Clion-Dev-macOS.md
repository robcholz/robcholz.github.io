# Setup CLion with STM32CubeMX project for STM32 Developement on macOS

Keil is very easy to handle for embedded development but might not have some functionalities such as code completion and inlay hint. This would trouble you especially when you want to conduct a big project.

IDEs by Jetbrains like Intellij and Pycharm are very popular in the market. They have many advantages including charming UIs, good usability, safe refactoring. Doubtlessly, their IDEs could greatly assist your coding works. CLion is a cross-platform IDE for C/C++ development by Jetbrains, and I will guide you to setup a basic development environment for STM32 in this tutorial.

## Tools

### Software

- A computer with macOS(for sure)
- CLion
- STM32CubeMX
- Homebrew
  
### Hardware

- STM32 MCU
- ST-Link/J-Link

## Installations

### Prerequisites

#### [CLion](https://www.jetbrains.com/clion/download/#section=mac)

> The version should be higher than 2019.2.

#### [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html#get-software)

>Downloading requires email verification.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/open_package.png" width="350">
</p>

- After you unzip the downloaded file, right-click the STM32CubeMX package and click `Show Package Contents` and right click to open the executable file inside the package.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/malware_issue.png" width="350">
</p>

- There will be an error window popped up. Click `Cancel`.
  
<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/privacy_setting.png" width="350">
</p>

- Open `Security & Privacy` in `System Preferences` and click `Allow Anyway`.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/open_cubemx.png" width="350">
</p>
  
- Open STM32CubeMX executable file again in the package and click `Open`.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/installation_wizard.png" width="350">
</p>

- Install STM32CubeMX.
  
#### [Homebrew](https://brew.sh/)

>Validate the installation `brew -v`.

You should have installed these tools above before you continue the next step.

#### ARM Toolchain

- Run `brew tap ArmMbed/homebrew-formulae` and `brew install arm-none-eabi-gcc` in the terminal.

>Validate the installation: `arm-none-eabi-gcc -v`.

#### OpenOCD

`brew install open-ocd`

>Validate the installation: `openocd -v`.

## CLion Configurations

### OpenOCD & STM32CubeMX Paths

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/embedded_dev_tools_set.png" width="350">
</p>

- Generally, both of your OpenOCD and CubeMX locations should be as same as me. Remember to test your paths by clicking `Test`.

### Toolchains

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/toolchains.png" width="350">
</p>

- Set build tools, C/C++ compilers and debuggers. You should use `Bundled GDB` or like me, manually set another GDB path for `Debugger` option.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/new_project.png" width="350">
</p>

- Create a new `STM32CubeMX` project.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/select_board_type.png" width="350">
</p>

- Here, you can either click `Use` to choose a board type or click `Skip` to choose one later.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/open_with_cubemx.png" width="350">
</p>

- Click `Open with STM32CubeMX` to open the application.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/mcu_before.png" width="350">
</p>

- The default MCU is `STM32F030F4Px`.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/mcu_after.png" width="350">
</p>

- You can use STM32CubeMX like what you do everyday.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/ide_selection.png" width="350">
</p>

>- You have to select `STM32CubeIDe` in `Toolchain / IDE` setting, and the `Project Name` should be kept same as the project name in CLion.

<p align="middle">
  <img src="./../assets/imgs/2023_01_21_CLion_Dev_macOS/edit_config.png" width="350">
</p>

- After you generate code and overwrite the old project files, click `Assist` and choose a board type in `Run/Debug Configurations`.

>- You also need to edit the board config file in accordance to the version of your ST-Link.

Congrats! You can now build, upload, and debug in CLion.
