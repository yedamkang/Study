#Last week's assignment
print("Integer:",1,"String:","ABC","Float:",3.14)
print("Integer: %d String: %s Float: %0.2f" % (1, "ABC", 3.14)) #prints up to two decimal places
print("Integer: {0} String: {1} Float: {2}". format(1,"ABC",3.14))
print(f"Integer: {1} String: {"ABC"} Float: {3.14}")
a=10
b="ABC"
c=3.14
print(f"Integer: {1} String: {"ABC"} Float: {3.14}") #this is the style most commonly used today

a="abcdcefc"
print(a.count("c")) #a.count() returns how many times "c" appears in string a
print(len(a)) #len() asks for the length of this variable

a="abcdecfc"
b=",".join(a)
print(b)

a=[4,2,1,"ABC",3]
print(type(a)) #tells us the type of a)
b="3.14"
print(type(b))

a=[4,2,1,"ABC",3] #indexing starts from 0
print(type(a))
print(a[3][1]) #the 2nd item (index 1) inside the 4th item (index 3)
print(a[2])

a=[1,2,3,4,5]
b=a[:2] #from the start up to a[1] (just before index 2)
c=a[2:]
print(b)
print(c)

a=[1,2,3,4,5]
print(a[:2])
print(a[2:])
b=[7,8,9]
c=a+b*3
print(c)
a[2]=3.14
print(a)
del a[3]
print(a)

a=[1,2,3,4,5]
print(a)
a[1]=10
a.sort()
print(a)
a.sort(reverse=True)
print(a)



a={"A+" : 4.5, "A" : 4.0, "B+" : 3.5}
a["B-"] = 3.5
print(a)
print(a["A"])
a['test']='abcd'
print(a)
del a["B+"]
print(a)
print(a.keys())
print(a.values())
print(list(a.keys()))
print(list(a.items()))
print(4.5 in a)
print("A" in a)



userInput = int(input("Enter score: "))
print(userInput+5)

#1. Take one integer as input; if it's 60 or above, print "Pass".
userInput=int(input("Enter score: "))
if userInput >= 60:
    print("Pass")
else :
    print("Fail")
print("Program terminated")

#2. Take one integer as input and print a letter grade: 90+ is A, 80+ is B, 70+ is C, 60+ is D, below 60 is F
userInput=int(input("Enter score: "))
if userInput >= 90:
    print("A")
elif userInput >= 80:
    print("B")
elif userInput >= 70:
    print("C")
elif userInput >= 60:
    print("D")
else :
    print("F")


#3. Write a program that takes two integers and one operator as input, then prints the result
a=int(input("Enter first number: "))
b=int(input("Enter second number: "))
c=input("Enter operator: ")
if c == "+":
    print("The result is",a+b,".")
elif c == "-":
    print("The result is",a-b,".")
elif c == "*":
    print("The result is",a*b,".")
elif c== "/":
    print("The result is",a/b,".")
else :
    print("Invalid operator entered.")

#4. Same problem as above (professor's sample answer) -> remove this to run my own version
firstinput=int(input("Enter first number: "))
secondinput=int(input("Enter second number: "))
op=input("Enter operator: ")
if op == "+":
    result =firstinput + secondinput
elif op == "-":
    result =firstinput - secondinput
elif op == "*":
    result =firstinput * secondinput
elif op == "/":
    result =firstinput / secondinput
else:
    print("Invalid operator entered.")
print(f"{firstinput},{op}, {secondinput}= {result}")


#5. Write a program that takes one integer as input and determines whether it's even or odd.
userInput = int(input("Enter an integer: "))
if userInput % 2 == 0:
    print(userInput,"is even.")
else:
    print(userInput,"is odd.")
