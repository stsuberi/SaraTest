# **CloudShell Autodiscovery Tool**  

Release date: January 2019

Document version: 1.0

# In This Guide

* [Introduction](#introduction)
* [Installation](#installation)
    * [Installation Prerequisites](#installation-prerequisites)
    * [Workflow](#workflow)
    * [Installing the Autodiscovery tool](#installing-the-autodiscovery-tool)
* [Using the Autodiscovery Tool](#using-the-autodiscovery-tool)
    * [Help Commands](#help-commands)
* [Autodiscover devices in CloudShell](#autodiscover-devices-in-cloudshell)
    * [Autodiscovering devices modeled in CloudShell](#autodiscovering-devices-modeled-in-cloudshell)

# Introduction
The Autodiscovery tool enables CloudShell admins to discover a large number of devices at once “into” CloudShell, instead of having to manually create them one by one in CloudShell Portal. 

Since the tool performs a bulk discovery of devices, the relevant shells must be imported into CloudShell prior to running the tool. 

The tool supports devices that are modeled in CloudShell, but can also be customized to discover devices that are not modeled in CloudShell, see [Autodiscovering devices not modeled in CloudShell](#autodiscovering-devices-not-modeled-in-cloudshell). 

# Installation
## Installation Prerequisites
*	Windows, Linux, or Mac OS versions that support Python v2
*	Network access to the devices you want to discover
*	SNMP enabled on all devices
*	CloudShell version 8.0 and above
*	Python 2.7.x

    **Important:** If you have another version of Python installed on the autodiscovery machine, this may cause unexpected behavior.
*	pip

## Workflow
1.	Create a list of the devices you want to discover, by providing specific IPs and/or IP ranges.
2.	Make sure you have an appropriate shell for each device you wish to discover. 
3.	We recommend to first search for the shells in the [Quali Community Integrations](https://community.quali.com/integrations) page. Note that you can also extend existing shells to match the device’s specifications or create new shells from scratch - see the [CloudShell Dev guide](https://devguide.quali.com/introduction/9.0.0/the-cloudshell-devguide.html) for more information.
4.	Import the shells into CloudShell - see [Importing Shells](https://help.quali.com/Online%20Help/9.1/Portal/Content/CSP/MNG/Mng-Shells.htm#Adding) in the CloudShell online help.
5.	Run the Autodiscovery tool. When the process completes, the discovered device resources are included in the Inventory dashboard in CloudShell Portal. 

## Installing the Autodiscovery tool

There are two ways to install the Autodiscovery tool:
* Install via pip (public PyPi repository): 

   ```pip install cloudshell-autodiscovery```
   
* Install from the tool’s GitHub repository source:  

   ```
   git clone git@github.com:QualiSystems/cloudshell-autodiscovery.git
   
   cd cloudshell-autodiscovery
   
   pip install -r requirements.txt 
   
   python setup.py install
   ```
   If git is not installed, replace the first line with the following: 
         
      git clone https://github.com/QualiSystems/cloudshell-autodiscovery.git
      
# Using the Autodiscovery Tool
The tool is installed in the machine’s default Python27 folder. For example: *c:\Python27\Scripts folder*. 

 ![](https://github.com/stsuberi/SaraTest/blob/master/autodiscovery-install-files.png)

To use the tool, navigate to this folder in command-line, unless you have set these folders as env variables which will allow you to run the tool from anywhere on the machine.

* **Note:** It is recommended to add the python and pip installation folder paths to your local environment variables. For example, C:\Python27 and C:\Python27\Scripts. This will enable you to run the python/pip commands from any folder.

You can perform these procedures in either offline or online mode. In online mode, you generate the autodiscovered device configurations and create them as is, while in offline mode, you can optionally modify the autodiscovered device configurations before creating and discovering them into CloudShell. 

## Help Commands

To list the commands available in this tool, run the following command-line: 

```autodiscovery --help```

To learn what version of the Autodiscovery tool you are using, run the following command-line: 

```autodiscovery version --help```

To view specific options associated with any autodiscovery command, type the command and add --help. For example:

```autodiscovery <echo-input-template> --help```

# Autodiscover devices in CloudShell

This chapter explains how to discover devices in CloudShell using the Autodiscovery tool. The tool supports devices that are modeled by Quali-published shells and devices for which you have a new or extended shell. 

   * [Autodiscovering devices modeled in CloudShell](#autodiscovering-devices-modeled-in-cloudShell)
   * [Autodiscovering devices not modeled in CloudShell](#autodiscovering-devices-not-modeled-in-cloudShell)
   
## Autodiscovering devices modeled in CloudShell  

**To autodiscover devices modeled in CloudShell:**

1. Open command line and navigate to the autodiscovery tool’s installation folder. 

2. To generate the input file, run the following command-line.

   ```autodiscovery echo-input-template --save-to-file input.yml```

   To generate the file in json format, change “yml” to “json”.
   
   The *input* file is created in the folder where you ran the command. If you want the file to be created in a different location, specify the full path to this location.
   
   For reference, see sample input files: Input file in YAML format or Input file in JSON format.

   To change the name of the file from the default *input.yml*, replace the <input filename> in the command below: 
   
   ```autodiscovery echo-input-template --save-to-file <input filename>.[yml|json]```

3. Open the *input* file in your preferred editor and update the device info and CloudShell server credentials.

   1. Update the fields to include the details of the devices you want to discover as follows:
   
   |Field|Description|
   |:---|:---|
   |IP of devices to discover|**devices-ips:** Add a single device ip or a range of device ips and the domain in which to create them.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**range:** If you want to add a string of devices, it must follow this format: xxx.xxx.xx.100-110. You can have a range within the IP address in any segment of the address, for example xxx.xxx.9.1-10.xxx.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**domain:** Specify the CloudShell domain. If you want the devices to be created in the Global domain (default), omit this line.|
   |IP and credentials for the CloudShell API|**cloudshell:**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**ip:** Address of the CloudShell API<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**user:** Admin user on CloudShell<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**password:** Admin user's password|
   |Possible SNMP community strings|**community-strings:** Add possible SNMP read community strings for the devices, such as public, public2 etc.|
   |Additional settings per Vendor|**vendor-settings:** <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**Default:**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **cli-credentials**: (mandatory) Add default values to be used if all devices have the same CLI credentials, including user, password, enable password etc.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **folder-path:** Add the folder path as it appears in CloudShell Resource Manager Client.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**Cisco/Juniper:** (vendor specific information) Add other device credentials as required for specific vendors.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **cli-credentials:** Add user and password<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **folder-path:** Add the folder path as it appears in CloudShell Resource Manager Client.|
   
   2. Save your changes. Make sure you do not save the file to a different folder.
   
4. At this point, you can choose to immediately discover the devices as resources into CloudShell or make modifications to the device settings before discovering them. Perform the appropriate procedure:

   **To immediately discover the devices in CloudShell:**
   
   * Run the following command-line from the folder containing the input file:
   
         autodiscovery run --input-file input.yml
         
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**If you changed the file name, make sure you replace “input.yml” with the new name.**

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The devices are discovered in CloudShell. A *discovery_report.xlsx* file is produced in the input file’s containing folder, providing the following information about the discovered devices:
   
   |Field|Description|
   |:---|:---|
   |IP|Device IP|
   |Vendor|Device vendor, for example: Cisco|
   |sysObjectID|OID unique name for each device|
   |Description|Device description|
   |SNMP Read Community|SNMP Read Community string, for example: Public|
   |Model Type|Device model type, for example: router, switch, etc.|
   |Device Name|Resource’s display name in CloudShell| 
   |Domain|**Global** (default) or other domain assigned in the input file in CloudShell|
   |Folder|Containing folder of the resource, as displayed in CloudShell Portal’s **Inventory** dashboard and the Resource catalog in the blueprint and sandbox diagrams.|
   |Attributes|Resource attributes, for example: Enable SNMP=False, SNMP Read Community=Public. User can add any attribute defined in the shell model. 
   |Added to CloudShell|Indicates the devices that were added to CloudShell as resources. Possible values are: Skipped, Failed, and Success.|
   |Comment|Any issues related to the processing of a specific device|
   
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Notes:**
   
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; To generate a log file, add the following tag:
 
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--log-file <log filename>

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To run this command-line without discovering the resources on CloudShell, i.e. only create the resources in CloudShell but do not discover them, add the following tag. 
   
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; --no-autoload

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;After the tool creates the resources in CloudShell, you will have to manually discover each individual resource in CloudShell.
    
   **To edit device details before discovery:**
   
   1. To generate an Excel report, run the following command-line from the folder containing the input file:
   
      ```autodiscovery run --input-file input.yml --report-file <report filename> --offline```
   
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - By default the report file is saved to the current user’s C: drive folder. However, you can choose to save the file in a different existing folder, for example: 
    
     ```autodiscovery run --input-file input.yml --report-file C:\Users\Administrator\temp\<report filename> --offline ```
    
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Notes:**
   
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; To generate the report in console format instead of .xlsx (default), add the following tag:
 
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;--report-type console

   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To generate a log file, add the following tag:
   
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; --log-file <log filename>

  2. Update the report file as appropriate.
  
  3. To discover the devices into CloudShell from the report, run the following command-line:
  
  ```autodiscovery run-from-report --input-file input.yml --report-file <report filename>.xlsx```
   
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; - You must run this command from the same folder where the report file is saved. By default, the file is saved to the location where you ran the command.  
   
 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**Notes:**
    
    To generate a log file, add the following tag: 
   -- log-file <log filename>

    
   
   
