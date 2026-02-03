# Installation

## Maya

AdonisFX is distributed for Maya as a **standard module** (.mod). To install the module, follow these steps:

1. Download the AdonisFX package from [Inbibo’s website](https://inbibo.co.uk/adonisfx/downloads).
2. Extract the contents into any folder of your choice.
3. Add the path to that extracted folder to the `MAYA_MODULE_PATH` environment variable (details below).
4. Launch Maya and load AdonisFX from **Windows > Settings/Preferences > Plug-in Manager**.

When Maya starts, it evaluates all directories listed in `MAYA_MODULE_PATH` to locate module files such as `AdonisFX.mod`. Therefore, the environment variable must include the folder containing that file.

There are two ways to configure `MAYA_MODULE_PATH`:

- **Method 1:** Set the value inside the `Maya.env` configuration file
- **Method 2:** Set the value as a system-wide or user-wide environment variable

> [!NOTE]
> - AdonisFX is distributed for multiple Maya versions. If you have multiple Maya versions installed, make sure to [download](https://inbibo.co.uk/adonisfx/downloads) the right AdonisFX build and configure the environment to point to the right AdonisFX version.
> - Remember that multiple versions of AdonisFX can be installed, but only one can be loaded at a time.

### Windows

#### Method 1: Configure Maya.env

1. The default location of the `Maya.env` file is `drive:/Users/username/Documents/maya/%MAYA_VERSION%`.
2. Add `MAYA_MODULE_PATH = drive:/path/to/AdonisFX/folder` to the file.
3. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ";" characters.

#### Method 2: Configure System Environment

1. Open the System Properties window which can be found by searching for *environment variables* in the Windows search bar.
2. Click on *Environment Variables* and a new window will be displayed showing all the environment variables configured at the system level and for the current user.
3. Click on *New...* button for the level that you prefer (system or user) and configure `MAYA_MODULE_PATH` with the path containing the `AdonisFX.mod` file.
4. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ";" characters.


### Linux

#### Method 1: Configure Maya.env

1. The default location of the `Maya.env` file is `~/maya/$MAYA_VERSION`.
2. Add `MAYA_MODULE_PATH = /path/to/AdonisFX/folder` to the file.
3. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ":" characters.

#### Method 2: Configure System Environment

1. From the terminal, open your preferred text editor to modify the file `~/.bashrc`.
2. Add this command to export the environment variable:

   `export MAYA_MODULE_PATH="/path/to/AdonisFX/folder:${MAYA_MODULE_PATH}"`

3. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ":" characters.


## Houdini

AdonisFX is distributed for Houdini as a **standard package** (.json). To install the package, please do the following:

1. Download the AdonisFX package from [Inbibo’s website](https://inbibo.co.uk/adonisfx/downloads).
2. Extract the contents into any folder of your choice.
3. Add the path to that extracted folder to the `HOUDINI_PACKAGE_DIR` and `ADONISFX_INSTALL_PATH` environment variables.
4. Launch Houdini and the AdonisFX package will be automatically loaded.

When Houdini starts up, it evaluates all paths pointed by the `HOUDINI_PACKAGE_DIR` environment variable to search for packages that are typically defined as JSON files. In order to allow Houdini to find AdonisFX, that environment variable has to include the path where the `AdonisFX.json` file is located.

The need to set `ADONISFX_INSTALL_PATH` as well is to allow Houdini to complete the environment configuration using paths relative to the AdonisFX installation folder.

In the following sections we explain how to do this for Windows and Linux.

> [!NOTE]
> - AdonisFX is distributed for multiple Houdini versions. If you have multiple Houdini versions installed, make sure to [download](https://inbibo.co.uk/adonisfx/downloads) the right AdonisFX build and configure the environment to point to the right AdonisFX version.
> - Remember that multiple versions of AdonisFX can be installed, but only one can be loaded at a time.

### Windows

1. Open the System Properties window which can be found by searching for *environment variables* in the Windows search bar.
2. Click on *Environment Variables* and a new window will be displayed showing all the environment variables configured at the system level and for the current user.
3. Click on *New...* button for the level that you prefer (system or user) and configure `HOUDINI_PACKAGE_DIR` with the path containing the `AdonisFX.json` file.
4. Do the same for `ADONISFX_INSTALL_PATH`.
5. AdonisFX will be loaded the next time you launch Houdini.

> [!NOTE]
> - If you need to configure other packages for `HOUDINI_PACKAGE_DIR`, concatenate them separated by ";" characters.
> - For `ADONISFX_INSTALL_PATH`, only a single installation path should be provided.


### Linux

1. From the terminal, open your preferred text editor to modify the file `~/.bashrc`.
2. Add the command to export `HOUDINI_PACKAGE_DIR` as follows:

    `export HOUDINI_PACKAGE_DIR="/path/to/AdonisFX/folder:${HOUDINI_PACKAGE_DIR}"`

3. Add also the command to export `ADONISFX_INSTALL_PATH`:

    `export ADONISFX_INSTALL_PATH="/path/to/AdonisFX/folder"`

4. AdonisFX will be loaded the next time you launch Houdini.

> [!NOTE]
> - If you need to configure other packages for `HOUDINI_PACKAGE_DIR`, concatenate them separated by ":" characters.
> - For `ADONISFX_INSTALL_PATH`, only a single installation path should be provided.
