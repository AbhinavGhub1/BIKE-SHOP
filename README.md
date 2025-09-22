# BIKE-SHOP
Show room for selling a Second hand bikes for low prices including Discount according to TAX and Roadprice
cart = []
bike_menu = {
    "RXZ"     : 100000, 
    "RX100"   : 80000, 
    "KARISHMA": 50000, 
    "SHOGUN"  : 45000, 
    "SAMURAI" : 40000, 
    "RD350"   : 500000, 
    "GT650"   : 450000, 
    "SPLENDOR": 30000, 
    "SHAOLIN" : 35000
}

total_price = 0

# Ask user for name
customer_name = input("Enter your name: ").strip()

print(f"\n-------- BIKE SHOP MENU --------")

for bike, price in bike_menu.items():
    print(f"{bike}: {price}")
print("-------------------------------")

while True:
    order = input("\nEnter a bike name from the menu (or type 'done' to finish): ").strip()

    if order.lower() == "done":
        break

    if order not in bike_menu:
        print(" Sorry, that bike is not on the menu.")
        continue

    try:
        quantity = int(input("Enter the quantity: "))
        if quantity <= 0:
            print(" Quantity should be greater than 0.")
            continue
    except ValueError:
        print(" Please enter a valid number for quantity.")
        continue

    single_price = bike_menu[order]
    item_total = single_price * quantity
    cart.append(f"{order}*{quantity}: {single_price}*{quantity} = ₹{item_total}")
    total_price += item_total

# Apply discount
bill = {"totalprice": total_price, "total": 0, "discount": 0}

if total_price > 100000:
    discount = total_price * 0.20
else:
    discount = total_price * 0.10

final_total = total_price - discount
bill["discount"] = discount
bill["total"] = final_total

# Display bill
print("\n------ Cart Summary ------")
if cart:
    for item in cart:
        print(item)
else:
    print("Your cart is empty.")

print(f"\nTotal Price before discount: ₹{total_price}")
print(f"Discount applied: ₹{discount}")
print(f"Final Total after discount: ₹{final_total}")




# Save bill to a file
BILLS = f"{customer_name}_bill.txt"

with open(BILLS, "w", encoding="utf-8") as file:
    file.write(f"-------- Bill for {customer_name} --------\n")
    for item in cart:
        file.write(item + "\n")
    file.write(f"\nTotal Price before discount: ₹{total_price}\n")
    
    file.write(f"Discount applied: ₹{discount}\n")
    
    file.write(f"Final Total after discount: ₹{final_total}\n")

print(f"\n Bill saved to '{BILLS}' successfully!")



# import os  # Already at the top

# # Create 'bills' folder if it doesn't exist
# folder_name = "bills"
# os.makedirs(folder_name, exist_ok=True)

# # Build file path with folder
# filename = os.path.join(folder_name, f"{customer_name}_bill.txt")

# with open(filename, "w", encoding="utf-8") as file:
#     file.write(f"--- Bill for {customer_name} ---\n")
#     for item in cart:
#         file.write(item + "\n")
#     file.write(f"\nTotal Price before discount: ₹{total_price}\n")
#     file.write(f"Discount applied: ₹{discount}\n")
#     file.write(f"Final Total after discount: ₹{final_total}\n")

# print(f"\n✅ Bill saved to '{filename}' successfully!")
