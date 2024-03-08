# Licensing

AdonisFX requires a successful license activation for commercial use. For non-commercial and testing purposes a trial period of 30 days can be requested.
In this page the different licensing components of AdonisFX will be explained in combination with the requirements and steps for activating the product.

AdonisFX supports two *Licensing Modes*:

- **Node-Locked Licensing:** License mode that locks AdonisFX to one particular computer with a particular hardware footprint. Using the license key on a different computer would disable the ability to activate the software.
- **Floating Licensing:** License mode that allows different users to request licenses from a common license pool (served by a server) avoiding so the use restriction of the software to a single machine.

AdonisFX also distinguishes between two *Licensing Types*:

- **Interactive:** License type that allows the user to use AdonisFX from the graphical interface of the software where AdonisFX was loaded. This licensing type is intended for users that want to build scenes, manipulate and interact with AdonisFX using visual and interactive feedback.
- **Batch:** License type that allows the user to use AdonisFX from a batch script or terminal without the ability to use the graphical interface for manipulating the software. This licensing type is intended for users that want to run AdonisFX from a terminal to for example render a scene on the farm after setting the scene up using an Interactive License.

To be able to activate AdonisFX it is required to purchase a `PRODUCT KEY`. Product keys can be purchased through Inbibo's official website [PENDING](https://www.inbibo.co.uk/). AdonisFX product keys have the following characteristics:

- A `PRODUCT KEY` is associated to one single license type: Interactive or Batch. If the user wants to use AdonisFX both in Interactive and Batch mode, two separate product keys have to be purchased.
- A product key consists of **28** alphanumeric characters separated by "-" which is provided to the user when purchasing AdonisFX through the website: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**

To support different ways of activating a `PRODUCT KEY`, two ways of activating AdonisFX are supported:

- **Online Activation:** This activation mode required the user to be connected to the internet. This process allows AdonisFX to connect to the licensing server for validation and does not require the user to create XML files for the activation process.
- **Offline Activation:** This activation mode does not require the user to be connected to the internet. Through different XML files (activation request file and activation response file) it is possible to activate licenses on machines that do not have direct access to the internet. This activation mode requires the generation of several XML files which have to be interchanged with support for the activation process to conclude.

## Node-Locked Licensing

Node-Locked Licensing in AdonisFX requires the activation of a `PRODUCT KEY` on one single machine. As commented before, this activation process can be concluded using an online or offline process and requires the user to activate the product for batch and interactive modes separately.

Node-Locked Licensing product keys can be purchased through Inbibo's official website [PENDING](https://www.inbibo.co.uk/).

To be able to move node-locked licenses to a different machine the license has to be deactivated and activated again on the new machine.

> [!NOTE]
> Node-Locked Licensing is the default license mode in AdonisFX. To explicitly switch to Node-Locked licensing in AdonisFX set the environment variable `ADN_LICENSE_MODE` to `0`.

### Interactive

**Online Node-Locked Interactive Activation**

This activation mode *requires access to the internet* for activating licenses.

Whenever activating AdonisFX for the first time for a specific DCC in interactive mode, a series of dialogs requesting information are prompted. These dialogs allow to enter a valid `PRODUCT KEY` or to launch AdonisFX in trial mode for non-commercial purposes.

To activate AdonisFX in Online Node-Locked Interactive mode:
  1. Load the plug-in from the desired location depending on the target DCC.
  2. A dialog will show up with two options: **Activate** to enter a valid `PRODUCT KEY` and activate AdonisFX; **Continue With Trial** to start or continue a 30 day trial period.

<figure style="width:80%; margin-left:10%" markdown>
      ![Activation Dialog](images/adn_activation_dialog.png)
      <figcaption><b>Figure 1:</b> Activation Dialog.</figcaption>
</figure>

    
  3. Enter a valid product key in the text edit after selecting **Activate**.

<figure style="width:80%; margin-left:10%" markdown>
      ![Activation Add Product Key](images/adn_add_product_key_dialog.png)
      <figcaption><b>Figure 2:</b> Activation Add Product Key.</figcaption>
</figure>

    - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
  4. After entering a valid product key and pressing **Activate** a confirmation dialog will appear.

<figure style="width:80%; margin-left:10%" markdown>
      ![Product Activated Dialog](images/adn_activated_product_key_dialog.png)
      <figcaption><b>Figure 3:</b> Product Activated Dialog.</figcaption>
</figure>

