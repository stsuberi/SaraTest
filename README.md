# Ixia Chassis 2G Shell 
<p align="left">
<img src="https://github.com/QualiSystems/devguide_source/raw/master/logo.png" width="150" height="150"></img>
</p>

## Overview
A Shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

### Traffic Generator Shells
CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) from a sandbox. In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator device and ports, and a controller service that runs the chassis commands, such as Load Configuration File, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells, allowing you to accurately model your real-life architecture. For example, scenarios where the chassis and controller are located on different machines.

For more information, see [Traffic Generators Overview](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator).

### About Ixia Chassis 2G Shell
This 2nd generation Shell provides you with connectivity and management capabilities such as device structure discovery and power management for Ixia chassis. 

To model an Ixia chassis device in CloudShell, use the Ixia Chassis 2G Shell and a controller Shell. The Ixia Chassis shell can be used with either of the following controllers: 

▪ <a href="https://community.quali.com/repos/1259/ixia-ixnetwork-controller-shell" target="_blank">Ixia IxNetwork Controller Shell</a>

▪ <a href="https://community.quali.com/repos/1396/ixia-ixload-controller-shell" target="_blank">Ixia IxLoad Controller Shell</a>

### Document version
The Ixia Chassis 2G Shell document version is 1.2.3.

### Standard version
The Ixia Chassis 2G Shell 2.0.4 is based on the Traffic Shell standard *cloudshell_traffic_generator_chassis_standard_1_0_2.yaml*.

