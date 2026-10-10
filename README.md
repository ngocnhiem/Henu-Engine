# Henu Engine 

Henu Engine is an open-source, real-time, multi-platform 3D engine that enables developers and content creators to build AAA games, cinema-quality 3D worlds, Henu Engine is based on [O3DE (Open 3D Engine)](https://github.com/o3de/o3de/)

## Roadmap
Progress against the roadmap is tracked [Roadmap and process](https://github.com/users/ngocnhiem/projects/3).

## Download and Install

This repository uses Git LFS for storing large binary files.  

Verify you have Git LFS installed by running the following command to print the version number.
```
git lfs --version 
```

If Git LFS is not installed, download and run the installer from: [https://git-lfs.github.com/](https://git-lfs.github.com/).

### Install Git LFS hooks 
```
git lfs install
```

## Building the Engine

### Build requirements and redistributables

For the latest details and system requirements.

#### Minimum
*   OS: Windows or Linux.
*   Chip:Intel Core i3 or Amd Ryzen 3.
*   Ram: 8 GB (best 16 GB).
*   Storage: 90 GB.
*   Graphic Card: Nvidia GTX 1050 and Amd RX 560 or Arc A310

#### Maximum
*   Chip: Intel Core Ultra 9 or AMD Ryzen 9
*   Ram: 32 GB (best 64GB)
*   Storage: 200GB 
*   Graphic Card: Nvidia RTX 5090 and Amd RX 7900 XTX (RX 9060 XTX) or Arc B580

#### Windows 

*   Visual Studio 2019 16.9.2 minimum (All editions supported, including Community): [https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/)
    *   Check [System Requirements](https://o3de.org/docs/welcome-guide/requirements/) for other supported versions.
    *   Install the following workloads:
        *   Game Development with C++
        *   MSVC v142 - VS 2019 C++ x64/x86
        *   C++ 2019 redistributable update
*   CMake 3.25.0 minimum: [https://cmake.org/download/#latest](https://cmake.org/download/#latest) (Release Candidate versions are not supported)

### Quick start engine setup

To set up a project-centric source engine, complete the following steps. For other build options, refer to [Setting up O3DE from GitHub](https://o3de.org/docs/welcome-guide/setup/setup-from-github/) in the documentation.

1.  Create a writable folder to cache downloadable third-party packages. You can also use this to store other redistributable SDKs.
    
1.  Install the following redistributables:
    - Visual Studio and VC++ redistributable can be installed to any location.
    - CMake can be installed to any location, as long as it's available in the system path.

1.  Configure the engine source into a solution using this command line, replacing `<your build path>`, `<your source path>`, and `<3rdParty package path>` with the paths you've created:
    ```
    cmake -B <your build path> -S <your source path> -G "Visual Studio 17" -DLY_3RDPARTY_PATH=<3rdParty package path>
    ```
    
    Example:
    ```
    cmake -B C:\henu\build\windows -S C:\o3de -G "Visual Studio 1" -DLY_3RDPARTY_PATH=C:\o3de-packages
    ```
    
    > Note:  Do not use trailing slashes for the <3rdParty package path>.

1.  Alternatively, you can do this through the CMake GUI:
    
    1.  Start `cmake-gui.exe`.
    1.  Select the local path of the repo under "Where is the source code".
    1.  Select a path where to build binaries under "Where to build the binaries".
    1.  Click **Add Entry** and add a cache entry for the <3rdParty package path> folder you created, using the following values:
        1.  **Name:** LY_3RDPARTY_PATH
        1.  **Type:** STRING
        1.  **Value:** `<3rdParty package path>`
    1.  Click **Configure**.
    1.  Wait for the key values to populate. Update or add any additional fields that are needed for your project.
    1.  Click **Generate**.
    
1.  Register the engine with this command:
    ```
    scripts\o3de.bat register --this-engine
    ```

1.  The configuration of the solution is complete. You are now ready to create a project and build the engine.

For more details on the steps above, refer to [Setting up O3DE from GitHub](https://o3de.org/docs/welcome-guide/setup/setup-from-github/) in the documentation.

### Setting up new projects and building the engine

1. From the henu repo folder, set up a new project using the `Henu create-project` command.
    ```
    scripts\Henu.bat create-project --project-path <your new project path>
    ```

1. Configure a solution for your project.
    ```
    cmake -B <your project build path> -S <your new project source path> -G "Visual Studio 17"
    ```

    Example:
    ```
    cmake -B C:\my-project\build\windows -S C:\my-project -G "Visual Studio 17"
    ```
    
    > Note:  Do not use trailing slashes for the <3rdParty cache path>.

1. Build the project, Asset Processor, and Editor to binaries by running this command inside your project:
    ```
    cmake --build <your project build path> --target <New Project Name>.GameLauncher Editor --config profile -- /m
    ```
    
    > Note: Your project name used in the build target is the same as the directory name of your project.

This will compile after some time and binaries will be available in the project build path you've specified, under `bin/profile`.
