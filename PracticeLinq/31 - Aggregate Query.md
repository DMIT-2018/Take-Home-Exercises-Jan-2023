# 31.  Queries Using Aggregate (Method Syntax)

  ##### Database
  * Westwind</br>
  ##### Setup
  * Use "C# Statement" and/or "C# Program"</br></br>
  <details>
<summary>Simple Aggregates Caught All</summary>

**Given a list of Products, return a single result.**

* Count
* Min Price 
* Max Price
* Average Price
* Total Price (This is assuming that someone bought one of each thing.)
* **We only want to see those products that have are not discontinued**

<details>
<summary>Solution</summary>

  ```cs
Products
	.Select(x => new
	{
		Count = Products
					.Where(x => x.Discontinued == false)
					.Count(),
		MinPrice = Products
					.Where(x => x.Discontinued == false)
					.Min(x => x.UnitPrice),
		MaxPrice = Products
					.Where(x => x.Discontinued == false)
					.Select(x => x.UnitPrice).Max(),
		AveragePrice = Products
					.Where(x => x.Discontinued == false)
					.Average(x => x.UnitPrice),
		TotalPrice = Products
					.Where(x => x.Discontinued == false)
					.Select(x => x.UnitPrice).Sum()
	}
)
.FirstOrDefault()
.Dump();
 ```
 </details>

### Output
 ![](Images/31%20-%20Simple%20Aggregate%201.png)
</details>

---  
<details>
<summary>Count</summary>

**Given a list of Suppliers, return the following information.**

* Supplier Name (shown as Name) 
* Number of Products they supply (shown as ProductCount)

* **Order by Number of Products from largest to smallest, Name**  

  
<details>
<summary>Solution</summary>

  ```cs
Suppliers
.Select(s => new
{
	Name = s.CompanyName,
	ProductCount = Products
				.Where(p => p.SupplierID == s.SupplierID)
				.Count()
}).OrderByDescending(x => x.ProductCount)
.ThenBy(x => x.Name)
.Dump();
 ```
</details>

### Output
![](Images/31%20-%20Count.png)
</details>

--- 
<details>
<summary>Sum - Strongly Type</summary>

**Given a list of Suppliers, return the following information.**

* Supplier Name (shown as Name) 
* History
  * Products sold by the supplier (shown as name)
  * Total quantity sold to customer.  They will used this information to figure out which is the best selling items (shown as QuantitySold)

* **Order by Suppliers then Quantity of items sold from largest to smallest, Name**  

  
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
		History = Products
					.Where(p => p.SupplierID == s.SupplierID)
					.Select(p => new HistoryView()
					{
						Name = p.ProductName,
						QuantitySold = OrderDetails
						.Where(od => od.ProductID == p.ProductID)
						.Sum(od => od.Quantity)

					}).OrderByDescending(x => x.QuantitySold)
	})
	.Dump();
}

public class HistoryView
{
	public string Name { get; set; }
	public int? QuantitySold { get; set; }
}
 ```
</details>

### Output
![](Images/31%20-%20Sum%20Strongly%20Type.png)
</details>

---  
</br>

[Readme.md](./Readme.md)


DMIT 2018 Take Homework<br><br>
© 2023 Northern Alberta Institute of Technology <br>
All Rights Reserved


