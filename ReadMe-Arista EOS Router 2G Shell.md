![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# **Arista EOS Router 2G Shell**  

Release date: June 2018

Shell version: 1.0.0

Document version: 1.0

# In This Guide

* [Overview](#overview)
* [Downloading the Shell](#downloading-the-shell)
* [Importing and Configuring the Shell](#importing-and-configuring-the-shell)
* [Updating Python Dependencies for Shells](#updating-python-dependencies-for-shells)
* [Typical Workflows](#typical-workflows)
* [References](#references)
* [Release Notes](#release-notes)


# Overview
A shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

### Networking Shells
CloudShell's networking shells provide L2 or L3 connectivity between resources and/or private cloud Apps.

### **Arista EOS Router 2G Shell**
**Arista EOS Router 2G** shell provides you with connectivity and management capabilities such as device structure discovery and power management for the **Arista EOS Router**. 

For more information on the **Arista EOS Router**, see the official **Arista** product documentation.

### Standard version
**Arista EOS Router 2G Shell** is based on the Networking Shell Standard version 5.0.2.

For detailed information about the shell’s structure and attributes, see the [Networking Shell Standard](https://github.com/QualiSystems/cloudshell-standards/blob/master/Documentation/networking_standard.md) in GitHub.

### Requirements

Release: **Arista EOS Router 2G Shell version 1.0.0**

▪ CloudShell version: **8.0 and above**

### Data Model

The shell's data model includes all shell metadata, families, and attributes.

#### **Arista EOS Router 2G Shell Families and Models**

The router families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
|CS_Router|Arista EOS Router 2G|Generic Arista EOS router 2G|
|CS_Chassis|Generic Chassis|Default router chassis|
|CS_Module|Generic Module|Modules located on the chassis|
|CS_SubModule|Generic Sub Module|Sub modules|
|CS_Port|Generic Port|Interface|
|CS_PortChannel|Generic Port Channel|Group of interfaces|
|CS_PowerPort|Generic Power Port|Power supply module|

#### **Arista EOS Router 2G Shell Attributes**

**Note:** Attributes noted with an * also appear in the **Discover** resource dialog box (**Inventory**>**Resource**>**Discover**).

The attribute names and types are listed in the following table:

|Attribute|Type|Default value|Description|
|:---|:---|:---|:---|
|Name|String||Name of the Arista EOS Router in CloudShell|
|Address*|String||IP address of the Arista EOS Router|
|Folder|String|Root|CloudShell folder in which to place the resource.|
|Visibility|Lookup|Family Default (Everyone)|Visibility determines who can see the resource in the diagram, search pane, and in the **Inventory** dashboard. By default the visibility is defined in the resource family and can be changed for a specific resource.<br> Possible values: **Family Default (Everyone)**, **Admin only**, and **Everyone**.|
|Remote Connection|Lookup|Family Default (Enable)|Remote connection determines if you can remotely connect to the resource. By default the remote connection is defined in the resource family and can be changed for a specific resource. <br>Possible values: **Family Default (Enable)**, **Enable**, and **Disable**.|
|User*|String||Username for Arista CLI (should be privileged user)|
|Password*|Password||Password for Arista CLI|
|Enable Password*|Password||Enable Password for Arista CLI|
|Sessions Concurrency Limit*|Numeric|1|Maximum number of concurrent sessions that the driver can open to the device. Defines the number of commands that can run concurrently. Default (1) means no concurrency.|
|System Name|String||A unique identifier for the device, if it exists in the device terminal/OS.|
|Contact Name|String||Name of contact registered in the device|
|OS Version|String||Operating system version|
|Vendor|String ||Name of device manufacturer|
|Location|String||Identifier of the device's physical location, for example, Lab1/Floor2/Row5/Slot4.|
|Model|String||The device model. This information is typically used for abstract resource filtering.|
|Model Name|String||The catalog name of the device model. This attribute will be displayed in CloudShell instead of the CloudShell model.|
|Enable SNMP*|Boolean|True|If set to **True**, and SNMP isn’t enabled on the device, the shell will automatically enable SNMP on the device when the Autoload command is called, using the **SNMP Write** or **Read Community** value. If the value is empty, this will result in an error. SNMP must be enabled on the device for the Autoload command to run successfully.| 
|Disable SNMP*|Boolean|False|If set to **True**, the shell will automatically disable SNMP after the Autoload command execution is completed.| 
|SNMP Read Community*|Password||SNMP Read Community string is like a password. Sent along with each SNMP Get Request and allows (or denies) access to the device for the Autoload functionality to run successfully.|
|SNMP Write Community*|Password||SNMP Write Community is like a password. Sent along with each SNMP Set Request and allows (or denies) changing MIB values.|
|SNMP V3 User|String||SNMP version 3 user name, relevant only if SNMP v3 is in use.|
|SNMP V3 Password|Password||SNMP version 3 password, relevant only if SNMP v3 is in use.|
|SNMP V3 Private Key|String||SNMP version 3 private key, relevant only if SNMP v3 is in use.|
|SNMP V3 Authentication Protocol|Lookup|No Authentication Protocol|Relevant only if SNMP v3 is in use. <br>Possible values: **No Authentication Protocol**, **MD5**, and **SHA**.|
|SNMP V3 Privacy Protocol|Lookup|No Privacy Protocol|Relevant only if SNMP v3 is in use. <br>Possible values: **No Privacy Protocol**, **DES**, **3DES-EDE**, **AES-128**, **AES-192**, and **AES-256**.|
|SNMP Version*|String|v2c|Specifies the SNMP version Autoload will use to load attributes. <br>Possible values: **v1**, **v2c**, and **v3**.|
|Console Server IP Address*|String||Shell allows you to connect to the device through the console server. IP Address of console server in IPv4 format.|
|Console User*|String||User name for the console server|
|Console Password*|Password||Password for the console server|
|Console Port*|Numeric||Port for the console server, usually the TCP port, which the device is associated with.|
|CLI Connection Type*|Lookup|Auto|Protocol which the shell will use to connect to the device. <br>Possible values: **Auto**, **Console**, **SSH**, **Telnet**, and **TCP**. <br>If **Auto** is selected, the driver will choose the available connection type automatically. |
|CLI TCP Port*|Numeric||TCP Port to user for CLI connection. If empty, a default CLI port will be used based on the chosen protocol, for example Telnet will use port 23.|
|Power Management*|Boolean|False|Used by the power management service, if enabled to determine whether to automatically manage the device power status.|
|Backup Type*|String|File System|Supported protocols for saving and restoring configuration and firmware files. <br>Possible values: **File System**, **FTP** and **TFTP**.| 
|Backup Location*|String||Used by the save and restore orchestration to determine where backups should be saved.|
|Backup User*|String||Username for the storage server used for saving and restoring configuration and firmware files.|
|Backup Password*|Password||Password for the storage server used for saving and restoring configuration and firmware files.| 
|VRF Management Name*|String||Default VRF Management if configured in the network and no input was passed in the **Save**, **Restore** or **Load Firmware** commands.|
|Model|String||Element model (Module or Chassis, etc.)|
|Serial Number|String||Element serial number (Module or Chassis, etc.)
|Model Name|String|||
|Version|String||Element version (Module or Chassis, etc.)|
|Mac Address|String||Interface Mac address|
|L2 Protocol Type|String||Interface protocol type|
|IPv4 Address|String||Interface IPv4 address|
|IPv6 Address|String||Interface IPv6 address|
|Port Description|String||Interface description|
|Bandwidth|Numeric|0|Interface speed|
|MTU|Numeric|0|Interface MTU|
|Duplex|Lookup|Half|Interface duplex.<br> Possible values: **Half**, or **Full**.|
|Adjacent|String||If Lldp is enabled on port, **Adjacent** shows connected device name and interface.|
|Protocol Type|Lookup|Transparent|Attribute for internal usage|
|Auto Negotiation|Boolean|False|Shows if Auto negotiation is enabled on the interface.|
|Association|String||Interfaces added to certain port-channel|


### Automation
This section describes the automation (drivers) associated with the data model. The shell’s driver is provided as part of the shell package. There are two types of automation processes, Autoload and Resource.  Autoload is executed when creating the resource in the Inventory dashboard, while resource commands are run in the Sandbox, providing that the resource has been discovered and is online.

|Command|Description|
|:-----|:-----|
|Autoload|Discovers the chassis, its hierarchy and attributes when creating the resource. The command can be rerun in the **Inventory** dashboard and not in the sandbox, as for other commands.|
|Health Check|Checks if the device is up and connectable.|
|Send Custom Command (I don't see this on the command pane of the resource in a blueprint)|Sends command (String) to the device, and prints the output. All commands will be executed in the **Enable** mode, however it will not allow to enter configuration mode.|
|Run Custom Config Command|Sends command to the device in configuration mode, and prints output. All commands will be executed in the enable mode, accessible only via the API.|
|Save|Creates a configuration file and saves it in the provided destination.<br>Set the command inputs as follows:<br>* **Folder Path** (String): ?????<br>* **Configuration Type** (Enum): **Startup** or **Running**<br>* **VRF Management Name**: ????|
|Restore|Restores a configuration file.<br>* **Path** (String):????<br>* **Configuration Type** (Enum): **Startup** or **Running** ????<br>* **Restore Method** (Enum): **Override** or **Append** ????<br>* **VRF Management Name** (String):????|
|Load Firmware|Uploads and updates firmware on the resource.<br>Set the command inputs as follows:<br>* **Path** (String): ?????<br>* **VRF Management Name** (String): ????|

# Downloading the Shell
The **Arista EOS Router 2G** shell is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The shell comprises:

|File name|Description|
|:---|:---|
|AristaEosRouterShell2G.zip|Arista EOS Router 2G shell package|
|cloudshell-networking-arista-eos-router-shell-2g-dependencies-package-1.0.X.zip|Shell Python dependencies (for offline deployments only)|

# Importing and Configuring the Shell
This section describes how to import the **Arista EOS Router 2G version 1.0.0** shell and configure and modify the shell’s devices.

### Importing the shell into CloudShell

**To import the shell into CloudShell:**
  1. Make sure you have the shell’s zip package. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  
  2. In CloudShell Portal, as Global administrator, open the **Manage – Shells** page.
  
  3. Click **Import**.
  
  4. In the dialog box, navigate to the shell's zip package, select it and click **Open**.

The shell is displayed in the **Shells** page and can be used by domain administrators in all CloudShell domains to create new inventory resources, as explained in [Adding Inventory Resources](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/INVN/Add-Rsrc-Tmplt.htm?Highlight=adding%20inventory%20resources). 

### Offline installation of a shell

**Note:** Offline installation instructions are relevant only if CloudShell Execution Server has no access to PyPi. You can skip this section if your execution server has access to PyPi. For additional information, see the online help topic on offline dependencies.

In offline mode, import the shell into CloudShell and place any dependencies in the appropriate dependencies folder. The dependencies folder may differ, depending on the CloudShell version you are using:

* For CloudShell version 8.3 and above, see [Adding Shell and script packages to the local PyPi Server repository](#adding-shell-and-script-packages-to-the-local-pypi-server-repository).

* For CloudShell version 8.2, perform the appropriate procedure: [Adding Shell and script packages to the local PyPi Server repository](#adding-shell-and-script-packages-to-the-local-pypi-server-repository) or [Setting the python pythonOfflineRepositoryPath configuration key](#setting-the-python-pythonofflinerepositorypath-configuration-key).

* For CloudShell versions prior to 8.2, see [Setting the python pythonOfflineRepositoryPath configuration key](#setting-the-python-pythonofflinerepositorypath-configuration-key).

### Adding shell and script packages to the local PyPi Server repository
If your Quali Server and/or execution servers work offline, you will need to copy all required Python packages, including the out-of-the-box ones, to the PyPi Server's repository on the Quali Server computer (by default *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Config\Pypi Server Repository*).

For more information, see [Configuring CloudShell to Execute Python Commands in Offline Mode](http://help.quali.com/Online%20Help/9.0/Portal/Content/Admn/Cnfgr-Pyth-Env-Wrk-Offln.htm?Highlight=Configuring%20CloudShell%20to%20Execute%20Python%20Commands%20in%20Offline%20Mode).

**To add Python packages to the local PyPi Server repository:**
  1. If you haven't created and configured the local PyPi Server repository to work with the execution server, perform the steps in [Add Python packages to the local PyPi Server repository (offlinemode)](http://help.quali.com/Online%20Help/9.0/Portal/Content/Admn/Cnfgr-Pyth-Env-Wrk-Offln.htm?Highlight=offline%20dependencies#Add). 
  
  2. For each shell or script you add into CloudShell, do one of the following (from an online computer):
      * Connect to the Internet and download each dependency specified in the *requirements.txt* file with the following command: 
`pip download -r requirements.txt`. 
     The shell or script's requirements are downloaded as zip files.

      * In the [Quali Community's Integrations](https://community.quali.com/integrations) page, locate the shell and click the shell's **Download** link. In the page that is displayed, from the Downloads area, extract the dependencies package zip file.

3. Place these zip files in the local PyPi Server repository.
 
### Setting the python PythonOfflineRepositoryPath configuration key
Before PyPi Server was introduced as CloudShell’s python package management mechanism, the `PythonOfflineRepositoryPath` key was used to set the default offline package repository on the Quali Server machine, and could be used on specific Execution Server machines to set a different folder. 

**To set the offline python repository:**
1. Download the *cloudshell-networking-arista-eos-router-shell-2g-dependencies-package-1.0.X.zip* file, see [Downloading the Shell](#downloading-the-shell).

2. Unzip it to a local repository. Make sure the execution server has access to this folder. 

3.  On the Quali Server machine, in the *~\CloudShell\Server\customer.config* file, add the following key to specify the path to the default python package folder (for all Execution Servers):  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`

4. If you want to override the default folder for a specific Execution Server, on the Execution Server machine, in the *~TestShell\Execution Server\customer.config* file, add the following key:  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`

5. Restart the Execution Server.

### Configuring a new resource
This section explains how to create a new resource from the shell.

In CloudShell, the component that models the device is called a resource. It is based on the shell that models the device and allows the CloudShell user and API to remotely control the device from CloudShell.

You can also modify existing resources, see [Managing Resources in the Inventory](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/INVN/Mng-Rsrc-in-Invnt.htm?Highlight=managing%20resources).

**To create a resource for the device:**
  1. In the CloudShell Portal, in the **Inventory** dashboard, click **Add New**. 
     ![](https://github.com/stsuberi/SaraTest/blob/master/create_a_resource_device.png)
     
  2. From the list, select **AristaEosRouterShell2G**.
  
  3. Enter the **Name** and **IP address** of the **Arista EOS Router**.
  
  4. Click **Create**.
  
  5. In the **Resource** dialog box, enter the device's settings, see [Device Name Attributes](*device-name-attributes). 
  
  6. Click **Continue**.

CloudShell validates the device’s settings and updates the new resource with the device’s structure (if the device has a structure).

# Updating Python Dependencies for Shells
This section explains how to update your Python dependencies folder. This is required when you upgrade a shell that uses new/updated dependencies. It applies to both online and offline dependencies.

### Updating offline Python dependencies
**To update offline Python dependencies:**
1. Download the latest Python dependencies package zip file locally.

2. Extract the zip file to the suitable offline package folder(s). 

3. Restart any execution server that has a live instance of the relevant driver or script. This requires running the Execution Server's configuration wizard, as explained in the [Configure the Execution Server](http://help.quali.com/doc/9.0/CS-Install/content/ig/configure%20cloudshell%20products/cfg-ts-exec-srver.htm?Highlight=configure%20the%20execution%20server) topic of the CloudShell Suite Installation guide. 

### Updating online Python dependencies
In online mode, the execution server automatically downloads and extracts the appropriate dependencies file to the online Python dependencies repository every time a new instance of the driver or script is created.

**To update online Python dependencies:**
* If there is a live instance of the shell's driver or script, restart the execution server, as explained above. If an instance does not exist, the execution server will download the Python dependencies the next time a command of the driver or script runs.

# Typical Workflows 

#### **Workflow 1** - *Save configuration* 
1. In CloudShell Portal, reserve the Arista EOS resource and run the `Save` command.

2. In the command input field, enter the following information:
	* **Folder Path**: For example, *tftp://ipaddress/shared folder*
	* **Configuration Type**: either **Running** or **Startup**
	* **VRF Management Name**: provide the management VRF name if exists.

The startup or running configuration will be saved to a file named *<ResourceName>-<startup/running-config>-<timestamp>*, which will be stored in the folder path you entered.

#### **Workflow 2** - *Restore configuration* 
1. In CloudShell Portal, reserve the Arista EOS resource.

2. Run the resource command `Restore`.

3. Enter the following input parameters:
	* **Path**: This is a mandatory input field. Enter the full path of the configuration file. 
	* **Restore Method**: This is an optional input field. Can be **Override**. If nothing is entered in this input field, the Override method will be used. 
	* **Configuration Type**: This is a mandatory input field. Possible values **Startup** or **Running**.
	* **VRF Management Name**: This is an optional input field. Provide the management VRF name if exists.

#### **Workflow 3** - *Load firmware* 
1. Login to CloudShell portal and reserve the Arista EOS resource.
2. Run the resource command `Load Firmware`. 
3. Enter the following input parameters:
	* **Path** (mandatory input field). Enter the full path to the firmware file on remote host. For example: tftp://10.1.1.1/both.tim

# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation, see [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 

# Release Notes 
**Arista EOS Router 2G version 1.0.0**

### What's New

* Shell based on TOSCA Standards
* Separate namespace for each shell

### Known Issues
* Doesn’t support configuring SNMP v3
