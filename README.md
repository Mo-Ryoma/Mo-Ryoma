import os

class ExpenseTracker:
    def __init__(self, filename="expenses.txt"):
        self.filename = filename
        if not os.path.exists(self.filename):
            with open(self.filename, "w") as file:
                file.write("Date,Description,Amount\n")
    
    def add_expense(self, date, description, amount):
        with open(self.filename, "a") as file:
            file.write(f"{date},{description},{amount}\n")
        print(f"Expense added: {description} - ${amount}")
    
    def view_expenses(self):
        with open(self.filename, "r") as file:
            lines = file.readlines()[1:]  # Skip header
            if lines:
                print("\nExpenses:")
                total = 0
                for line in lines:
                    date, description, amount = line.strip().split(",")
                    print(f"Date: {date}, Description: {description}, Amount: ${amount}")
                    total += float(amount)
                print(f"\nTotal Expenses: ${total}")
            else:
                print("No expenses recorded yet.")
    
    def delete_expense(self):
        if os.path.exists(self.filename):
            os.remove(self.filename)
            print("All expenses deleted!")
        else:
            print("No expenses to delete.")

if __name__ == "__main__":
    tracker = ExpenseTracker()
    
    while True:
        print("\n1. Add Expense")
        print("\n2. View Expenses")
        print("\n3. Delete All Expenses")
        print("\n4. Exit")

        choice = input("\nEnter your choice: ")

        if choice == "1":
            date = input("Enter date (YYYY-MM-DD): ")
            description = input("Enter description: ")
            amount = input("Enter amount: ")
            tracker.add_expense(date, description, amount)
        elif choice == "2":
            tracker.view_expenses()
        elif choice == "3":
            tracker.delete_expense()
        elif choice == "4":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")
