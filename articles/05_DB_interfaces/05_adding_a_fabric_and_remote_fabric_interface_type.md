# Adding a Fabric / Remote Fabric Interface Type

A new DB interface can be created in Fabric based on **Internal Fabric** or **Remote Fabric** interface types. 
* An **Internal Fabric** interface type refers to a local Fabric Server and holds settings like User, Password, and Debug Server. It does not include a Host and a Port since this interface refers to the local Fabric server.
* A **Fabric Remote** interface type refers to a remote Fabric server that belongs to a different Fabric cluster. Unlike an internal (local) Fabric DB interface, its settings include the Host and Port of the remote Fabric server.

An **Internal Fabric** (local Fabric) DB interface type is defined in a project in the following cases:
* When defining a different local Fabric user for a specific Fabric activity or command. 
* When using the data as input for a [Parser] or any Fabric Project function.
* When building an LU based on another LU. For example, when creating LU Tables in an Order LU based on a Customer LU.

A **Fabric Remote** DB interface type is defined in a project in the following cases: 
* When getting data from a remote Fabric cluster.
* When using a Fabric Remote interface to run the [Query Builder] on Fabric. 

### How do I Create an Internal Fabric Interface?

1. Go to the **Project Tree**, click **Shared Objects**, right click **Interfaces**, and then select **New Interface**.
2.	Click **Interface Type** to open the dropdown list and then select **Fabric**.
3.	Define the **User** and **Password** of the internal Fabric interface.
4.	Click [**Test Connection**](https://github.com/k2view-academy/K2View-Academy/wiki/Creating-a-New-Database-Interface) to verify that the connection settings are correct.
5.	Click **Save**.

### How do I Create a Remote Fabric Interface?

1.	Go to the **Project Tree**, click **Shared Objects**, right click **Interfaces**, and then select **New Interface**.
2.	Click **Interface Type** to open the dropdown list and then select **Fabric Remote**.
3.	Populate the [**Connection Settings**](https://github.com/k2view-academy/K2View-Academy/wiki/DB-Interfaces-Overview) fields.
4.	Click [**Test Connection**](https://github.com/k2view-academy/K2View-Academy/wiki/Creating-a-New-Database-Interface) to verify that the connection settings are correct.
5.	Click **Save**.

