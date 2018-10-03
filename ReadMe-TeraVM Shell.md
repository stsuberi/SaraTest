![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# **TeraVM Shells**  

Release date: December 2017

Shell version: 1.0.0

Document version: 1.0.0

# In This Guide

* [Overview](#overview)
* [Downloading the Shell](#downloading-the-shell)
* [Importing and Configuring the Shell](#importing-and-configuring-the-shell)
* [Updating Python Dependencies for Shells](#updating-python-dependencies-for-shells)
* [Typical Workflow and Scenarios](#typical-workflow-and-scenarios)
* [References](#references)

# Overview
A shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

### Traffic Generator Shells
CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) from a sandbox. In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator device and ports, and a controller service that runs the chassis commands, such as Load Configuration File, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells, allowing you to accurately model your real-life architecture. For example, scenarios where the chassis and controller are located on different machines.

For additional information on traffic generator shell architecture, and setting up and using a traffic generator in CloudShell, see the [Traffic Generators Overiew](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator%20overview) online help topic.

### **Tera VM Shells**
**TeraVM** shells provides you with connectivity and management capabilities such as device structure discovery and power management for the **TeraVM**. 

For more information on the **TeraVM**, see the official **TeraVM** product documentation.

To model a **TeraVM** device in CloudShell, you must use the following shells: 

▪ <a href="**[https://community.quali.com/repos/3286/teravm-chassis-2g-shell]**" target="_blank">**TeraVM Chassis 2G Shell**</a>, which provides data model and autoload functionality to model and load the TeraVM to resource management.

▪ <a href="**[https://community.quali.com/repos/3287/teravm-controller-shell]**" target="_blank">**TeraVM Controller 1G Shell**</a> (service), which provides automation commands to run the VM Chassis, such as Load Configuration, Start Traffic, Get Results. 

### Standard version
The **TeraVM** shells are based on the Traffic Shell Standard version 1.0.0.

For detailed information about the shell’s structure and attributes, see the [Traffic Shell standard](https://github.com/QualiSystems/shell-traffic-standard/blob/master/spec/traffic_standard.md) in GitHub.

### Requirements

Release: **TeraVM Shell** 1.0.0

▪ TeraVM version: 13.4

▪ CloudShell version: 7.0 and above

### Data Model

The shell's data model includes all shell metadata, families, and attributes.

#### **TeraVM Chassis Families and Models**

The chassis families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
|Traffic Generator Chassis|TeraVM Chassis|TeraVM Chassis|
|Module|Generic Traffic Generator Module|Modules located on the chassis|
|Port|Generic Traffic Generator Port|Generic Traffic Generator Port|

#### **TeraVM Chassis Attributes**

The chassis attribute names and types are listed in the following table:

|Attribute|Type|Description|
|:---|:---|:---|
|Controller Group|String|Name of the controller group that the traffic generator is associated with or the group(s) (comma-separated) that the traffic controller is part of.|
|Logical Name|String|Port's logical name in the test configuration. If left empty, automatic allocation will be applied.|
|Media Type|String|Interface media type. <br> Possible values include: **Fiber** and/or **Copper** (comma-separated)|
|Model|String|Device Model. This information is typically used for abstract resource filtering.|
|Supported Speeds|String|Speed supported by the interface (comma-separated).|
|Server Description|String|Full description of the server. Usually includes the OS, exact firmware version and additional device characteristics.|
|Version|String|Firmware version of the resource.|
|Vendor|String|Vendor name.|

#### **TeraVM Controller Attributes**

The controller attribute names and types are listed in the following table:

|Attribute|Type|Default value|Description|
|:---|:---|:---|:---|
|Test Files Location|String||Location for test related files.|
|User|String||Username for the TeraVM CLI.|
|Password|Password|Password for the TeraVM CLI.|
|CLI Connection Type|Lookup|Auto|Protocol which the shell will use to connect to the device. <br> Available methods include: **Auto**, **Console**, **SSH**, **Telnet**, and **TCP**.|
|CLI TCP Port|Numeric||TCP port to use for the CLI connection. If left empty, a default CLI port will be used based on the chosen protocol.<br> For example, Telnet will use port 23.|
|Sessions Concurrency Limit|Numeric|1|Number of sessions that can be opened on the device. Defines the number of commands that can run concurrently.|

### Automation
This section describes the automation (drivers or scripts) associated with the data model. The shell’s driver is provided as part of the shell package. There are two types of automation processes, Autoload and Resource.  Autoload is executed when creating the resource in the Inventory dashboard, while resource commands are run in the Sandbox, providing that the resource has been discovered and is online.

For Traffic Generator shells, commands are configured and executed from the controller service in the sandbox, with the exception of the Autoload command, which is executed when creating the resource.

#### **TeraVM Chassis**
|Command|Description|
|:-----|:-----|
|Autoload|Discovers all switches, modules and leaf ports (free ports that can be used for connections) connected to the controller. It will add them as a child resources for the current resource.|

#### **TeraVM Controller**
|Command|Description|
|:-----|:-----|
|Load Configuration|Loads configuration file and reserves necessary ports.|
|Start Traffic|Starts a test with the current configuration.|
|Stop Traffic|Stops running the test.|
|Get Results|Gets the test result file and attaches it to the reservation.|

# Downloading the Shell
The **TeraVM** shells are available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The shells comprise:

|File name|Description|
|:---|:---|
|TeraVM_Chassis_Shell_Package.zip|TeraVM Chassis shell package|
|TeraVM_Controller_Shell_Package.zip|TeraVM Controller shell package|
|teravm-offline-dependencies-1.0.0.zip|Shell Python dependencies (for offline deployments only)|
|Cleanup Reservation.zip|Teardown script for cleaning a reservation.|

# Importing and Configuring the Shells
This section describes how to import the **TeraVM** shells and configure and modify the shell’s devices.

### Importing the shells into CloudShell

**To import the TeraVM Controller 1G shell into CloudShell:**
  1. Make sure you have the shell’s zip package. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  
  2. Backup your database. 
  
  3. Log in to CloudShell Portal as administrator of the relevant domain.
  
  4. In the **Admin** menu, select **Import Package**.
  
  ![](https://github.com/stsuberi/SaraTest/blob/master/import_package.png)
  
  5. In the dialog box, navigate to the shell's zip package, select it and click **Open**.
  
The shell is displayed in the **Drivers/Resource** page. 
  
  **To import the TeraVM Chassis 2G shell into CloudShell:**
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
1. Download the **[Shell Offline Requirements .zip File Name]** file, see [Downloading the Shell](#downloading-the-shell).

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

**To create a resource for the TeraVM Chassis 2G shell device:**
  1. In the CloudShell Portal, in the **Inventory** dashboard, click **Add New**. 
     ![](https://github.com/stsuberi/SaraTest/blob/master/create_a_resource_device.png)
     
  2. From the list, select **TeraVM Chassis** shell.
  
  3. Enter the **Name** and **IP address** of the **TeraVM Chassis**.
  
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

# Typical Workflow and Scenarios 
(if not applicable - remove section)

**Scenario 1 - Creating a new blueprint**
1. Creating a new blueprint.
   * Log in to CloudShell Portal and create a new blueprint (**Blueprint Catalog>Create Blueprint**).
   * Give the blueprint a name.
2. Add resources and services to the blueprint. 
   * Click the **Resource** button and add the TeraVM Chassis resource and all needed ports into the diagram. 
   * Associate the port sub resources with the TeraVM interfaces, by specifying the port attribute **Logical Name**.
   * Click the **App/Services** tab and add the **TeraVMController** service.
3. Add a teardown script, which runs the **cleanup_reservation** driver command when the reservation ends. This command releases ports which were used by the reservation. 
   * Go to the **Scripts** management page **Manage>Scripts>Blueprint**, click **Add New Script** and choose the **Cleanup Reservation.zip** file. 
   * Click **Edit** for the new added script and change **Script Type** to **Teardown**.
   * Go back to the created blueprint and open properties, **Blueprint>Properties**. 
   * In the **Driver** section select **Python Setup & Teardown**, add **Estimated teardown duration** 1 min.
   * Click **Add Script** and choose **Cleanup Reservation** from the list. 
   * Click **Update** to save changes.

**Scenario 2 - Running a test**
1. Enter your blueprint.
2. From the TeraVMController service, run the **Load Configuration** command.
   * Hover over the TeraVMController service and click **Commands**.
   * In the **Resource Commands** pane, click the **Load Configuration** command.
   * Specify the **TeraVM config file** with the path of your test configuration file. <br>It can be a full path, or relative path under the location specified in the attribute **Test Files Location**, such as *<reservation_id>/test_group.xml*, or only *test_group.xml*, if it is a current sandbox. Make sure the path is accessible to the execution server running the command.
   * Click **Run**, to load the test configuration to the TeraVM controller.
3. Run the **Start Test** command.
4. Run the **Stop Test** command.
5. Get the test's result file.
   * Run the **Get Result** command.
   * The result file is attached to the sandbox.

# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation, see [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 
