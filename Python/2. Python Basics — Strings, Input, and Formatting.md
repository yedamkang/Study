a=15
b=6
print(a//b)
print(a%b)
print(b*2)
print(b**2)

a="Hello world!"
b=' Sungshin Univ. '
print(a+b)
print(a*5)

a="Hello \n world!"
print(a)

a="""Hello
wor
ld!
"""
print(a)

a="Hello world!"
print(a)
b=len(a)
print(b)
print(len(a))

a=12
print(a)
print(type(a))

#Write a program that takes two numbers as input and prints their sum. (Problem)
a=input("Enter an integer: ") #input() always reads what's entered as a string
b=input("Enter an integer: ")
print(a+b)

#Write a program that takes two numbers as input and prints their sum. (Answer)
a=input("Enter an integer: ") #int() converts a string into an integer
a=int(a)
b=int(input("Enter an integer: "))
print("The sum of the two numbers is",a+b,".")

#Write a program that takes two numbers as input and prints the quotient and remainder (Answer)
a=int(input("Enter an integer: "))
b=int(input("Enter an integer: "))
print("Quotient: ",a//b, "Remainder: ",a%b, ".")

a="Life is too short, You need Python" #think of each position as an index
print(a[0])
print(a[12])
print(a[-1])

a="Life is too short, You need Python"
print(a[0:6])
print(a[:6])
print(a[8:])

a="Life is too short, You need Python"
b=a[0:6]
print(a)
print(b)

print("I eat %d apples."%3)

print("I eat %s apples." %"five")

b=3
print("Hi, this is %d and it's %10s." %(b,"five"))

b=3
print("Hi, this is %d and it's %-15s." %(b,"five"))

b=3
print("Hi, this is %d and it's %-15s. %10.2f" % (b,"five",3.14))

print("Hello Mr./Ms. {0}, {1}, and {2}, nice to meet all three of you". format("Tom","Amy","Mike"))

a=10
b=20
print(f"The value of a is {a}, and the value of b is {b}")