> [!NOTE]
> If the product key is invalid or connecting with the licensing servers failed, a dialog will appear suggesting to retry the activation.

<figure style="width:80%; margin-left:10%" markdown>
      ![Activation Retry Adding Product Key](images/adn_try_again_product_key_dialog.png)
      <figcaption><b>Figure 4:</b> Activation Retry Adding Product Key.</figcaption>
</figure>

  5. AdonisFX is activated and ready to be used.

> [!NOTE]
> For deactivating licenses, please contact support.

**Offline Node-Locked Interactive Activation**

This activation mode does *not require access to the internet* for activating licenses.

To be able to activate AdonisFX in interactive mode without relying on internet access an *Activation Request* and a *Activation Response* have to be generated.
To ease this process several executable files are provided to generate the associated XML files for activation.

To activate AdonisFX in Offline Node-Locked Interactive mode:

  1. Open `AdonisFX/bin`.
  2. Run `OfflineRequest` from `AdonisFX/bin` with admin privileges.
  3. Select **Interactive** mode by entering the value `0`.
  4. Enter a valid product key.
      - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
      - A XML file `InteractiveOfflineRequest.xml` will be generated in the same folder.
  5. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request (username and date).
  6. In a maximum of 24h an `InteractiveOfflineResponse.xml` will be returned to the source e-mail address.
  7. Download and save the response in the same folder `AdonisFX/bin`.
  8. Execute `OfflineReponse` from `AdonisFX/bin` with admin privileges.
  9. Select **Interactive** mode again by entering the value `0`.
  10. The response will be registered and AdonisFX will be ready to be used.
      - Once the activation period has concluded, a new activation request and response have to be generated.

> [!NOTE]
> For deactivating licenses, please contact support.

### Batch

**Online Node-Locked Batch Activation**

This activation mode *requires access to the internet* for activating licenses.

Whenever activating AdonisFX for the first time for a specific DCC in batch mode, a product key has to be registered previously. Activating batch mode requires the use of an executable that eases the activation process of the product.

To activate AdonisFX in Online Node-Locked Batch mode:

  1. Run `ActivateBatch` from `AdonisFX/bin` with admin privileges.
  2. Enter the `PRODUCT KEY`.
      - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
  3. AdonisFX is activated and ready to be used.

**Offline Node-Locked Batch Activation**

This activation mode does *not require access to the internet* for activating licenses.

To be able to activate AdonisFX in batch mode without relying on internet access an *Activation Request* and a *Activation Response* have to be generated.
To ease this process several executable files are provided to generate the associated XML files for activation.

To activate AdonisFX in Offline Node-Locked Batch mode:

  1. Open `AdonisFX/bin`.
  2. Run `OfflineRequest` from `AdonisFX/bin` with admin privileges.
  3. Select **Batch** mode by entering the value `1`.
  4. Enter a valid product key.
      - A XML file `BatchOfflineRequest.xml` will be generated in the same folder.
  5. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request (username and date).
  6. In a maximum of 24h a `BatchOfflineResponse.xml` will be returned to the source e-mail address.
  7. Download and save the response in the same folder `AdonisFX/bin`.
  8. Execute `OfflineReponse` from `AdonisFX/bin` with admin privileges.
  9. Select **Batch** mode again by entering the value `1`.
  10. The response will be registered and AdonisFX will be ready to be used.
      - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
      - Once the activation period has concluded, a new activation request and response have to be generated.

> [!NOTE]
> For deactivating licenses, please contact support.

### Trial

AdonisFX allows the user to use the product for **30 days** in Node-Locked Interactive mode. This means that the trial can be used using the graphical interface for one single machine at a time. The trial period requires activation which can be handled in an online or offline way.

Trial licenses are intended for testing and non-commercial purposes. To use AdonisFX for commercial purposes a `PRODUCT KEY` must be purchased through Inbibo's official website [PENDING](https://www.inbibo.co.uk/) and activated.

See the **AdonisFX EULA** (PENDING) for details.

**Online Trial Activation**

This activation mode *requires access to the internet* for activating the trial mode.

It will allow the user to use AdonisFX for 30 days without providing a `PRODUCT KEY`. Once that trial period is over, the user will be asked to introduce a valid product key.

To activate AdonisFX in Online Node-Locked Interactive Trial mode:

  1. Load the plug-in from the desired location depending on the target DCC.
  2. Select **Continue With Trial** from the activation dialog.

