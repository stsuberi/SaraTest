![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# IxChariot Server 1G Shell 

Release date: **September 2018**

Shell version: **1.1.1**

Document version: **1.0.0**

# In This Guide:

* [Overview](#overview)
* [Importing and Configuring the Shell](#importing-and-configuring-the-shell)
* [Updating Python Dependencies for Shells](#updating-python-dependencies-for-shells)
* [Typical Workflow and Scenarios](#typical-workflow-and-scenarios)
* [References](#references)
* [Release Notes](#release-notes)


# Overview
A shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.
___
**Note:** We recommend using a 2nd gen shell where possible. Using a 1st gen shell may limit some shell management capabilities. For more information, see [Shell Overview – “Our Shell”](http://help.quali.com/Online%20Help/8.3/Portal/Content/CSP/LAB-MNG/Shells.htm?Highlight=shell%20overview).
___

### Traffic Generator Shells
CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) from a sandbox. In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator device and ports, and a controller service that runs the chassis commands, such as Load Configuration File, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells, allowing you to accurately model your real-life architecture. For example, scenarios where the chassis and controller are located on different machines.

For more information, see [Traffic Generators Overview](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator).

### **IxChariot Server 1G Shell**
**IxChariot Server 1G Shell** provides you with connectivity and management capabilities such as device structure discovery and power management for the **IxChariot server**. 

For more information on the **IxChariot Server**, see the official **IxChariot** product documentation.

To model an _**[Device Name]**_ device in CloudShell, use one of the following controllers, which provides automation commands to run on the chassis, such as Load Configuration, Start Traffic/Test, Get Statistics: (**Is this section relevant for this shell?**)

▪ <a href="_**[Controller Shell https from Quali's Community Integrations page]**_" target="_blank">_**[Controller Shell Name]**_</a>

▪ <a href="_**[Controller Shell https from Quali's Community Integrations page]**_" target="_blank">_**[Controller Shell Name]**_</a>

### Standard version
**IxChariot Server 1G Shell** 1.1.1 is based on the Traffic Shell standard version 3.0.0. **(The link to the Traffic Shell standard is to 2.0.0)**

For detailed information about the shell’s structure and attributes, see the [Traffic Shell standard](https://github.com/QualiSystems/shell-traffic-standard/blob/master/spec/traffic_standard.md) in GitHub.

### Supported OS
▪ Windows

### Requirements

Release 1.1.1:

	▪ CloudShell version: 8.1 and above

	▪ IxChariot versions: 9.5, 9.6

	▪ IxChariot Python API library: Can be downloaded from the IxChariot Server

### Downloading the Shell
The **IxChariot Server 1G Shell** is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The shell comprises:

|File name|Description|
|:---|:---|
|**Ixia-IxChariotServer-Shell.zip**|IxChariot Server shell package|
|**Ixia-IxChariotServer-Shell_offline_requirements.zip**|Shell Python dependencies (for offline deployments only)|
|**ReadMe-IxChariot Server Shell.md**|Documentation|

### Automation (Is this section relevant for this shell?)
This section describes the automation (drivers or scripts) associated with the data model. The shell’s driver is associated with the model and provided as part of the shell package).
For Traffic Generator Shells, commands are configured and executed from the controller service in the sandbox, with the exception of the Autoload command, which is executed when creating the resource.

|Command|Description|
|:-----|:-----|
|Autoload|Discovers the chassis, its hierarchy and attributes when creating the resource. The command can be rerun in the Inventory dashboard and not in the sandbox, as for other commands.|

# Importing and Configuring the Shell
This section describes how to import the **IxChariot Server 1G Shell** and configure and modify the shell’s devices.

### Importing the shell into CloudShell

**To import the shell into CloudShell:**
  1. Make sure you have the shell’s .zip file. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  2. Backup your database.
  3. Log in to CloudShell Portal as administrator of the relevant domain.
  4. In the User menu select **Import Package**.
  
     ![](https://github.com/stsuberi/SaraTest/blob/master/import_package.png)
  5. Browse to the location of the downloaded shell file, select the relevant *.zip* file and Click **Open**. Alternatively, drag the shell’s .zip file into CloudShell Portal.

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
Before PyPi Server was introduced as CloudShell’s python package management mechanism, the `PythonOfflineRepositoryPath` key was used to set the default offline package repository on the Quali Server machine, and could be used on specific Execution Eerver machines to set a different folder. 

**To set the offline python repository:**
1. Download the *Ixia-IxChariotServer-Shell_offline_requirments.zip* file, see [Downloading the Shell](#downloading-the-shell).
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
  2. From the list, select **IxChariot Server**.
  3. Enter the IxChariot Server **Name** and **IP address**.
  4. Click **Create**.
  5. In the **Resource** dialog box, enter the device's settings, as follows:
  	 * Client Install Path - Path where the IxChariot Python API library was downloaded to.
  	 * User - User name for the IxChariot Server.
  	 * Password - Password for IxChariot Server. 
   	 * Power Management- Whether to automatically manage the device power status or not (standard CloudShell attribute).
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

## Data Model

The shell's data model includes all shell metadata, famiies, and attributes.

**[Device Name]** **Families and Models**

The chassis families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
||||
||||
||||
||||

**[Device Name]** **Attributes**

The attribute names and types are listed in the following table:

|Attribute|Type|Default value|Description|
|:---|:---|:---|:---|
|||||
|||||
|||||
|||||


# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation resources, see the [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 

# Release Notes 

### What's New

* No new functionality, just standardization.

### Known Issues
* NA