For detailed information about the Shell’s structure and attributes, see the [Traffic Shell standard](https://github.com/QualiSystems/shell-traffic-standard/blob/master/spec/traffic_standard.md) in GitHub.

### Supported OS
▪ Windows

### Requirements
▪ 2G Chassis Shell: CloudShell version 8.0 and above
▪ Controller Shells and 1G Chassis Shell: CloudShell version 7.0 and above

### Downloading the Shell
The Ixia Chassis 2G Shell is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The Shell comprises:

|File name|Description|
|:---|:---|
|ixia_chassis_shell.zip|Shell package|
|ixia_chassis_shell_offline_requirements.zip|Shell Python dependecies (for offline deployments only)|
|Ixia Chassis Shell Doc.ReadMe|Documentation|

### Automation
This section describes the automation (drivers or scripts) associated with the data model. The automation code (either script or driver) is associated with the model and provided as part of the Shell package (in the .zip file). 

For Traffic Generator shells, commands are configured and executed from the controller service in the sandbox, with the exception of the Autoload command, which is executed when creating the resource.

|Command|Description|
|-----|-----|
|Autoload|Discovers the chassis, its hierarchy and attributes when creating the resource. The command can be rerun in the Inventory dashboard and not in the sandbox, as for other commands.|

**Controllers compatible with Ixia Chassis 2G Shell**

The Ixia Chassis shell is compatible with two different controllers, see [About Ixia Chassis 2G Shell](#about-ixia-chassis-2g-shell).

## Importing and Configuring the Shell
This section describes how to import, configure and modify the Ixia Chassis 2G Shell.

### Importing the Shell into CloudShell

**To import the Shell into CloudShell:**
  1. Make sure you have the Shell’s .zip file. If not, download the Shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  2. In CloudShell Portal, as Global administrator, open the **Manage – Shells** page.
  3. Click **Import**.
  4. In the dialog box, navigate to the Shell's .zip file, select it and click **Open**.

The Shell is displayed in the **Shells** page and can be used by domain administrators in all CloudShell domains to create new inventory resources, as explained in [Adding Inventory Resources](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/INVN/Add-Rsrc-Tmplt.htm?Highlight=adding%20inventory%20resources). 

### Offline installation of a Shell
___
**Note:** Offline installation instructions are relevant only if CloudShell Execution Server has no access to PyPi. You can skip this section if your execution server has access to PyPi. For additional information, see the online help topic on offline dependencies.
___

In offline mode, import the shell into CloudShell and place any dependencies in the appropriate dependencies folder. The dependencies folder may differ, depending on the CloudShell version you are using:

1. For CloudShell version 8.3 and above, see [Add Shell and script packages to the local PyPi Server repository](#add-shell-and-script-packages-to-the-local-pypi-server-repository).
2. For CloudShell version 8.2, perform the appropriate procedure: [Add Shell and script packages to the local PyPi Server repository](#add-shell-and-script-packages-to-the-local-pypi-server-repository) or [Set the python pythonOfflineRepositoryPath configuration key](#set-the-python-pythonofflinerepositorypath-configuration-key).
3. For CloudShell versions prior to 8.2, see [Set the python pythonOfflineRepositoryPath configuration key](#set-the-python-pythonofflinerepositorypath-configuration-key).

### Adding Shell and script packages to the local PyPi Server repository
If your Quali Server and/or execution servers work offline, you will need to copy all required Python packages, including the out-of-the-box ones, to the PyPi Server's repository on the Quali Servercomputer (by default *C:\Program Files (x86)\QualiSystems\CloudShell\Server\Config\Pypi Server Repository*).

For more information, see [Configuring CloudShell to Execute Python Commands in Offline Mode](http://help.quali.com/Online%20Help/9.0/Portal/Content/Admn/Cnfgr-Pyth-Env-Wrk-Offln.htm?Highlight=Configuring%20CloudShell%20to%20Execute%20Python%20Commands%20in%20Offline%20Mode).

**To add Python packages to the local PyPi Server repository:**
  1. If you haven't created and configured the local PyPi Server repository to work with the execution server, perform the steps in [Add Python packages to the local PyPi Server repository (offlinemode)](http://help.quali.com/Online%20Help/9.0/Portal/Content/Admn/Cnfgr-Pyth-Env-Wrk-Offln.htm?Highlight=offline%20dependencies#Add). 
  2. For each Shell or script you add into CloudShell, do one of the following (from an online computer):
      * Connect to the Internet and download each dependency specified in the *requirements.txt* file with the following command: 
*pip download -r requirements.txt*. 
     The Shell or script's requirements are downloaded as zip files.

      * In the [Quali Community's Integrations](https://community.quali.com/integrations) page, locate the Shell and click the Shell's **Download** link. In the page that is displayed, from the Downloads area, extract the dependencies package zip file.

3. Place these zip files in the local PyPi Server repository.
 
### Setting the python PythonOfflineRepositoryPath configuration key
Before PyPi Server was introduced as CloudShell’s python package management mechanism, the `PythonOfflineRepositoryPath` key was used to set the default offline package repository on the Quali Server machine, and could be used on specific Execution Eerver machines to set a different folder. 

**To set the offline python repository:**
1. Download the *ixia_chassis_shell_offline_requirments.zip* file, see [Downloading the Shell](#downloading-the-shell).
2. Unzip it to a local repository. Make sure the execution server has access to this folder. 
3.  On the Quali Server machine, in the *~\CloudShell\Server\customer.config* file, add the following key to specify the path to the default python package folder (for all Execution Servers):  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`
4. If you want to override the default folder for a specific Execution Server, on the Execution Server machine, in the `~TestShell\Execution Server\customer.config` file, add the following key:  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`
5. Restart the Execution Server.

### Configuring a new resource
In CloudShell, the component that models the device is called a resource. It is based on the Shell that models the device and allows the CloudShell user and API to remotely control the device from CloudShell.

You can also modify existing resources, see [Managing Resources in the Inventory](http://help.quali.com/Online%20Help/8.3/Portal/Content/CSP/INVN/Mng-Rsrc-in-Invnt.htm?Highlight=managing%20resources).

**To create a resource for the device:**
  1. In the CloudShell Portal, in the **Inventory** dashboard, click **Add New**. 
     ![](https://github.com/stsuberi/SaraTest/blob/master/create_a_resource_device.png)
  2. From the list, select the **Ixia Chassis 2G Shell**.
  3. Enter the Ixia chassis **Name** and **IP address**.
  4. Click **Create**.
  5. In the **Resource** dialog box, enter the device's settings, as follows: 
      * If Ixia Chassis is Windows based and is accessible directly to the Execution Server then there is no need for additional settings.
      * If Ixia Chassis is Linux based and is accessible directly to the Execution Server then enter the following setting:
          * Controller TCP Port: 8022 (Linux IxOS ssh port)
      * If Ixia Chassis is not directly accessible to the Execution Server then there must be an IxTclServer serving as a proxy between the Execution Server and the chassis, enter the following settings:
          * Controller Address: address of the IxTclServer
          * Controller TCP Port: TCP port of IxTclServer (leave empty for default 4555 port) 
  6. Click **Continue**.

This command discovers the device, fills in its attribute values and creates the device’s structure in CloudShell (if the device has a structure).

## Updating Python Dependencies for Shells
This section explains how to update your Python dependencies folder. This is required when you upgrade a Shell that uses new/updated dependencies. It applies to both online and offline dependencies.

### Updating offline Python dependencies
**To update offline Python dependencies:**
1. Download the latest Python dependencies package zip file locally.
2. Extract the zip file to the suitable offline package folder(s). 
3. Restart any execution server that has a live instance of the relevant driver or script. This requires running the Execution Server's configuration wizard, as explained in the [Configure the Execution Server](http://help.quali.com/doc/9.0/CS-Install/content/ig/configure%20cloudshell%20products/cfg-ts-exec-srver.htm?Highlight=configure%20the%20execution%20server) topic of the CloudShell Suite Installation guide. 

### Updating online Python dependencies
In online mode, the execution server automatically downloads and extracts the appropriate dependencies file to the online Python dependencies repository every time a new instance of the driver or script is created.

**To update online Python dependencies:**
* If there is a live instance of the Shell's driver or script, restart the execution server, as explained above. If an instance does not exist, the execution server will download the Python dependencies the next time a command of the driver or script runs.

## Data Model
**Ixia Chassis Families and Models**

The chassis families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
|Traffic Generator Chassis|Ixia Chassis|Ixia Chassis|
|Module|Generic Traffic Generator Module|Modules located on the chassis|
|Port Group|Generic Port Group|Generic Port Group|
|Port|Generic Traffic Generator Port|Generic Traffic Generator Port|

**Ixia Chassis Attributes**

The attribute names and types are listed in the following table:

|Attribute|Type|Default value|Description|
|:---|:---|:---|:---|
|Model Name|String||The catalog name of the device model. This attribute will be displayed in CloudShell instead of the CloudShell model.|
|Serial Number|Text||The serial number of the resource.|
|Server Description|String||The full description of the server. Usually includes the OS, exact firmware version, and additional characteristics of the device.|
|Vendor|String||The firmware version of the resource.|

## References
For best practices, instructional training and video tutorials, and comprehensive product and API documentation, see the [Quali Community's Integrations](https://community.quali.com/integrations) page. 

To suggest an idea for the product and improve the product for everyone, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 

## Release Notes
### What's new

* Set unknown port speed to zero.
* Support new card types.
* Show only active ports instead of all ports.

### Known Issues
* Resource groups are not modeled. Resource groups are modeled as port with speed that represents to total speed of the group. The index of the representing port is the index of the active port of the group.
