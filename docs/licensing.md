# Licensing

AdonisFX requires a successful license activation for commercial use. For non-commercial and testing purposes a trial period of 30 days can be requested.
In this page the different licensing components of AdonisFX will be explained in combination with the requirements and steps for activating the product.

AdonisFX supports two *Licensing Modes*:

- **Node-Locked Licensing:** License mode that locks AdonisFX to one particular computer with a particular hardware footprint. After the activation on a computer, using the license key on a different computer would disable the ability to activate the software.
- **Floating Licensing:** License mode that allows different users to request licenses from a common license pool (served by a server) avoiding the use restriction of the software to a single machine.

AdonisFX also distinguishes between two *Licensing Types*:

- **Interactive:** License type that allows the user to use AdonisFX from the graphical interface of the software where AdonisFX was loaded. This licensing type is intended for users that want to build scenes, manipulate and interact with AdonisFX using visual and interactive feedback.
- **Batch:** License type that allows the user to use AdonisFX from a batch script or terminal without the ability to use the graphical interface for manipulating the software. This licensing type is intended for users that want to run AdonisFX from a terminal to for example render a scene on the farm after setting the scene up using an Interactive License.

To be able to activate AdonisFX it is required to purchase a `PRODUCT KEY`. Product keys can be purchased through Inbibo's official [website](https://inbibo.co.uk/adonisfx#prices). AdonisFX product keys have the following characteristics:

- A `PRODUCT KEY` is associated with one single license type: Interactive or Batch. If the user wants to use AdonisFX both in Interactive and Batch mode, two separate product keys have to be purchased.
- A product key consists of **28** alphanumeric characters separated by "-" which is provided to the user when purchasing AdonisFX through the website: `XXXX-XXXX-XXXX-XXXX-XXXX-XXXX-XXXX`.

## Node-Locked Licensing

Node-Locked Licensing in AdonisFX requires the activation of a `PRODUCT KEY` on one single machine. As commented before, this activation process requires the user to activate the product for batch and interactive modes separately.

> [!NOTE]
> Node-Locked Licensing is the default license mode in AdonisFX. To explicitly switch to Node-Locked licensing in AdonisFX, set the environment variable `ADN_LICENSE_MODE` to `0`.

### Interactive

Whenever activating AdonisFX for the first time for a specific DCC in interactive mode, a series of dialogs requesting information are prompted. These dialogs allow users to enter a valid `PRODUCT KEY` or to launch AdonisFX in trial mode for non-commercial purposes.

To activate AdonisFX in Node-Locked Interactive mode:
  1. Launch Maya.
  2. Load the plug-in.
  3. Go to AdonisFX Menu > *Activate License*. A dialog will show up with two options: *Activate* to enter a valid `PRODUCT KEY` in order to enable the full license; *Continue With Trial* to continue with the 30 day trial period.

<figure style="width:80%; margin-left:10%" markdown>
      ![Activation Dialog](images/licensing_activation_dialog.png)
      <figcaption><b>Figure 1</b>: Activation Dialog.</figcaption>
</figure>

  4. Click on Activate. A dialog will show up to introduce a product key.

<figure style="width:80%; margin-left:10%" markdown>
      ![Activation Add Product Key](images/licensing_add_product_key_dialog.png)
      <figcaption><b>Figure 2</b>: Activation Add Product Key.</figcaption>
</figure>
    
  5. Enter the product key associated with the Interactive Node-Locked License. A confirmation dialog will appear (Figure 3). If the product key is invalid or connecting with the licensing servers failed, a dialog will appear suggesting to retry the activation (Figure 4).

<figure style="width:80%; margin-left:10%" markdown>
      ![Product Activated Dialog](images/licensing_activated_product_key_dialog.png)
      <figcaption><b>Figure 3</b>: Product Activated Dialog.</figcaption>
</figure>

<figure style="width:80%; margin-left:10%" markdown>
      ![Activation Retry Adding Product Key](images/licensing_try_again_product_key_dialog.png)
      <figcaption><b>Figure 4</b>: Activation Retry Adding Product Key.</figcaption>
</figure>

  6. AdonisFX is activated. Restart Maya or reload the plugin to start using all features from AdonisFX.

