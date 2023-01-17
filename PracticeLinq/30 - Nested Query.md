# 30 - Nested Query (Method Syntax)

  ##### Database
  * Westwind</br>
  ##### Setup
  * Use C# Program</br></br>

<details>
<summary>Anonymous Types Nested Query</summary>

**Given a list of Categories, return the following information.**

* Category Name (shown as Name) 
* Description
* Items (*NOTE:  We are using **Items** so not to cause confusion by calling it **Products***)
  * Product Name (shown as Name)
  * Unit Price (shown as Price)
* **Order by Category Name, Product Name**  
  
<details>
<summary>Solution</summary>

  ```cs
void Main()
{
	Categories
		.OrderBy(c => c.CategoryName)
		.Select(c => new 
		{
			Name = c.CategoryName,
			Description = c.Description,
			Products = Products
						.Where(p => p.CategoryID == c.CategoryID)
						.OrderBy(p => p.ProductName)
						.Select(p => new
						{
							Name = p.ProductName,
							Price = p.UnitPrice
						}
						).ToList()
		}).Dump();

}
 ```
</details>

### Output
![](Images/30%20-%20Nested%20Query%20-%20Anonymous%20Types%201.png)
</details>

---    
<details>
<summary>Anonymous Types Nested Query (Part 2)</summary>

**Given a list of Suppliers, return the following information.**

* Supplier Name (shown as Name) 
* Contact Name
* City
* Items (*NOTE:  We are using **Items** so not to cause confusion by calling it **Products***)
  * Product Name (shown as Name)
  * Unit Price (shown as Price)
* **Order by Category Name, Product Price from largest to smallest**  
* **We only want to see those products that have a value less than $10.00**
  
<details>
<summary>Solution</summary>

  ```cs
void Main()
{
	Suppliers		
		.OrderBy(s => s.CompanyName)
		.Select(s => new
		{
			Name = s.CompanyName,
			ContactName = s.ContactName,
			City = s.Address.City,
			Items = Products
				.Where(p => p.UnitPrice < 10)
				.OrderByDescending(p => p.UnitPrice)
				.Select(p => new
				{
					Name = p.ProductName,
					Price = p.UnitPrice
				})
	
		}).Dump();
}
 ```
</details>

### Output
![](Images/30%20-%20Nested%20Query%20-%20Anonymous%20Types%202.png)
</details>

---    
<details>
<summary>Strongly Type Nested Query</summary>

**Given a list of Categories, return the following information.**

* Category Name (shown as Name) 
* Description
* Items (*NOTE:  We are using **Items** so not to cause confusion by calling it **Products***)
  * Product Name (shown as Name)
  * Unit Price (shown as Price)
* **Order by Category Name, Product Name**  
  
**NOTE:  The strongly type name will be CategoryView & ProductView**
<details>
<summary>Solution</summary>

  ```cs
void Main()
{
	Categories
		.OrderBy(c => c.CategoryName)
		.Select(c => new CategoryView()
		{
			Name = c.CategoryName,
			Description = c.Description,
			Products = Products
						.Where(p => p.CategoryID == c.CategoryID)
						.OrderBy(p => p.ProductName)
						.Select(p => new ProductView()
						{
							Name = p.ProductName,
							Price = p.UnitPrice
						}
						).ToList()
		}).Dump();

}

public class CategoryView
{
	public string Name { get; set; }
	public string Description { get; set; }
	public List<ProductView> Products { get; set; }
}

public class ProductView
{
	public string Name { get; set; }
	public decimal Price { get; set; }
}
 ```
</details>

### Output
![](Images/30%20-%20Nested%20Query%201.png)
</details>

---
<details>
<summary>Strongly Type Nested Query (Part 2)</summary>

**Given a list of Order, return the following information.**

* OrderID
* Order Date (shown as OrderDate) *NOTE:  When creating the property in the view, the DateTime is **nullable** (Please reference by to 1517)*
* Customer Name (shown as CustomerName) 
* Contact Name (shown as ContactName)  
* Details
  * Product Name (shown as Name)
  * Quantity
  * Unit Price (shown as Price)
  * Extend Price (shown as LineTotal)
* **Order by Customer Name, Product Name**  
* **We only want to see those orders that were in May of 2018**
  
**NOTE:  The strongly type name must end in View  ie: XxxxView**
<details>
<summary>Solution</summary>

  ```cs
void Main()
{
	Orders
		.Where(o => o.OrderDate.Value.Month == 5 &&
				o.OrderDate.Value.Year == 2018)
		.OrderBy(o => o.Customer.CompanyName)
		.Select(o => new OrderView()
		{
			OrderID = o.OrderID,
			OrderDate = o.OrderDate,
			CustomerName = o.Customer.CompanyName,
			ContactName = o.Customer.ContactName,
			Details = OrderDetails
						.Where(od => od.OrderID == o.OrderID)
						.OrderBy(od => od.Product.ProductName)
						.Select(od => new OrderDetailView()
						{
							Name = od.Product.ProductName,
							Quantity = od.Quantity,
							Price = od.UnitPrice,
							LineTotal = (od.Quantity * od.UnitPrice)
						}).ToList()

		}).Dump();
}

public class OrderView
{
	public int OrderID { get; set; }
	public DateTime? OrderDate { get; set; }
	public string CustomerName { get; set; }
	public string ContactName { get; set; }
	public List<OrderDetailView> Details { get; set; }
}

public class OrderDetailView
{
	public string Name { get; set; }
	public int Quantity { get; set; }
	public decimal Price { get; set; }
	public decimal LineTotal { get; set; }
}
 ```
</details>

### Output
![](Images/30%20-%20Nested%20Query%202.png)
</details>

---  

</br>

[Readme.md](./Readme.md)


DMIT 2018 Take Homework<br><br>
© 2023 Northern Alberta Institute of Technology <br>
All Rights Reserved

