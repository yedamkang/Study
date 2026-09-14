# Parent class
class Account:
    def __init__(self, owner, accountNo, money):
        self.owner = owner
        self.accountNo = accountNo
        self.money = money

    # Print account info
    def info(self):
        return f"Name: {self.owner}, Account No: {self.accountNo}, Balance: {self.money}"

    # Withdraw
    def withdraw(self, amount):
        if amount > self.money:
            print("Insufficient balance.")
        else:
            self.money -= amount
            print(f"Withdrawal complete, balance: {self.money}")

    # Deposit
    def deposit(self, amount):
        self.money += amount


# Child class
class CheckCard(Account):
    def __init__(self, owner, accountNo, money, cardNo, password):
        # Call the parent constructor
        super().__init__(owner, accountNo, money)

        # Member variables unique to the child class
        self.cardNo = cardNo
        self.password = password

    # info
    def info(self):
        return (
            f"Name: {self.owner}, Account No: {self.accountNo}, Balance: {self.money}\n"
            f"Card No: {self.cardNo}, Password: {self.password}"
        )

    # Withdraw after verifying card number and password
    def withdraw(self, amount, cardNo, password):
        if self.cardNo != cardNo or self.password != password:
            print("Incorrect card number or password.")
        elif amount > self.money:
            print("Insufficient balance.")
        else:
            self.money -= amount
            print(f"Withdrawal complete, balance: {self.money}")


user1 = Account("John Smith", "222-1111", 20000)

print(user1.info())

user1.withdraw(25000)
print(user1.info())

user1.deposit(4000)
print(user1.info())


dy = CheckCard("David Kim", "123-456-78910", 10000, "50-50-51", "1234")

dy.withdraw(1500, "5011-50-51", "1234")
print(dy.info())

dy.withdraw(1500, "50-50-51", "1234")
print(dy.info())

dy.deposit(2000)
print(dy.info())
