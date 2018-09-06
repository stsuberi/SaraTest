![](https://github.com/stsuberi/SaraTest/blob/master/cloudshell_logo.png)

# BreakingPoint VE Static VBlade 2G Shell 

**Release date:** July 2018

Shell version 1.0.0

Document version 1.0.0

## Overview
A Shell integrates a device model, application or other technology with CloudShell. A shell consists of a data model that defines how the device and its properties are modeled in CloudShell, along with automation that enables interaction with the device via CloudShell.

### Traffic Generator Shells
CloudShell's traffic generator shells enable you to conduct traffic test activities on Devices Under Test (DUT) or Systems Under Test (SUT) from a sandbox. In CloudShell, a traffic generator is typically modeled using a chassis resource, which represents the traffic generator device and ports, and a controller service that runs the chassis commands, such as Load Configuration File, Start Traffic and Get Statistics. Chassis and controllers are modeled by different shells, allowing you to accurately model your real-life architecture. For example, scenarios where the chassis and controller are located on different machines.

For more information, see [Traffic Generators Overview](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator).

### About BreakingPoint VE Static VBlade 2G Shell
This 2nd generation Shell provides you with connectivity and management capabilities such as device structure discovery and power management for the BreakingPoint VE Static VBlade. 

To model a BreakingPoint VE Static VBlade ShelI in CloudShell, use the following: 
 
▪ [BreakingPoint Static VChassis](https://community.quali.com/repos/3910/breakingpoint-static-vchassis-shell), which provides data model and autoload functionality to model and load the BreakingPoint Static VChassis to resource management.

▪ [BreakingPoint Controller 1G Shell (service)](https://community.quali.com/repos/1295/breaking-point-controller-shell), which provides functionality to load test configuration, run tests, get test results, etc.

### Standard version
The BreakingPoint VE Static VBlade 2G Shell is based on the Deployed App Standard version 1.0.3.

### Requirements
▪ CloudShell version 8.3 and above

▪ BreakingPoint versions 8.20 and above

▪ Breaking Point Controller Shell 1.2.3 and above


### Downloading the Shell
The BreakingPoint SVE Static VBlade Shell is available from the [Quali Community Integrations](https://community.quali.com/integrations) page. 

Download the files into a temporary location on your local machine. 

The Shell comprises:

|File name|Description|
|:-----|:-----|
|Breaking.Point.Static.Virtual.Blade.Shell.zip|BreakingPoint VE Static VBlade 2G Shell package|
|breakingpoint-static-offline-dependencies.zip|Shell Python dependencies (for offline deployments only)|

### Automation
This section describes the automation (drivers or scripts) associated with the data model. The automation code (either script or driver) is associated with the model and provided as part of the Shell package (in the .zip file). 

For Traffic Generator shells, commands are configured and executed from the controller service in the sandbox, with the exception of the Autoload command, which is executed when creating the resource.

The following commands are associated with a model inside the Shell:

**BreakingPoint Controller 1G Shell**

|Command|Description|
|:-----|:-----|
|Load Configuration|Load configuration file prepared by your admin. The load configuration file includes the settings to run the traffic test. For example, packet size, number of packets to send in parallel, interval at which to send packet batches, etc. The file also reserves the necessary ports. <br>**Note**: The load configuration file must be accessible from the Execution Server, see [Traffic Generators Overview](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/LAB-MNG/Trffc-Gens.htm?Highlight=traffic%20generator).|
|Start Traffic|Start the test to generate and send the traffic to the DUT according to the settings provided in the configuration file.|
|Stop Traffic|Stop running the test to stop sending traffic from the traffic generator.|
|Get Result|Get the test result file and attach it to the sandbox.|
|Get Statistics|Get real time statistics of the traffic test in either JSON or CSV format. <br>Set the command's inputs as follows: <br>▪ **View Name**: Type of statistics to return. For example, Port Statistics, Traffic Item Statistics, Flow Statistics, etc. The types available may differ depending on the traffic generator. <br>▪ **Output Type (Enum)**: **JSON** or **CSV**. JSON prints the statistics to the sandbox's output, which is useful for API calls that can then use the output, while CSV attaches a CSV file with the test's statistics to the sandbox.|
|Get Test File|Download the test file to the location specified in the **Test Files Location** attribute defined when you added the service to your blueprint.|

## Importing and Configuring the Shell
This section describes how to import, configure and modify the BreakingPoint VE Static VBlade 2G ShelI.

### Importing the Shell into CloudShell

**To import the Shell into CloudShell:**
  1. Make sure you have the Shell’s .zip file. If not, download the Shell from the [Quali Community's Integrations](https://community.quali.com/integrations) page.
  2. In CloudShell Portal, as Global administrator, open the **Manage – Shells page**.
  3. Click **Import**.
  4. In the dialog box, navigate to the Shell’s .zip file, select it and click **Open**.
    
The Shell is displayed in the **Shells** page and can be used by domain administrators in all CloudShell domains to create new inventory resources, as explained in [Adding Inventory Resources](http://help.quali.com/Online%20Help/9.0/Portal/Content/CSP/INVN/Add-Rsrc-Tmplt.htm?Highlight=adding%20inventory%20resources). 

### Offline installation of a Shell
___
**Note:** Offline installation instructions are relevant only if CloudShell Execution Server has no access to PyPi. You can skip this section if your execution server has access to PyPi. For additional information, see the online help topic on offline dependencies.
___

In offline mode, import the shell into CloudShell and place any dependencies in the appropriate dependencies folder, see [Adding Shell and script packages to the local PyPi Server repository](#add-shell-and-script-packages-to-the-local-pypi-server-repository).

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
 
### Configuring a new resource
In CloudShell, the component that models the device is called a resource. It is based on the Shell that models the device and allows the CloudShell user and API to remotely control the device from CloudShell.

You can also modify existing resources, see [Managing Resources in the Inventory](http://help.quali.com/Online%20Help/8.3/Portal/Content/CSP/INVN/Mng-Rsrc-in-Invnt.htm?Highlight=managing%20resources).

**To create a resource for the device:**
  1. In CloudShell Portal, in the **Inventory** dashboard, click **Add New**. 
     ![](https://github.com/stsuberi/SaraTest/blob/master/create_a_resource_device.png)
  2. From the list, select **BP vBlade** Shell.
  3. Enter the Blade's **Name** and **IP address**.
  4. Click **Create**.
  5. In the **Resource** dialog box, enter all the fields relevant for this device: 
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
**BreakingPoint Blade Families and Models**

The Blade families and models are listed in the following table:

|Family|Model|Description|
|:---|:---|:---|
|CS_GenericAppFamily|BP vBlade|Static Virtual BreakingPoint modules located on the chassis|
|CS_Port|BP vBlade.GenericVPort|Generic Virtual Port|

**BreakingPoint Static VBlade Attributes**

The VBlade attribute names and types are listed in the following table:

|Attribute|Type|Default value|Description|
|:---|:---|:---|:---|
|Password|Password||Password is required by some CLI protocols such as Telnet as well as by the device configuration.|
|Public IP|String||The name of the controller group that the traffic generator is associated with or the group(s) (comma-separated) the traffic controller is part of.|
|User|String||User with administrative privileges.|
|vBlade vCenter VM|String||Virtual Blade vCenter VM to use in VM creation. <br>Should include the full path and the vm name, for example:<br>*QualiFolder/VM121*|
|vCenter Name|String||vCenter resource name in CloudShell|
|vChassis vCenter VM|String||Virtual Chassis vCenter VM to use in the VM creation. <br>Should include the full path and the name of the VM, for example:<br> *QualiFolder/VM121*|

**BreakingPoint Controller Attributes**

The controller attribute names and types are listed in the following table:

|Attribute|Type|Default value|Description|
|:---|:---|:---|:---|
|Test Files Location|String||Location for test related files.|

## Typical Workflow and Scenarios
### Use cases and scenarios

**Scenario 1 - Chassis Autoload**
See [Configuring a new resource](#configuring-a-new-resource).

**Scenario 2 - Creating a new environment**
1. Creating a new environment.
   * Enter CloudShell portal and create a new **Blueprints>Create Blueprint**.
   * Specify the blueprint name.
2. Adding resources and services to the environment. 
   * Click the **Resource** tab and add the Breaking Point Chassis resource and all needed Ports. 
   * Associate the Port sub resources with the Breaking Point Network Neighborhood Interfaces, by specifying the port attribute **Logical Name** with the BP interface ID.
   * Click the **App/Services** tab and add the **BreakingPointController** service.
   * Specify the attribute **Test Files Location**, where test files will be downloaded.
3. Adding teardown script, which runs driver command `cleanup_reservation` when reservation ends. This command releases ports which were used by the reservation. 
   * Go to the **Scripts** management page **Manage>Scripts>Environment**, click **Add New Script** and choose the **Cleanup Reservarion.zip** file. Click **Edit** for the new added script and change **Script Type** to **Teardown**.
   * Go back to the created blueprint and open properties, **Blueprint>Properties**. In the **Driver** section select **Python Setup & Teardown**, add **Estimated teardown duration** 1 min., then click **Add Script** and chose **Cleanup Reservation** from the list. To save changes click **Update**.

**Scenario 3 - Getting test file with network configuration**

*You cannot change predefined Tests and Network Neighborhoods.  Predefined Network Neighborhoods will not be included in Test files.*

This scenario helps you use predefined Tests and Network Neighborhoods.

1. Duplicating Breaking Point Network Neighborhood configuration.
   * Open the Breaking Point UI.
   * Go to **Control Center>Open Neighborhood**.
   * Find and select **Network Neighborhood** from the list.
   * Click **Save As** and enter **New Network Neighborhood Name**, click **Ok**.
2. Duplicating the Breaking Point Test.
   * Go to **Test>Open Test**.
   * Find and select the **Test** from the list.
   * Press **Save As** and save it with a new name.
3. Changing Network Neighborhood in the duplicated test.
   * Find and select the duplicated test from the list and open it.
   * In the section **Network Neighborhood** click ‘…’, find and select the duplicated Network Neighborhood.
   * Click **Save**.
4. Running the `GetTestFile BreakingPointController` command.
   * Enter CloudShell Portal, newly created blueprint and reserve it.
   * Run the BreakingComandController service command `GetTestFile` with the duplicated test name.
   * Open the folder specified in the attribute **Test Files Location**+<reservation_id> to view the file with the name of your duplicated test (extension “bpt”).

**Scenario 4 - Running a test**
1. Enter your blueprint.
2. Running BreakingPointController service Load Configuration command.
   * Click BreakingPointController **Commands** and enter the service commands.
   * Find the Load Configuration command and enter the run menu.
   * Specify the **Breaking Point config file** with the path of your test configuration file. <br>It can be a full path, or relative path under the location specified in the attribute **Test Files Location**, such as *<reservation_id>/test_name.bpt*, or only *test_name.bpt*, if it is a current sandbox.
   * Click **Run**, to load the test and network configuration from this file and reserve necessary ports.
3. Running **Start Test**.
   * Click BreakingPointController **Commands** and enter the service commands.
   * Find the **Start Traffic** command and click enter to run the menu.
   * Set **Blocking** to True, if you have to wait until the test finishes, or False. 
   * Click **Run**.
4. Running **Stop Test**.
<br>If you ran the test with “Blocking” equals False, you can immediately stop the test.
   * Run command `Stop Traffic`.
5. Getting result file.
   * Run command `Get Result`.
   * The result file is attached to the sandbox.

## References
For best practices, instructional training and video tutorials, and comprehensive product and API documentation, see the [Quali Community's Integrations](https://community.quali.com/integrations) page. 

To suggest an idea for the product and improve the product for everyone, see [Quali's Idea box](https://community.quali.com/ideabox). 

To connect with Quali users and experts from around the world, ask questions and discuss issues, see [Quali's Community forums](https://community.quali.com/forums). 