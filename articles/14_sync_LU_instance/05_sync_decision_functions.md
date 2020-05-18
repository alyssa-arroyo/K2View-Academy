# Sync - Decision Functions

## Sync- Decision Functions Overview

A Decision Function is a Java project function that assesses whether a sync is performed on an LUI.
* Decision functions cannot have input parameters and must have one output Boolean parameter.
* A sync is performed when a decision function returns **True**.
* A sync is not performed when a decision function returns **False**.
* Decision functions can be defined at LU Schema, LU Table or Table Population levels.
  * When defined at an LU Schema level, the decision function runs on each Table Population of each table in the LU Schema.  
  * When defined on an LU Table, the decision function runs over each Table Population in the LU Table.
  * If the decision function returns the same result for each population, it is recommended to set it on the Root Table’s population. Then invoke the [skipSync() method](https://github.com/k2view-academy/K2View-Academy/wiki/Skip-Sync) in the decision function code to skip the sync of the LUI if the conditions of the sync are not met. This way, Fabric performs a one-time execution of the decision function on each LUI instead of executing the decision function on each population. 
  * When defined for a Table Population, the decision function runs on the defined population.

[**Click for more information about Creating a Decision Function.**](https://github.com/k2view-academy/K2View-Academy/wiki/Sync--Decision-Functions#how-can-i-create-a-decision-function)\
**Click for more information about Sync Levels.**\
[**Click for more information about the Skip Sync Method.**](https://github.com/k2view-academy/K2View-Academy/wiki/Skip-Sync)

### Decision Functions for LUI Sync- Example Use Cases
Decision functions are required when the sync on an LUI needs specific logic to examine whether the data is synced from the source.

**Example** 
* Check the source environment of the execution.
* Sync the LUI if one of the following conditions is met:
  * First sync of the LUI.
  * LU Schema has changed since the last sync.
  * Source environment is Production.
* Checking if the LU Schema has changed may return a different result on each LU Table and returns True only for changed LU Tables. Therefore, you must define the decision function on the LU Schema to be executed by Fabric on each population:
  * First sync. The decision function returns True for all LU populations, i.e., Fabric executes all populations when synchronizing the LUI.
  * Running a sync on the Production environment. The decision function returns True for all LU populations, i.e., Fabric executes all populations when synchronizing the LUI.
  * Schema modifications. The decision function returns True only for LU Tables that have changed since the last LUI sync, i.e. only populations of the modified LU Tables are executed by the Sync process.

**Click for more information about Environments Management in Fabric.**\
[**Click for Code Examples of Decision Functions.**](https://github.com/k2view-academy/K2View-Academy/wiki/Sync--Decision-Functions)

**Example 2**

Support different versions of the source systems when populating the LU. 
The Development version may be different to the Production version and may have new tables or fields which do not exist in the Production version.\
Examples:
* A new field is defined for the CUSTOMER table in the Development source version: LAST_ACTIVITY_DATE.\
     When populating the CUSTOMER LU table, define two populations:
  * Production population, do not include LAST_ACTIVITY_DATE in the Select statement.
  * Development population, select LAST_ACTIVITY_DATE from the source table.
* The CASE_ACTIVITY_LOG is a new table defined in the Development source version. The population of this table must run only when running the sync on the Development source version.

The source version can be checked using a global variable: SOURCE_PRODUCT_VERSION. This global variable may have each one of the following values: 
* PROD (Production). 
* DEV (Development).

**Click for more information about Globals**

To enable Fabric to align the implementation logic to the source version, do the following:
1. Define two decision functions:\
  a. Decision function 1: Return True if the source version is Production. Otherwise, return False.\
  b. Decision function 2: Return True if the source version is Development. Otherwise, return False.
2. Attach Decision Function 1 to population objects aligned with the Production version.
3. Attach Decision Function 2 to population objects aligned with the Development version.

**Example 3**

Run a sync during off-peak hours.  
A decision function can check the current date and time. 
* If the current date and time = off-peak, return True to Sync the LUI.
* If the current date and time = peak, return False to skip the Sync.\
In this example, it is recommended to use the [skipSync() method](https://github.com/k2view-academy/K2View-Academy/wiki/Skip-Sync) in the decision function to perform a one-time execution of the decision function per LUI.

### How Can I Create a Decision Function?
1.	Go to the **Project Tree**, click the **LU** or **Shared Objects** and then right click the **Java folder**.
2.	Click **New Function** and set the **Function Type** to **Decision Function**.
3.	Define the **Name** of the **Function**.
4.	To define the **Category** of the **Function** either:\
  a. Select a **Category** from the dropdown list.\
  b. Type in a **New Category**.
5.	Write the **Function Code** and return **True** or **False**. The **Decision Function** overrides the **Sync Mode** also when it is defined as **FORCE**. 
6.	Click **Save**.

**Click for more information about Creating Functions**.\
[**Click for more information about Decision Function Checks and Considerations.**](https://github.com/k2view-academy/K2View-Academy/wiki/Decision-Function-Checks-and-Considerations-Table)\
[**Click for more information about Decision Function Code Examples.**](https://github.com/k2view-academy/K2View-Academy/wiki/Decision-Function-Checks-and-Considerations-Table#decision-functions---code-examples)

[![Previous](https://k2vacademy.s3.amazonaws.com/General/Previous.png)](https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Methods)[<img align="right" width="60" height="54" src="https://k2vacademy.s3.amazonaws.com/General/Next.png">](https://github.com/k2view-academy/K2View-Academy/wiki/Decision-Function-Checks-and-Considerations-Table)
















