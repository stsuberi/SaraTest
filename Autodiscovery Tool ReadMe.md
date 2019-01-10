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

**Help Commands

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
   |Additional settings per Vendor|**vendor-settings:** <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**Default:**<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **cli-credentials**: (mandatory) Add default values to be used if all devices have the same CLI credentials, including user, password, enable password etc.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **folder-path:** Add the folder path as it appears in CloudShell Resource Manager Client.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;•**Cisco/Juniper:** (vendor specific information) Add other device credentials as required for specific vendors.<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **cli-credentials:** Add user and password<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- **folder-path:** Add the folder path as it appears in CloudShell Resource Manager Client.|