> [!NOTE]
> - This activation mode requires access to the internet for activating licenses.
> - For deactivating licenses to switch to a different machine, please contact support.

### Batch

Whenever activating AdonisFX for the first time for a specific DCC in batch mode, a product key has to be registered previously. Activating batch mode requires the use of an executable that eases the activation process of the product.

To activate AdonisFX in Node-Locked Batch mode:

  1. Go to `AdonisFX/bin` in the AdonisFX installation folder.
  2. Run `ActivateBatch`.
  3. Enter the `PRODUCT KEY`.
  4. AdonisFX is activated and ready to be used.

### Trial

AdonisFX allows the user to use the product for **30 days** in Node-Locked Interactive mode. This means that the trial can be used using the graphical interface for one single machine at a time. The trial period requires activation which can be handled in an online or offline way.

Trial licenses are intended for testing and non-commercial purposes. To use AdonisFX for commercial purposes a `PRODUCT KEY` must be purchased through Inbibo's official [website](https://inbibo.co.uk/adonisfx#prices) and activated. See the AdonisFX [End User License Agreement](https://inbibo.co.uk/adonisfx-maya-eula) for details.

**Online Trial Activation**

It will allow the user to use AdonisFX for 30 days without providing a `PRODUCT KEY`. Once that trial period is over, the user will be asked to introduce a valid product key. If not provided, then AdonisFX will not load and could not be used.

In this case, the activation does not require any input from the user. The trial period is registered automatically the first time that AdonisFX is loaded from a workstation with internet access.

> [!NOTE]
> This activation mode requires access to the internet.

**Offline Trial Activation**

It will allow the user to use AdonisFX for 30 days without providing a `PRODUCT KEY`. Once that trial period is over, the user will be asked to introduce a valid product key. If not provided, then AdonisFX will not load and could not be used.

To activate AdonisFX in Offline Node-Locked Interactive Trial mode:

  1. Go to `AdonisFX/bin` in the AdonisFX installation folder.
  2. Run `TrialOfflineRequest` with admin privileges. An XML file `TrialOfflineRequest.xml` will be generated in the same folder.
  4. Send the request file to **adonis.support@inbibo.co.uk** providing enough information to backtrack the source of the activation request.
  5. In a maximum of 24h a `TrialOfflineResponse.xml` will be returned to the source e-mail address.
  6. Download and save the response in the same folder `AdonisFX/bin`.
  7. Execute `TrialOfflineResponse` (also in `AdonisFX/bin`) with admin privileges.
  8. The response will be registered and AdonisFX will be ready to be used.

> [!NOTE]
> This activation mode does not require access to the internet.

## Floating Licensing

This section will explain how to configure, run and set-up the licensing server for leasing floating licenses when the goal is to not restrict the use of AdonisFX to one single machine. AdonisFX floating licensing system requires the use of a license server in charge of providing, dropping and handling licenses from an active lease "pool". When the amount of requested licenses surpasses the amount of licenses purchased for that floating license server no further activations of AdonisFX can be made until a lease is dropped and returned to the lease "pool" (i.e. the plug-in is unloaded or the DCC process ends).

To be able to request leases from the license server it is necessary to activate the product with a `PRODUCT KEY` on the server side. Once activated it is required to have direct connection between the requestor instance and the licensing server to be able to balance the leases accordingly.

The following sections explain the steps to install and run the server, as well as how to configure the environment to allow processes request leases.

### Install Server

