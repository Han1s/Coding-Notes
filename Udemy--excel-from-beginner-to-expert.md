# II. Microsoft Excel Fundamentals

## 6. Introduction to Excel Fundamentals

- double click (e.g. home) tab to collapse ribbon

## 7. Customizing Quick Access Toolbar

- you can customize it by the drop arrow in the left top corner



# III. Entering and Editing Text and Formulas

## 14. Working with numeric Data

- numeric data should be right aligned due to decimals

- if a number has green arrow next to it, its probably a string, not a number. Excel can convert it.

  

## 15. Entering Date Values in Excel

- right aligned
- treated as numeric values
- `dd/mm/yyyy` format
- you can create a custom format in `home/number/format/custom -> mm-yyyy`

## 17. Creating basic formulas

- calculations always start with equal sign
  - `=100+200`returns 300
  - `=B1+B2`returns the result

## 18. Relative Versus Absolute Cell Reference In Formulas

- **absolute cell references**
  - refers to the particular cells
  - `=B4+B5+B6`
  - `=E8/$E$9` - the dollar signs mark the value as absolute
- **relative cell references**
  - copying formulas changes the formulas relative to the column / row
  - it performs the same formula relative to the location

## 10. Order of operation

- in Formulas use **Formulas Auditing** -> **Evaluate Formula** to debug formulas



# IV. Working with Basic Excel Functions

- **Excel Function** is a predefined calculation
  - `=SUM(B4:B8)`
- 3 Parts of an Excel Function
  - **=**
  - **Function Name**
  - **Arguments**
- use **argument window** which is the little **fx** in the function window
- there is several hundred function



## 21. SUM()

## 22. MIN() & MAX()

## 23. AVERAGE()

## 24. COUNT()

- counts the number of numeric values

## 25. Adjacent Cells Error in Excel Calculations

- the small green corner gives tips if you click the warning
- you can accept or ignore the error

## 26. AutoSum command

- automatically sum up cells
- just select the empty cells and click
- `Alt = ` 

## 28. Using Autofill

- the little box in the right bottom corner
- just drag to spread formulas



## V. Modifying an Excel Worksheet

## 30. Inserting and Deleting Rows and Columns

- `ctr +`inserts row
- `ctrl -` deletes row
- `ctrl shift +`inserts column
- `ctrl shift - deletes column`

## 31. Changing the width and height of cells

- to automatically adjust column just double click the  column border between letters
- you can also adjust multiple columns by selecting all of them by dragging the border a bit\

## 32. Hiding and unhiding rows and columns

- hiding from printing as well
- just right click and hide



# VI. Formatting Data

## 40. Formatting Data as Currency values

- **home -> number**



## 42. Format Painter

- **home -> clipboard -> format painter**
  - 1 click - copy one cell
  - 2 clicks - copy until Esc

## 43. Creating Styles to Format Data

- similar to word
- **home -> styles**

## 44. Merging and Centering Cells

- **home -> alignment -> merge and center**
  - use carefully
  - good especially for titles

## 45. Conditional Formatting

- applies formatting based on condition
- **home -> styles -> conditional formatting**
- to edit the rule **conditional formatting -> Manage rules**



# VII. Inserting Images and Shapes

## 49. Formatting Shapes

- use **shape format** tab when selecting shape

## 50. Working with Smart Arts

- usually used in powerpoint
- in **insert -> illustrations -> smartart**
- many options are online as well



# VIII. Creating Basic Charts in Excel

`=[cell]` connects the cell to another cell and shows the same thing (maybe for titles and stuff)

- pie charts are better for a single row of data
- refer to the cheatsheet about the data in the pdf



# IX. Printing an Excel Worksheet

- if you scroll out youll see the lines dividing the print sheets
- choose scaling as well
- you can reduce margins as well
- **page layout view** in **view > page layout**
- you can edit the header and footer as well
- you can print specific cells as well or use print area



# X. Templates

- basic structure is completed for you and just fill data
- use templates from the preconfigured one
- to create a tyemplate you need to change the save type to **excep template**



# XIV. Working with an Excel list

- always format the first row as headers
- make sure there are no empty rows or columns in the list



## 71. Sorting a List Using Single Level Sort

- you can sort via **data** tab -> **sort & filter**

## 72. Sorting a list using multi-level sorts

- **data** > **sort & filter** > **Sort** > **Add level**

## 73. Using custom sorts

- for example for month names
- **data** > **sort & filter** > **Sort** > **sort by** > **custom**

## 74. Using Auto Filter tools

- click in the list and click on **data** > **filter**
  - arrows will appear in the header

## 75. Subtotals in the list

