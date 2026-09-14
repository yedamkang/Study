# #1. Take Rock-Paper-Scissors input from the user and play against the computer. Also implement a best-of-three rule where the first to win 3 rounds wins overall.
import random
z=["Rock","Paper","Scissors"]

win=0

while True:
    com=random.choice(z)
    print("Computer's choice:",com)
    user=input("Enter Rock, Paper, or Scissors: ")
    if user==com:
        print("Tie")
    elif (user=="Rock" and com == "Scissors") or (user == "Scissors" and com == "Paper") or (user == "Paper" and com == "Rock"):
        print("You win")
        win=win+1
        if win == 3:
            break
    else :
        print("You lose")


#2. Take a string from the user and make a solo word-chain game. Ignore any special pronunciation rules, and end the game if the user enters 0, repeats an already-used word, or gives a wrong answer.
myList=[]

while True:
    userInput=input("Enter a word (0 to quit): ")

    if userInput == "0":
        print(myList)
        break
    if userInput in myList:
        print("That word has already been used. You lose.", myList)
        break

    if len(myList)>0:
        if myList[-1][-1] == userInput[0] :  #e.g. if the list is [apple, elephant], "elephant" starts with the last letter of "apple"
            myList.append(userInput)
        else:
            print(f"The next word must start with '{myList[-1][-1]}'. You lose.")
            break
    else:
        myList.append(userInput)


myList=["abc","def"]
print(myList[-1])
print(myList[-1][-1])

#3. Up-Down game rules
#Generate a random value between 1 and 100.
import random
com=random.randint(1,101)

# print(com)
count=0

while True:
    userInput=int(input("Enter a number between 1 and 100: "))
    count=count+1

    if userInput == com:
        if count<=5:
            print("Great, you found the number within 5 tries.")
        elif 6<=count<=10:
            print("Good, you found the number within 6-10 tries.")
        else:
            print("Bad, but you found the number.")
        break
