[![Build Status](https://github.com/ArduPilot/mavlink/workflows/Test%20and%20deploy/badge.svg)](https://github.com/ArduPilot/mavlink/actions?query=branch%3Amaster)

## MAVLink ##

MAVLink -- Micro Air Vehicle Message Marshalling Library.

MAVLink is a very lightweight, header-only message library for communication between drones and/or ground control stations. It consists primarily of message-set specifications for different systems ("dialects") defined in XML files, and Python tools that convert these into appropriate source code for [supported languages](https://mavlink.io/en/#supported_languages). There are additional Python scripts providing examples and utilities for working with MAVLink data.

> **Tip** MAVLink is very well suited for applications with very limited communication bandwidth. Its reference implementation in C is highly optimized for resource-constrained systems with limited RAM and flash memory. It is field-proven and deployed in many products where it serves as interoperability interface between components of different manufacturers.

Key Links:
* Development Website: https://ardupilot.org/dev/
* Source: [Mavlink Generator](https://github.com/ArduPilot/pymavlink)
* Discussion: [Discord Mavlink Channel](https://discord.com/channels/674039678562861068/728017546313466047)
* Discussion: [Discord pymavlink Channel](https://discord.com/channels/674039678562861068/930641827592306718)
* [Documentation/Website](https://mavlink.io/en/) (mavlink.io/en/)
* [Discussion/Support](https://mavlink.io/en/#support) (Slack)
* [Contributing](https://mavlink.io/en/contributing/contributing.html)

### License ###

MAVLink is licensed under the terms of the Lesser General Public License (version 3) of the Free Software Foundation (LGPLv3). The C-language version of MAVLink is a header-only library which is generated as MIT-licensed code. MAVLink can therefore be used without limits in any closed-source application without publishing the source code of the closed-source application.

See the *COPYING* file for more info.

# More information by @h3rm4nn-99

# What's this?
This repo contains a fork of the main MAVLink project. The key difference between this version and the upstream one consists in the addition of a novel **message definition file** that contains (as of now) three new messages:
- `KEYEXCHANGE`: this message enables the UAV to share its **public key** with the GCS;
- `KEYEXCHANGEGCS`: likewise, this message enables the GCS to share its **public key** with the UAV. This message has to be sent in response to the previous one;
- `CAPSULE`: since this project deals with a KEM, we need to generate a **capsule** that contains the **session key** to be used with a **symmetric cipher**. This message enables the UAV to send the KEM capsule to the GCS.
- `CAPSULEACK`: this message is sent by the GCS in response to a CAPSULE message sent by the UAV

# How do I generate the library?

~~To generate the new headers you can use the included `mavgenerate.py` script. This tools includes an easy-to-use GUI.~~ 

~~Assuming you have already cloned this repo and you have `python3` installed on your system, run this command in the repo root:~~

```bash
$ python3 mavgenerate.py
```

~~When the tool opens, point it to the [ardupilotmega.xml](message_definitions/v1.0/ardupilotmega.xml) file to use the custom definition and specify an output folder to store the newly-generated headers. Just make sure to specify **C** as the programming language and **2.0** as the wire protocol.~~

Since this repository is a submodule of the **ardupilot** project, the entire library will be generated during its build process.

# I'm too lazy, give me the headers already
~~No ready-made headers are provided as of now. They will be added to a specific repository when the key exchange protocol becomes ready.~~

The customized library is available [here](https://github.com/h3rm4nn-99/generated-mavlink-headers)