- first you need to sort the column based on what you want
- **data > outline > subtotal**

## 76. Format a list as a table

- click in the list
- **home > styles > format as table**

## 77. Conditional Formatting to Find Duplicates

- `ctrl + shift + down arrow` selects all cells in a column up until column
- highlight cells => home => conditional formatting => highlight duplicates

## 78. Removing Duplicates

- if you have table Design -> remove duplicates
- if not data -> remove duplicates



# 15. Excel List Functions

## 79. DSUM()

- we can add criteria to the **SUM()** function. E.g. where category is x.
- you need to write List header ('Category') into a cell and the filtered category ('Rent') below it, then you add those two to the criteria

## 81. DSUM() with OR criteria

- you just write another category and include it in the criteria

## 82. DSUM() with AND criteria

- you just write another category and value next to it and include it

## 83. DAVERAGE()

- you use it the same way the DSUM()

## 84. DCOUNT()

- it will only count numbers
- DCOUNTA() will count everything

## 85. SUBTOTAL()

- its similar as DSUM or DAVERAGE but if you **filter** the list it actually accounts for it compared to those



# 16. Excel Data Validation

## 87. Creating Excel Validation Sheet

= select cells and then via **data** tab - **data validation**



## 89. Adding a Custom Excel Data Validation error

- warning allows pressing fowrad with the incorrect value



## 90. Dynamic Formulas by Using Excel Data Validation Techniques

- you can also reference list as options



# XVII. Importing Data From Excel

## 92. Importing Data from Text Files

- e.g. **tab-delimited / csv** file
  - **Data >  From TEXT/CSV**
- You can also import **databases** from e.g. **Microsoft Access**
  - this is a connected document, meaning if the db gets edited excel gets updated as well after refresh



## 97. Exporting Data

- sometimes if an app does not communicate with excel directly its a good way to transfer data via csv or something
  - you can either use **file > export** or **save as...**, both of them lead to the same result



# XVIII. Pivot tables

- its a summarization of a large list into a pivot table structure

## 99. Creating a Pivot Table

- format the list as a table (click into a list **> home > format as table**)
- name the table in **table design** tab
- **insert > pivot table > new tab**

## 100. Modify Pivot Table Calculations

- take the headers and drag them in the corresponding section

## 101. Grouping PivotTable Data

- in **[pivotTableName] Analyze** you can group and ungroup fields

- the order of groups in the drag and drop fields matters

  

## 102. Formatting PivotTable Data

- **value field settings** in dragables > **number format**

## 103. Modifying PivotTable Calculations

- by default we get a **sum** for a number for example and **count** for a string
- **value field settings** in dragables > **average**
- What if we wanna see increase / decrease?
  - **value field settings** > **show values as** > **% difference from previous**

## 104. Drilling into Pivot Tables

- if you double click on a value this creates a new sheet and gives you a data that makes up that value

## 105. Creating a Pivot Chart

- **analyze > pivot chart**

## 106. Filtering PivotTable Data

- drag a field into a filter dragable

## 107. Filtering with a slicer tool

- **analyze > insert slicer**

# XIV. Excel Power Pivot

## 109. Why Power Pivot

- it connects multiple tables

## 110. Activating the PowerPivot Tool

- **file > options > addins > power pivot**

## 111. Creating model with powerpivot

- click on table **> power pivot > add to data model** for both tables
- now we have to **relate** the table sets

## 112. Model Relationship

- **home > diagram view > grab the relationship from the parent to the child**
  - you can also right click the header and **create a relationship** with a child

## 113. Create PivotTable based on Data Models

- from dataset **home > pivot table > create**

## 114. Excel Power Pivot KPIs (key performance indicators)

- KPIs are a way to add visuals to your data model
- go to a table **> manage > home > calculations > AutoSum > average > create KPI** 
  - KPI will now appear in the PivotTable options
- you can also dat icons via conditional formatting

# 20. Working with large Sets of Data in Excel

## 115. Using the Freeze Panes Tool

- **View > window > Freeze Panes** works for everything above selected

## 116. Grouping Data (Columns and Rows)

- **select column > data > outline > group**

## 117. Printing Large Sets of Data

- if it overreaches the height:	
  - **page layout > page setup > print titles > sheet > rows to repeat at top**
- if the width overreaches:
  - **page layout > page setup > print titles > sheet > page order > over, then down**

## 118. Linking Worksheets (3D Formulas)

- to reference other sheets (years represent sheet names)
  - 2013'!B4+'2014'!B4+'2015'!B4

## 119. Consolidating Data from multiple Worksheets

- **Data > Data Tools > Consolidate**
