
# MyGUI

This guide provides instructions for building MyGUI on macOS, Windows, and Linux.

## Prerequisites

1. **CMake** - Cross-platform build system generator.
2. **A C++ Compiler** - GCC for Linux, Xcode for macOS, Visual Studio for Windows.
3. **Dependencies** - OGRE, Boost, SDL2, SDL2_image.

## macOS

1. **Install Homebrew** (if not already installed):

   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

2. **Install Dependencies**:

   ```bash
   brew install cmake pkg-config doxygen sdl2 sdl2_image boost
   ```

3. **Build OGRE** (Assuming OGRE source is in `/path/to/ogre`):

   ```bash
   cd /path/to/ogre
   mkdir build && cd build
   cmake -DCMAKE_INSTALL_PREFIX=/path/to/ogre/install ..
   make -j4
   make install
   ```

4. **Clone MyGUI and Build**:

   ```bash
   git clone https://github.com/finalverse/mygui.git
   cd mygui
   mkdir build && cd build
   cmake -DOGRE_DIR=/path/to/ogre/install -DMYGUI_RENDERSYSTEM=4 \
         -DSDL2_IMAGE_INCLUDE_DIR=/usr/local/include/SDL2 \
         -DSDL2_IMAGE_LIBRARY=/usr/local/lib/libSDL2_image.dylib \
         ..
   make -j4
   ```

## Windows

1. **Install Dependencies**:
   - [CMake](https://cmake.org/download/)
   - [Visual Studio](https://visualstudio.microsoft.com/)
   - [SDL2](https://www.libsdl.org/download-2.0.php)
   - [SDL2_image](https://www.libsdl.org/projects/SDL_image/)
   - [Boost](https://www.boost.org/)
   - [OGRE](https://www.ogre3d.org/)

2. **Set Environment Variables** for SDL2 and SDL2_image:

   ```cmd
   set SDL2_DIR=C:\path\to\SDL2
   set SDL2_IMAGE_DIR=C:\path\to\SDL2_image
   ```

3. **Build OGRE**:

   Open CMake GUI, configure and generate the Visual Studio project for OGRE, then build it in Visual Studio.

4. **Clone MyGUI and Build**:

   ```cmd
   git clone https://github.com/finalverse/mygui.git
   cd mygui
   mkdir build && cd build
   cmake -G "Visual Studio 16 2019" -DOGRE_DIR=C:\path\to\ogre\install -DMYGUI_RENDERSYSTEM=4 \
         -DSDL2_IMAGE_INCLUDE_DIR=%SDL2_IMAGE_DIR%\include \
         -DSDL2_IMAGE_LIBRARY=%SDL2_IMAGE_DIR%\lib\SDL2_image.lib \
         ..
   ```

   Open the generated MyGUI solution in Visual Studio and build it.

## Linux

1. **Install Dependencies**:

   ```bash
   sudo apt-get update
   sudo apt-get install -y build-essential cmake pkg-config doxygen libsdl2-dev libsdl2-image-dev libboost-all-dev
   ```

2. **Build OGRE** (Assuming OGRE source is in `/path/to/ogre`):

   ```bash
   cd /path/to/ogre
   mkdir build && cd build
   cmake -DCMAKE_INSTALL_PREFIX=/path/to/ogre/install ..
   make -j4
   make install
   ```

3. **Clone MyGUI and Build**:

   ```bash
   git clone https://github.com/finalverse/mygui.git
   cd mygui
   mkdir build && cd build
   cmake -DOGRE_DIR=/path/to/ogre/install -DMYGUI_RENDERSYSTEM=4 ..
   make -j4
   ```

## Additional Resources

- [MyGUI Documentation](https://mygui.info/)
- [OGRE Documentation](https://ogrecave.github.io/ogre/)

## Troubleshooting

- Ensure all paths are correctly specified.
- Install any missing dependencies as indicated by CMake error messages.
- For any issues, please refer to the documentation or open an issue in this repository.

## Additional Documentation

For detailed information about the underlying engine structure of MyGUI, refer to the following documents.
-  [MyGUI Engine Build Instructions](MyGUI_BUILD_INSTRUCTIONS.md) (this README.md)
-  [MyGUI Engine Structure](MyGUI_ENGINE_STRUCTURE.md) 