<figure style="width:80%; margin-left:10%" markdown>
        ![Activation Dialog](images/adn_activation_dialog.png)
        <figcaption><b>Figure 9:</b> Activation Dialog.</figcaption>
</figure>
      
  3. AdonisFX will inform about the amount of days left for the trial license.

<figure style="width:30%; margin-left:10%" markdown>
        ![Trial Dialog](images/adn_your_trial_expires_dialog.png)
        <figcaption><b>Figure 10:</b> Trial Dialog.</figcaption>
</figure>
      
  4. The trial will deactivate the product after 30 days and will ask for a valid product key.
  5. AdonisFX is activated and ready to be used in trial mode.

**Offline Trial Activation**

This activation mode does *not require access to the internet* for activating the trial mode.

It will allow the user to use AdonisFX for 30 days without providing a `PRODUCT KEY`. Once that trial period is over, the user will be asked to introduce a valid product key.

To activate AdonisFX in Offline Node-Locked Interactive Trial mode:

  1. Open `AdonisFX/bin`.
  2. Run `TrialOfflineRequest` from `AdonisFX/bin` with admin privileges.
  3. Enter a valid product key.
      - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
      - A XML file `TrialOfflineRequest.xml` will be generated in the same folder.
  4. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request (username and date).
  5. In a maximum of 24h a `TrialOfflineResponse.xml` will be returned to the source e-mail address.
  6. Download and save the response in the same folder `AdonisFX/bin`.
  7. Execute `TrialOfflineResponse` from `AdonisFX/bin` with admin privileges.
  8. The response will be registered and AdonisFX will be ready to be used.
      - Once the activation period has concluded, a new activation request and response have to be generated.

## Floating Licensing

This section will explain how to configure, run and set-up the licensing server and AdonisFX for leasing floating licenses when the goal is to not restrict the use of AdonisFX to one single machine. AdonisFX floating licensing system requires the use of a license server in charge of providing, dropping and handling licenses from an active lease "pool". When the amount of requested licenses surpass the amount of licenses purchased for that floating license server no further activations of AdonisFX can be made until a lease is dropped and returned to the lease "pool". If for example 20 licenses had been purchased, then one of them will remain leased until the plug-in is unloaded from the target DCC.

It is possible to run the license server on one operating system and run instances of AdonisFX on a different operating system.

