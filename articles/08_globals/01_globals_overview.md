# Globals Overview

### What are Globals?
Globals are predefined variables that can be accessed by different objects within a project and are used when the same information is required repeatedly by various Fabric objects. For example, to define the source application version or a date format in order use the same value in several Fabric objects. 
* Globals are saved in a Java file as static variables and can be used by all Fabric object types like Project functions or Table Population objects.
* Globals can be defined as Final and then they cannot be overridden in Java code or by a command that runs on the Fabric Server.
* Globals that are not defined as Final can be overridden.

**Click for more information about Globals Override Commands.**

The scope of a Global depends on how it is defined, which can be either:
* Shared Objects, whereby the Global is available to all objects in a Project under all Logical Units, Reference Tables and Web Services.
* [Logical Unit](https://github.com/k2view-academy/K2View-Academy/wiki/Logical-Units-Overview), whereby the Global is available within the specific Logical Unit where it is defined.

If the same Global is defined at both Shared Objects and Logical Unit levels, the Logical Unit definition is used within the scope of that Logical Unit. Other Logical Units use the Shared Objects definition.

**Click for more information about Using Globals in Fabric.**

### How do I Create or Edit a Global?
1. Do either:\
    a. Go to the **Project Tree**, click **Logical Units > <LU name> -> Java** and then click **Globals.java** to open 
    **Globals** window. \
    b. Go to the **Project Tree**, click **Shared Objects > Java** and then click **SharedGlobals.java** to open 
    **Globals** window. 

2. Populate the settings as follows:\
  a.	Enter a **Global Name** in the **Name** column.\
  b.	Enter a value in the **Value** column.\
  c.	(Optional) Enter a **Category** in the **Category** column.\
  d.	(Optional) Enter a **Comment** in the **Comment** column.\
  e.	Check if the **Global** is **Final**.

3. Click **Save**.

**Notes**
* Each Global defined via the Globals window is created in either Globals.java under the LU or in SharedGlobals.java under the Shared Object. 
* A Global can be edited via the respective Globals window or by opening the source file in Fabric Studio. 

**Click for more information about using Globals - Code Examples.**


