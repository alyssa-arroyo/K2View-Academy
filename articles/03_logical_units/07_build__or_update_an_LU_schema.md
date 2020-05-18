# Using Auto Discovery to Build or Update an LU Schema

The Fabric Studio [**Auto Discovery Wizard**](https://github.com/k2view-academy/K2View-Academy/wiki/Auto-Discovery-Wizard) enables you to automatically generate or edit an LU DB Schema based on predefined database constraints. 

### How Do I Define a New Logical Unit (LU) Using the Auto Discovery Wizard? 

1. Go to the **Project Tree**, right click **Logical Units** and then click **New Logical Unit** to display the **Logical Unit** dialog box. 
2. Complete the **Name** field.
3. By default the **Open LU Auto Discovery** option is checked whereby the [**Auto Discovery Wizard**](https://github.com/k2view-academy/K2View-Academy/wiki/Auto-Discovery-Wizard) automatically opens. To manually create an **LU**, uncheck **Open LU Auto Discovery**.  
4. Click **OK**. 

### How Do I Add the Auto Discovery Functionality to an Existing Schema?
Auto Discovery allows you to append or override existing LU and can be useful when there is a need to add additional tables to an existing Schema from a different interface. 

To use the [**Auto Discovery Wizard**](https://github.com/k2view-academy/K2View-Academy/wiki/Auto-Discovery-Wizard) to add tables to an LU schema, do either:

**Option 1**
1. Go to the **Project Tree**, right click the **LU Name** and the click **Auto Discovery Wizard**.
2. Run the **Auto Discovery Wizard**.
3. When the **Studio** asks you if you want to **override the LU schema**, do the following: \
  a. Click **YES** to override the existing schema and create a new one based on Auto Discovery.\
  b. Click **NO** to add the tables to the existing schema.

**Option 2**
1. Open the **LU Schema** and right click a **column** in an LU  **table**.
2. Select **Auto Discovery Wizard**.

![image](https://k2vacademy.s3.amazonaws.com/Fabric/1_LU_Schema_and_Overview/1.7_Auto_Discovery_Build_or_Update_Schema/1.7_pic_1.png)

3. Run the [**Auto Discovery Wizard**](https://github.com/k2view-academy/K2View-Academy/wiki/Auto-Discovery-Wizard). A new [**Grouped SubGraph**](https://github.com/k2view-academy/K2View-Academy/wiki/LU-Schema---Group-and-Ungroup-Tables) of tables is added to the selected column.

![image](https://k2vacademy.s3.amazonaws.com/Fabric/1_LU_Schema_and_Overview/1.7_Auto_Discovery_Build_or_Update_Schema/1.7_pic_2.png)