The licensing server is provided and shipped with the installation of AdonisFX for x64 architectures and can be run on Windows or Linux. For more builds please visit [https://wyday.com/download/](https://wyday.com/download/).

To be able to request leases from the license server it is necessary to activate the product with a `PRODUCT KEY` on the server side. Once activated it is required to have direct connection between the requestor AdonisFX instance and the licensing server to be able to balance the leases accordingly.

In AdonisFX the steps for setting up floating licenses is the following:

  1. Locate or download the server software.
  2. Configure the server to the expected requirements using the associated config file.
  3. Activate the server using online or offline activation using a purchased `PRODUCT KEY`.
  4. Start the server to start providing leases to the client instances of AdonisFX.

> [!NOTE]
> Node-Locked Licensing is defaulted in AdonisFX. To explicitly switch to Floating licensing in AdonisFX set the environment variable `ADN_LICENSE_MODE` to `1`.

### Install Server

#### Windows

The first step to be able to serve leases from the lease pool is to activate, configure and run/install the licensing server on a dedicated machine.

The steps to run or install the floating licensing server on a dedicated Windows machine are the following:

  1. Locate the `TurboFloatServer.exe` in `AdonisFX/licensing/turbo_float_server`. If a different executable is required please visit [https://wyday.com/download/](https://wyday.com/download/).
  2. Copy the folder to a preferred location.
  3. Copy and paste the `TurboActivate.dat` file (interactive or batch, depending on the server to install) in the same location:
      - `AdonisFX/licensing/interactive/TurboActivate.dat` for interactive mode licenses.
      - `AdonisFX/licensing/batch/TurboActivate.dat` for batch mode licenses.
  4. The content after copying the files should follow this structure:

<figure style="width:80%; margin-left:10%" markdown>
        ![Turbo Float Folder](images/adn_turbo_float_folder.png)
        <figcaption><b>Figure 11:</b> Turbo Float Folder.</figcaption>
</figure>
      
  5. Before running the license server and activating the license, several elements of the `TurboFloatServer-config.xml` can be tweaked. Like for example:
      - *Connection port, thread count, lease length, logs, grace periods, and proxies*. For more information visit [Configuring the TurboFloat Server](https://wyday.com/limelm/help/turbofloat-server/#config). Write down the configured port number for when setting up the environment variables in the **Run** section.
      - Find the full list of customizable parameters in the `.xml` file comments.

**Online Floating Server Activation**

This activation mode *requires access to the internet* for activating the floating licensing server.

Activating floating licenses only requires the activation of the licensing server which will be the one in charge of handling and balancing the leases.

The steps to activate the floating licensing server online are the following:

  1. Open a terminal in the folder where the `TurboFloatServer.exe` is located.
  2. Run the following command for activation: `TurboFloatServer.exe -a="YOUR-PRODUCT-KEY"`
      - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
      - Make sure to open the terminal with admin privileges.
      - This step assumes that the server `.xml` file and `.dat` file are located in the same folder as the server executable. To provide a custom path run the following command for the activation: `TurboFloatServer.exe -a="YOUR-PRODUCT-KEY" -pdets="YourTurboActivate.dat" -config="Config.xml"`
      - Deactivate an activated license: `TurboFloatServer.exe -deact`
  3. The server is now ready and can be run with the commands explained in the **Run** section.

**Offline Floating Server Activation**

This activation mode does not *require access to the internet* for activating the floating licensing server.

Activating floating licenses only requires the activation of the licensing server which will be the one in charge of handling and balancing the leases. In some cases this activation must happen without the access to the internet. To be able to activate AdonisFX using floating licensing without relying on internet access an *Activation Request* and a *Activation Response* have to be generated.

The steps to activate the floating licensing server online are the following:

  1. Open a terminal in the folder where the `TurboFloatServer.exe` is located.
  2. Run the following command to generate the activation request: `TurboFloatServer.exe -a="YOUR-PRODUCT-KEY" -areq="<PATH>/ActivationRequest.xml"`
      - An `ActivationRequest.xml` will be stored on disk if the activation process succeeded.
  3. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request (username and date).
  4. In a maximum of 24h an `ActivationResponse.xml` will be returned to the source e-mail address.
  5. Run the following command to obtain the data from the activation response and activate the server: `TurboFloatServer.exe -a -aresp="<PATH>/ActivationResponse.xml"`
  6. The server is now ready and can be run with the commands explained in the **Run** section.

> [!NOTE]
> - Monthly licenses require an internet connection. Floating licenses require internet only for the license server. Workstations can remain disconnected and protected.
> - For deactivating licenses, please contact support.

#### Linux

The first step to be able to serve leases from the lease pool is to activate, configure and run/install the server on a dedicated machine.

The steps to run or install the floating licensing server on a dedicated Linux machine are the following:

  1. Locate the `turbofloatserver` in `AdonisFX/licensing/turbo_float_server`. If a different executable is required please visit [https://wyday.com/download/](https://wyday.com/download/).
  2. Copy the folder to a preferred location.
  3. Copy and paste the `TurboActivate.dat` file (interactive or batch, depending on the server to install) in the same location:
      - `AdonisFX/licensing/interactive/TurboActivate.dat` for interactive mode licenses.
      - `AdonisFX/licensing/batch/TurboActivate.dat` for batch mode licenses.
  4. The content after copying the files should following a similar structure as to Windows.
  5. Before running the license server and activating the license, several elements of the `TurboFloatServer-config.xml` can be tweaked. Like for example:
      - *Connection port, thread count, lease length, logs, grace periods, and proxies*. For more information visit [Configuring the TurboFloat Server](https://wyday.com/limelm/help/turbofloat-server/#config). Write down the configured port number for when setting up the environment variables in the **Run** section.
      - Find the full list of customizable parameters in the `.xml` file comments.

**Online Floating Server Activation**

This activation mode *requires access to the internet* for activating the floating licensing server.

Activating floating licenses only requires the activation of the licensing server which will be the one in charge of handling and balancing the leases.

The steps to activate the floating licensing server online are the following:

  1. Open a terminal in the folder where the `turbofloatserver` is located.
  2. Run the following command for activation: `./turbofloatserver -a="YOUR-PRODUCT-KEY"`
      - It might be require to launch this command with `sudo` privileges.
      - The `PRODUCT KEY` has the following format: **XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX**
      - This step assumes that the server `.xml` file and `.dat` file are located in the same folder as the server executable. To provide a custom path run the following command for the activation: `./turbofloatserver -a="YOUR-PRODUCT-KEY" -pdets="YourTurboActivate.dat" -config="Config.xml"`
      - Deactivate an activated license: `./turbofloatserver -deact`
  3. The server is now ready and can be run with the commands explained in the **Run** section.

**Offline Floating Server Activation**

This activation mode does not *require access to the internet* for activating the floating licensing server.

Activating floating licenses only requires the activation of the licensing server which will be the one in charge of handling and balancing the leases. In some cases this activation must happen without the access to the internet. To be able to activate AdonisFX using floating licensing without relying on internet access an *Activation Request* and a *Activation Response* have to be generated.

The steps to activate the floating licensing server online are the following:

  1. Open a terminal in the folder where the `turbofloatserver` is located.
  2. Run the following command to generate the activation request: `./turbofloatserver -a="YOUR-PRODUCT-KEY" -areq="<PATH>/ActivationRequest.xml"`
      - An `ActivationRequest.xml` will be stored on disk if the activation process succeeded.
  3. Send the request file to **adnsupport@inbibo.co.uk** providing enough information to backtrack the source of the activation request (username and date).
  4. In a maximum of 24h an `ActivationResponse.xml` will be returned to the source e-mail address.
  5. Run the following command to obtain the data from the activation response and activate the server: `./turbofloatserver -a -aresp="<PATH>/ActivationResponse.xml"`
  6. The server is now ready and can be run with the commands explained in the **Run** section.

> [!NOTE]
> - Monthly licenses require an internet connection. Floating licenses require internet only for the license server. Workstations can remain disconnected and protected.
> - For deactivating licenses, please contact support.

### Run 

To be able to run AdonisFX using floating license these 4 criteria have to be met:

  1. The floating server is running or installed and machines have access to it.
  2. The machine with AdonisFX installed has direct access to the floating server. Use `ping` command to check connectivity.
  3. The licensing mode is set to floating in AdonisFX.
  4. The server address is properly configured on the client machine.

#### Run the floating server

##### Windows

To run the floating server on Windows (after following the activation steps) execute the following command: `TurboFloatServer.exe -x` or `TurboFloatServer.exe -x -pdets="YourTurboActivate.dat" -config="Config.xml"` when using custom destinations for the `.xml` and `.dat` files. To configure the server properly from the configuration file it is required to do the modifications prior to launching the server.

It is also possible to install the server avoiding the need to run the server manually: `TurboFloatServer.exe -i` or `TurboFloatServer.exe -i -pdets="YourTurboActivate.dat" -config="Config.xml"` when using custom destinations for the `.xml` and `.dat` files. For more information visit [Installing the TurboFloat Server](https://wyday.com/limelm/help/turbofloat-server/#install).

For more commands and information for deactivation refer to [https://wyday.com/limelm/help/turbofloat-server/](https://wyday.com/limelm/help/turbofloat-server/).

##### Linux

To run the floating server on Linux (after following the activation steps) execute the following command: `./turbofloatserver -x` or `./turbofloatserver -x -pdets="YourTurboActivate.dat" -config="Config.xml"` when using custom destinations for the `.xml` and `.dat` files. To configure the server properly from the configuration file it is required to do the modifications prior to launching the server.

It is not possible to install the server on Linux. For more information and information about deactivation, refer to [https://wyday.com/limelm/help/turbofloat-server/](https://wyday.com/limelm/help/turbofloat-server/).

#### Configure the server address on the machine with AdonisFX installed

After activating and launching the licensing server it is necessary to configure some parameters on the client machines where AdonisFX will be running on. These parameters are environment variables than set the licensing mode to floating licensing mode and set an IP address for the licensing server.

To conclude the configuration of the floating licensing in AdonisFX configure the following environment variables:

  1. Set `ADN_LICENSE_MODE` to `1`. Make sure to apply this change before launching AdonisFX.
  2. Set `ADN_LICENSE_SERVER` to `<IP-ADDRESS>:<PORT-NUMBER>`. Eg. `127.0.0.1:13`. If no port number was provided whe system will default to port `13`. Make sure to apply this change before launching AdonisFX.
  3. When launching AdonisFX in the target DCC, if the connection to the active license server could be established, it will try to obtain a valid lease and if granted activate the plug-in.
  4. AdonisFX is activated and ready to be used using floating licensing with the maximum amount of purchased leases. Depending on the configuration of the server it is possible to monitor the leases from the terminal.
