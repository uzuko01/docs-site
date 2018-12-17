# Zowe CLI Plug-in for IBM IMS
The Zowe CLI Plug-in for IBM® Information Management System (IMS)™ lets you extend Zowe CLI to interact with IMS resources (programs and transactions). You can use the plug-in to create new IMS applications or update existing IMS applications. For more information about IMS, see [IBM Information Management System (IMS)](https://www.ibm.com/it-infrastructure/z/ims).

  - [Use Cases](#use-cases)
  - [Prerequisites](#prerequisites)
  - [Installing](#installing)
  - [Setting up profiles](#setting-up-profiles)
  - [Commands](#commands)

## Use cases

As an application developer or DevOps administrator, you can use Zowe CLI Plug-in for IBM IMS to perform the following tasks:

- Refresh IMS transactions, programs, and dependent IMS regions. 
- Deploy application code into IMS production or test systems.
- Write scripts to automate IMS actions that you traditionally perform using ISPF editors, TSO, and SPOC. 

## Prerequisites

Before you install the plug-in, meet the following prerequisites:

  - [Install Zowe CLI](cli-installcli.md) on your computer.
  - Ensure that IBM [IMS v14.1.0](https://www.ibm.com/support/knowledgecenter/en/SSEPH2_14.1.0/com.ibm.ims14.doc/ims_product_landing_v14.html) or later is installed and running in your mainframe environment.

## Installing

Use one of the two following methods that you can use to install the Zowe CLI Plug-in for IBM IMS:

- [Installing from online registry](#installing-from-online-registry)

- [Installing from local package](#installing-from-local-package)

**Note:** For more information about how to install multiple plug-ins, update to a specific version of a plug-ins, and install from specific registries, see [Install Plug-ins](cli-installplugins.md).

### Installing from online registry

To install Zowe CLI from an online registry, complete the following steps:

1. Set your npm registry if you did not already do so when you installed Zowe CLI. Issue the following command:

    ```
    npm config set @brightside:registry https://api.bintray.com/npm/ca/brightside
    ```

2. Open a command line window and issue the following command:

    ``` 
    zowe plugins install @brightside/ims@next
    ```

3. (Optional) After the command execution completes, issue the following command to validate that the installation completed successfully.

    ```
    zowe plugins validate ims
    ```

    Successful validation of the IBM IMS plug-in returns the response: `Successfully validated`.

### Installing from local package

If you downloaded the Zowe CLI `zowe-cli-bundle.zip` package, complete the following steps to install the Zowe CLI Plug-in for IMS:

1. Open a command line window and change the local directory where you extracted the `zowe-cli-bundle.zip` file. If you do not have the `zowe-cli-bundle.zip` file, see the topic [Install Zowe CLI from local package](cli-installcli.html#installing-zowe-cli-from-local-package) for information about how to obtain and extract it.

2. Issue the following command to install the plug-in:

    ```
    zowe plugins install zowe-cli-ims-<VERSION_NUMBER>.tgz
    ```
    - **<VERSION_NUMBER>**

        The version of Zowe CLI Plug-in for IMS that you want to install from the package. The following is an example of a full package name for the plug-in: `zowe-ims-2.0.0-next.201810161407.tgz`


3. (Optional) After the command execution completes, issue the following command to validate that the installation completed successfully.
  
    ```
    zowe plugins validate @brightside/ims
    ```
    Successful validation of the IMS plug-in returns the response: `Successfully validated`. You can safely ignore `*** Warning:` messages related to Imperative CLI Framework.
      
## Setting up profiles

An `ims` profile is required to issue commands in the IMS group that interact with IMS regions. The `ims` profile contains your host, port, username, and password for the IBM CMCI server of your choice. You can create multiple profiles and switch between them as needed.

Issue the following command to create an `ims` profile: 

```
zowe profiles create ims <profile name> -H <host> -P <port> -u <user> -p <password>
```

**Note:** For more information about the syntax, actions, and options for a `profiles create` command, open Zowe CLI and issue the following command:

```
zowe profiles create ims -h
```

The result of the command displays as a success or failure message. You can use your profile when you issue commands in the `ims` command group.

## Commands

The Zowe CLI Plug-in for IBM IMS adds the following commands to Zowe CLI:

  - [Creating IMS resources](#creating-ims-resources)
  - [Deleting IMS resources](#deleting-ims-resources)
  - [Refreshing IMS resources](#refreshing-ims-resources)
  - [Querying IMS resources](#querying-ims-resources)
  - [Starting IMS resources](#starting-ims-resources)
  - [Stopping IMS resources](#stopping-ims-resources)

### Creating IMS resources

The define command lets you define programs and transactions to CICS so that you can deploy and test the changes to your CICS application. To display a list of possible objects and options, issue the following command:

```
zowe ims create -h
```

**Example:**

Define a program named `myProgram` to the region named `myRegion` in the CICS system definition (CSD) group `myGroup:`

```
zowe ims define program myProgram myGroup --region-name myRegion
```

### Deleting IMS resources

The delete command lets you delete previously defined CICS programs or transactions to help you deploy and test the changes to your CICS application. To display a list of possible objects and options, issue the following command:

```
zowe ims delete -h
```

**Example:**

Delete a program named PGM123 from the CICS region named MYREGION:

```
zowe ims delete program PGM123 --region-name MYREGION
```

### Refreshing IMS resources

The discard command lets you remove existing CICS program or transaction definitions to help you deploy and test the changes to your CICS application. To display a list of possible objects and options, issue the following command:

```
zowe ims discard -h
```

**Example:**

Discard a program named PGM123 from the CICS region named MYREGION:

```
zowe ims discard program PGM123 --region-name MYREGION
```

### Querying IMS resources

The get command lets you get a list of programs and transactions that are installed in your CICS region so that you can determine if they were installed successfully and defined properly. To display a list of objects and options, issue the following command:

```
zowe ims get -h
```

**Example:**

Return a list of program resources from a CICS region named MYREGION:

```
zowe ims get resource CICSProgram --region-name MYREGION
```

### Starting IMS resources

The install command lets you install resources, such as programs and transactions, to a CICS region so that you can deploy and test the changes to your CICS application. To display a list of possible objects and options, issue the following command:

``` 
zowe ims install -h
```

**Example:**

Install a transaction named TRN1 to the region named MYREGION in the CSD group named MYGRP:

```
zowe ims install transaction TRN1 MYGRP --region-name MYREGION
```

### Stopping IMS resources

The refresh command lets you refresh changes to a CICS program so that you can deploy and test the changes to your CICS application. To display a list of objects and options, issue the following command:

```
zowe ims refresh -h
```

**Example:**

Refresh a program named PGM123 from the region named MYREGION:

```
zowe ims refresh PGM123 --region-name MYREGION
```
