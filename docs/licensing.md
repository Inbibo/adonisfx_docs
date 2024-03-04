# Licensing

AdonisFX requires a successful license activation for commercial use. For non-commercial and testing purposes a trial period of 30 days can be requested.
In this page the different licensing components of AdonisFX will be explained in combination with the requirements and steps for activating the product.

AdonisFX supports two *Licensing Modes*:

- **Node-Locked Licensing:** License mode that locks AdonisFX to one particular computer with a particular hardware footprint. Using the license key on a different computer would disable the ability to activate and use the software.
- **Floating Licensing:** License mode that allows different users to request licenses from a common license pool (served by a server) avoiding so the use restriction of the software to a single machine.

AdonisFX also distinguishes between two *Licensing Types*:

- **Interactive:** License type that allows the user to use AdonisFX from the graphical interface of the software where AdonisFX was loaded. This licensing type is intended for users that want to build scenes, manipulate and interact with AdonisFX using visual and interactive feedback.
- **Batch:** License type that allows the user to use AdonisFX from a batch script or terminal without the ability to use the graphical interface for manipulating the software. This licensing type is intended for users that want to run AdonisFX from a terminal, to for example render a scene on the farm after setting the scene up using an Interactive License.

To be able to activate AdonisFX it is required to purchase a **PRODUCT KEY**. Product keys can be puurchase through Inbibo's official website **https://www.inbibo.co.uk/**. AdonisFX product keys have the following characteristics:

- A **PRODUCT KEY** is associated to one single license type: Interactive or Batch. If the user wants to use AdonisFX both in Interactive and Batch mode, two separate product keys have to be purchased.
- A product key consists of **28** alphanumeric characters separated by "-" which is provided to the user when purchasing AdonisFX throught the website: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**

To support different ways of activating a **PRODUCT KEY**, two ways of activating AdonisFX are supported:

- **On-line Activation:** This activation mode required the user to be connected to the internet. This process allows AdonisFX to connected to the licensing server for validation and does not require the user to create XML files for the activation process.
- **Off-line Activation:** This activation mode does not require the user to be connected to the internet. Through different XML files (activation request file and activation response file) is it possible to activate licenses on machines that do not have direct access to the internet. This activation mode requires the generation of several XML files which have to be interchanged with support for the activation process to conclude.

## Node-Locked Licensing

- Requires activation
- Can be batch or interactive

### Interactive

**Online Node-Locked Interactive Activation**

- Via dialog on plugin load ("Activate")
- Add screenshots:
    - DIALOG_ACTIVATE_QUESTION
    - DIALOG_ENTER_PRODUCT_KEY
    - DIALOG_ACTIVATED_SUCCESSFULLY

**Offline Node-Locked Interactive Activation**

- Via OfflineRequest and OfflineResponse
- Executables have to be run with adnim privileges
- Execute OfflineRequest (from the given folder AdonisFX/bin)
- Select Interactive in the console (add screenshot)
- Enter product key
- An xml file "InteractiveOfflineRequest.xml" will be generated in the same folder
- Send the request file to **adnsupport@inbibo.co.uk**
- In maximum 24h you will receive the response InteractiveOfflineResponse.xml
- Make sure to save the response in the same folder AdonisFX/bin
- Exeucte OfflineReposnse (from the given folder AdonisFX/bin)
- Select Interactive in the console
- The response will be registered

### Batch

**Online Node-Locked Batch Activation**

- Via ActivateBatch.exe (in AdonisFX/bin)
- Admin privileges are required
- Execute the program
- Enter your product key
- The product will get activated

**Offline Node-Locked Batch Activation**

- Via OfflineRequest and OfflineResponse
- Execute OfflineRequest (from the given folder AdonisFX/bin)
- Select Batch in the console (add screenshot)
- Enter product key
- An xml file "BatchOfflineRequest.xml" will be generated in the same folder
- Send the request file to **adnsupport@inbibo.co.uk**
- In maximum 24h you will receive the response BatchOfflineResponse.xml
- Make sure to save the response in the same folder AdonisFX/bin
- Exeucte OfflineReposnse (from the given folder AdonisFX/bin)
- Select Batch in the console
- The response will be registered

### Trial

- Only available node-locked + interactive
- 30 days
- Requires activation, that can be online or offline

**Online Trial Activation**

- Via dialog on plugin load ("Continue With Trial")
- Add screenshots:
    - DIALOG_ACTIVATE_QUESTION
    - DIALOG_TRIAL

**Offline Trial Activation**

- Via TrialOfflineRequest and TrialOfflineResponse
- Executables have to be run with adnim privileges
- Execute TrialOfflineRequest (from the given folder AdonisFX/bin)
- An xml file "TrialOfflineRequest.xml" will be generated in the same folder
- Send the request file to **adnsupport@inbibo.co.uk**
- In maximum 24h you will receive the response TrialOfflineResponse.xml
- Make sure to save the response in the same folder AdonisFX/bin
- Exeucte TrialOfflineResponse (from the given folder AdonisFX/bin)
- The response will be registered

## Floating Licensing

- Explain the turbofloat server is needed
- Explain that the windows and linux binaries provided are for x64, if you need another build, please download it from: https://wyday.com/download/
    - Interanl note: check how ragdolldynamics does: https://learn.ragdolldynamics.com/floating-licence/

### Install Server

- it can be found in AdonisFX/licensing/turbo_float_server
- copy the folder to the preferred location
- copy and paste the TurboActivate.dat file (interactive or batch, depending on the server you want to install) in the same location
- Add screenshot of the folder, how it should look: the binary, the config.xml file, the .dat file
- Explain that config.xml file can be edited

**Online Float Server Activation**

- run server with -a and the product key

**Offline Float Server Activation**

- run server with -areq and -a
- An xml file will be generated at the specified destination
- Send the request file to **adnsupport@inbibo.co.uk**
- In maximum 24h you will receive the response
- run -a -aresp providing the path to the response

### Run 

- Explain execute (windows and linux)
- Explain environment config ADN_LICENSE_MODE and ADN_LICENSE_SERVER
- Launch maya
