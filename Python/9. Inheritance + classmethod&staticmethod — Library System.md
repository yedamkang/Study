class Book:
    total_books = 0

    def __init__(self, title, author):
        self.title = title
        self.author = author
        self.is_borrowed = False
        Book.total_books += 1

    @classmethod
    def get_total_books(cls):
        print(f"The library currently has {cls.total_books} books registered.")

    @staticmethod
    def validate_title(title):
        if title == "" or title == "   ":
            return False
        return True

    def borrow_book(self):
        if self.is_borrowed:
            print("This book is already checked out.")
        else:
            self.is_borrowed = True
            print(f"[{self.title}] has been checked out.")

    def return_book(self):
        self.is_borrowed = False
        print(f"[{self.title}] has been returned.")


class EBook(Book):
    def __init__(self, title, author, file_size, link):
        super().__init__(title, author)
        self.file_size = file_size
        self.link = link

    def borrow_book(self):
        print(f"An ebook download link has been sent. Link: {self.link}")


print(Book.validate_title("   "))
print(Book.validate_title("Python Programming"))

book1 = Book("The Python Handbook", "John Smith")
book2 = Book("Introduction to Algorithms", "David Lee")
ebook1 = EBook("Data Analysis Basics", "Michael Kim", 15, "http://library.com/download/101")

Book.get_total_books()

book1.borrow_book()
book1.borrow_book()
book1.return_book()

ebook1.borrow_book()
