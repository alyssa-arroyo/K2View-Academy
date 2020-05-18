# Sync Methods

## Sync Properties
Sync properties can be defined on an LU Schema, LU Table, or Table Population level.

**A Sync property contains the following settings:**
<table>
<tbody>
<tr>
<td width="104">
<p><strong>Timeout (sec)<strong></p>
</td>
<td width="500">
<p>The timeout in seconds for syncing the LUI.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Sync Method<strong></p>
</td>
<td width="500">
<p>None, Time Interval, Inherited and Decision Function.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Parameters<strong></p>
</td>
<td width="500">
<p>Settings of the selected Sync method. For more details see the <a href="https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Methods#sync-methods">Sync Methods section below &nbsp;</a>.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Delete Instance if Not Exists<strong></p>
</td>
<td width="500">
<p>When marked as True, Fabric deletes the LUI if the LUI is not found in the source system.</p>
<p>When marked as False (default), the instance is retained in Fabric even if the instance is not found in the source system.</p>
</td>
</tr>
</tbody>
</table>

[Click for more information about Set Timeout for Sync](https://github.com/k2view-academy/K2View-Academy/wiki/Sync-Timeout). 

## Sync Methods 
### None 
<table>
<tbody>
<tr>
<td width="104">
<p><strong>Sync Method<strong></p>
</td>
<td width="500">
<p>None</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Description<strong></p>
</td>
<td width="500">
<p>Do not sync</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Parameters<strong></p>
</td>
<td width="500">
<p>NA</p>
</td>
</tr>
</tbody>
</table>

### Time Interval 
<table>
<tbody>
<tr>
<td width="104">
<p><strong>Sync Method</strong></p>
</td>
<td width="500">
<p>Time interval.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Description</strong></p>
</td>
<td width="500">
<p>Synchronization is implemented automatically after each predefined time interval to check if the latest update of the instance in Fabric occurred before the time interval of the specific instance.</p>
<p>&middot;&nbsp;&nbsp;&nbsp; When Yes, data is extracted from the source and reloaded to Fabric.</p>
<p>&middot;&nbsp;&nbsp;&nbsp; If not, the current data in Fabric is used.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Parameters</strong></p>
</td>
<td width="500">
<p>Perform sync every:&nbsp;</p>
<p>Format = D.HH:DD:MM.</p>
<p>Default = 1 day.</p>
</td>
</tr>
</tbody>
</table>

### [Decision Function](https://github.com/k2view-academy/K2View-Academy/wiki/Sync--Decision-Functions)
<table>
<thead>
<tr>
<td width="104">
<p><strong>Sync Method</strong></p>
</td>
<td width="500">
<p>Decision</p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="104">
<p><strong>Description</strong></p>
</td>
<td width="500">
<p>Synchronization is implemented according to the decision function which returns a Boolean (True / False) parameter. If the decision function returns False, do not sync the object.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Parameters</strong></p>
</td>
<td width="500">
<p>Decision function: select the decision function from the Predefined Decision Functions dropdown list.</p>
</td>
</tr>
</tbody>
</table>

### Inherited 
<table>
<tbody>
<tr>
<td width="104">
<p><strong>Sync Method</strong></p>
</td>
<td width="500">
<p>Inherited.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Description</strong></p>
</td>
<td width="500">
<p>Synchronization of each level inherits the sync rule of its direct parent branch according to the following hierarchy:</p>
<p>&middot;&nbsp;&nbsp;&nbsp; LU Table inherits from the LU Schema.</p>
<p>&middot;&nbsp;&nbsp;&nbsp; Table Population inherits from the LU Table.</p>
</td>
</tr>
<tr>
<td width="104">
<p><strong>Parameters</strong></p>
</td>
<td width="500">
<p>&nbsp;</p>
</td>
</tr>
</tbody>
</table>
Click for more information about LU Sync Levels.

## Truncate Before Sync 
The Truncate Before Sync property can be set on an LU Table or a Table Population. When Truncate Before Sync = True, whether on the LU Table or on one of its populations, the entire LU Table is truncated before the related populations are executed for this LU Table. Therefore, there is a logical dependence between this setting and the Sync mode.

## Sync Methods - Use Cases
<table style="width: 705px;">
<tbody>
<tr>
<td style="width: 550px;" colspan="2">
<p><strong>When is a sync method selected?</strong></p>
</td>
</tr>
<tr>
<td style="width: 155px;">
<p><strong>None</strong></p>
</td>
<td style="width: 395px;">
<p>The source does not change or becomes unavailable and therefore requires a one-time only load.</p>
<p>After it is loaded, Fabric becomes the system of record for the data whereby Fabric may get update transactions on the data. For example, add a new payment.</p>
</td>
</tr>
<tr>
<td style="width: 155px;">
<p><strong>Time Interval</strong></p>
</td>
<td style="width: 395px;">
<p>Sync every X times to ensure the data is up to date.</p>
</td>
</tr>
<tr>
<td style="width: 155px;">
<p><strong><a href="https://github.com/k2view-academy/K2View-Academy/wiki/Sync--Decision-Functions">Decision Function &nbsp;</a></strong></p>
</td>
<td style="width: 395px;">
<p>Requires specific logic to check if the data needs to be synced from the source.</p>
</td>
</tr>
</tbody>
</table>

### EXAMPLES
<table width="705">
<thead>
<tr>
<td width="72">
<p><strong>Sync Method</strong></p>
</td>
<td width="315">
<p><strong>Example 1</strong></p>
</td>
<td width="315">
<p><strong>Example 2</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="72">
<p><strong>None</strong></p>
</td>
<td width="252">
<p>Load task execution statistics. Once the execution is finished, load its statistics. The statistics are not updated.</p>
</td>
<td width="294">
<p>Get initial Customer data loaded from the Billing system.</p>
<p>Additional payment transactions may then be sent by the Payment Gateway system to update the Payment LUI Table for the customer. There is no need to re-load the entire Customer object from the Billing system.</p>
</td>
</tr>
<tr>
<td width="72">
<p><strong>Time Interval</strong></p>
</td>
<td width="252">
<p>Sync the data every day or every week.</p>
</td>
<td width="294">
<p>Sync the data every day.</p>
</td>
</tr>
<tr>
<td width="72">
<p><strong>Decision Function</strong></p>
</td>
<td width="252">
<p>Check the source environment: Do not run a sync on the Production environment. However, if the source environment is a Testing environment, run a sync.</p>
</td>
<td width="294">
<p>An LU that can be populated by a different source system.</p>
<p>Set a different population with different logic for each table and then check the environment on the decision function of each population to decide if the population needs to be executed based on the environment.</p>
<p>Check the time and run a sync only during off-peak hours.</p>
</td>
</tr>
</tbody>
</table>

[![Previous](https://k2vacademy.s3.amazonaws.com/General/Previous.png)](https://github.com/k2view-academy/K2View-Academy/wiki/Sync---Ignore-Source-Exception)([<img align="right" width="60" height="54" src="https://k2vacademy.s3.amazonaws.com/General/Next.png">](https://github.com/k2view-academy/K2View-Academy/wiki/Sync--Decision-Functions)