# **CloudShell Autodiscovery Tool**  

Release date: January 2019

Document version: 1.0

# In This Guide

* [Introduction](#introduction)
* [Installation](#installation)
    * [Installation Prerequisites](#installation-prerequisites)
    * [Workflow](#workflow)
    * [Installing the Autodiscovery tool](#installing-the-autodiscovery-tool)


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

   ```git clone https://github.com/QualiSystems/cloudshell-autodiscovery.git```
