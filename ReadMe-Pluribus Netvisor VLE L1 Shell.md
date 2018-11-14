
![](https://github.com/QualiSystems/cloudshell-shells-documentaion-templates/blob/master/cloudshell_logo.png)

# **Pluribus Netvisor VLE L1 Shell**  

Release date: October 2018

Shell version: 1.0.1

Document version: 1.0

# In This Guide

* [Overview](#overview)
* [Downloading the Shell](#downloading-the-shell)
* [Importing and Configuring the Shell](#importing-and-configuring-the-shell)
* [Updating Python Dependencies for Shells](#updating-python-dependencies-for-shells)
* [Upgrading the L1 Shell and Datamodel](#upgrading-the-l1-shell-and-datamodel)
* [References](#references)
* [Release Notes](#release-notes)


# Overview
A shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

### L1 Switch Shells
L1 switch shells allow CloudShell to manage networking connectivity between physical resources and private cloud provider Apps, such as vCenter.

For additional information, see the [L1 Switches](http://help.quali.com/Online%20Help/9.0/Portal/Content/Admn/Cnct-Ctrl-L1-Swch.htm?Highlight=L1%20switch) online help topic.

### **Pluribus Netvisor VLE L1 Shell**
**Pluribus Netvisor VLE L1** shell provides you with the capability to communicate with network topology managed by the Pluribus Netvisor nvOS in VLE mode.

The shell allows CloudShell users to interact with the device, for example, create and modify route mappings, get device information, and more.

For more information on the **Pluribus Netvisor VLE L1**, see the official **Pluribus Netvisor** product documentation.

### Standard version
The **Pluribus Netvisor VLE L1** shell is based on the [**Layer 1 Switch Shell Standard**](https://github.com/QualiSystems/shell-L1-template).

### Supported OS
▪ Pluribus Netvisor 3.0.0 and above

### Requirements

Release: **CloudShell Pluribus Netvisor VLE L1**

▪ CloudShell version: 8.3 GA and above

▪ Pluribus Netvisor VLE: all versions

**Note**: For support on an earlier CloudShell version, contact your customer support representative.

### Data Model

The shell's data model includes all shell metadata, families, and attributes.

#### **Pluribus Netvisor VLE L1 Families and Models**

The L1 switch families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
|L1 Switch|Pluribus Netvisor VLE Fabric|Pluribus Netvisor fabric|
|L1 Switch Blade|Generic L1 Module|Pluribus fabric node|
|L1 Switch Port|Generic L1 Port|Pluribus port|

#### **Pluribus Netvisor VLE L1 Attributes**

The Pluribus Netvisor VLE Fabric attribute names and types are listed in the following table:

|Attribute|Type|Description|
|:---|:---|:---|
|Password|Password|CLI Password|
|User|String|CLI Username|
|Fabric Name|String|Fabric name|
|Serial Number|String|Serial number|

The Generic L1 Module attribute names and types are listed in the following table:

|Attribute|Type|Description|
|:---|:---|:---|
|Model Name|String|Model name|
|Serial Number|String|Serial number|

The Generic L1 Port attribute names and types are listed in the following table:

|Attribute|Type|Default|Description|
|:---|:---|:---|:---|
|Auto Negotiation|Boolean|True|Port auto negotiation|
|Duplex|Lookup|Full|Port Duplex|
|Port Speed|String||Port speed|
|Protocol|Lookup|Transparent|Port protocol|
|Protocol Type Value|String ||Port protocol type value|
|Protocol Value|String ||Port protocol value|
|Rx Power (dBm)|String|0|Optical Port RX signal strength|
|Tx Power (dBm)|String|0|Optical Port TX signal strength|
|Wavelength|String|0|Optical Port Wavelength|

### Automation
This section describes the automation (drivers) associated with the data model. The shell’s driver is provided as part of the shell package. There are two types of automation processes, Autoload and Resource.  Autoload is executed when creating the resource in the **Inventory** dashboard, while resource commands are run in the sandbox.

|Command|Description|
|:-----|:-----|
|Autoload|Discovers and creates the internal resources of the root resource (for example, switch cards and ports).|
|MapBidi|Creates a bidir connection between two ports.|
|MapClear|Clears any connection ending in this port.|
|MapClearTo|Clears a unidir connection between two ports.|

**Note:** You can only activate a TAP connection after activating a parent mapuni/mapbidi connection. 

# Downloading the Shell
The **Pluribus Netvisor VLE L1** shell is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

The shell comprises:

|File name|Description|
|:---|:---|
|cloudshell-L1-pluribus_netvisor_vle\install_driver.bat|Pluribus Netvisor VLE L1 shell installation script.|
|cloudshell-L1-pluribus_netvisor_vle\pluribus_netvisor_vle_runtime_config.yml|Pluribus Netvisor VLE L1 shell configuration file.|
|cloudshell-L1-pluribus_netvisor_vle\datamodel\Pluribus Netvisor VLE_ResourceConfiguration.xml|XML file containing the resource structure, attributes and capabilities of the L1 switches of the same vendor.|

# Importing and Configuring the Shell
This section describes how to import the **Pluribus Netvisor VLE L1 Shell** and configure and modify the shell’s devices.

### Importing and configuring the shell in CloudShell

**To import and configure the shell in CloudShell:**
  1. Make sure you have the shell’s zip package. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  
  2. Extract the *cloudshell-L1-pluribus_netvisor_vle-1.0.1.zip* package to the following location on the Quali Server machine: 
  *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers*
  
  3. Run the *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers\cloudshell-L1-pluribus_netvisor_vle\install_driver.bat* file.
  
  4. Import the new data model.
      1. In **Resource Manager Client>Admin**, right-click **Resource Families** and select **Import**.
      2. Select the *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers\cloudshell-L1-pluribus_netvisor_vle\datamodel\pluribus_netvisor_vle_ResourceConfiguration.xml* file.
      3. Click **Open**.
	
  5. Create an L1 resource.
      1. In **Resource Explorer**, right-click **Root** and select **New>Resource**.
      2. Enter the **Name** and **Address**.
      3. Select the **L1 Switch** family.
      4. Ensure that the correct **Model** (Pluribus Netvisor VLE Fabric) and **Driver** (PLURIBUS NETVISOR VLE) are selected.
      5. Click **OK**.
	
  6. Auto Load the new resource.
      1. In **Resource Explorer**, right-click the new resource and select **Configuration**.
      2. In the **Internal Resources** pane, right-click the switch and select **Exclude**. 
      3. Click the **Auto Load** button at the bottom of the **Configuration** tab.
	
  7. Define the resource connections on the L1 switch.
      1. Right-click the resource and select **Configuration>Connections**.
      2. Connect a resource's port to a different port in the switch resource by clicking each port's **Connected To** button, selecting the resource's **Family** and **Resource**, and selecting the port to connect.
      3. Click **OK** in the **Resource connection** dialog box.
      4. Save your changes.


### Offline installation of a shell
Shell installation installs the required dependencies from the shell's zip package.

The *install_driver.bat* script creates a virtual environment on the Quali Server machine under *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers\cloudshell-l1-<drivername>* and installs the required dependencies in this virtual environment from the extracted L1 shell folder (under *~cloudshell-l1\packages*).

# Updating Python Dependencies for Shells
This section explains how to update your Python dependencies folder. This is required when you upgrade a shell that uses new/updated dependencies. It applies to both online and offline dependencies. 

L1 shells do not have separate Python dependencies files. All dependencies are included in the L1 shell itself and are installed along with the shell. Therefore, in order to update the shell's Python dependencies, you must upgrade the shell. See [Upgrading the L1 Shell and Datamodel](#upgrading-the-l1-shell-and-datamodel).

# Upgrading the L1 Shell and Datamodel

**To upgrade the L1 shell and datamodel:**
1. In the Quali Server machine, remove or rename the L1 shell's folder located in the *Drivers* folder: *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers*.

2. Extract the new L1 shell to the *Drivers* folder: *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers*.

3. In the extracted L1 shell's folder, run *install_driver.bat*.

4. Create a new folder: *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Configuration*.

5. Copy the upgraded shell's datamodel file from:

	*C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers\cloudshell-L1-driver_name\datamodeldriver_name_ResourceConfiguration.xml*
	
	to:
	
	*C:\Program Files (x86)\QualiSystems\CloudShell\Server\Configuration*.

6. Run *C:\Program Files (x86)\QualiSystems\CloudShell\Server\QsMigrationUtility.exe*.


# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation, see [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 

# Release Notes 

### What's New

For release updates, see the shell's [GitHub releases page](https://github.com/QualiSystems/cloudshell-L1-netvisor_virtualwire/releases).
