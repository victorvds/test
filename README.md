# Weekly Budget Helper
# CS 100 Final Project

def get_budget():
    """
    Ask the user for a weekly budget and make sure
    the amount entered is a positive number.
    """
    while True:
        try:
            budget = float(input("Enter your weekly budget: $"))

            if budget <= 0:
                print("Error: Budget must be greater than 0.")
            else:
                return budget

        except ValueError:
            print("Error: Please enter a valid number.")


def add_expense():
    """
    Let the user enter expense categories and amounts.
    Each expense is stored in a list.
    """
    expenses = []

    while True:
        category = input("Enter expense category: ")

        while True:
            try:
                amount = float(input("Enter expense amount: $"))

                if amount < 0:
                    print("Error: Expense cannot be negative.")
                else:
                    break

            except ValueError:
                print("Error: Please enter a valid number.")

        expenses.append([category, amount])

        another = input("Would you like to add another expense? (yes/no): ").lower()

        if another != "yes":
            break

    return expenses


def calculate_total_spending(expenses):
    """
    Add all expense amounts together and return the total.
    """
    total = 0

    for expense in expenses:
        total += expense[1]

    return total


def calculate_remaining_budget(budget, total_spending):
    """
    Calculate the remaining budget after expenses.
    """
    return budget - total_spending


def summarize_categories(expenses):
    """
    Organize spending by category and total each category.
    """
    categories = {}

    for expense in expenses:
        category = expense[0]
        amount = expense[1]

        if category in categories:
            categories[category] += amount
        else:
            categories[category] = amount

    return categories


def display_results(budget, expenses):
    """
    Display the final budget summary and category totals.
    """
    total_spending = calculate_total_spending(expenses)
    remaining_budget = calculate_remaining_budget(budget, total_spending)
    categories = summarize_categories(expenses)

    print("\n========== WEEKLY BUDGET SUMMARY ==========")
    print(f"Weekly Budget: ${budget:.2f}")
    print(f"Total Spending: ${total_spending:.2f}")
    print(f"Remaining Budget: ${remaining_budget:.2f}")

    if total_spending > budget:
        print("You are over budget.")
    else:
        print("You are within budget.")

    print("\nSpending by Category:")

    if len(categories) == 0:
        print("No expenses entered.")
    else:
        for category, amount in categories.items():
            print(f"{category}: ${amount:.2f}")


def main():
    """
    Run the Weekly Budget Helper program.
    """
    print("Welcome to the Weekly Budget Helper!")

    budget = get_budget()
    expenses = add_expense()

    display_results(budget, expenses)


main()
