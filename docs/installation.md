# Installation

## Maya

AdonisFX is distributed for Maya as a standard module. To install the module, please do the following:

1. Download the AdonisFX zipped package from the Inbibo's website.
2. Extract the contents into the destination folder that you prefer.
3. Append the path to the destination folder to the `MAYA_MODULE_PATH` environment variable. Check the next sections for more information.
4. Launch Maya and load AdonisFX from Windows > Settings/Preferences > Plug-in Manager.

When Maya starts up, it evaluates all paths pointed by the `MAYA_MODULE_PATH` environment variable to search and load modules like AdonisFX. In order to allow Maya to find AdonisFX, that environment variable has to include the path where the `AdonisFX.mod` file is located. 

AdonisFX is distributed for Maya 2022, 2023 and 2024. If you have multiple Maya versions installed, make sure to [download](https://inbibo.co.uk/adonisfx/downloads) the right AdonisFX build and configure the environment to point to the right AdonisFX version. Remind that multiple versions of AdonisFX can be installed, but only one can be loaded at a time.

### Configure Environment

There are two different methods of configuring this variable:

- **Method 1**: setting the value in the `Maya.env` config file.
- **Method 2**: setting the value in the system to be permanent.

In the following sections we explain these two methods for Windows and Linux.

#### Method 1 on Windows

1. The default location of `Maya.env` file is `drive:/Users/username/Documents/maya/%MAYA_VERSION%`.

<figure style="width:60%; margin-left:10%" markdown>
  ![Windows Maya.env file location.](/images/windows_maya_env_file_location.png)
  <figcaption><b>Figure 1</b>: Location of Maya.env file in Windows. Example for Maya 2024.</figcaption>
</figure>

2. Add `MAYA_MODULE_PATH = drive:/path/to/AdonisFX/folder` to the file.

3. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure multiple paths, concatenate them separated by ";" character.

#### Method 2 on Windows

1. Open the System Properties window which can be found by searching for *environment variables* in the Windows search bar.

<figure style="width:60%; margin-left:10%" markdown>
  ![Windows system properties.](/images/windows_system_properties.png)
  <figcaption><b>Figure 2</b>: System Properties window.</figcaption>
</figure>

2. Click on *Environment Variables* and a new window will be displayed showing all the environment variables configured at the system level and for the current user.

<figure style="width:40%; margin-left:10%" markdown>
  ![Windows environment variables.](/images/windows_environment_variables.png)
  <figcaption><b>Figure 3</b>: Environment variables of the system.</figcaption>
</figure>

3. Click on *New...* button for the level that you prefer (system or user) and configure `MAYA_MODULE_PATH` with the path containing the `AdonisFX.mod` file.

<figure style="width:60%; margin-left:10%" markdown>
  ![Windows add new environment variable.](/images/windows_add_new_env.png)
  <figcaption><b>Figure 4</b>: Configure MAYA_MODULE_PATH as new environment variable.</figcaption>
</figure>

4. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure multiple paths, concatenate them separated by ";" character.

#### Method 1 on Linux

1. The default location of `Maya.env` file is `~/maya/$MAYA_VERSION`.

<figure style="width:60%; margin-left:10%" markdown>
  ![Linux Maya.env file location.](/images/linux_maya_env_file_location.png)
  <figcaption><b>Figure 5</b>: Location of Maya.env in Linux. Example for Maya 2022.</figcaption>
</figure>

2. Add `MAYA_MODULE_PATH = /path/to/AdonisFX/folder` to the file.

3. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure multiple paths, concatenate them separated by ":" character.

#### Method 2 on Linux

1. From the terminal, open your preferred text editor to modify the file `~/.bashrc`.

2. Add the command to export the environment variable as shown in the image below.

<figure style="width:60%; margin-left:10%" markdown>
  ![Linux configure environment variable.](/images/linux_add_new_env.png)
  <figcaption><b>Figure 6</b>: Configure MAYA_MODULE_PATH as new environment variable.</figcaption>
</figure>

3. AdonisFX will be loaded the next time you launch Maya.

> [!NOTE]
> If you need to configure multiple paths, concatenate them separated by ":" character.

<!--
## Houdini

AdonisFX is distributed for Houdini as a standard package. To install the package, please do the following:

1. Download the AdonisFX zipped package from the Inbibo's website [TODO: #2 add link].
2. Unzip the contents into the destination folder that you prefer.
3. Add folder containg the AdonisFX.json file to the `HOUDINI_PACKAGE_DIR` environment variable.

The `HOUDINI_PACKAGE_DIR` must be set in your environemnt. For example:

- Windows: `set HOUDINI_PACKAGE_DIR=%HOUDINI_PACKAGE_DIR%;/path/to/AdonisFX/folder`
- Linux: `export HOUDINI_PACKAGE_DIR=$HOUDINI_PACKAGE_DIR:/path/to/AdonisFX/folder`
-->