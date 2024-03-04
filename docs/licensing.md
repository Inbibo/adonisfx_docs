# Licensing

- Expose 2 licensing modes: Node-Locked or Floating
- Expose 2 licensing types: interactive or batch
- Explain activation requires a Product Key
  - Explain the Product Key is associated to a license type
  - Explain format of product keys XXXX-XXXX-etc
- Explain 2 activation modes: online (requires connection to the internet) or offline (requires the execution of programs and contact with support to send and receive XML files)

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
