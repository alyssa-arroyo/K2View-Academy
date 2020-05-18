# Fabric Studio Log Files

Fabric Studio enables you to develop, test and monitor projects within the Studio using Fabric’s test and log capabilities. 

To display a list of recent messages from the server, click
![image] Server / Activity Logs (left menu). By default, this window only displays warnings and error messages, however additional messages and notices can also be reviewed.\ The following are the main log options:
* Server logs.
* Activity logs.
* Compilation errors.

**Click for more information about UI Components and Menus.**

### How do I Review Server / Activity Logs and Compilation Errors?
**Server Logs**
1. Click ![image]  **Server Logs** and then click either **Errors**, **Warnings** or **Messages** to display the relevant server logs list.

![image]

2. Right click in the **Log’s list** area to display the following context menu options:
   a. **Select Open Selected Items Data in Notepad**, to review the entire error or notification message.
   b. **Select Copy Selected Items Data**, to copy the entire text onto the clipboard.
   c. **Clear List** to remove the listed logs. Clear list can also be accessed by clicking the **Clear List** icon (top pane).

**Activity Logs**  

3. Click ![image]  **Activity Logs** to open the Activity Logs window.

![image]

4. Follow **Step 2** to select and review the log. 

**Compilation Errors**

5. Click ![image]  **Compilation Errors** to open the following window. 

![image]

6. Follow **Step 2** to select and review the log. 

**Output**

7. Click ![image]   **Output** to open the following window where you can review the K2Fabric log:

![image]

### Debugging Logs and Messages
 
Logs and messages can also be used for debugging purposes. The following methods are available:\
reportUserMessage ():

Enables Fabric Studio’s Debug options and a quick sanity review of the implementation. This method can be added to any Java code and viewed by clicking Messages under the Server Logs area. Messages are generated either by invoking the Fabric Studio [Data Viewer] or by executing the [Table Population Debug] option.

The recommended usage for this option is to debug a project during its implementation stages in order to prevent overloading Fabric Server runtime logs (k2Fabric.log). After the Debug process is complete, it is recommended to either delete the Debug message or to comment it out. 

![image]

For example: **fnCreateInstID** under Customer LU

 if (i_id!=null && !i_id.isEmpty()){
// Increase the input by 10 and return      
      reportUserMessage("o_id:"+(Integer.sum(Integer.valueOf(i_id),10)+""));
	return Integer.sum(Integer.valueOf(i_id),10)+"";
   }
log.info ():


Enables Fabric’s runtime Debug options. This method can be added to any Java code and its output can be viewed after deployment and during runtime. The runtime log (k2fabric.log) can be reviewed in the Fabric Server’s Logs directory or in the Studio’s Output logs.\
For example: **fnCreateInstID** under Customer LU
 
if (i_id!=null && !i_id.isEmpty()){
```java// Increase the input by 10 and return
        log.info("o_id: "(Integer.sum(Integer.valueOf(i_id),10)+""));
	  return Integer.sum(Integer.valueOf(i_id),10)+"";






