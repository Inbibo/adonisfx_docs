# Installation

## Maya

AdonisFX is distributed for Maya as a standard module. To install the module, please do the following:

1. Download the AdonisFX zipped package from the Inbibo's website.
2. Extract the contents into the destination folder that you prefer.
3. Append the path to the destination folder to the `MAYA_MODULE_PATH` environment variable. Check the next section for more information.
4. Launch Maya and load AdonisFX from Windows > Settings/Preferences > Plug-in Manager.

### Configure Environment

When Maya starts up, it evaluates all paths pointed by the `MAYA_MODULE_PATH` environment variable to search and load modules like AdonisFX. In order to allow Maya to find AdonisFX, that environment variable has to include the path where the AdonisFX.mod file is located. There are two methods of configuring this variable: Setting the value in the `Maya.env` config file; or setting the value in the system to be permanent.

#### Configure Maya.env File

TODO

- Windows: `drive:/Users/username/Documents/maya/%MAYA_VERSION%`
- Linux: `~/maya/$MAYA_VERSION`

#### Configure System Environment Variables

TODO

> [!NOTE = Set Environment Variale]
> === Windows
> 
> `set MAYA_MODULE_PATH=%MAYA_MODULE_PATH%;/path/to/AdonisFX/folder`
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