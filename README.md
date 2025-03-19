import java.util.*;
class Product
{
	int id;
	String name;
	double price;
	int quantity;
	
	void setDetails(int prodID, String prodName, double prodPrice, int prodQuantity)
	{
		id=prodID;
		name=prodName;
		price=prodPrice;
		quantity=prodQuantity;
	}
	void displayDetails()
	{
		System.out.println("ID : "+id+" , Name : "+name+" , Price : "+price+" , Quantity : "+quantity);
	}
	int getId()
	{
		return id;
	}
	String getName()
	{
		return name;
	}
	double getPrice()
	{
		return price;
	}
	int getQuantity()
	{
		return quantity;
	}
	void setQuantity(int newQuantity)
	{
		quantity=newQuantity;
	}
}
class Store
{
	Product[] products;
	int count;
	Store(int size)
	{
		products=new Product[size];
		count=0;
	}
	
	void addProduct(Product p)
	{
		if(count<products.length)
		{
			products[count]=p;
			count++;
			System.out.println("Product added successfully !");
		}
		else
		{
			System.out.println("Inventory is full!");
		}
	}
	
	void searchProduct(int searchId)
	{
		for(int i=0;i<count;i++)
		{
			if(products[i].getId()== searchId)
			{
				System.out.println("Product found :");
				products[i].displayDetails();
				return;
			}
		}
		System.out.println("product not found.");
	}
	void updateQuantity(int productId, int newQuantity)
	{
		for(int i=0;i<count;i++)
		{
			if(products[i].getId()==productId)
			{
				products[i].setQuantity(newQuantity);
				System.out.println("Quantity updated successfully. ");
				return;
			}
		}
		System.out.println("Product not found. ");
	}
	void calculateTotalValue()
	{
		double totalValue=0;
		for(int i=0;i<count;i++)
		{
			totalValue+=products[i].getPrice()*products[i].getQuantity();
		}
		System.out.println("Total inventory value : "+totalValue);
	}
	void findCostliestProduct()
	{
		if(count==0)
		{
			System.out.println("No products in inventory. ");
			return;
		}
		Product costliest=products[0];
		for(int i=1;i<count;i++)
		{
			if(products[i].getPrice()>costliest.getPrice())
			{
				costliest=products[i];
			}
		}
		System.out.println("Costliest product :");
		costliest.displayDetails();
	}
		void displayProducts(int n)
		{
			for(int i=0;i<n;i++)
			{
			System.out.println("product ID : "+products[i].id);
			System.out.println("product Name : "+products[i].name);
			System.out.println("product price : "+products[i].price);
			System.out.println("product quantity : "+products[i].quantity);			
			}
		}
}
class Customer
{
	long number;
	String name;
	
	void setCustomerDetails(long number, String name)
	{
		this.number=number;
		this.name=name;
	}
	void displayCustomerDetails()
	{
		System.out.println("number : "+number+" , Name : "+name);
	}
	long getnumber()
	{
		return number;
	}
	
	Customer[] Customers;
	int count;
	Customer()
	{}
	Customer(int size)
	{
		Customers=new Customer[size];
		count=0;
	}
	void addCustomer(Customer p)
	{
		if(count<Customers.length)
		{
			Customers[count]=p;
			count++;
			System.out.println("Customer added successfully !");
		}

	}
	void searchCustomer(String searchName)
	{
		for(int i=0;i<count;i++)
		{
			if((this.name).equals(searchName))
			{
				System.out.println("Customer found :");
				Customers[i].displayCustomerDetails();
				return;
			}
		}
		System.out.println("Customer not found.");
	}
	
}
class Main
{
	public static void main(String args[])
	{
		System.out.println("*************************************");
		System.out.println("Welcome to store  management system");
		System.out.println("*************************************");
		Scanner sc=new Scanner(System.in);
		System.out.println("Enter a maximum number of product in the store :");
		int n=sc.nextInt();
		System.out.println("Enter  number of Customer :");
		int nu=sc.nextInt();
		Customer customer=new Customer(nu);
		Store store=new Store(n);
		boolean a=true;
		while(a)
		{
			System.out.println("1. Add Product");
			System.out.println("2. Display all product");
			System.out.println("3. Search Product by Name");
			System.out.println("4. Update Product Quantity");
			System.out.println("5. Display Total Inventory Value");
			System.out.println("6. Find Costliest Product");
			System.out.println("7. Add Customer");
			System.out.println("8. Exit");
			System.out.print("Enter your choice : ");
			int choice=sc.nextInt();
			switch(choice)
			{
				case 1:
				for(int i=1;i<=n;i++)
				{
					Product product=new Product();
					System.out.println("Enter product ID for Product"+i);
					int id=sc.nextInt();
					sc.nextLine();
					System.out.println("Enter product name for Product"+i);
					String name=sc.nextLine();
					name.toLowerCase();
					System.out.println("Enter product price for Product"+i);
					double price=sc.nextDouble();
					System.out.println("Enter product quantity for product "+i);
					int quantity=sc.nextInt();
					product.setDetails(id,name,price,quantity);
					store.addProduct(product); 					
				}
				break;
				
				case 2:
					for(int i=1;i<=n;i++)
					{
						store.displayProducts(n);
					}
				break;
				
				case 3:
					sc.nextLine();
					System.out.println("Enter product ID to search : ");
					int searchproId=sc.nextInt();
					store.searchProduct(searchproId);
					break;
				
				case 4:
					System.out.println("Enter product ID to update : ");
					int productId=sc.nextInt();
					System.out.println("Enter new Quantity");
					int newQuantity=sc.nextInt();
					store.updateQuantity(productId, newQuantity);
					break;
					
				case 5:
					store.calculateTotalValue();
					break;
				
				case 6:
				store.findCostliestProduct();
				break;
				
				case 7:
				for(int i=1;i<=nu;i++)
				{
					Customer cu=new Customer();
					System.out.println("Enter Customer number for Customer"+i);
					long number=sc.nextLong();
					sc.nextLine();
					System.out.println("Enter Customer name for Customer"+i);
					String name=sc.nextLine();
					name.toLowerCase();
					customer.setCustomerDetails(number,name);
					customer.addCustomer(cu);
				}
					break;
				
				case 8:
					System.out.println("Thanks for coming please visit again");
					a=false;
					break;
				
				default:
				System.out.println("Invalid choice, Please enter number between 1 to 8");
				
			} 
		}
	}
}
