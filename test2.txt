#budget tracker app
import json
def add_expense(expenses, description, amount):
    expenses.append({"description": description, "amount": amount})
    print(f"Added expense: {description}, Amount: {amount}")

def get_total_expenses(expenses):
    return sum(expense['amount'] for expense in expenses)

def get_balance(budget, expenses):
    return budget - get_total_expenses(expenses)

def show_budget_details(budget, expenses):
    print(f"Total Budget: {budget}")
    print("Expenses:")
    for expense in expenses:
        print(f"- {expense['description']}:{expense['amount']}")
    print(f"total spent:{get_total_expenses(expenses)}")
    print(f"remaining budget:{get_balance(budget,expenses)}")


def load_budget_data(filepath):
    try:
        with open(filepath,'r')as file:
            data = json.loads(file)
            return data['initial_budget'],data['expenses']
    except(FileNotFoundError,json.JSONDecodeError):
        return 0,[] #return  default valves if the file doesn't exist or isempty/corrupted

def save_budget_details(filepath,initial_budget,expenses):
    data={
        'initial_budget':initial_budget,
        'expenses':expenses
    } 
    with open(filepath,'w') as file :
        json.dump(data,file, indent=4)
 
def main():
    print("welcome to the budget app")
    #filedpath='budget_data.json' #define the path to your JSON file 
    #initial_budget, expenses = load_budget_data(filedpath)
    initial_budget=float(input("please enter your initial budget:"))
    budget=initial_budget
    expenses=[]
    while True:
        print("\nwhat would you like to do ?")
        print("add an expenses")
        print(" show budget detals")
        print("exit")
        choice = input("enter a your choice (1/2/3): ")

        if choice=="1":
            description=input("enter expense description:")
            amount=float(input("ente a expense amount: "))
            add_expense(expenses,description,amount)
        elif choice =="2":
            show_budget_details(budget,expenses)
        elif choice =="3":
            print("exiting budget app.goodbye!")
            break
        else:
            print("invalid choice ,please choose again.")

if __name__=="__main__":
    main()
