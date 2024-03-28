# Installation

## Maya

AdonisFX is distributed for Maya as a standard module. To install the module, please do the following:

1. Download the AdonisFX zipped package from the Inbibo's website.
2. Extract the contents into the destination folder that you prefer.
3. Append the path to the destination folder to the `MAYA_MODULE_PATH` environment variable. Check the next sections for more information.
4. Launch Maya and load AdonisFX from Windows > Settings/Preferences > Plug-in Manager.

### Configure Environment

When Maya starts up, it evaluates all paths pointed by the `MAYA_MODULE_PATH` environment variable to search and load modules like AdonisFX. In order to allow Maya to find AdonisFX, that environment variable has to include the path where the AdonisFX.mod file is located. 

AdonisFX is distributed for Maya 2022, 2023 and 2024. If you have multiple Maya versions installed, make sure to [download](https://inbibo.co.uk/adonisfx/downloads) the right AdonisFX build and configure the environment to point to the right AdonisFX version. Remind that multiple versions of AdonisFX can be installed, but only one can be loaded at a time.

There are two different methods of configuring this variable: Setting the value in the `Maya.env` config file; or setting the value in the system to be permanent. In the following sections we explain these two methods for Windows and Linux.

#### Configure Environment On Windows

##### Method 1: Maya.env

The Maya.env file is version dependent. It means that every instance of Maya will evaluate the environment file associated to its version. The default location of this file is `drive:/Users/username/Documents/maya/%MAYA_VERSION%`.

![Windows "Maya.env" file location.](/images/windows_maya_env_file_location.png)
<b>Figure 1</b>: Location of "Maya.env" file in Windows. Example for Maya 2024.

Add this line making sure to specify the folder containing the AdonisFX.mod file and the module will be loaded the next time you launch Maya:

`MAYA_MODULE_PATH = drive:/path/to/AdonisFX/folder`

##### Method 2: Environment variables of the system

Open the System Properties window which can be found by searching for *environment variables* in the Windows search bar.

![Windows system properties.](/images/windows_system_properties.png)
<b>Figure 2</b>: System Properties window.

Click on *Environment Variables* and a new window will pop showing all the environment variables configured at the system level and for the current user.

![Windows environment variables.](/images/windows_environment_variables.png)
<b>Figure 3</b>: Environment variables of the system.

Click on *New...* button for the level that you prefer (system or user) and configure `MAYA_MODULE_PATH` with the path containing the AdonisFX.mod file.

![Windows add new environment variable.](/images/windows_add_new_env.png)
<b>Figure 4</b>: Configure MAYA_MODULE_PATH as new environment variable.

#### Configure Environment On Linux

##### Method 1: Maya.env

The Maya.env file is version dependent. It means that every instance of Maya will evaluate the environment file associated to its version. The default location of this file is `~/maya/$MAYA_VERSION`.

![Linux "Maya.env" file location.](/images/linux_maya_env_file_location.png)
<b>Figure 5</b>: Location of "Maya.env" in Linux. Example for Maya 2022.

Add this line making sure to specify the folder containing the AdonisFX.mod file and the module will be loaded the next time you launch Maya:

`MAYA_MODULE_PATH = drive:/path/to/AdonisFX/folder`

##### Method 2: Environment variables of the system

From the terminal, open your preferred text editor to modify the file `~/.bashrc`.

![Linux edit bashrc file.](/images/linux_edit_environment.png)
<b>Figure 6</b>: Edit environment from the *~/.bashrc* file.

Add the command to export the environment variable as shown in the image below.

![Linux configure environment variable.](/images/linux_add_new_env.png)
<b>Figure 7</b>: Configure MAYA_MODULE_PATH as new environment variable.

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