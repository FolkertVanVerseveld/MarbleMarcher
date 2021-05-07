# Marble Marcher Sandbox

Marble Marcher Sandbox is an interactive Marble Marcher level explorer where the user is able to manipulate
the parameters of various aspects of the game.

The goal of this project is to allow experimenting with the fragment shader rendering the scene in order to understand
the performance impact of different parameters.

## System Dependencies
* [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page)
* [SFML 2.5.0](https://www.sfml-dev.org)

### MacOS
On macOS these can be conveniently installed using [Homebrew](https://brew.sh):

`brew install cmake eigen sfml`

Alternatively, [vcpkg](https://github.com/Microsoft/vcpkg) can be used:

`vcpkg install eigen3 sfml`

### Arch Linux
`sudo pacman -S eigen sfml git cmake make`

## Building
### MacOS
* `mkdir build && cd build`
* `cmake -DCMAKE_CXX_FLAGS="-I/usr/local/include" -DIMGUI_DIR="$(pwd)/../vendor/imgui" -DIMGUI_SFML_FIND_SFML=OFF ..`
    * If you use `vcpkg`, add the flag `-DCMAKE_TOOLCHAIN_FILE=[path/to/vcpkg]/scripts/buildsystems/vcpkg.cmake`
* `cd ..`
* `cmake --build build`

Alternatively, one can use the platform-dependent build system, for example `Make`:

* `make -C build`
### Arch Linux
* `cd ~`
* `git clone https://github.com/HackerPoet/MarbleMarcher.git`
* `cd MarbleMarcher`
* `mkdir build && cd build`
* `cmake ..`
* `cd ..`
* `cmake --build build`
* `cp build/MarbleMarcher ./`


## Launching
* Make sure that the current working directory contains the `assets` folder
* Run the executable generated by CMake, located in `build` (or a subdirectory)
* If running MarbleMarcher from a tarball and you see a message like

> ./MarbleMarcher: error while loading shared libraries: libsfml-graphics.so.2.5: cannot open shared object file: No such file or directory

You'll just need to run MarbleMarcher with the correct `LD_LIBRARY_PATH`:

```shell
LD_LIBRARY_PATH=`pwd`/usr/lib ./MarbleMarcher
```
