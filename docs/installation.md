# Installation

## Maya

AdonisFX is distributed for Maya as a standard module. To install the module, please do the following:

1. Download the AdonisFX zipped package from the Inbibo's website.
2. Extract the contents into the destination folder that you prefer.
3. Append the path to the destination folder to the `MAYA_MODULE_PATH` environment variable. Check the next section for more information.
4. Launch Maya and load AdonisFX from Windows > Settings/Preferences > Plug-in Manager.

### Configure Environment

When Maya starts up, it evaluates all paths pointed by the `MAYA_MODULE_PATH` environment variable to search and load modules like AdonisFX. In order to allow Maya to find AdonisFX, that environment variable has to include the path where the AdonisFX.mod file is located. 

AdonisFX is distributed for Maya 2022, 2023 and 2024. If you have multiple Maya versions installed, make sure to [download](https://inbibo.co.uk/adonisfx/downloads) the right AdonisFX build and configure the environment to point to the right AdonisFX version. Remind that multiple versions of AdonisFX can be installed, but only one can be loaded at a time.

There are two methods of configuring this variable: Setting the value in the `Maya.env` config file; or setting the value in the system to be permanent.

#### Configure Maya.env File

The Maya.env file is version dependent. It means that every instance of Maya will evaluate the environment file associated to its version. The default location of this file is:

> [!NOTE = Maya.env Location]
>
> <figure markdown>
>  ![File location maya.env Windows](/images/maya_env_file_location_windows.png)
>  <figcaption><b>Figure 1</b>: File location of "maya.env" file in Windows.</figcaption>
> </figure>
>
> `drive:/Users/username/Documents/maya/%MAYA_VERSION%`
>
> <figure markdown>
>  ![File location maya.env Linux](/images/maya_env_file_location_linux.png)
>  <figcaption><b>Figure 2</b>: File location of "maya.env" file in Linux.</figcaption>
> </figure>
>
> `~/maya/$MAYA_VERSION`

Add this line to the file and AdonisFX module will be loaded the next time you launch Maya:

> [!NOTE]
> `MAYA_MODULE_PATH = drive:/path/to/AdonisFX/folder`

#### Configure System Environment Variables

A different way of configuring the enviroment is setting an enviroment variable of the system for the `MAYA_MODULE_PATH`. The variable can be set on a persistent or a temporal way. The persistent way will be independent to the session or terminal opened. The temporal approach will be dependent to the session or terminal in which the variable was set.

##### Steps to set `MAYA_MODULE_PATH` as a system enviroment variable on Windows (persistent)

  1. Use the Windows searcher and look for "Edit enviroment variables for your account". "Edit the system enviroment variables" would work too, needing in this case permissions.

<figure markdown>
      ![edit enviroment variables search](/images/search_edit_env_variables.png)
      <figcaption><b>Figure 3</b>: Searching for "Edit enviroment variables for your account" at windows.</figcaption>
</figure>

  2. New window will be displayed with the enviroment variables of the user. IF there is a variable "MAYA_MODULE_PATH" we will select it and press "Edit..." if not we will press "New...".

<figure markdown>
      ![enviroment variables window windows](/images/enviroment_variables_window_windows.png)
      <figcaption><b>Figure 4</b>: Enviroment variable window at windows.</figcaption>
</figure>

  3. "MAYA_MODULE_PATH" has to be provided as the variable name and for the value the path to where the AdonisFX.mod file is located. Use of "Browse Directory..." might be useful.

<figure markdown>
      ![create user enviroment variable window](/images/new_user_variable_windows.png)
      <figcaption><b>Figure 5</b>: Creating new user enviroment variable.</figcaption>
</figure>

  4. After adding the variable is needed to press "Ok" or "Apply" at the previous window to the creation one to confirm the variable creation.

##### Steps to set `MAYA_MODULE_PATH` as a system enviroment variable on Linux (persistent)

  1. Open a terminal and with the preferred text editor manipulate the file "~/.bashrc".

<figure markdown>
      ![edit bashrc file from terminal](/images/terminal_edit_bashrc.png)
      <figcaption><b>Figure 6</b>: Linux terminal openning a text editor to edit file ".bashrc".</figcaption>
</figure>

  2. At the end of the file add the following line and save the changes. `export MAYA_MODULE_PATH=$MAYA_MODULE_PATH:/path/to/AdonisFX/folder`.
  3. Close the terminal.

> [!NOTE = Check Environment Variale]
> In order to confirm that your persistent variable is properly set, open a terminal and execute the following line.
>
>  - At Windows `set MAYA_MODULE_PATH`.
>  - At Linux `echo $MAYA_MODULE_PATH`.
>
> The path to the AdonisFX.mod file should be printed.

##### Steps to set `MAYA_MODULE_PATH` as a system enviroment variable (temporal)

1. Open a terminal.
2. Execute the following line depending on your operative system.
    - At Windows `set MAYA_MODULE_PATH=%MAYA_MODULE_PATH%;drive:/path/to/AdonisFX/folder`
    - At Linux `export MAYA_MODULE_PATH=$MAYA_MODULE_PATH:/path/to/AdonisFX/folder`
3. Open Maya from the terminal.
    - At Windows `drive:/Program Files/Autodesk/Maya%MAYA_VERSION%/bin/maya.exe`
    - At Linux `/usr/autodesk/maya$MAYA_VERSION/bin/maya`
4. The variable will be dependent to the terminal. As soon as the terminal is closed the variable will be removed.

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