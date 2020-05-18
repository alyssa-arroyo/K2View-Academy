# Sync - Decision Functions Checks and Considerations Table

When a decision function returns False it always skips a sync. Therefore, when writing decision function code, always refer to the Decision Function Checks and Considerations Table below.

<table>
<tbody>
<tr>
<td width="132">
<p><strong>Check</strong></p>
</td>
<td width="472">
<p>Should the Sync on the LUI be skipped?</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Consideration</strong></p>
</td>
<td width="472">
<p>When defining a decision function on the LU Schema, the decision function runs on every population in the LU Schema.</p>
<p>If the decision function returns the same result for each population, it is recommended to set it on the Root Table&rsquo;s population. Then invoke the <strong>skipSync()</strong> method in the decision function code to skip the sync of the LUI if the conditions of the sync are not met. This way, Fabric performs a one-time execution of the decision function on each LUI instead of executing the decision function on each population.</p>
<p>For example, setting the decision functions to check whether the current time is during peak or off-peak hours.</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Fabric Function</strong></p>
</td>
<td width="472">public static&nbsp;void&nbsp;skipSync()</td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr>
<td width="132">
<p><strong>Check</strong></p>
</td>
<td width="472">
<p>Is it a first sync?</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Consideration</strong></p>
</td>
<td width="472">
<p>If the instance does not exist in Fabric and this is the first sync, consider enabling the sync on the LU instance.</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Fabric Function</strong></p>
</td>
<td width="472">
<p>public static&nbsp;boolean&nbsp;isFirstSync()</p>
<p>Returns:</p>
<p>&middot;&nbsp;&nbsp;&nbsp; First sync = True.</p>
<p>&middot;&nbsp;&nbsp;&nbsp; Subsequent sync = False.</p>
</td>
</tr>
</tbody>
</table>

<table>
<tbody>
<tr>
<td width="132">
<p><strong>Check</strong></p>
</td>
<td width="472">
<p>What is the sync mode?</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Consideration</strong></p>
</td>
<td width="472">
<p>Check the session&rsquo;s sync mode. Consider enabling a sync on the LUI&rsquo;s ID when the sync mode is set to FORCE.</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Fabric Function</strong></p>
</td>
<td width="472">public static&nbsp;<a href="https://docs.oracle.com/javase/8/docs/api/java/lang/String.html?is-external=true">String</a>&nbsp;getSyncMode()
<p>Returns:</p>
<p>Current sync mode.</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<table>
<tbody>
<tr>
<td width="132">
<p><strong>Check</strong></p>
</td>
<td width="472">
<p>Has the LU Schema Changed Since the Last Sync?</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Consideration</strong></p>
</td>
<td width="472">
<p>If the LU schema has changed since the last sync of the LUI, consider synchronizing the instance to include the latest LU Schema changes.</p>
</td>
</tr>
<tr>
<td width="132">
<p><strong>Fabric Function</strong></p>
</td>
<td width="472">public static&nbsp;boolean&nbsp;isStructureChanged()
<p>Returns:</p>
<p>True / False.</p>
</td>
</tr>
</tbody>
</table>



[**Click to go to the Decision Functions Overview.**](https://github.com/k2view-academy/K2View-Academy/wiki/Sync--Decision-Functions)\
[**Click for more information about Sync Modes.**](https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Modes)\
[**Click for more information about Sync Scenarios.**](https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Behavior---Summary-Table)\
[**Click for more information about the Skip Sync Method.**](https://github.com/k2view-academy/K2View-Academy/wiki/Skip-Sync)

Click to display a list of Fabric API: http://<Fabric IP address>:3213/static/doc/user-api/index.html

### Decision Functions - Code Examples

**Example 1**

Add a decision function on the LU Schema level to check the source environment and enable the sync of the LUI in the following scenarios:
* First sync of the LUI.
* LU Schema has been changed.
* The source environment is Production.

// Init the Boolean by true\
Boolean syncInd = true;\
// Check the source environment\
String env = getActiveEnvironmentName();

// If the active environment is not production, this sync is not the first sync of the instance, and the schema is not changed => do not sync the instance\
if(!env.toLowerCase().equals("prod") && !isFirstSync() && !isStructureChanged())\
	syncInd = false;

// DEBUG- note- the output of getTableName() was added to the log, since when setting 
// a decision function on the LU schema- it runs on each population of every LU table of the
// schema

log.info("fnCheckSourceEnv- table name: " + getTableName() + ", active env: " + env.toLowerCase() + ", isFirstSync: " + isFirstSync() +
", isStructureChanged: " +  isStructureChanged() + ", Sync indicator: " + syncInd.toString());\
return syncInd;

**Example 2**

Add a decision function on the population level in an LU Table which is populated only when run on a Development source environment. When run on a Production environment, do not populate this table, since this table does not exist in the Production DB.

// Init the Boolean by true\
Boolean syncInd = true;

// Check the product version (application version) global. Populate ACTIVITY table only of the source version is 'dev'\
String prodVer = SOURCE_PRODUCT_VERSION;

if(!prodVer.toLowerCase().equals("dev") )\
	syncInd = false;

// DEBUG
log.info("fnCheckSourceVersion- product version: " + prodVer + ", isFirstSync: " + isFirstSync() + ", isStructureChanged: " +  isStructureChanged() + ", Syc indicator: " + syncInd.toString());

return syncInd;

**Example 3**

Add a decision function on the CASE LU Table to check if the CONTRACT LU Table has been updated. The check is based on a session level Global (key) which is set to True by the population of the CONTRACT LU Table. 

// Init the Boolean by true\
Boolean syncInd = true;\
// Check the UPDATE_CONTRACT session level key.\
syncInd = UPDATE_CONTRACT ;\
return syncInd;

**Example 4**

Add a decision function on the LU Schema level to check if the current time is during peak hours or if this sync is the first sync of the LUI. If the current time is during peak hours and the instance already exists in Fabric, skip the sync of the LUI.

```java
Boolean syncInd = false;\
Boolean offPeak=true;\
LocalTime start = LocalTime.parse( "09:00:00" );\
LocalTime end = LocalTime.parse( "17:00:00" );\
LocalTime now = LocalTime.now();

if(now.isAfter(start) && now.isBefore(end))\
	offPeak=false;

if(isFirstSync() || offPeak)\
	syncInd = true;

// DEBUG\
log.info("now: " + now.toString()+ ", is offPeak: " + offPeak + ", now: " + now.toString() + " , isFirstSync(): " + isFirstSync() + " sync ind: " + syncInd);

if(!syncInd)\
     skipSync();

return syncInd;
```
Note that the fnCheckSourceEnv , fnCheckSourceVersion, and fnCheckOffPeak functions are displayed in the Demo Fabric Project under the Code tab.

[![Previous](https://k2vacademy.s3.amazonaws.com/General/Previous.png)](https://github.com/k2view-academy/K2View-Academy/wiki/Sync--Decision-Functions)[<img align="right" width="60" height="54" src="https://k2vacademy.s3.amazonaws.com/General/Next.png">](https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Method--Levels)












