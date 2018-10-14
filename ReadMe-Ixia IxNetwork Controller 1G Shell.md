
![](https://github.com/QualiSystems/cloudshell-shells-documentaion-templates/blob/master/cloudshell_logo.png)

# **Ixia IxNetwork Controller 1G Shell**  

Release date: June 2018

Shell version: 1.6.0

Document version: A

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

**Note:** We recommend using a 2nd gen shell where possible. Using a 1st gen shell may limit some shell management capabilities. For more information, see [Shell Overview – “Our Shell”](http://help.quali.com/Online%20Help/8.3/Portal/Content/CSP/LAB-MNG/Shells.htm?Highlight=shell%20overview).

### Traffic Generator Shells
CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) from a sandbox. In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator device and ports, and a controller service that runs the chassis commands, such as Load Configuration File, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells, allowing you to accurately model your real-life architecture. For example, scenarios where the chassis and controller are located on different machines.

For additional information on traffic generator shell architecture, and setting up and using a traffic generator in CloudShell, see the [Traffic Generators Overiew](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator%20overview) online help topic.

### **Ixia IxNetwork Controller 1G Shell**
The **Ixia IxNetwork Controller 1G** shell provides you with connectivity and management capabilities such as device structure discovery and power management for the **Ixia IxNetwork Controller**. 

For more information on the **Ixia IxNetwork Controller**, see the official **Ixia** product documentation.

The **Ixia IxNetwork Controller** provides automation commands to run on the chassis, such as Load Configuration, Start/Stop Traffic, Get Statistics. 

### Standard version
The **Ixia IxNetwork Controller 1G** shell is based on the Traffic Shell Standard version 3.0.0.

For detailed information about the shell’s structure and attributes, see the [Traffic Shell standard](https://github.com/QualiSystems/shell-traffic-standard/blob/master/spec/traffic_standard.md) in GitHub.

### Supported OS
▪ Windows

### Requirements

Release: **Ixia IxNetwork Controller 1G version 1.6.0**

▪ IxNetwork API Server: 8.0.1 GA and above

▪ IxNetwork Connection Manager: 8.40 EA and above 

▪ CloudShell: 8.1 and above

### Data Model

The shell's data model includes all shell metadata, families, and attributes.

#### **Ixia IxNetwork Controller 1G Shell Families and Models**

The controller's families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
||||
||||
||||
||||

#### **Ixia IxNetwork Controller 1G Shell Attributes**

The attribute names and types are listed in the following table:

|Attribute|Type|Default value|Description|
|:---|:---|:---|:---|
|||||
|||||
|||||
|||||

### Automation
This section describes the automation (drivers) associated with the data model. The shell’s driver is provided as part of the shell package. There are two types of automation processes, Autoload and Resource.  Autoload is executed when creating the resource in the Inventory dashboard, while resource commands are run in the Sandbox, providing that the resource has been discovered and is online.

For Traffic Generator shells, commands are configured and executed from the controller service in the sandbox, with the exception of the Autoload command, which is executed when creating the resource.

|Command|Description|
|:-----|:-----|
|Autoload|Discovers the chassis, its hierarchy and attributes when creating the resource. The command can be rerun in the **Inventory** dashboard and not in the sandbox, as for other commands.|
|Load Configuration|Loads configuration and reserves ports.<br>Set the command inputs as follows:<br>* **Ixia config file name**: Full path to the Ixia configuration file name.|
|Start ARP/ND|Send ARP/ND for all protocols.|
|Start Protocols|Starts all protocols.|
|Stop Protocols|Stops all protocols.|
|Start Traffic|Starts L2-3 traffic.<br>Possible values:<br>* **True**: Returns after traffic finishes to run<br>* **False**: Returns immediately|
|Stop Traffic|Stops L2-L3 traffic.|
|Get Statistics|Gets view statistics.<br>Possible values:<br>* **View Name**, **Port statistics**, **Traffic item statistics**, **Flow statistics**, etc.<br>* **Output type**: **CSV**, **JSON**. If **CSV**, the statistics will be attached to the reservation csv file.|
|Run Quick Test|Runs Quick test.<br>Set the command inputs as follows:<br>* **Quick Test Name**: Name of quick test to run.|

# Downloading the Shell
The **Ixia IxNetwork Controller 1G** shell is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The shell comprises:

|File name|Description|
|:---|:---|
|ixia_ixnetwork_controller.zip|IxNetwork Controller 1G shell package|
|ixia_ixnetwork_controller_offline_requirements.zip|Shell Python dependencies (for offline deployments only)|

## Importing and Configuring the Shell
This section describes how to import the BreakingPoint 1G shells and configure and modify the shell’s devices. 

### Importing the shell into CloudShell

**To import the shell into CloudShell:**
  1. Make sure you have the shell’s zip package. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  
  2. Backup your database.
  
  3. Log in to CloudShell Portal as administrator of the relevant domain.
  
  4. In the User menu select **Import Package**.
  
     ![](https://github.com/stsuberi/SaraTest/blob/master/import_package.png)
     
  5. Browse to the location of the downloaded shell file, select the relevant *.zip* file and Click **Open**. Alternatively, drag the shell’s .zip file into CloudShell Portal.

The shell is displayed in the **Drivers>Resource** page and can be used by domain administrators in all CloudShell domains to create new inventory resources, as explained in [Adding Inventory Resources](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/INVN/Add-Rsrc-Tmplt.htm?Highlight=adding%20inventory%20resources).  

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
1. Download the *ixia_ixnetwork_controller_offline_requirements.zip* file, see [Downloading the Shell](#downloading-the-shell).

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
     ![](https://github.com/QualiSystems/cloudshell-shells-documentaion-templates/blob/master/create_a_resource_device.png)
     
  2. From the list, select **[Shell Name]**.
  
  3. Enter the **Name** and **IP address** of the **[Device Name]** (if applicable).
  
  4. Click **Create**.
  
  5. In the **Resource** dialog box, enter the device's settings, see [Device Name Attributes](*device-name-attributes). 
  
  6. Click **Continue**.

CloudShell validates the device’s settings and updates the new resource with the device’s structure (if the device has a structure).

### Configuring a new service
This section explains how to create a new service from the shell.

In CloudShell, the component that models the device is called a resource. It is based on the shell that models the device and allows the CloudShell user and API to remotely control the device from CloudShell.

You can also modify existing resources, see [Managing Resources in the Inventory](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/INVN/Mng-Rsrc-in-Invnt.htm?Highlight=managing%20resources).

**To configure a service for the device:**
  1. In CloudShell Resource Manager, in the **Inventory** tab, click **Resource Families**. 
     ![](https://github.com/stsuberi/SaraTest/blob/master/create_a_resource_device.png)
     
  2. In the **Traffic Generator Controller** folder, select **IxNetwork Controller**.
   ![](https://github.com/stsuberi/SaraTest/blob/master/ixnetwork_controller.png)
  
  3. In the **Attributes** tab, enter the **Default Values** for the IxNetwork Controller service as follows:
  
     * Controller Address - IP address of the API server/Connection Manager. Default is localhost.
     * Controller TCP Port - TCP port of the API server/Connection manager. Default is 11009.
     * User - User name for the IxChariot Server. (IGNORE – for future use.)
     * Password - Password for the IxChariot Server.(IGNORE – for future use.)
     
  4. Click **Save**.
  
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

# Typical Workflow 

**Workflow 1** - *Using the IxNetwork controller to run IxNetwork traffic* 

1. Create a Blueprint
	1. Create a Blueprint with IxNetwork controller service and Ixia chassis resource ports. Number of Ixia ports in the blueprint should match the number of ports in the IxNetwork configuration. 
	For example: if we have a configuration with two ports - 
	![](https://github.com/stsuberi/SaraTest/blob/master/ixnetwork_controller_configuration_two_ports.png)
	2. Create a Blueprint with two IxNetwork ports
	![](https://github.com/stsuberi/SaraTest/blob/master/ixnetwork_controller_blueprint_two_ports.png)

2. Reserve the Sandbox.

3. Create a Sandbox from the Blueprint.

4. Edit the IxNetwork Controller Service parameters if required, see Configuring a new service above.
![](https://github.com/stsuberi/SaraTest/blob/master/ixnetwork_controller_configuration_parameters.png)

5. Map configuration ports to Sandbox ports. For each port in the IxNetwork configuration assign physical port from the ports in the sandbox. Open the attributes tab and set the Logical Name to the port name in the configuration.
![](https://github.com/stsuberi/SaraTest/blob/master/ixnetwork_controller_mapping_ports.png)

# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation, see [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 

# Release Notes 
(if not applicable - remove section)

### Known Issues
• Performance
	* The REST API performance is very poor. Loading configuration and reserving ports can take up dozens of seconds depending on the specific setup. It is advised to start idle connections on the Connection Manager to reduce startup time.
• No available connection on connection manager
	* In case there is no available connection on the connection manager the user must login to the Connection Manager and close zombie connections or create new connections.
• Licensing
	* If license server on Connection Manager / API server is not configured Load Configuration might success but ports will be in Down state and any further operation will fail.
• Reserved ports
	* If ports are reserved by other users Load Configuration might success but ports will be in Down state and any further operation will fail. 