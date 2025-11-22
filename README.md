class Account:
    def __init__(self, account_no, pin, balance):
        self.account_no = account_no
        self.pin = pin
        self.balance = balance

    def verify_pin(self, entered_pin):
        return entered_pin == self.pin

    def debit(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            print(f"₹{amount} Debited Successfully. New Balance: ₹{self.balance}")
        else:
            print("❌ Insufficient Balance!")

    def credit(self, amount):
        self.balance += amount
        print(f"₹{amount} Credited Successfully. New Balance: ₹{self.balance}")

    def check_balance(self):
        print(f"💰 Your Current Balance is: ₹{self.balance}")

    def change_pin(self, old_pin, new_pin):
        if self.verify_pin(old_pin):
            self.pin = new_pin
            print("🔐 PIN Changed Successfully!")
        else:
            print("❌ Incorrect Old PIN!")

# ------------------------------------
# Create Multiple Bank Accounts
# ------------------------------------

accounts = {
    "1001": Account("1001", 1111, 5000),
    "1002": Account("1002", 2222, 8000),
    "1003": Account("1003", 3333, 12000)
}

# ------------------------------------
# ATM MACHINE START
# ------------------------------------

print("🏦 Welcome to Python ATM\n")

acc_no = input("👉 Enter Account Number: ")

if acc_no in accounts:
    account = accounts[acc_no]
    pin = int(input("🔐 Enter PIN: "))

    if account.verify_pin(pin):
        print("\n✔ Login Successful!")

        while True:
            print("\n===== ATM MENU =====")
            print("1. Check Balance")
            print("2. Withdraw Money")
            print("3. Deposit Money")
            print("4. Change PIN")
            print("5. Exit ATM")

            choice = input("👉 Enter your choice: ")

            if choice == "1":
                account.check_balance()

            elif choice == "2":
                amt = int(input("💸 Enter amount to withdraw: "))
                account.debit(amt)

            elif choice == "3":
                amt = int(input("💰 Enter amount to deposit: "))
                account.credit(amt)

            elif choice == "4":
                old_pin = int(input("🔐 Enter old PIN: "))
                new_pin = int(input("🆕 Enter new PIN: "))
                account.change_pin(old_pin, new_pin)

            elif choice == "5":
                print("👋 Thank you for using Python ATM!")
                break

            else:
                print("❌ Invalid Choice. Try again.")

    else:
        print("❌ Incorrect PIN!")
else:
    print("❌ Account Not Found!")
