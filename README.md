# coffee-machine-oop
Coffee Machine OOP
This project simulates a coffee machine using Object-Oriented Programming (OOP) principles. The machine can serve different types of coffee, process payments, and provide reports on its resources and earnings.

Project Structure
Coffee_Machine_OOP.py: Main file that runs the coffee machine.
menu.py: Contains classes for MenuItem and Menu.
coffee_maker.py: Contains the CoffeeMaker class.
money_machine.py: Contains the MoneyMachine class.
Classes and Their Responsibilities
Coffee_Machine_OOP.py
This is the main entry point for the coffee machine simulation. It initializes instances of MoneyMachine, CoffeeMaker, and Menu, and contains the main loop to interact with the user.

CoffeeMaker
coffee_maker.py


class CoffeeMaker:
    """Models the machine that makes the coffee"""
    def __init__(self):
        self.resources = {
            "water": 300,
            "milk": 200,
            "coffee": 100,
        }

    def report(self):
        """Prints a report of all resources."""
        print(f"Water: {self.resources['water']}ml")
        print(f"Milk: {self.resources['milk']}ml")
        print(f"Coffee: {self.resources['coffee']}g")

    def is_resource_sufficient(self, drink):
        """Returns True when order can be made, False if ingredients are insufficient."""
        can_make = True
        for item in drink.ingredients:
            if drink.ingredients[item] > self.resources[item]:
                print(f"Sorry there is not enough {item}.")
                can_make = False
        return can_make

    def make_coffee(self, order):
        """Deducts the required ingredients from the resources."""
        for item in order.ingredients:
            self.resources[item] -= order.ingredients[item]
        print(f"Here is your {order.name} ☕️. Enjoy!")
MenuItem and Menu
menu.py


class MenuItem:
    """Models each Menu Item."""
    def __init__(self, name, water, milk, coffee, cost):
        self.name = name
        self.cost = cost
        self.ingredients = {
            "water": water,
            "milk": milk,
            "coffee": coffee
        }


class Menu:
    """Models the Menu with drinks."""
    def __init__(self):
        self.menu = [
            MenuItem(name="latte", water=200, milk=150, coffee=24, cost=2.5),
            MenuItem(name="espresso", water=50, milk=0, coffee=18, cost=1.5),
            MenuItem(name="cappuccino", water=250, milk=50, coffee=24, cost=3),
                     ]

    def get_items(self):
        """Returns all the names of the available menu items"""
        options = ""
        for item in self.menu:
            options += f"{item.name}/"
        return options

    def find_drink(self, order_name):
        """Searches the menu for a particular drink by name. Returns that item if it exists, otherwise returns None"""
        for item in self.menu:
            if item.name == order_name:
                return item
        print("Sorry that item is not available.")
MoneyMachine
money_machine.py


class MoneyMachine:
    CURRENCY = "$"

    COIN_VALUES = {
        "quarters": 0.25,
        "dimes": 0.10,
        "nickles": 0.05,
        "pennies": 0.01
    }

    def __init__(self):
        self.profit = 0
        self.money_received = 0

    def report(self):
        """Prints the current profit"""
        print(f"Money: {self.CURRENCY}{self.profit}")

    def process_coins(self):
        """Returns the total calculated from coins inserted."""
        print("Please insert coins.")
        for coin in self.COIN_VALUES:
            self.money_received += int(input(f"How many {coin}?: ")) * self.COIN_VALUES[coin]
        return self.money_received

    def make_payment(self, cost):
        """Returns True when payment is accepted, or False if insufficient."""
        self.process_coins()
        if self.money_received >= cost:
            change = round(self.money_received - cost, 2)
            print(f"Here is {self.CURRENCY}{change} in change.")
            self.profit += cost
            self.money_received = 0
            return True
        else:
            print("Sorry that's not enough money. Money refunded.")
            self.money_received = 0
            return False
Prerequisites
Python 3.x
Running the Project
Clone the repository:

git clone https://github.com/your-username/coffee-machine-oop.git
cd coffee-machine-oop
Run the main file:

python Coffee_Machine_OOP.py
How to Use
The machine will prompt you to enter your choice of coffee (latte, espresso, or cappuccino).
Type report to get a report of the current resources and profit.
Type off to turn off the machine.
Follow the prompts to insert coins when purchasing a coffee.
Example Interaction
vbnet

Water: 300ml
Milk: 200ml
Coffee: 100g
Money: $0
What would you like? (latte/espresso/cappuccino): latte
Please insert coins.
How many quarters?: 10
How many dimes?: 0
How many nickles?: 0
How many pennies?: 0
Here is $0.5 in change.
Here is your latte ☕️. Enjoy!
Author
Your Name