The licensing server is provided and shipped within the installation of AdonisFX for x64 architectures and can be run on Windows or Linux. For more architectures, please visit this [page](https://wyday.com/download/).

The first step to be able to serve leases from the lease pool is to activate, configure and run the licensing server on a dedicated machine:

1. Locate the server in `AdonisFX/licensing/turbo_float_server`.
2. Copy the folder to a preferred location.
3. Copy and paste the `TurboActivate.dat` file (interactive or batch, depending on the server to install) in the same location:
    - `AdonisFX/licensing/interactive/TurboActivate.dat` for interactive mode licenses.
    - `AdonisFX/licensing/batch/TurboActivate.dat` for batch mode licenses.
4. The content after copying the files should follow the structure in Figure 5.
5. Before running the license server and activating the license, several elements of the `TurboFloatServer-config.xml` can be tweaked. Like for example:
    - *Connection port, thread count, lease length, logs, grace periods, and proxies*. For more information visit this [page](https://wyday.com/limelm/help/turbofloat-server/#config). Write down the configured port number for when setting up the environment variables in this [section](#run-server).
    - Find the full list of customizable parameters in the `.xml` file comments.

<figure style="width:80%; margin-left:10%" markdown>
  ![Turbo Float Folder](images/licensing_turbo_float_folder.png)
  <figcaption><b>Figure 5</b>: Folder containing the TurboFloatServer (Windows) and the configuration files.</figcaption>
</figure>

### Activate Server

Activating floating licenses only requires the activation of the licensing server which will be the one in charge of handling and balancing the leases. To activate the server:

1. Open a terminal in the folder where the server is located with admin privileges.
2. Run the following command for activation:

> [!NOTE = Activate Server]
> === Windows
> 
> `TurboFloatServer.exe -a="PRODUCT-KEY"`
>
>  === Linux
>
> `./turbofloatserver -a="PRODUCT-KEY"`

3. The server is now ready and can be run with the commands explained in this [section](#run-server).

The activation command assumes that the server executable, the `.xml` file and the `.dat` file are located in the same folder. To provide a custom path to the configuration files, run the following command instead:

> [!NOTE = Activate Server With Custom Location]
> === Windows
> 
> `TurboFloatServer.exe -a="PRODUCT-KEY" -pdets="YourTurboActivate.dat" -config="Config.xml"`
>
>  === Linux
>
> `./turbofloatserver -a="PRODUCT-KEY" -pdets="YourTurboActivate.dat" -config="Config.xml"`

Remember that floating licenses require internet access only for the machine running the server, while the workstations intended to query leases to the server can remain disconnected and protected.

If the server needs to be installed in a different machine, it will be required to deactivate the license before being able to activate it again in the new machine. To deactivate a license, execute:

> [!NOTE = Activate Server]
> === Windows
> 
> `TurboFloatServer.exe -deact`
>
>  === Linux
>
> `./turbofloatserver -deact`

### Run Server

To run the floating server execute the command below. To configure the server properly from the configuration file, it is required to do any modifications to the file prior to launching the server.

> [!NOTE = Run Server]
> === Windows
> 
> `TurboFloatServer.exe -x`
>
>  === Linux
>
> `./turbofloatserver -x`

The command above assumes that the server executable, the `.xml` file and the `.dat` file are located in the same folder. To provide a custom path to the configuration files, run the following command instead:

> [!NOTE = Run Server]
> === Windows
> 
> `TurboFloatServer.exe -x -pdets="YourTurboActivate.dat" -config="Config.xml"`
>
>  === Linux
>
> `./turbofloatserver -x -pdets="YourTurboActivate.dat" -config="Config.xml"`

On Windows, it is also possible to install a service in charge of running the server in the background. Please, refer to this [link](https://wyday.com/limelm/help/turbofloat-server/#install) for more information.

### Client Configuration

To be able to run AdonisFX using a floating license, make sure the floating server is running and the client machine intended to use AdonisFX has direct access to the floating server. Then, configure the licensing mode and the IP address in the environment of the client machine:

  1. Set `ADN_LICENSE_MODE` to `1`. Make sure to apply this change before launching AdonisFX.
  2. Set `ADN_LICENSE_SERVER` for interactive licenses and `ADN_LICENSE_SERVER_BATCH` for batch licenses to `<IP-ADDRESS>:<PORT-NUMBER>` (e.g. `127.0.0.1:13`). If no port number was provided the system will default to port `13`.

When launching AdonisFX in the target DCC, if the connection to the active license server could be established, it will try to obtain a valid lease and if granted it will load the plug-in.

> [!NOTE]
> - Make sure to configure the required environment variables before loading AdonisFX.
> - Node-Locked Licensing is defaulted in AdonisFX meaning that if `ADN_LICENSE_MODE` is not set to `1` or not provided, then AdonisFX will attempt to load Node-Locked licenses.
