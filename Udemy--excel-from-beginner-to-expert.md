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

