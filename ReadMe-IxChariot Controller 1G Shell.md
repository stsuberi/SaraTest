![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# **IxChariot Controller 1G Shell**  

Release date: **September 2018**

Shell version: **1.2.0**

Document version: **1.0.0**

# In This Guide

* [Overview](#overview)
* [Importing and Configuring the Shell](#importing-and-configuring-the-shell)
* [Updating Python Dependencies for Shells](#updating-python-dependencies-for-shells)
* [Typical Workflow and Scenarios](#typical-workflow-and-scenarios)
* [References](#references)
* [Release Notes](#release-notes)


# Overview
A shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

**Note:** We recommend using a 2nd gen shell where possible. Using a 1st gen shell may limit some shell management capabilities. For more information, see [Shell Overview – “Our Shell”](http://help.quali.com/Online%20Help/8.3/Portal/Content/CSP/LAB-MNG/Shells.htm?Highlight=shell%20overview).

### Traffic Generator Shells
CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) from a sandbox. In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator device and ports, and a controller service that runs the chassis commands, such as Load Configuration File, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells, allowing you to accurately model your real-life architecture. For example, scenarios where the chassis and controller are located on different machines.

For more information, see [Traffic Generators Overview](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator).

To model an IxNetwork in CloudShell, you need the IxChariot Controller 1G Shell and the IxChariot Server 1G Shell.

### **IxChariot Controller 1G Shell**
The **IxChariot Controller 1G Shell** provides you with connectivity and management capabilities such as device structure discovery, running tests, and test results for the **IxChariot** application. 

For more information on the **IxChariot Controller**, see the official **IxChariot** product documentation.

**Note:** This shell can only be used with a 1st generation IxChariot Server shell resource.  

### Supported OS
▪ **Windows**

### Requirements

Release 1.2.1:

	▪ CloudShell version: 8.1 and above

	▪ IxChariot versions: 9.5, 9.6

	▪ IxChariot Python API library: Can be downloaded from the IxChariot Server

### Downloading the Shell
The **IxChariot Controller 1G Shell** is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The shell comprises:

|File name|Description|
|:---|:---|
|**Ixia-IxChariot-Controller.zip**|IxChariot Controller shell package|
|**Ixia-IxChariot-Controller_offline_requirements.zip**|Shell Python dependencies (for offline deployments only)|
|**ReadMe-IxChariot Controller Shell.md**|Documentation|

### Automation
This section describes the automation (drivers or scripts) associated with the data model. The shell’s driver is associated with the model and provided as part of the shell package).
For Traffic Generator Shells, commands are configured and executed from the controller service in the sandbox, with the exception of the Autoload command, which is executed when creating the resource.

|Command|Description|Parameters|Returns
|:-----|:-----|:-----|:-----|
|Load Configuration <br>(load_config)|Reserves endpoints and loads configuration|IxChariot Config (ixc_config) - loads IxChariot config|Session ID|
|Start Test <br>(start_test)|Starts the test|Blocking <br> (blocking)|True - returns after test is finished<br> False - returns immediately|
|Stop Test <br>(stop_test)|||
|Get Statistics <br>(get_statistics)|Gets the statistics view|View Name (view_name) - The name of the view to retrieve. NA if output type is PDF - NA.<br>Output Type (output_type) - CSV or PDF. The requested statistics will be attached to the reservation CSV file.|If output types is CSV, returns the CSV file. If output type is PDF, returns the path to the PDF so that it can be downloaded.|

# Importing and Configuring the Shell
This section describes how to import the **IxChariot Controller 1G Shell** and configure and modify the shell’s service.

### Importing the shell into CloudShell

**To import the shell into CloudShell:**
 1. Make sure you have the shell’s .zip file. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  2. Backup your database.
  3. Log in to CloudShell Portal as administrator of the relevant domain.
  4. In the User menu select **Import Package**.
  
     ![](https://github.com/stsuberi/SaraTest/blob/master/import_package.png)
  5. Browse to the location of the downloaded shell file, select the relevant *.zip* file and Click **Open**. Alternatively, drag the shell’s .zip file into CloudShell Portal.

The shell is displayed in the **Shells** page and can be used by domain administrators in all CloudShell domains to create new inventory resources, as explained in [Adding Inventory Resources](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/INVN/Add-Rsrc-Tmplt.htm?Highlight=adding%20inventory%20resources). 

### Configuring a new service

**To configure a service for the device:**
  1. In CloudShell Resource Manager, in the **Inventory** tab, click **Resource Families**. 
     ![](https://github.com/stsuberi/SaraTest/blob/master/create_a_resource_device.png)
  2. In the **Traffic Generator Controller** folder, select **IxChariot Controller**.
  3. In the **Attributes** tab, enter the **Default Values** for the IxChariot Controller service as follows:
  
    * Client Install Path - Path where IxChariot Python API library was downloaded to.
    * Controller Address - IP address of the IxChariot Server.
    * User - User name for the IxChariot Server.
    * Password - Password for the IxChariot Server.
  4. Click **Save**.
  
CloudShell validates the device’s settings and updates the new resource with the device’s structure (if the device has a structure).

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
1. Download the **Ixia-IxChariot-Controller_offline_requirements.zip** file, see [Downloading the Shell](#downloading-the-shell).
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

## Data Model

The shell's data model includes all shell metadata, families, and attributes.

**[Device Name]** **Families and Models**

The controller families and models are listed in the following table:

|Family|Model|
|:---|:---|
|Traffic Generator Controller|IxChariot Controller|

# Typical Workflow and Scenarios 

**Scenario 1 - Using a controller to run IxChariot Traffic** 
1. Create a Blueprint with an IxChariot Controller service and IxChariot resource endpoints.
     * For example, for a configuration with a single flow:

![](https://github.com/stsuberi/SaraTest/blob/master/ixchariot_controller_single_flow.png)
     * Create a blueprint with two IxChariot endpoints:

![](https://github.com/stsuberi/SaraTest/blob/master/ixchariot_blueprint_two_endpoints.png)

2. Create a Sandbox from the Blueprint.
3. Edit the IxChariot Controller Service parameters if required.

![](https://github.com/stsuberi/SaraTest/blob/master/ixchariot_controller_parameters.png)

See [Configuring a new service](#configuring-a-new-service).

4. Map the configuration ports to the Sandbox ports.
For Source/Destination ends in the IxChariot configuration, assign endpoints from the endpoints in the Sandbox. Open the **Attributes** tab and set the **Logical Name** attribute to **Source** or **Destination** as follows:
     * For single flow configuration, set **Logical Name** to **Src** or **Dst** based on the role of the endpoint in the configuration setup.
     * For multiple flow configuration, set the flow number as well to **SRC-1**, **DST-2**, etc.
     * If you want to use the same endpoint for a Src of one flow and a Dst of another flow, set a list of roles separated by a space, **Src-1 Dst-2 and Src-2 Dst**.
     
![](https://github.com/stsuberi/SaraTest/blob/master/ixchariot_resource_attributes.png)     


# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation resources, see the [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 

# Release Notes 

### What's New

* Multiple endpoints per flow
* Multiple flows
* Generating of PDF report – for IxChariot server version 9.6

### Known Issues
* NA
