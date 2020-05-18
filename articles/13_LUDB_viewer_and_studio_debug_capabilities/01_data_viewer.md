# Data Viewer

The Data Viewer enables you to view a Logical Unit database, add debugging capabilities and improve testing abilities and defect resolution times. Since a Logical Unit database is in-memory, it can be viewed by dumping it into an SQLite file which can be shared via email or a common file directory for additional investigations using the Fabric Studio. This file can also be used to execute SQL queries and for analysis.\
Data Viewer files are saved under the LU VirtualDB_Data directory in:  \Fabric\ <project name> \Implementation\LogicalUnits\<LU name>\VirtualDB_Data.

**Click for more information about Logical Units.**

### How do I View Data in a Logical Unit?

![image]

1. Go to the **Project Tree**, click **Logical Units**, hover over the **Logical Unit** and click ![image] to open the **Data Viewer** window.
2. In the **Instance ID** field (top central pane) complete the **Instance ID** or **Instance ID by Function** fields and then click ![image] **Play** to generate a new **Data Viewer file**. 
Fabric retrieves data via the interfaces defined for the LU from the source DB and runs the LU mapping and transformation rules to create a new file for the LU instance. The LU instance is displayed in the tree. 
3. Click the **Instance ID** to open the **Instances Tree** dropdown list.

![image]

4. Click the **Instance DB file** to display its **tables** under the **Instance DB tree**.

![image]

5. Click a **table** to display its data and then right click the **table** to open a context menu with the following options:\
   a. **Show Data**, displays the table’s data.\
   b. **Show Schema**, displays the table’s structure.\
   c. **Show Indexes**, displays the table’s indexes, if defined.

**Click for more information about Logical Units.**

### What are the Data Viewer Components?

The Logical Unit DB Viewer contains the following areas:
* Instance ID.
* Instance Tree.
* Instance DB Tree.
* Scripting Area.
* Results Pane and Toolbar.

![image]

### Instance ID

The Instance ID area has the following components:

![image] 
### Import DB File 
	
When clicked, loads and displays an external Data Viewer file. 


### Instance ID

To complete this field, do either:
* Enter a specific Instance ID value.
* Select a previously stored Instance ID from the dropdown list.
* Write a function to generate the Instance ID. Note that this function must return a string as an output


For example:\
Instance ID by function: **fnCreateInstID** (205):

if (i_id!=null && !i_id.isEmpty()){
	 return Integer.sum(Integer.valueOf(i_id),10)+"";
   }
return "0";

![image]

When clicked, retrieves and saves the data file of the Instance ID for debugging.
	
### Instances Tree
The Instance Tree area (top left) displays a tree of available data files in the following order: 
* LU.
* Instance. 
* Dated file name.

### Instance DB Tree

The Instance DB Tree area (bottom left) displays the Table Tree which includes: 
* **k2_lu_object_info**, contains statistics per table, population and enrichment function.
* **k2_main_info**, contains the LU’s basic information like LU Name or Instance ID.
* **k2_object_stats**, contains [object] timing statistics. 
* **Reference tables under k2_Ref**. Note that these are only displayed as part of the Instance DB tree when the reference object is enabled in the LU Schema properties.

To display the values of a table in the tree, right click the table and select either:
* **Show Data**, to display the table or view it in the Results pane.
* **Show Schema**, to display the table structure in the Results pane.
* **Show Indexes**, to display the table indexes in the Results pane.

**Click for more information about References.**

### Results Pane and Toolbar
(Bottom right) Displays the data or schema requested with the row count.
 
![image]

### Scripting Area
An SQL scripting area where you can write and run SQL statements on the selected Logical Unit DB (Upper right pane).

![image]


The following options are supported:

### How do I Run an SQL Statement in the Data Viewer? 

Run and execute the SQL statement from the scripting area on the selected DB file:
1. Enter the **SQL statement** using **SQLite syntax** into the Scripting area. 
2. Select the **DB file** to be used to run the statement from the dropdown list. 
3. Do the following:\
    a. Click **Run** or **Run on New Tab** under the **Scripting area**.\
    b. Press **F5** or **Ctrl + Enter**. Separate multiple queries with ‘;’.
4. View results in the **Results pane**.

### How do I Export a Logical Unit Data File?
1. Go to the **Instance DB** Tree and right click the **DB File**. 
2. Click **Export Selected DB Files** and select the **Location** and **File Name** of the exported file. 
3. **Save** your changes. 

### Additional (Right Click) DB File Options
* **Open DB** opens the **Instance DB Tree** of the selected DB files. 
* **Delete Selected DB Files**, deletes the selected **Instance DB files** from the **project folder**:
  Fabric\<project name> \Implementation\LogicalUnits\<LU name>\VirtualDB_Data.


**Notes**\
The latest Data Viewer file can be used in the following components:
* New functions / Web Services, the latest Data Viewer is displayed in the Databases dropdown list whereby the LU table can be invoked on the code. 
**Click for more information on How to Create a New Function.**
* LU Schema, create a new table based on SQL Options to open the DB query where you can select the latest Data Viewer file. **Click for more information about Adding a Table to a Schema.**
* Population object / DB query, to display the latest Data Viewer file in the Database dropdown list. **Click for more information about Creating a New Table Population.**
* Debugging population objects. **Click for more information about Debugging a Table Population.** 






