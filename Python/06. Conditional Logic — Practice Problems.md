#1. Write a program that takes two integers as input and prints their difference. The larger number must be entered first.
a=int(input("Enter first integer: "))
b=int(input("Enter second integer: "))
print(a-b)

#2. Take one number as input and print "Positive" or "Negative".
userInput=int(input("Enter a number: "))
if userInput > 0:
    print("Positive")
elif userInput == 0:
    print("Neither positive nor negative")
else:
    print("Negative")

#3. Take one number as input and print "Even" or "Odd".
userInput=int(input("Enter a number: "))
if userInput % 2 == 0:
    print("Even")
else:
    print("Odd")

#4. Take scores (0-99) for 3 subjects, compute the total and average, then print "Pass" if the average is 60+ and "Fail" otherwise. However, if even one subject is below 60, it's "Fail" (e.g. 70,70,9 => Fail)
a=int(input("Enter first score: "))
b=int(input("Enter second score: "))
c=int(input("Enter third score: "))
total=a+b+c
average=total/3
if average >= 60:
    print(a,b,c ,"=> Pass")
elif a<60 or b<60 or c< 60:
    print(a,b,c , "Fail")
else:
    print(a,b,c ,"=> Fail")

#5. Take two integers as input, divide them, and print the "quotient" and "remainder". If either number is 0, print "Cannot divide by zero".
a=int(input("Enter first integer: "))
b=int(input("Enter second integer: "))
if a ==0 or b == 0:
    print("Cannot divide by zero.")
else:
    print("Quotient: ",a//b,"Remainder: ",a%b)

#6. Write a program that prints a letter grade based on a student's average score. 90+ is A, 80+ is B, 70+ is C, 60+ is D, and below that is F.
userInput=int(input("Enter student's average score: "))
if userInput >= 90:
    print("A")
elif userInput >= 80:
    print("B")
elif userInput >= 70:
    print("C")
elif userInput >= 50:
    print("D")
else:
    print("F")

#7. Complete a program that prints a category based on age. (0-7: preschooler, 8-13: elementary student, 14-16: middle schooler, 17-19: high schooler, 20+: adult)
userInput=int(input("Enter age: "))
if 0<=userInput<=7:
    print("Preschooler")
elif 8<=userInput<=13:
    print("Elementary student")
elif 14<=userInput<=16:
    print("Middle schooler")
elif 17<=userInput<=19:
    print("High schooler")
elif userInput >= 20:
    print("Adult")
else:
    print("Not a valid category")


#8. Determine whether a year is a leap year
    #A leap year is a year that is a multiple of 4 but not a multiple of 100, OR a multiple of 400. For example, 2012 is a multiple of 4 and not a multiple of 100, so it's a leap year.
    #1900 is a multiple of 100 but not a multiple of 400, so it's not a leap year. 2000 is a multiple of 400, so it is a leap year.
userInput=int(input("Enter a year: "))
if (userInput % 4== 0 and userInput % 100!= 0) or userInput % 400 == 0:
    print(userInput ,"is a leap year")
else:
    print(userInput ,"is not a leap year")

#9. Take one score as input and print "Pass" if it's 60 or above, "Fail" if it's below 60.
userInput=int(input("Enter score: "))
if userInput >= 60:
    print("Pass")
else:
    print("Fail")


#How to use print
# print("The value of the two numbers is: ", a+b. ".")
# print("{0}+{1}={2}".format(a,b,a+b))
# print("%d+%d=%d"%(a,b,a+b))
# print(f"{a}+{b}={a+b}")

a=[1,2,3,4] #list
print(5 in a) #is the value 5 in list a?

a=10
while a>0: #keep running this loop until the condition becomes false
    print(f"The value of a is: {a}")
    a=a-1

a=10
while True: #this condition keeps running repeatedly
    print(f"The value of a is: {a}")
    a=a-1




#10. Print numbers from 1 to 10
a=1
while a<=10:
    print(a)
    a=a+1

#11. Print numbers from 10 down to 1.
a=10
while a>=1:
    print(a)
    a=a-1

#12. Print all multiples of 3 between 1 and 100.
a=1
while a<=100:
    if a%3==0:
        print(a)
    a=a+1

#13. Print the sum of all multiples of 3 between 1 and 100.
a=1
total=0
while a<=100:
    if a%3==0:
        total=total+a
    a=a+1
print(total)



#14. Write a program that takes one integer from the user and prints the sum from 1 up to that value.
userInput=int(input("Enter an integer: "))
a=1
total=0
while userInput>=a :
    total=total+a
    a = a + 1
print(f"Total: {total}")
