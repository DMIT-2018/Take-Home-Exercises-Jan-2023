# 32.  Group By (Method Syntax)

  ##### Database
  * Westwind</br>
  ##### Setup
  * Use "C# Statement" and/or "C# Program"</br></br>
  
<details>
<summary>Group By (Part 1)</summary>

**Given a list of Product, return the following information.**

* Product Name (shown as ProductName)
* Orders Detail (shown as Details)
  * Order ID
  * Customer Name (shown as Customer)
  * Order Date
  * Quantity Sold (shown as Sold)
  
* **Order Product Name and Quantity Descending**  
* **We only want to see the following:**
  * **Products that have been sold in 2018**
  * **Only those Products that have been sold 40 or more**

<details>
<summary>Solution</summary>

  ```cs
Products
	.GroupBy(p => new { p.ProductID, p.ProductName })
	//  using pg to indicate that we are now reference the group by collection and not the product collection
	.OrderBy(pg => pg.Key.ProductName)
	.Select(pg => new
	{
		ProductName = pg.Key.ProductName,
		Details = OrderDetails
				.Where(od => od.ProductID == pg.Key.ProductID 
						&& od.Order.OrderDate.Value.Year == 2018
						&& od.Quantity >= 40)
				.OrderByDescending(od => od.Quantity)
				.Select(od => new {
				OrderID = od.OrderID,
				Customer = od.Order.Customer.CompanyName,
				OrderDate = od.Order.OrderDate,
				Sold = od.Quantity
				})
	}).Dump();
 ```
</details>

### Output
![](Images/32%20-%20GroupBy%201.png)
</details>

--- 
<details>
<summary>Group By (Part 2)</summary>

**Given a list of Categories, return the following information.**

* Category Name (shown as CategoryName)
* Product Detail (shown as Details)
  * Product Name (shown as ProductName)
  * Total Quantity Sold (shown as TotalSold)
  
* **Order Category Name and Product Name**  
* **NOTE:  When getting the Total Quantity Sold, you will have to cast the Quantity as nullable.  IE:  (int?)x.Quantity**

<details>
<summary>Solution</summary>

  ```cs
Categories
	.GroupBy(c => new { c.CategoryID, c.CategoryName})
	//  using cg to indicate that we are now reference the "group by" collection and not the Categories collection
	.OrderBy(cg => cg.Key.CategoryName)
	.Select(cg => new
	{
		CategoryName = cg.Key.CategoryName,
		Details = Products
					.Where(p => p.CategoryID == cg.Key.CategoryID)
					.OrderBy(p => p.ProductName)
					.Select(p => new 
					{
					ProductName = p.ProductName,
					TotalSold = p.OrderDetails.Sum(x => (int?)x.Quantity)
					})
	})
	.Dump();
 ```
</details>

### Output
![](Images/32%20-%20GroupBy%202.png)
</details>

--- 
</br>

[Readme.md](./Readme.md)


DMIT 2018 Take Homework<br><br>
© 2023 Northern Alberta Institute of Technology <br>
All Rights Reserved


