# Installation

## Maya

Adonis is distributed for Maya as a **standard module** (.mod). To install the module, follow these steps:

1. Download the Adonis package from [Inbibo’s website](https://inbibo.co.uk/downloads?tab=adonisfx).
2. Extract the contents into any folder of your choice.
3. Add the path to that extracted folder to the `MAYA_MODULE_PATH` environment variable (details below).
4. Launch Maya and load Adonis from **Windows > Settings/Preferences > Plug-in Manager**.

When Maya starts, it evaluates all directories listed in `MAYA_MODULE_PATH` to locate module files such as `Adonis.mod`. Therefore, the environment variable must include the folder containing that file.

There are two ways to configure `MAYA_MODULE_PATH`:

- **Method 1:** Set the value inside the `Maya.env` configuration file
- **Method 2:** Set the value as a system-wide or user-wide environment variable

> [!NOTE]
> - Adonis is distributed for multiple Maya versions. If you have multiple Maya versions installed, make sure to [download](https://inbibo.co.uk/downloads?tab=adonisfx) the right Adonis build and configure the environment to point to the right Adonis version.
> - Remember that multiple versions of Adonis can be installed, but only one can be loaded at a time.

### Windows

#### Method 1: Configure Maya.env

1. The default location of the `Maya.env` file is `drive:/Users/username/Documents/maya/%MAYA_VERSION%`.
2. Add `MAYA_MODULE_PATH = drive:/path/to/Adonis/folder` to the file.
3. Adonis will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ";" characters.

#### Method 2: Configure System Environment

1. Open the System Properties window which can be found by searching for *environment variables* in the Windows search bar.
2. Click on *Environment Variables* and a new window will be displayed showing all the environment variables configured at the system level and for the current user.
3. Click on *New...* button for the level that you prefer (system or user) and configure `MAYA_MODULE_PATH` with the path containing the `Adonis.mod` file.
4. Adonis will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ";" characters.


### Linux

#### Method 1: Configure Maya.env

1. The default location of the `Maya.env` file is `~/maya/$MAYA_VERSION`.
2. Add `MAYA_MODULE_PATH = /path/to/Adonis/folder` to the file.
3. Adonis will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ":" characters.

#### Method 2: Configure System Environment

1. From the terminal, open your preferred text editor to modify the file `~/.bashrc`.
2. Add this command to export the environment variable:

   `export MAYA_MODULE_PATH="/path/to/Adonis/folder:${MAYA_MODULE_PATH}"`

3. Adonis will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure other modules, concatenate them separated by ":" characters.


## Houdini

Adonis is distributed for Houdini as a **standard package** (.json). To install the package, please do the following:

1. Download the Adonis package from [Inbibo’s website](https://inbibo.co.uk/downloads?tab=adonisfx).
2. Extract the contents into any folder of your choice.
3. Add the path to that extracted folder to the `HOUDINI_PACKAGE_DIR` and `ADN_INSTALL_PATH` environment variables.
4. Launch Houdini and the Adonis package will be automatically loaded.

When Houdini starts up, it evaluates all paths pointed by the `HOUDINI_PACKAGE_DIR` environment variable to search for packages that are typically defined as JSON files. In order to allow Houdini to find Adonis, that environment variable has to include the path where the `Adonis.json` file is located.

The need to set `ADN_INSTALL_PATH` as well is to allow Houdini to complete the environment configuration using paths relative to the Adonis installation folder.

In the following sections we explain how to do this for Windows and Linux.

> [!NOTE]
> - Adonis is distributed for multiple Houdini versions. If you have multiple Houdini versions installed, make sure to [download](https://inbibo.co.uk/downloads?tab=adonisfx) the right Adonis build and configure the environment to point to the right Adonis version.
> - Remember that multiple versions of Adonis can be installed, but only one can be loaded at a time.

### Windows

1. Open the System Properties window which can be found by searching for *environment variables* in the Windows search bar.
2. Click on *Environment Variables* and a new window will be displayed showing all the environment variables configured at the system level and for the current user.
3. Click on *New...* button for the level that you prefer (system or user) and configure `HOUDINI_PACKAGE_DIR` with the path containing the `Adonis.json` file.
4. Do the same for `ADN_INSTALL_PATH`.
5. Adonis will be loaded the next time you launch Houdini.

> [!NOTE]
> - If you need to configure other packages for `HOUDINI_PACKAGE_DIR`, concatenate them separated by ";" characters.
> - For `ADN_INSTALL_PATH`, only a single installation path should be provided.


### Linux

1. From the terminal, open your preferred text editor to modify the file `~/.bashrc`.
2. Add the command to export `HOUDINI_PACKAGE_DIR` as follows:

    `export HOUDINI_PACKAGE_DIR="/path/to/Adonis/folder:${HOUDINI_PACKAGE_DIR}"`

3. Add also the command to export `ADN_INSTALL_PATH`:

    `export ADN_INSTALL_PATH="/path/to/Adonis/folder"`

4. Adonis will be loaded the next time you launch Houdini.

> [!NOTE]
> - If you need to configure other packages for `HOUDINI_PACKAGE_DIR`, concatenate them separated by ":" characters.
> - For `ADN_INSTALL_PATH`, only a single installation path should be provided.

## ML Dependencies

Some Adonis features require additional Python machine learning dependencies to be installed. These dependencies are used for:

- **Training**, when running neural network training through the **Training Script** or the **Neural Training Tool**.
- **Inference**, when evaluating trained models through **AdnMLDeformer** or **AdnSmartTissue**.

The ML dependencies are not installed by default and must be installed separately before using any of these features.

### Method 1: Install from the DCC

Both Maya and Houdini include a utility to install the required ML dependencies directly from the Adonis menu:

**Adonis > Utils > Install ML Dependencies**

### Method 2: Automatic Installation from the Neural Training Tool

When launching a training session through the **Neural Training Tool**, Adonis automatically checks whether the required ML dependencies are available.

If they are not installed, the tool will display a dialog prompting you to install them before the training process starts.

### Method 3: Install Using the Command-Line Script

The ML dependencies can also be installed using the standalone installation scripts located in:

- `Adonis/python/adnml/install_dependencies.bat` on Windows.
- `Adonis/python/adnml/install_dependencies.sh` on Linux

This method is particularly useful when running training through the **Training Script** outside of Maya or Houdini, or when preparing a machine for automated training workflows.

> [!NOTE]
> Machine learning dependencies are installed inside the Adonis installation directory rather than system-wide. As a result, the system environment remains unchanged and no global Python packages are installed.
