# Licensing

AdonisFX requires a successful license activation for commercial use. For non-commercial and testing purposes a trial period of 30 days can be requested.
In this page the different licensing components of AdonisFX will be explained in combination with the requirements and steps for activating the product.

AdonisFX supports two *Licensing Modes*:

- **Node-Locked Licensing:** License mode that locks AdonisFX to one particular computer with a particular hardware footprint. Using the license key on a different computer would disable the ability to activate the software.
- **Floating Licensing:** License mode that allows different users to request licenses from a common license pool (served by a server) avoiding so the use restriction of the software to a single machine.

AdonisFX also distinguishes between two *Licensing Types*:

- **Interactive:** License type that allows the user to use AdonisFX from the graphical interface of the software where AdonisFX was loaded. This licensing type is intended for users that want to build scenes, manipulate and interact with AdonisFX using visual and interactive feedback.
- **Batch:** License type that allows the user to use AdonisFX from a batch script or terminal without the ability to use the graphical interface for manipulating the software. This licensing type is intended for users that want to run AdonisFX from a terminal to for example render a scene on the farm after setting the scene up using an Interactive License.

To be able to activate AdonisFX it is required to purchase a `PRODUCT KEY`. Product keys can be purchase through Inbibo's official website [https://www.inbibo.co.uk/](https://www.inbibo.co.uk/). AdonisFX product keys have the following characteristics:

- A `PRODUCT KEY` is associated to one single license type: Interactive or Batch. If the user wants to use AdonisFX both in Interactive and Batch mode, two separate product keys have to be purchased.
- A product key consists of **28** alphanumeric characters separated by "-" which is provided to the user when purchasing AdonisFX throught the website: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**

To support different ways of activating a `PRODUCT KEY`, two ways of activating AdonisFX are supported:

- **On-line Activation:** This activation mode required the user to be connected to the internet. This process allows AdonisFX to connected to the licensing server for validation and does not require the user to create XML files for the activation process.
- **Off-line Activation:** This activation mode does not require the user to be connected to the internet. Through different XML files (activation request file and activation response file) is it possible to activate licenses on machines that do not have direct access to the internet. This activation mode requires the generation of several XML files which have to be interchanged with support for the activation process to conclude.

## Node-Locked Licensings

Node-Locked Licensing in AdonisFX requires the activation of a `PRODUCT KEY` on one single machine. As commented before, this activation process can be concluded using an on-line or off-line process and requires the user to activate the product for batch and interactive modes separately.

NOTE: Node-Locked Licensing is defaulted in AdonisFX. To explicitly switch to Node-Locked licensing in AdonisFX set the environment variable `ADN_LICENSE_MODE` to `0`.

### Interactive

**Online Node-Locked Interactive Activation**

This activation mode *requires access to the internet* for activating licenses.

Whenever activating AdonisFX for the first time for a specific DCC in interactive mode, a series of dialogs requesting information are prompted. These dialogs allow to enter a valid `PRODUCT KEY` or to launch AdonisFX in trial mode for non-commercial purposes.

To activate AdonisFX in Online Node-Locked Interactive mode:

1. Load the plug-in from the desired location depending on the target DCC.
2. A dialog will show up with two options:

    <figure style="width:80%" markdown>
      ![Activation Dialog](images/adn_activation_dialog.png)
      <figcaption><b>Figure 1:</b> Activation Dialog.</figcaption>
    </figure>

    - **Activate:** Enter a valid `PRODUCT KEY` and activate AdonisFX.
    - **Continue With Trial:** Continue with the 30 day trial period.
 
3. Enter a valid product key in the text edit after selecting **Activate**:

    <figure style="width:80%" markdown>
      ![Activation Add Product Key](images/adn_add_product_key_dialog.png)
      <figcaption><b>Figure 2:</b> Activation Add Product Key.</figcaption>
    </figure>

    - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**

4. After entering a valid product key a confirmation dialog will appear:
    <figure style="width:80%" markdown>
      ![Activation Add Product Key](images/adn_activated_product_key_dialog.png)
      <figcaption><b>Figure 3:</b> Activation Add Product Key.</figcaption>
    </figure>

    NOTE: If the product key is invalid or connecting with the licensing servers failed, a dialog will appear suggesting to try the activation again.
    <figure style="width:80%" markdown>
      ![Activation Retry Adding Product Key](images/adn_try_again_product_key_dialog.png)
      <figcaption><b>Figure 4:</b> Activation Retry Adding Product Key.</figcaption>
    </figure>

5. AdonisFX is activated and ready to be used.

**Offline Node-Locked Interactive Activation**

This activation mode does *not require access to the internet* for activating licenses.

To be able to activate AdonisFX in interactive mode without relying on internet access an *Activation Request* and a *Activation Response* have to be generated.
To agilize this process several executable files are provided to generate the associated XML files for activation.

To activate AdonisFX in Offline Node-Locked Interactive mode:

1. Open `AdonisFX/bin`.
2. Run `OfflineRequest` from `AdonisFX/bin` with admin priviledges.
3. Select **Interactive** mode by entering the value `0`.
4. Enter a valid product key.
    - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
    - A XML file `InteractiveOfflineRequest.xml` will be generated in the same folder.

5. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request.
6. In a maximum of 24h an `InteractiveOfflineResponse.xml` will be returned to the source e-mail address.
7. Save the response in the same folder `AdonisFX/bin`.
8. Execute `OfflineReponse` from `AdonisFX/bin` with admin priviledges.
9. Select **Interactive** mode again by entering the value `0`.
10. The response will be registered and AdonisFX will be ready to be used.
    - Once the activation period has concluded, a new activation request and reponse has to be generated.

### Batch

**Online Node-Locked Batch Activation**

This activation mode *requires access to the internet* for activating licenses.

Whenever activating AdonisFX for the first time for a specific DCC in batch mode, a product key has to be registered previously. Activating batch mode requires the use of an executable that agilizes the activation of the product.

To activate AdonisFX in Online Node-Locked Batch mode:

1. Run `ActivateBatch` from `AdonisFX/bin` with admin priviledges.
2. Enter the `PRODUCT KEY`
    - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
3. AdonisFX is activated and ready to be used.

**Offline Node-Locked Batch Activation**

This activation mode does *not require access to the internet* for activating licenses.

To be able to activate AdonisFX in batch mode without relying on internet access an *Activation Request* and a *Activation Response* have to be generated.
To agilize this process several executable files are provided to generate the associated XML files for activation.

To activate AdonisFX in Offline Node-Locked Batch mode:

1. Open `AdonisFX/bin`.
2. Run `OfflineRequest` from `AdonisFX/bin` with admin priviledges.
3. Select **Batch** mode by entering the value `1`.
4. Enter a valid product key.
    - A XML file `BatchOfflineRequest.xml` will be generated in the same folder.

5. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request.
6. In a maximum of 24h an `BatchOfflineResponse.xml` will be returned to the source e-mail address.
7. Save the response in the same folder `AdonisFX/bin`.
8. Execute `OfflineReponse` from `AdonisFX/bin` with admin priviledges.
9. Select **Batch** mode again by entering the value `1`.
10. The response will be registered and AdonisFX will be ready to be used.
    - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
    - Once the activation period has concluded, a new activation request and reponse has to be generated.

### Trial

AdonisFX allows the user to use the product for **30 days** in Node-Locked Interactive mode. This means that the trial can be used using the graphical interface for one single machine at a time. The trial period requires activation which can be handled in an on-line or off-line way.

Trial licenses are intended for testing and non-commercial purposes. To use AdonisFX for commercial purposes a `PRODUCT KEY` must be purchased and activated.

See the **AdonisFX EULA** for details.

**Online Trial Activation**

This activation mode does *not require access to the internet* for activating licenses.

It will allow the user to use AdonisFX for 30 days without providing a `PRODUCT KEY`. Once that trial period is over, the user will be asked to introduce a valid product key.

To activate AdonisFX in Online Node-Locked Interactive Trial mode:

1. Load the plug-in from the desired location depending on the target DCC.
2. Select **Continue With Trial** from the activation dialog.

    <figure style="width:80%" markdown>
      ![Activation Dialog](images/adn_activation_dialog.png)
      <figcaption><b>Figure 9:</b> Activation Dialog.</figcaption>
    </figure>

3. AdonisFX will inform about the amount of days left for the trial license.
    <figure style="width:80%" markdown>
      ![Trial Dialog](images/adn_your_trial_expires_dialog.png)
      <figcaption><b>Figure 10:</b> Trial Dialog.</figcaption>
    </figure>

4. The trial will deactivate the product after 30 days asking for a product key.
5. AdonisFX is activated and ready to be used in trial mode.

**Offline Trial Activation**

This activation mode does *not require access to the internet* for activating licenses.

It will allow the user to use AdonisFX for 30 days without providing a `PRODUCT KEY`. Once that trial period is over, the user will be asked to introduce a valid product key.

To activate AdonisFX in Offline Node-Locked Interactive Trial mode:

1. Open `AdonisFX/bin`.
2. Run `TrialOfflineRequest` from `AdonisFX/bin` with admin priviledges.
3. Enter a valid product key.
    - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
    - A XML file `TrialOfflineRequest.xml` will be generated in the same folder.
4. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request.
5. In a maximum of 24h an `TrialOfflineResponse.xml` will be returned to the source e-mail address.
6. Save the response in the same folder `AdonisFX/bin`.
7. Execute `TrialOfflineResponse` from `AdonisFX/bin` with admin priviledges.
8. The response will be registered and AdonisFX will be ready to be used.
    - Once the activation period has concluded, a new activation request and reponse has to be generated.

## Floating Licensing

NOTE: Node-Locked Licensing is defaulted in AdonisFX. To explicitly switch to Floating licensing in AdonisFX set the environment variable `ADN_LICENSE_MODE` to `1`.

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
