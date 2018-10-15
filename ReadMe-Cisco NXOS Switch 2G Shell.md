![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# **Cisco NXOS Switch 2G Shell**  

Release date: March 2017

Shell version: 1.0.0

Document version: 1.0.0

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
CloudShell's networking shells provide L2 or L3 connectivity between resources and/or Apps.

### **Cisco NXOS Switch 2G Shell**
The **Cisco NXOS Switch 2G** shell provides you with connectivity and management capabilities such as device structure discovery and power management for the **Cisco NXOS Switch**. 

For more information on the **Cisco NXOS Switch**, see the official **Cisco** product documentation.

### Standard version
**Cisco NXOS Switch 2G Shell 1.0.0** is based on the Networking Shell Standard version **5.0.0**.

For detailed information about the shell’s structure and attributes, see the [Networking Shell Standard](https://github.com/QualiSystems/cloudshell-standards/blob/master/Documentation/networking_standard.md) in GitHub.

### Requirements

Release: **Cisco NXOS Switch 2G Shell 1.0.0**

▪ CloudShell version: 8.0 and above

▪ Cisco OS: Cisco NXOS

▪ Certified models: Nexus 7k

### Data Model

The shell's data model includes all shell metadata, families, and attributes.

#### **Cisco NXOS Switch 2G Shell Families and Models**

The Cisco NXOS Switch families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
|CS_Switch|Cisco NXOS Switch 2G|Generic Cisco NXOS Switch 2 Generation |
|CS_Chassis|Generic Chassis|Default Switch chassis|
|CS_Module|Generic Module|Modules located on the chassis|
|CS_SubModule|Generic Sub Module|Sub modules|
|CS_Port|Generic Port|Interface|
|CS_PortChannel|Generic Port Channel|Group of interfaces|
|CS_PowerPort|Generic Power Port|Power Supply module|

#### **Cisco NXOS Switch 2G Shell Attributes**

The attribute names and types are listed in the following section of the Networking Shell Standard:

https://github.com/QualiSystems/cloudshell-standards/blob/master/Documentation/networking_standard.md#attributes

**[Notes:]** <br>(Include as needed to explain differences between this shell's attributes and attributes documented in the Shell Standard.)

### Automation
This section describes the automation (drivers) associated with the data model. The shell’s driver is provided as part of the shell package. There are two types of automation processes, Autoload and Resource.  Autoload is executed when creating the resource in the Inventory dashboard, while resource commands are run in the Sandbox, providing that the resource has been discovered and is online.

The command names and types are listed in the following section of the Networking Shell Standard:

https://github.com/QualiSystems/cloudshell-standards/blob/master/Documentation/networking_standard.md#commands

**[Notes:]**<br>(Include as needed to explain differences between this shell's commands and commands documented in the Shell Standard.)

# Downloading the Shell
The **Cisco NXOS Switch 2G Shell** shell is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The shell comprises:

|File name|Description|
|:---|:---|
|CiscoNxosSwitchShell2G.zip|Cisco IOS Switch shell package|
|cloudshell-networking-cisco-nxos-2-gen-dependencies-package-1.0.X.zip|Shell Python dependencies (for offline deployments only)|

# Importing and Configuring the Shell
This section describes how to import the **Cisco NXOS Switch 2G Shell 1.0.0** shell and configure and modify the shell’s devices.

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
1. Download the *cloudshell-networking-cisco-nxos-2-gen-dependencies-package-1.0.X.zip* file, see [Downloading the Shell](#downloading-the-shell).

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
     
  2. From the list, select **Cisco NXOS Switch 2G**.
  
  3. Enter the **Name** and **IP address** of the **Cisco NXOS Switch**.
  
  4. Click **Create**.
  
  5. In the **Resource** dialog box, enter the device's settings, see [Device Name Attributes](*device-name-attributes). Make sure you enter the device's SNMP version and credentials.
  
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
1. In CloudShell Portal, reserve the **Cisco NXOS** resource.

2. Run the **Save** resource command.

3. In the command inputs field, enter the following information:
	* **Folder Path**: For example, *tftp://ipaddress/shared folder*.
	* **Configuration Type**: **Startup** or **Running**.
	* **VRF Management Name**: Provide the VRF Management name, if relevant.
	
4. Click **Run**.

The Startup or Running configuration is saved to a file named *<ResourceName>-<startup/running-config>-<timestamp>*, which will be stored in the folder path you entered above.

#### **Workflow 2** - *Restore configuration* 
1. In CloudShell Portal, reserve the **Cisco NXOS** resource.

2. Run the **Restore** resource command.

3. In the command inputs field, enter the following information:
	* **Path**: (Mandatory) Enter the full path of the configuration file. 
	* **Restore Method**: (Optional) Possible values are **Override** or **Append**. If left empty, the **Override** method is used. 
	* **Configuration Type**: (Mandatory) Possible values are **Startup** or **Running**.
	* **VRF Management Name**: (Optional) Provide the VRF Management name, if relevant.
	
4. Click **Run**.

#### **Workflow 3** - *Load firmware* 
1. In CloudShell portal, reserve the **Cisco NXOS** resource.

2. Run the **Load Firmware** resource command. 

3. In the command inputs field, enter the following information:
	* **Remote Host** (Mandatory). Enter the full path to the firmware file on the remote host, for example: *tftp://10.1.1.1/nxos12.SE1-smp-k8.bin* 
	* **File Path** (Mandatory). Enter the destination filename on the device itself, for example: *bootflash:/nxos12.SE1-smp-k8.bin*.
	
4. Click **Run**.

# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation, see [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 

# Release Notes 

**Cisco NXOS Switch 2G Shell 1.0.0**


### What's New

* Console Session support was added. You must do the following:
	* Set the **Session Concurrency Limit** attribute to 1.
	* Set the following attributes: **Console Server IP Address**, **Console Port**, **User**, **Password**.
	
* A new restore override flow was implemented, which requires a **Console Session**.
