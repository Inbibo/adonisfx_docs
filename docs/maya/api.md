# API

### Experimental Python API

> [!CAUTION]
> - This API is experimental and will be subject to changes in following versions of AdonisFX.
> - The use of this API in production applications is not supported.

A Python API has been developed to allow Technical Directors implementing custom Python scripts to export and rebuild AdonisFX rigs from script. It allows users to extract the setup from a rig in Maya and rebuild it in another Maya scene. As this API is experimental, please do not hesitate to send an email to **adnsupport@inbibo.co.uk** to provide any feedback and/or requests. The support and development teams will work together to incorporate users' feedback and refine the implementation.

The API can be found in `AdonisFX/python/adn/api/adnx.py` and the definitions can be imported with the Python command `from adn.api.adnx import *`.
