import json
import os
from datetime import date

FILE_NAME = "expenses.json"


def load_data():
    if not os.path.exists(FILE_NAME):
        return []
    try:
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    except:
        return []


def save_data(records):
    with open(FILE_NAME, "w") as file:
        json.dump(records, file, indent=2)


def add_entry(entry_type):
    print(f"\nAdding a new {entry_type.upper()} record:")
    amount = input("Amount: ").strip()

    try:
        amount = float(amount)
    except:
        print(" Amount must be a number.")
        return

    category = input("Category (Food, Travel, etc.): ").strip() or "General"
    datestr = input("Date (YYYY-MM-DD) [Press enter for today]: ").strip()

    if not datestr:
        datestr = date.today().isoformat()

    note = input("Any note (optional): ").strip()

    record = {
        "type": entry_type,
        "amount": amount,
        "category": category,
        "date": datestr,
        "note": note
    }

    data = load_data()
    data.append(record)
    save_data(data)

    print(" Record saved successfully!")


def show_all():
    data = load_data()

    if not data:
        print("\nNo records found yet.")
        return

    print("\n--- All Records ---")
    for i, r in enumerate(data, start=1):
        print(f"{i}. {r['date']} | {r['type']} | ₹{r['amount']} | {r['category']} | {r['note']}")


def monthly_summary():
    month = input("Enter month (YYYY-MM): ").strip()

    if not month:
        print(" Please enter a valid month.")
        return

    data = load_data()
    total_income = 0
    total_expense = 0

    for r in data:
        if r["date"].startswith(month):
            if r["type"] == "income":
                total_income += r["amount"]
            else:
                total_expense += r["amount"]

    print("\n--- Monthly Summary ---")
    print(f"Month: {month}")
    print(f"Total Income : ₹{total_income}")
    print(f"Total Expense: ₹{total_expense}")
    print(f"Net Balance : ₹{total_income - total_expense}")

def menu():
    while True:
        print("\n==============================")
        print("     SIMPLE EXPENSE TRACKER")
        print("==============================")
        print("1) Add Expense")
        print("2) Add Income")
        print("3) View All Records")
        print("4) Monthly Summary")
        print("0) Exit")

        choice = input("Choose an option: ").strip()

        if choice == "1":
            add_entry("expense")
        elif choice == "2":
            add_entry("income")
        elif choice == "3":
            show_all()
        elif choice == "4":
            monthly_summary()
        elif choice == "0":
            print("Goodbye")
            break
        else:
            print(" Invalid choice. Try again")


if __name__ == "__main__":
    menu()
