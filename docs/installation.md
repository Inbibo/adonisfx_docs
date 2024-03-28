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

TODO - add screenshot of the maya.env file location. Ideally, one for windows, one for linux. Ideally, inside the Note (check if having an image inside a note section works)

> [!NOTE = Maya.env Location]
> === Windows
> 
> `drive:/Users/username/Documents/maya/%MAYA_VERSION%`
>
>  === Linux
>
> `~/maya/$MAYA_VERSION`

Add this line to the file and AdonisFX module will be loaded the next time you launch Maya:

> [!NOTE]
> `MAYA_MODULE_PATH = drive:/path/to/AdonisFX/folder`

#### Configure System Environment Variables

TODO - section for windows with screenshots on how to configure the environment variables of the system. Important! the Windows UI has to be in English

TODO - section for linux with screenshots on how to configure the .bashrc or .profile. Important! the Windows UI has to be in English

TODO - Probably remove the following note:
> [!NOTE = Set Environment Variale]
> === Windows
> 
> `set MAYA_MODULE_PATH=%MAYA_MODULE_PATH%;drive:/path/to/AdonisFX/folder`
>
>  === Linux
>
> `export MAYA_MODULE_PATH=$MAYA_MODULE_PATH:/path/to/AdonisFX/folder`



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