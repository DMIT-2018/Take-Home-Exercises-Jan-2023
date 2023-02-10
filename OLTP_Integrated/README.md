# OLTP Planning Document Exercise ![Weight](https://img.shields.io/badge/Weight-5%25-blue)

## Marking Rubric ![Marks](https://img.shields.io/badge/Total%20Marks-15-blueviolet)

| Earned  | Marks | Section                           |
| :-----: | :---: | --------------------------------- |
|   |   2   | Planning Milestone and Issue with Task comment   |
|   |   1   | Document Components as requested    |
|   |   3   | Query Data Model(s)   |
|   |   3   | Command Data Model(s)    |
|   |   3   | Query Service Method(s)    |
|   |   3   | Command Service Method   |
|   |  -4   | Penalties Max -4 (e.g.: milestone and or issue missing, insufficient commits, non-informative commit messages)* |
|   |  15   | **Total** |


### Marking Rubric

| Weight | Breakdown |
| ----   | --------- |
| **1** | 1 = Proficient (requirement is met)<br />0 = Incomplete (requirement poorly/not met, major errors, missing large portions) |
| **2** | 2 = Proficient (requirement is met)<br />1 = Limited (requirement is satisfactorily met, several errors)<br />0 = Incomplete (requirement poorly/not met, major errors, missing large portions) |
| **2** | 3 = Proficient (requirement is met, no recommendations)<br />2 = Satisfactory (requirement met, minor/missing errors/details )<br />1 = Limited (requirement is satisfactorily met, major/missing errors/details)<br />0 = Incomplete (requirement poorly/not met, major errors, missing large portions) |

----

[Back to Exercises](../README.md)

> Private Classroom GitHub Repo Only

Given the following user-interface, document your implementation plan for the **complete functionality** of this form. Follow the guidance and examples given by your instructor for your implementation plan. The form is designed to collect the picking information of an order after the picker has collected the items. The form will display the original order. The picker would have taken a copy of the original order, went through the store collecting the items on the order. Record the picked quantities on the order. Finally, returned the sheet to the office for entry by the clerk. The entire form will be processed as a single transaction in the BLL.

![Order Picking Sheet](./OrderPickingSheet.png)

## Processes

- Fetch: order number and picker id
  - returns Picker name, Customer information (3), order details (2)

- Clear
  - clears form

- Save
  - collects data from the form and submits for processing
    - order number, picker id, table data
 

## Requirements:

Create a OLTP Planning Document containing:

- Milestone
- Issue
  - Issue task list comment
  - Data Model comment
    - Query Model(s)
    - Command Model(s)
  - Query Service Method comment
  - Business Transaction Method comment


Note the following requirements when processing in the BLL:

- order number and picker id are required
- each order detail must have data
- picked quantity has zero-positve value
- picked quantity not the same as ordered quantity must have a comment
- update existing order details

  ## Grocery Picking ERD

  ![Order Picking RTD](./GroceryERD.png)
