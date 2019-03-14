# **CloudShell L1 Migration Tool**  

Release date: March 2019

Document version: 1.0

Written in Python 2.7.10

# In This Guide
* [Introduction](#introduction)
    * [Workflow](#workflow)
* [Installation](#installation)
    * [Installation Prerequisites](#installation-prerequisites)
    * [Installing the Autodiscovery tool](#installing-the-autodiscovery-tool)
* [Using the Autodiscovery Tool](#using-the-autodiscovery-tool)
    * [Help Commands](#help-commands)
* [Autodiscovering Devices in CloudShell](#autodiscovering-devices-in-cloudshell)
    * [Autodiscovering devices modeled in CloudShell](#autodiscovering-devices-modeled-in-cloudshell)
    * [Autodiscovering devices not modeled in CloudShell](#autodiscovering-devices-not-modeled-in-cloudshell)
        * [Offline Mode](#offline-mode)
        * [Online Mode](#online-mode)
        * [Additional vendors configuration file editable parameters](#additional-vendors-configuration-file-editable-parameters)
* [Creating Connections on Discovered Devices](#creating-connections-on-discovered-devices)
* [Input Data Files](#input-data-files)
    * [Input file in YAML format](#input-file-in-yaml-format)
    * [Input file in JSON format](#input-file-in-json-format)
    * [Additional vendors configuration file in JSON format](#additional-vendors-configuration-file-in-JSON-format)

# Introduction
In order to benefit from the capabilities of Quali’s upgraded L1 shells, you must migrate your existing L1 resources (based on the old shells) to new resources based on the new shells. The L1 Migration tool automates the L1 resource migration process, automatically mapping the physical connections in the new L1 resources and updating active sandbox routes in the process.

Quali’s upgraded L1 shells include certain enhancements, such as the following:

* Developing and extending L1 shells is now easier
* New shells now support different operating system versions of a particular device. This reduces the need to continuously release new shells each time a shell is released with a new OS version. 
* New shells offer enhanced shell management and customization capabilities.

**Notes:**
* You can continue using your L1 resources based on the old L1 shells. However, you will not benefit from the capabilities of the new shells. 
* Quali provides support for these older shells. However, bug fixing services are only provided for the new shell versions. 

## Workflow

1.	Create a list of the L1 resources you want to migrate. See Show resources to generate a list of the L1 resources currently in CloudShell.

2.	Install the new L1 shell versions. You do not need to create a resource from these shells.

    a.	Search the Quali Community Integrations page for the new shells.
    
    b.	Import the shells into CloudShell. See Importing Shells in the CloudShell online help.
    
3.	Install the L1 Migration tool. See Installing the L1 Migration tool.

4.	Configure the L1 Migration tool. See Configure the L1 Migration tool.

5.	Back up the routes and connections of the L1 resources you want to migrate. See Backup resource connections and routes.

6.	Run the L1 Migration tool. See Migrating L1 resources. 

7.	If you are not satisfied with your results, you can restore the L1 resource routes and connections to their state prior to the migration. See Restore resource connections and routes.

The new resources are displayed in **Resource Manager Client’s Resource Explorer** with the prefix (“New_”). The migration process copies physical connections to the new resources. In active sandboxes, all existing routes are updated to use the new L1 resources.

8.	Following a successful migration, you are advised to remove the old resources.

# Installation

## Installation Prerequisites

* CloudShell version 7.0 and above
* pip

## Installing the L1 Migration tool

**To install the L1 Migration tool via pip (PyPi):**

* Run the following command-line: 



