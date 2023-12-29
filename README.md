def setup_donation_system():
    charities = []
    for i in range(3):
        charity_name = input(f"Enter name of charity {i+1}: ")
        charities.append(charity_name)
    return charities

def record_and_total_donation(charities, charity_totals):
    while True:
        try:
            print("\nCharities:")
            for i, charity in enumerate(charities):
                print(f"{i+1}. {charity}")
            charity_choice = int(input("Enter charity choice (1-3, or -1 to show totals): "))
            if charity_choice == -1:
                break
            if 1 <= charity_choice <= 3:
                shopping_bill = float(input("Enter value of customer's shopping bill: "))
                donation = shopping_bill * 0.01
                charity_totals[charity_choice - 1] += donation
                print(f"Donation of ${donation:.2f} made to {charities[charity_choice - 1]}")
            else:
                print("Invalid charity choice. Please enter 1, 2, 3, or -1.")
        except ValueError:
            print("Invalid input. Please enter numbers only.")

def show_totals(charities, charity_totals):
    sorted_totals = sorted(zip(charities, charity_totals), key=lambda x: x[1], reverse=True)
    grand_total = sum(charity_totals)
    print("\nTotal donations so far:")
    for charity, total in sorted_totals:
        print(f"{charity}: ${total:.2f}")
    print(f"\nGRAND TOTAL DONATED TO CHARITY: ${grand_total:.2f}")

charities = setup_donation_system()
charity_totals = [0, 0, 0]  # Initialize totals for each charity
record_and_total_donation(charities, charity_totals)
show_totals(charities, charity_totals)
