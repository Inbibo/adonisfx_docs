# Installation

## Maya

Adonis is distributed for Maya as a standard module. To install the module, please do the following:

1. Download the AdonisFX zipped package from the Inbibo's website [TODO: #2 add link].
2. Unzip the contents into the destination folder that you prefer.
3. Add folder containg the AdonisFX.mod file to the `MAYA_MODULE_PATH` environment variable.

To configure `MAYA_MODULE_PATH` you can directly modify the environment variable of the system. For example:

- Windows: `set MAYA_MODULE_PATH=%MAYA_MODULE_PATH%;/path/to/AdonisFX/folder`
- Linux: `export MAYA_MODULE_PATH=$MAYA_MODULE_PATH:/path/to/AdonisFX/folder`

An alternative method is to add `MAYA_MODULE_PATH = /path/to/AdonisFX/folder` in the `Maya.env` file which is located in:

- Windows: `drive:/Users/username/Documents/maya/%MAYA_VERSION%`
- Linux: `~/maya/$MAYA_VERSION`

## Houdini

Adonis is distributed for Houdini as a standard package. To install the package, please do the following:

1. Download the AdonisFX zipped package from the Inbibo's website [TODO: #2 add link].
2. Unzip the contents into the destination folder that you prefer.
3. Add folder containg the AdonisFX.json file to the `HOUDINI_PACKAGE_DIR` environment variable.

The `HOUDINI_PACKAGE_DIR` must be set in your environemnt. For example:

- Windows: `set HOUDINI_PACKAGE_DIR=%HOUDINI_PACKAGE_DIR%;/path/to/AdonisFX/folder`
- Linux: `export HOUDINI_PACKAGE_DIR=$HOUDINI_PACKAGE_DIR:/path/to/AdonisFX/folder`
