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
3. Configure package discovery using one of the methods below.
4. Launch or restart Houdini and the Adonis package will be automatically loaded with its SOPs, menu, icons, Python modules and licensing.

The extracted package has the following layout:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">&lt;package root&gt;/
    Adonis.json
    Adonis/
        bin/
        dso/
        icons/
        licensing/
        menu/
        otls/
        python/
        ...</code></pre>

> [!IMPORTANT]
> Keep `Adonis.json` and its sibling `Adonis/` directory together. The package uses `$HOUDINI_PACKAGE_PATH` to locate its contents relative to `Adonis.json`.

There are three ways to install the package:

- **Method 1:** Configure `HOUDINI_PACKAGE_DIR`
- **Method 2:** Load the package through Houdini's Package Browser
- **Method 3:** Copy the package into Houdini's `packages` directory

> [!NOTE]
> - Adonis is distributed for multiple Houdini versions. If you have multiple Houdini versions installed, make sure to [download](https://inbibo.co.uk/downloads?tab=adonisfx) the right Adonis build and configure the environment to point to the right Adonis version.
> - Remember that multiple versions of Adonis can be installed, but only one can be loaded at a time.

### Method 1: Configure HOUDINI_PACKAGE_DIR

When Houdini starts up, it evaluates all paths pointed by the `HOUDINI_PACKAGE_DIR` environment variable to search for packages that are typically defined as JSON files. In order to allow Houdini to find Adonis, that environment variable has to include the path where the `Adonis.json` file is located.

Set `HOUDINI_PACKAGE_DIR` as a system-wide or user-wide environment variable using the instructions below. Depending on your setup, you can also configure it through `houdini.env` by adding:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">HOUDINI_PACKAGE_DIR=&lt;folder containing Adonis.json&gt;</code></pre>

#### Windows

1. Open the System Properties window which can be found by searching for *environment variables* in the Windows search bar.
2. Click on *Environment Variables* and a new window will be displayed showing all the environment variables configured at the system level and for the current user.
3. Click on *New...* button for the level that you prefer (system or user) and configure `HOUDINI_PACKAGE_DIR` with the path containing the `Adonis.json` file.
4. Adonis will be loaded the next time you launch Houdini.

> [!NOTE]
> If you need to configure other packages for `HOUDINI_PACKAGE_DIR`, concatenate them separated by ";" characters.


#### Linux

1. From the terminal, open your preferred text editor to modify the file `~/.bashrc`.
2. Add the command to export `HOUDINI_PACKAGE_DIR` as follows:

    `export HOUDINI_PACKAGE_DIR="/path/to/Adonis/folder:${HOUDINI_PACKAGE_DIR}"`

3. Adonis will be loaded the next time you launch Houdini.

> [!NOTE]
> If you need to configure other packages for `HOUDINI_PACKAGE_DIR`, concatenate them separated by ":" characters.

### Method 2: Houdini Package Browser

1. Open Houdini's **Package Browser** and load the extracted `Adonis.json` file.
2. Enable autoload/reload-on-startup for the package to load Adonis automatically the next time Houdini starts.
3. Restart Houdini to complete the installation.

Loading the package through Package Browser can create an autoload reference in the Houdini user preferences, for example:

<pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">$HOUDINI_USER_PREF_DIR/packages/Adonis_autoload.json</code></pre>

The generated `Adonis_autoload.json` points to the original `Adonis.json`. When autoload/reload-on-startup is enabled, Houdini uses this reference to load Adonis automatically on startup. The actual Adonis installation is not copied into the user preferences folder, so keep the original `Adonis.json` and its sibling `Adonis/` directory in place.

> [!IMPORTANT]
> When loading the package into an already running Houdini session, the main Adonis menu and native SOP icons may not appear immediately. Restart Houdini after enabling the package so that the menu and icons are initialized correctly.

To stop Adonis from loading automatically, disable or remove the package from Package Browser. If the generated `Adonis_autoload.json` remains, close Houdini and remove that file from the Houdini `packages` preference directory.

### Method 3: Install into Houdini's packages Directory

1. Copy both `Adonis.json` and its sibling `Adonis/` directory into Houdini's package directory, for example `$HOUDINI_USER_PREF_DIR/packages/`.
2. Keep the following layout:

    <pre><code style="white-space: pre; margin: 20px 0; padding: 10px; box-sizing: border-box;">packages/
        Adonis.json
        Adonis/
            ...</code></pre>

3. Adonis will be loaded the next time you launch Houdini.

Houdini discovers the package automatically on startup. No environment variable configuration is required for this method.

## ML Dependencies

Some Adonis features require additional Python libraries to be installed. These dependencies are used for:

- **Training**, when running neural network training through the **Training Script** or the **Neural Training Tool**.
- **Inference**, when evaluating trained models on the GPU through **AdnMLDeformer** or **AdnSmartTissue**.

The ML dependencies are not installed by default and must be installed separately before using any of these features.

ML dependencies can be installed in the following ways:

1. From within Maya or Houdini using **Adonis > Utils > Install ML Dependencies**.
2. Through the **Neural Training Tool**. When starting a training session, the tool automatically checks whether the required dependencies are available and, if not, prompts the user to install them before training begins.
3. Using the standalone installation script in `Adonis/python/adnml/install_dependencies` (`.bat` in Windows; `.sh` in Linux).

The last method is particularly useful when running training through the Training Script outside of Maya or Houdini, or when preparing a machine for automated training workflows.

Installing the dependencies may take a few minutes.

> [!IMPORTANT]
> Machine learning dependencies are installed inside the Adonis installation directory rather than system-wide. As a result, the system environment remains unchanged and no global Python packages are installed.
