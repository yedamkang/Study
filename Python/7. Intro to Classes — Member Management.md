#Class definition - designing the cookie cutter
class Member:
    # 1. Initialize fields (member variables): store id, name, and point
    def __init__(self, id, name, point):
        # When you stamp the cookie cutter (create the object), you fill the dough with the initial info.
        self.id = id
        self.name = name
        self.point = point

    # 2. Change name (setName) and return it (getName)
    def setName(self, name):
        # A feature to modify the created cookie's name later.
        self.name = name

    def getName(self):
        # A feature to take the cookie's name out so you can check it.
        return self.name

    # 3. Change point (setPoint) and return it (getPoint)
    def setPoint(self, point):
        # A feature to modify the created cookie's point later.
        self.point = point

    def getPoint(self):
        # A feature to modify the created cookie's point later.
        return self.point

    # 4. Change id (setId) and return it (getId)
    def setId(self, id):
        # A feature to modify the created cookie's id later.
        self.id = id

    def getId(self):
        # A feature to modify the created cookie's id later.
        return self.id

    # 5. Print member info (printMember)
    def printMember(self):
        print(f"ID: {self.id}, Name: {self.name}, Points: {self.point}")


# Create an object - stamp out a cookie using the cookie cutter
# Use the "Member" cutter to create an actual cookie object called 'm1'.
m1 = Member("abc", "John Smith", 1000)

# Print current info
m1.printMember()

# Change name (John Smith -> John Doe)
m1.setName("John Doe")

# Print updated info
m1.printMember()

# Change point (1000 -> 1500)
m1.setPoint(1500)

# Use getPoint to retrieve the point, store it in a variable, and print it
m1_point = m1.getPoint()
print(m1_point)
