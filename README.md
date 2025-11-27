import datetime

#  Data structures
inventory = {}  # {item_id: {"name": str, "price": float, "stock": int}}
sales = []    # List of sales records

def add_item():
    item_id = input("Enter item ID: ")
    name = input("Enter item name: ")
    price = float(input("Enter item price: "))
    stock = int(input("Enter stock quantity: "))
    inventory[item_id] = {"name": name, "price": price, "stock": stock}
    print("Item added successfully!")

def view_inventory():
    print("\nCurrent Inventory:")
    for item_id, details in inventory.items():
        print(f"ID: {item_id}, Name: {details['name']}, Price: {details['price']}, Stock: {details['stock']}")
    print()

def update_item():
    item_id = input("Enter item ID to update: ")
    if item_id in inventory:
        name = input("Enter new name (leave blank to keep current): ")
        price_input = input("Enter new price (leave blank to keep current): ")
        stock_input = input("Enter new stock (leave blank to keep current): ")

        if name:
            inventory[item_id]["name"] = name
        if price_input:
            inventory[item_id]["price"] = float(price_input)
        if stock_input:
            inventory[item_id]["stock"] = int(stock_input)

        print("Item updated successfully!")
    else:
        print("Item not found!")

def record_sale():
    item_id = input("Enter item ID to sell: ")
    if item_id in inventory:
        quantity = int(input("Enter quantity to sell: "))
        if inventory[item_id]["stock"] >= quantity:
            inventory[item_id]["stock"] -= quantity
            sale_record = {
                "item_id": item_id,
                "name": inventory[item_id]["name"],
                "quantity": quantity,
                "total_price": inventory[item_id]["price"] * quantity,
                "date": datetime.datetime.now()
            }
            sales.append(sale_record)
            print("Sale recorded successfully!")
        else:
            print("Insufficient stock!")
    else:
        print("Item not found!")

def view_sales():
    print("\nSales Records:")
    total_revenue = 0
    for sale in sales:
        print(f"Item: {sale['name']}, Quantity: {sale['quantity']}, Total: {sale['total_price']}, Date: {sale['date']}")
        total_revenue += sale['total_price']
    print(f"Total Revenue: {total_revenue}\n")

def main():
    while True:
        print("Inventory and Sales System")
        print("1. Add Item")
        print("2. View Inventory")
        print("3. Update Item")
        print("4. Record Sale")
        print("5. View Sales")
        print("6. Exit")
        choice = input("Select an option (1-6): ")

        if choice == '1':
            add_item()
        elif choice == '2':
            view_inventory()
        elif choice == '3':
            update_item()
        elif choice == '4':
            record_sale()
        elif choice == '5':
            view_sales()
        elif choice == '6':
            print("Exiting system.")
            break
        else:
            print("Invalid choice! Please try again.")

if __name__ == "__main__":
    main()

