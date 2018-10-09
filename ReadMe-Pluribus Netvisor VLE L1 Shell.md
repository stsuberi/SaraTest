
![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# **Pluribus Netvisor VLE L1 Shell**  

Release date: October 2018

Shell version: 1.01

Document version: (Rev A.01)

# In This Guide

* [Overview](#overview)
* [Downloading the Shell](#downloading-the-shell)
* [Importing and Configuring the Shell](#importing-and-configuring-the-shell)
* [Updating Python Dependencies for Shells](#updating-python-dependencies-for-shells)
* [References](#references)


# Overview
A shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

### L1 Switch Shells
L1 switch shells allow CloudShell to manage networking connectivity between physical resources and private cloud provider Apps, such as vCenter.

For additional information, see the [L1 Switches](http://help.quali.com/Online%20Help/9.0/Portal/Content/Admn/Cnct-Ctrl-L1-Swch.htm?Highlight=L1%20switch) online help topic.

### **Pluribus Netvisor VLE L1 Shell**
**Pluribus Netvisor VLE L1** shell provides you with the capability to communicate with network topology managed by the Pluribus Netvisor nvOS in VLE mode.

CloudShell users can create routes and read values from the switch, using **Resource Manager Client** or CloudShell API.

For more information on the **Pluribus Netvisor VLE L1**, see the official **Pluribus Netvisor** product documentation.

### Supported OS
▪ Pluribus Netvisor 3.0.0 and above

### Requirements

Release: **CloudShell Pluribus Netvisor VLE L1 version 1.0.1**

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
This section describes the automation (drivers) associated with the data model. The shell’s driver is provided as part of the shell package. There are two types of automation processes, Autoload and Resource.  Autoload is executed when creating the resource in the Inventory dashboard, while resource commands are run in the Sandbox, providing that the resource has been discovered and is online.

|Command|Description|
|:-----|:-----|
|MapBidi|Creates a bidir connection between two ports.|
|MapClear|Clears any connection ending in this port.|
|MapClearTo|Clears a unidir connection between two ports.|

**Note:** You can only activate a TAP connection after activating a parent mapuni/mapbidi connection. 

# Downloading the Shell
The **Pluribus Netvisor VLE L1** shell is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

The shell comprises:

|File name|Description|
|:---|:---|
|cloudshell-L1-pluribus_netvisor_vle\install_driver.bat|Pluribus Netvisor VLE L1 shell installation script|
|cloudshell-L1-pluribus_netvisor_vle\pluribus_netvisor_vle_runtime_config.yml|Pluribus Netvisor VLE L1 shell configuration file|
|cloudshell-L1-pluribus_netvisor_vle\datamodel\Pluribus Netvisor VLE_ResourceConfiguration.xml|XML file containing the resource structure, attributes and capabilities of the L1 switches of the same vendor|

# Importing and Configuring the Shell
This section describes how to import the **Pluribus Netvisor VLE L1 Shell** and configure and modify the shell’s devices.

### Importing and configuring the shell in CloudShell

**To import and configure the shell in CloudShell:**
  1. Make sure you have the shell’s zip package. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  
  2. Extract the *cloudshell-L1-pluribus_netvisor_vle-1.0.1.zip* package to the following location on the Quali Server machine: 
  *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers*
  
  3. Run the *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers\cloudshell-L1-pluribus_netvisor_vle\install_driver.bat* file.
  
  4. Import the new data model.
      * **In Resource Manager Client>Admin**, right-click **Resource Families** and select **Import**.
      * Select the *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Drivers\cloudshell-L1-pluribus_netvisor_vle\datamodel\pluribus_netvisor_vle_ResourceConfiguration.xml* file.
      * Click **Open**.
	
  5. Create an L1 resource.
      * In **Resource Explorer**, right click **Root** and select **New>Resource**.
      * Enter the **Name** and **Address**.
      * Select the **L1 Switch** family.
      * Ensure that the correct **Model** (Pluribus Netvisor VLE Fabric) and **Driver** (PLURIBUS NETVISOR VLE) are selected.
      * Click **OK**.
	
  6. Auto Load the new resource.
      * In **Resource Explorer**, right click the new resource and select **Configuration**.
      * In the **Internal Resources** pane, right click the switch and select **Exclude**. 
      * Click the **Auto Load** button at the bottom of the **Configuration** tab.
	
  7. Define the resource connections on the L1 switch.
      * Right click the resource and select **Configuration>Connections**.
      * Connect a resource's port to a different port in the switch resource by clicking each port's **Connected To** button, selecting the resource's **Family** and **Resource**, and selecting the port to connect.


### Offline installation of a shell

**Note:** Offline installation instructions are relevant only if CloudShell Execution Server has no access to PyPi. You can skip this section if your execution server has access to PyPi. For additional information, see the online help topic on offline dependencies.

In offline mode, import the shell into CloudShell and place any dependencies in the appropriate dependencies folder.

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
 

**To set the offline python repository:**
1. Download the **[Shell Offline Requirements .zip File Name]** file, see [Downloading the Shell](#downloading-the-shell).

2. Unzip it to a local repository. Make sure the execution server has access to this folder. 

3.  On the Quali Server machine, in the *~\CloudShell\Server\customer.config* file, add the following key to specify the path to the default python package folder (for all Execution Servers):  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`

4. If you want to override the default folder for a specific Execution Server, on the Execution Server machine, in the *~TestShell\Execution Server\customer.config* file, add the following key:  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`

5. Restart the Execution Server.

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

# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation, see [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 
