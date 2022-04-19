# Visual Studio Code project template for STM32/CubeMX

This project is a basic example on how to use CubeMX with Visual Studio Code.

For detailed guide on creating this project step-by-step, and to know what to change when adapting this project to your MCU, see [my blog post](https://steelph0enix.github.io/posts/vscode-cubemx-setup/)

## Required software

* [STM32CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)
* [ARM-GCC toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads)
* [OpenOCD](https://openocd.org/) - this is actually optional, you can change the debugging interface to `stlink` in project config
* [compiledb](https://pypi.org/project/compiledb/) package for Python, as it's used to generate `compile_commands.json` for `clangd`. You can also modify this project to use [Bear](https://github.com/rizsotto/Bear) if you're working on Linux, but `compiledb` should work everywhere.
* GNU Make, if you're working on Linux/MacOS you should have it. If you're working on Windows, i recommend getting it from MSYS/MinGW-W64 install, or [WinLibs](https://winlibs.com/) - i use WinLibs, i've copied `mingw32-make.exe` and renamed the copy to `make.exe` to use it with `compiledb` and it works fine. **DO NOT use [Make for Windows](http://gnuwin32.sourceforge.net/packages/make.htm) with `compiledb`, it won't work due to UTF encoding issues - at least in my case**.

## CubeMX settings

Set project type to `Makefile`, nothing more.

## Required and recommended VSCode plugins

Besides the standard C/C++ plugins, this project is based on [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd) language server. For debugging, [Cortex Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug) plugin is used. I also recommend installing [ARM assembly](https://marketplace.visualstudio.com/items?itemName=dan-c-underwood.arm) and [LinkerScript](https://marketplace.visualstudio.com/items?itemName=ZixuanWang.linkerscript) syntax support.

### Common issues and solutions

* `compiledb` crashes due to UTF encoding issues - get `make` from different source
* `Import error: no module named site` - this comes from GDB dependency. To solve it, install [Python 2](https://www.python.org/downloads/release/python-278/), and create environmental variable called `PYTHONHOME`. Set it to Python2 installation path (`C:/Python27` by default). If you're using `compiledb`, make sure you empty this variable in `tasks.json` (it's done in this project), otherwise `compiledb` will try to run using Python 2 and fail misearbly.
