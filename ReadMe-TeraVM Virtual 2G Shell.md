![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# **TeraVM Virtual 2G Shells**  

Release date: April 2018

Shell version: 1.0.0

Document version: 1.0

# In This Guide

* [Overview](#overview)
* [Downloading the Shell](#downloading-the-shell)
* [Importing and Configuring the Shell](#importing-and-configuring-the-shell)
* [Updating Python Dependencies for Shells](#updating-python-dependencies-for-shells)
* [Typical Workflows](#typical-workflows)
* [References](#references)


# Overview
A shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

### Traffic Generator Shells
CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) from a sandbox. In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator device and ports, and a controller service that runs the chassis commands, such as Load Configuration File, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells, allowing you to accurately model your real-life architecture. For example, scenarios where the chassis and controller are located on different machines.

For additional information on traffic generator shell architecture, and setting up and using a traffic generator in CloudShell, see the [Traffic Generators Overiew](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator%20overview) online help topic.

### **TeraVM Virtual 2G Shells**
The **TeraVM Virtual 2G** shells provides you with connectivity and management capabilities such as device structure discovery and power management for the **TeraVM vChassis** and the **TeraVM vBlade**. 

For more information on the **TeraVM Virtual vChassis** or the **TeraVM Virtual vBlade**, see the official **TeraVM** product documentation.

To model an **TeraVM Virtual vChassis** device in CloudShell, use the following controller and vBlade: 

▪ [TeraVM Controller Shell (Service)](https://community.quali.com/repos/3287/teravm-controller-shell), which provides automation commands to run on the VChassis, such as Load Test Configuration, Start Traffic, Get Statistics.

▪ [CloudShell TeraVM vBlade 2G Shell](https://community.quali.com/repos/3403/cloudshell-teravm-vblade-shell), which provides connectivity and management capabilities such as device structure discovery and power management for the CloudShell TeraVM vChassis.

### Standard version
The **TeraVM Virtual 2G** shells are based on the Traffic Shell Standard 1.0.0.

For detailed information about the shell’s structure and attributes, see the [Traffic Shell standard](https://github.com/QualiSystems/shell-traffic-standard/blob/master/spec/traffic_standard.md) in GitHub.

### Requirements

Release: **TeraVM Virtual 2G shells 1.0.0**

▪ TeraVM versions: 13.4 and above

▪ CloudShell version: 8.2 and above

### Data Model

The shell data models includes all shell metadata, families, and attributes.

#### **TeraVM Chassis Families and Models**

The chassis families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
|Virtual Traffic Generator Chassis|TeraVM Chassis|TeraVM Deployed Controller|
|Module|TeraVM Virtual Traffic Generator Module|TeraVM Deployed Module|
|Port|TeraVM Virtual Traffic Generator Port|Port on the Deployed TeraVM Module|

#### **TeraVM Chassis Attributes**

The attribute names and types are listed in the following table:

|Attribute|Type|Description|
|:---|:---|:---|
|License Server|String|IP address or hostname of the License Server|
|Executive Server|String|IP address or hostname of the Executive Server|
|TVM Comms Network|String|TeraVM Comms Network name on the vCenter|
|TVM MGMT Network|String|TeraVM Management Network name on the vCenter|
|Password|Password|Password for the Deployed TeraVM Controller|
|User|String|Username for the Deployed TeraVM Controller|

#### **TeraVM Module Attributes (vBlade)**

The attribute names and types are listed in the following table:

|Attribute|Type|Description|
|:---|:---|:---|
|TVM Comms Network|String|TeraVM Comms Network name on the vCenter|
|TVM MGMT Network|String|TeraVM Management Network name on the vCenter|

#### **TeraVM Port Attributes**

The attribute names and types are listed in the following table:

|Attribute|Type|Description|
|:---|:---|:---|
|Logical Name|String|The port's logical name in the test configuration|
|Requested vNIC|String|vNIC number from vCenter|
|MAC Address|String|Port's MAC address|

### Automation
This section describes the automation (drivers) associated with the data model. The shell’s driver is provided as part of the shell package. There are two types of automation processes, Autoload and Resource.  Autoload is executed when creating the resource in the Inventory dashboard, while resource commands are run in the Sandbox, providing that the resource has been discovered and is online.

For Traffic Generator shells, commands are configured and executed from the controller service in the sandbox, with the exception of the Autoload command, which is executed when creating the resource.

|Command|Description|
|:-----|:-----|
|Autoload|Discovers the chassis, its hierarchy and attributes when creating the resource. The command can be rerun in the Inventory dashboard and not in the sandbox, as for other commands.|

#### TeraVM Controller Shell

|Command|Description|
|:-----|:-----|
|Load Configuration|Loads the configuration file and reserves necessary ports.<br>* **TeraVM config file** (String)(Mandatory): The configuration file name. Path should include the protocol type, for example *tftp://10.10.10.10/asdf*.<br>* **Use ports from reservation** (Enum): Possible values: **True** or **False**. Update the configuration file with ports from the current reservation by their **Logical Name** attributes.
|Start Traffic|Starts a test with the current configuration.|
|Stop Traffic|Stops running the test.|
|Get Results|Gets the test result file and attaches it to the reservation.|

# Downloading the Shell
The **TeraVM Virtual 2G** shells are available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The shells comprise:

|File name|Description|
|:---|:---|
|TeraVM_Controller_Shell_Package.zip|TeraVM Controller shell package|
|teravm-vchassis.zip|TeraVM vChassis shell package|
|teravm-vblade.zip|TeraVM vBlade shell package|
|teravm-offline-package-1.0.0.zip|Shell Python dependencies (for offline deployments only)|
|TeraVM.Sandbox.Setup.1.0.zip|CloudShell Reservation Setup script|

# Importing and Configuring the Shell
This section describes how to import the TeraVM Virtual shells and configure and modify the shell’s devices. 

### Importing the shells into CloudShell

**Note**: You will need to repeat these procedures, for the controller shell, the vChassis shell, and the vBlade shell.

**To import the shell into CloudShell:**
  1. Make sure you have the shell’s zip package. If not, download the shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  
  2. Backup your database.
  
  3. Log in to CloudShell Portal as administrator of the relevant domain.
  
  4. In the User menu select **Import Package**.
  
     ![](https://github.com/stsuberi/SaraTest/blob/master/import_package.png)
     
  5. Browse to the location of the downloaded shell file, select the relevant *.zip* file and Click **Open**. Alternatively, drag the shell’s .zip file into CloudShell Portal.

The TeraVM Controller shell is displayed in the **Services** page and can be used run custom code and automation processes in the sandbox. For more information on Services, see [Services Overview](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Services.htm?Highlight=services).

The vBlade and vChassis shells are now ready to be used to create new Apps, see [Configuring a new App](#configuring-a-new-app). For more information on Apps, see [Apps Overview](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Apps.htm?Highlight=applications). 

### Offline installation of a shell

**Note:** Offline installation instructions are relevant only if CloudShell Execution Server has no access to PyPi. You can skip this section if your execution server has access to PyPi. For additional information, see the online help topic on offline dependencies.

In offline mode, import the shell into CloudShell and place any dependencies in the appropriate dependencies folder. The dependencies folder may differ, depending on the CloudShell version you are using:

* For CloudShell version 8.3 and above, see [Adding Shell and script packages to the local PyPi Server repository](#adding-shell-and-script-packages-to-the-local-pypi-server-repository).

* For CloudShell version 8.2, perform the appropriate procedure: [Adding Shell and script packages to the local PyPi Server repository](#adding-shell-and-script-packages-to-the-local-pypi-server-repository) or [Setting the python pythonOfflineRepositoryPath configuration key](#setting-the-python-pythonofflinerepositorypath-configuration-key).

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
1. Download the *teravm-offline-package-1.0.0* file, see [Downloading the Shell](#downloading-the-shell).

2. Unzip it to a local repository. Make sure the execution server has access to this folder. 

3.  On the Quali Server machine, in the *~\CloudShell\Server\customer.config* file, add the following key to specify the path to the default python package folder (for all Execution Servers):  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`

4. If you want to override the default folder for a specific Execution Server, on the Execution Server machine, in the *~TestShell\Execution Server\customer.config* file, add the following key:  
	`<add key="PythonOfflineRepositoryPath" value="repository 
full path"/>`

5. Restart the Execution Server.

### Configuring a new App

#### Configuring a new App based on the vBlade shell

This section explains how to create an App template for the TeraVM vBlade shell (Module) to enable network connectivity between endpoints in the sandbox.

1. In CloudShell Portal, as Global administrator, open the **Manage – Apps** page.

2. Click **Add**.

3. Select **vCenter VM from Template**.

4. Enter the **Name** of the App and click **Create**.

5. In the **Deployment Paths** tab, select the **Cloud Provider** and enter the **vCenter Template** to be used in VM creation. It should include the full path and template name, for example QualiFolder/Template.

![](https://github.com/stsuberi/SaraTest/blob/master/teravm_module_app_deployment.PNG)

6. In the **App Resource** tab, select the **TeraVM Virtual Traffic Generator Module** shell and specify all the required configuration attributes for this shell, see [TeraVM Module Attributes (vBlade)](#teravm-module-attributes).

![](https://github.com/stsuberi/SaraTest/blob/master/teravm_module_app_resource.png)

7. Click **Done**.

#### Configuring a new App based on the vChassis shell

This section explains how to create an App template for the TeraVM vChassis shell to enable network connectivity between endpoints in the sandbox.

1. In CloudShell Portal, as Global administrator, open the **Manage – Apps** page.

2. Click **Add**.

3. Select **vCenter VM from Template**.

4. Enter the **Name** of the App and click **Create**.

5. In the **Deployment Paths** tab, select the **Cloud Provider** and enter the **vCenter Template** to be used in VM creation. It should include the full path and template name, for example QualiFolder/Template.

![](https://github.com/stsuberi/SaraTest/blob/master/teravm_chassis_app_deployment.png)

6. In the **App Resource** tab, perform the following steps for the blade:
	1. Select the **TeraVM Chassis** shell and specify all required configuration attributes for this shell:See attribute section.
	
	![](https://github.com/stsuberi/SaraTest/blob/master/teravm_chassis_app_deployment.PNG)
	
	2. Select the **TeraVM Virtual Traffic Generator Module** shell and specify all required configuration attributes for this shell. See attribute section.
	![](https://github.com/stsuberi/SaraTest/blob/master/ixvm_deployment_app_2g_app_resource.PNG)

7. Click **Done**.

### Configuring the TeraVM Controller 
This section explains how to configure the TeraVM Controller service to that.....

1. In your blueprint, add the TeraVMController service there. 

2. Specify the attribute Test Files Location (with value of location where test files will be downloaded). All other attributes aren't required and can be blank.

### Configuring the setup script
This section explains how to add the setup script for the **IxVM Deployment App Chassis 2G** shell.

**To add the setup script:**
1. Log in to CloudShell Portal as administrator of the relevant domain.

2. Go to the **Manage** dashboard and click **Scripts>Blueprint**.

3. Click **Add New Script**. From the list, select the downloaded setup script *IxVM.Sandbox.Setup.1.0.0.zip*.

4. Click **Edit** and change the **Script Type** to **Setup**.

5. Click **Save**.


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

**Workflow 1** - *Deploying the TeraVM Module and Controller* 
1. Create a new blueprint.
   * Log in to CloudShell Portal and create a new blueprint (**Blueprint Catalog>Create Blueprint**).
   * Give the blueprint a name.
   
2. Add Apps and services to the blueprint. 
   * Click the **App/Services** tab and add the following to the canvas:
   	1. **TeraVMController** service - Make sure that you specify attribute Test Files Location (with value of location where test files will be downloaded). All other attributes aren't required and can be blank. See "Configuring Controller attributes".
	2. **TeraVM Chassis** App
	3. **TeraVM Blade** App
	
3. Update the blueprint setup script, which .... 
   * Open properties, **Blueprint>Properties**. 
   * Remove Default Sandbox Setup 2.0 script by clicking on the trash icon nearby its name.
   * Click **Add Script** and choose **TeraVM.Sandbox.Setup.1.0** from the list. 
   * Click **Update** to save changes.
   
4. Run the **Reserve** command on the blueprint to deploy the TeraVM Controller and TeraVM Module.

**Workflow 2** - *Running a test* 
1. Enter your blueprint.

2. From the TeraVMController service, run the **Load Configuration** command.
   * Hover over the TeraVMController service and click **Commands**.
   * In the **Resource Commands** pane, click the **Load Configuration** command.
   * Specify the **TeraVM config file** with the path of your test configuration file. <br>It can be a full path, or relative path under the location specified in the attribute **Test Files Location**, such as *<reservation_id>/test_name.bpt*, or
only *test_name.bpt*, if it is current reservation. Make sure the path is accessible to the execution server running the command.
   * Click **Run**, to load the test configuration to the TeraVM Controller and reserve necessary ports.
   
3. Run the **Start Test** command.

4. Run the **Stop Test** command.

5. Get the test's result file.
   * Run the **Get Result** command.
   * The test's result file is attached to the sandbox.


# References
To download and share integrations, see [Quali Community's Integrations](https://community.quali.com/integrations). 

For instructional training and documentation, see [Quali University](https://www.quali.com/university/).

To suggest an idea for the product, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 
