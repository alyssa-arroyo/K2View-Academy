# Enrichment Function vs. Root Function - Comparison Analysis

Enrichment functions and [Root functions](/articles/07_table_population/11_1_creating_or_editing_a_root_function.md) are both Fabric [Project functions](/articles/07_table_population/08_project_functions.md) that can run complex logic on [LU Tables](/articles/06_LU_tables/01_LU_tables_overview.md) like invoking Fabric commands <!--Add a link to Fabric commands KI-->, complex data manipulations and SQL statements on different [DB interfaces](/articles/05_DB_interfaces/03_DB_interfaces_overview.md). Both Enrichment functions and Root functions run during an [LUI sync](/articles/14_sync_LU_instance/01_sync_LUI_overview.md).
There are major differences between Root functions and Enrichment functions and it is important to understand them in order to select the correct solution for each scenario. 

The following table displays the comparison analysis between Enrichment and Root functions and provides insight on how and when each function type should be used.

<table>
<thead>
<tr>
<td width="95">
<p>&nbsp;</p>
</td>
<td width="241">
<p><strong>Enrichment Function</strong></p>
</td>
<td width="269">
<p><strong>Root Function</strong></p>
</td>
</tr>
</thead>
<tbody>
<tr>
<td width="95">
<p><strong>Function Type</strong></p>
</td>
<td width="241">
<p>Regular Function</p>
</td>
<td width="269">
<p>Root Function</p>
</td>
</tr>
<tr>
<td width="95">
<p><strong>Structure</strong></p>
</td>
<td width="241">
<p>The Enrichment function does not have any Input/Output parameters.</p>
</td>
<td width="269">
<p>The Root function must have at least one Input parameter and yield an array of Objects (Object[]).</p>
</td>
</tr>
<tr>
<td width="95">
<p><strong>Execution Time</strong></p>
</td>
<td width="241">
<p>Executed after populating all <a href="/articles/06_LU_tables/01_LU_tables_overview.md">LU Tables</a> in the <a hef="/articles/03_logical_units/01_LU_overview.md">Logical Unit</a>.</p>
</td>
<td width="269">
<p>Upon LU Table population.</p>
</td>
</tr>
<tr>
<td width="95">
<p><strong>Operation</strong></p>
</td>
<td width="241">
<p>Performs insert, update, or delete of an LU Table's data after it has already been populated from a source object.</p>
</td>
<td width="269">
<p>Populates the LU Table.</p>
</td>
</tr>
<tr>
<td width="95">
<p><strong>Number of Objects</strong></p>
</td>
<td width="241">
<p>Multiple Enrichment functions can be attached to an LU Table. One Enrichment function can be attached to multiple LU Tables.</p>
</td>
<td width="269">
<p>Only one Root function per one Table Population object.</p>
</td>
</tr>
<tr>
<td width="95">
<p><strong>Execution Order</strong></p>
</td>
<td width="241">
<p>Enrichment execution order is defined at the LU Schema level.</p>
</td>
<td width="269">
<p>Population execution order is defined at the population level.</p>
</td>
</tr>
<tr>
<td width="95">
<p><strong>Access to LU Tables</strong></p>
</td>
<td width="241">
<p>Can extract data from any LU Table within the Logical Unit since it is executed after the population of all LU Tables.</p>
</td>
<td width="269">
<p>Can access other LU Tables if their population execution order is smaller than the execution order of the current population.</p>
</td>
</tr>
<tr>
<td width="95">
<p><strong>Number of Executions</strong></p>
</td>
<td width="241">
<p>The Enrichment function runs once per LU Table and LUI.&nbsp;</p>
<p>For example:</p>
<p>There are 1,500 subscribers for Customer 1. Each subscriber has multiple services.</p>
<p>The Enrichment function runs once and updates all the services of Customer 1.</p>
</td>
<td width="269">
<p class="CellBodyLeft">The number of executions of a Root function equals the number of records in the parent table.</p>
<p>For example:</p>
<p>There are 1,500 subscribers for Customer 1. Each subscriber has multiple services.</p>
<p>The Root function on the Services LU Table runs 1500 times and selects the services of each subscriber separately.</p>
</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>

[![Previous](/articles/images/Previous.png)](/articles/10_enrichment_function/01_enrichment_function_overview.md)[<img align="right" width="60" height="54" src="/articles/images/Next.png">](/articles/10_enrichment_function/03_create_edit_enrichment_function.md)
