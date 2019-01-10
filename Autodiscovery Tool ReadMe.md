# **CloudShell Autodiscovery Tool**  

Release date: January 2019

Document version: 1.0

# In This Guide

* [Introduction](#introduction)
* [Installation](#installation)
    - [Installation Prerequisites](#installation-prerequisites)


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

