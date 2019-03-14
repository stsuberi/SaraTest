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
7.	If you are not satisfied with your results, you can restore the L1 resource routes and connections to their state prior to the migration. See Restore resource connections and routes.<br>
The new resources are displayed in **Resource Manager Client’s Resource Explorer** with the prefix (“New_”). The migration process copies physical connections to the new resources. In active sandboxes, all existing routes are updated to use the new L1 resources.
8.	Following a successful migration, you are advised to remove the old resources.

# Installation

## Installation Prerequisites

* CloudShell version 7.0 and above
* pip

## Installing the L1 Migration tool

**To install the L1 Migration tool via pip (PyPi):**

* Run the following command-line: 

   ```pip install cloudshell-l1-migration```
   
# Help Commands

**To list the tool’s main commands:**

* Run the following command-line: 

   ```migration_tool --help```
   
To use the tool, navigate to the folder in command-line.

**Note:** It is recommended to add the python and pip installation folder paths to your local environment variables. For example, C:\Python27 and C:\Python27\Scripts. This will enable you to run the python/pip commands from any folder.

**To view the tool’s version number:**

* Run the following command-line: 

   ```migration_tool --version```
   
**To show detailed information for a main command:**

* Run the following command-line: 

   ```migration_tool <command> --help```
   
   Where **<command>** is the name of the main command.


# Configuration

**To configure the L1 Migration tool:**

1. Configure your CloudShell credentials: 

Run the following command-lines and replace your CS credentials within the <>. For example, replace <CSHost> with your CloudShell host, etc.: 
   
   ```
   migration_tool config host <CSHost>
   migration_tool config username <CSUserName>
   migration_tool config password <CSPassword>
   migration_tool config domain <CSDomain>
   migration_tool config port <CSPort>
   ```

2. Configure other elements of the tool:
•	**To view the tool’s current configuration, run the following command-line:**

   ```migration_tool config```
   
   After running this command, the following output (sample) is generated:
   

   ```username: admin
domain: Global
name_prefix: new_
logging_level: INFO
host: localhost
backup_location: C:\Users\Administrator\AppData\Roaming\Quali\migration_tool\Backup
password: ******
port: 8029```

•	**To specify the tool’s log level information:**

Run the following command-line:

Specify either **DEBUG** to obtain the most detailed logging information or **INFO** for basic logging information. If you do not specify a value here, the default value **(INFO)** will be used. Logging information is displayed in the output in your Command Prompt window after running a command.

   ```migration tool config logging_level <DEBUG or INFO>```

•	**To change the backup file’s containing folder:**

   Run the following command-line:
   
   ```migration_tool config backup_location C:\<FOLDER_PATH>```
   
The L1 Migration tool automatically creates a new backup file each time you run a migration command, saving your existing connections and routes in the following default location: C:\Users\<user>\AppData\Roaming\Quali\migration_tool\Backup. The file is generated in yaml format.

•	**To change the prefix for your new migrated resources:**

   Run the following command-line:
   
   ```migration_tool config name_prefix "<New>_"```

   Replace <New> with the desired prefix. 

•	**To generate a custom config file based on the tool’s default configuration:**

   Run the following command-line:
   
   ```migration_tool config --config <FILE-PATH> <config command>```
   
Replace <FILE-PATH> with the relative file path and name of the custom config file and <config command> with any command that updates a parameter in the config file. For example:

   ```migration_tool config --config test.conf name_prefix "test"```
   
You now have a custom config file, based on the default configuration, in the location specified.

The config file uses the “Yaml” format, however, any of the following file extensions can be used: .conf, .yaml, .or yml.

This file can now be used later as needed. It is helpful if you have more than one configuration. You can specify this config file when running a command.

•	**To list the patterns table (For Quali support use only!):**

   Run the following command-line:
   
   ```migration_tool config --patterns-table```
   
   Patterns distinguish blocks of relative addresses which are used for port association.  

•	**To add a new pattern associated with a resource Family/Model (For Quali support use only!):**

   Run the following command-line:
   

   ```migration_tool config --patterns_table "L1 Switch/Test Switch Chassis" ".*/(.*)/(.*)"```

