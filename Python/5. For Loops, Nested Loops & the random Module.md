#The input() function reads input from the user (always interpreted as a string)
#The int() function always converts it into a number
#a=int(input("Enter an integer:"))

#if condition: the condition must be either True or False.

#>,<,>=,<=,==,!= (relational operators)
#and, or (logical operators) => condition and condition

#while condition (True) => since it's always true, it keeps executing what's inside
#a=[1,2,3]
#b=2 in a
#print(b)
#The result is True.

a=[1,2,3,"AA","BB",100]
for x in a:
    if x == "AA":
        break #unconditionally exit the for loop
       #continue unconditionally goes back to the top of the for loop
        #if a for loop is nested inside another for loop, a break in the inner loop only exits the inner loop (only the one immediately surrounding it)
        #break and continue cannot be used without a for loop
    print(x)


for i in range(2,10):
    print(i)

for i in range(1,3):
    for j in range(1,5):
        print(f"i={i}, j={j}",end=" ")
    print()




# #1. Print numbers from 1 to 10
for i in range(1,11):
    print(i)

# #2. Print numbers from 10 down to 1
for i in range(10,0,-1):
    print(i)


# #3. Print all multiples of 3 between 1 and 100.
for i in range(3,101,3):
    print(i)


# #3-1. Write a program that takes a start value, an end value, and a multiple from the user, then prints the sum of all multiples between the start and end values.
start=int(input("Enter start value: "))
finish=int(input("Enter end value: "))
times=int(input("Enter multiple: "))

total=0
for i in range(start,finish+1):
    if i%times==0:
        total=total+i
print("The final total is %d"%total)


# #3-2. Take a multiplication table number as input and print that table
times=int(input("Enter multiplication table number: "))
for i in range(times,times*9+1,times):
    print(i)
for i in range(2,10):
    print(f"{times}+{i}={times*i}", end=" ")
print()


# #3-3. Write a program that prints the full multiplication table.
for i in range(1,10):
    for times in range(1,10):
        print(f"{i}*{times}={i*times}", end=" ")
    print()
print()


# #4. On day 1 you receive 1 won, and for the next 30 days you receive double the amount from the previous day. Find the total amount on day 30.


# #5. Print a solid rectangle using nested loops
size=int(input("Enter a size: "))
for i in range(size):
    for j in range(size):
        print("*",end="")
    print()

# #6. Take an integer as input, print that many rows, where each row has one more "*" than the previous row.
number=int(input("Enter an integer: "))
for i in range(1,number+1):
    for j in range(i):
        print("*",end="")
    print()
print()

# #7. Print the numbers from 1 to 10! *But skip printing when the number is 6!
for i in range(1,11):
    if i==6:
        continue
    print(i, end="")
print()

# #8. Between 50 and 100 patients visit the hospital with the flu each day. Find how many days it takes for the cumulative number of flu patients to first exceed 10,000.
import random
total_patients=0
days=0
while total_patients <=10000:
    daily_patients=random.randint(50,100)
    total_patients=total_patients+daily_patients
    days=days+1
print(f"On day {days}, the cumulative number of patients {total_patients} exceeded 10,000.")

#9. Write a program that takes a Korean resident registration number (national ID number) as input and prints the date of birth and gender. (Enter the ID number including the "-".)
jnumber=input("Enter ID number (include the '-'): ")
year=jnumber[0:2]
month=jnumber[2:4]
day=jnumber[4:6]
gender_code=jnumber[7]

if gender_code in ['1','3']:
    gender="Male"
elif gender_code in ['2','4']:
    gender="Female"

print(f"Date of birth: {year}, {month}, {day}.")
print(f"Gender: {gender}.")
print()

#10. Korea's "mask 5-day distribution system" assigns a day of the week to buy masks based on the last digit of your birth year.
# People whose last digit is 1 or 6 can buy on Monday, 2 or 7 on Tuesday, 3 or 8 on Wednesday, 4 or 9 on Thursday, and 5 or 0 on Friday.
#Write code that, given a user's ID number, prints which day of the week they are allowed to buy a mask.
name=input("Enter your name: ")
jumin=input("Enter your ID number: ")
last_number=int(jumin[1])

if last_number in [1,6]:
    day="Monday"
elif last_number in [2,7]:
    day="Tuesday"
elif last_number in [3,8]:
    days="Wednesday"
elif last_number in [4,9]:
    days="Thursday"
elif last_number in [5,0]:
    days="Friday"

print(f"{name}'s mask purchase day is {days}.")
print()
