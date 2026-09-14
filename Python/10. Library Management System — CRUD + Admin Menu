# -----------------------------
# Parent class: Book
# -----------------------------
class Book:

    total_books = 0   # class variable

    # Constructor
    def __init__(self, title, author):

        self.title = title
        self.author = author
        self.is_borrowed = False

        Book.total_books += 1

    # Class method
    @classmethod
    def get_total_books(cls):
        print(f"Total number of books: {cls.total_books}")

    # Static method
    @staticmethod
    def validate_title(title):

        # False if the title is empty or blank
        if title.strip() == "":
            return False

        return True

    # Borrow
    def borrow_book(self):

        if self.is_borrowed:
            print("This book is already checked out.")

        else:
            self.is_borrowed = True
            print("Book checked out successfully")

    # Return
    def return_book(self):

        self.is_borrowed = False
        print("Book returned successfully")


# -----------------------------
# Child class: Ebook
# -----------------------------
class Ebook(Book):

    # Constructor
    def __init__(self, title, author, file_size):

        super().__init__(title, author)

        self.file_size = file_size

    # Method overriding
    def borrow_book(self):

        self.is_borrowed = True

        print("An ebook download link has been sent.")


# -----------------------------
# Admin functionality class: Library
# -----------------------------
class Library:

    # Constructor
    def __init__(self):

        # List to store registered books
        self.books = []

    # Admin login
    def admin_login(self):

        password = input("Enter admin password: ")

        if password == "admin1234":
            return True

        return False

    # Register a book
    def add_book(self):

        kind = input("1. Regular book / 2. Ebook, choose one: ")

        title = input("Enter title: ")

        # Validate title
        if not Book.validate_title(title):
            print("Invalid title")
            return

        author = input("Enter author: ")

        # Regular book
        if kind == "1":

            book = Book(title, author)

        # Ebook
        elif kind == "2":

            file_size = input("Enter file size (MB): ")

            book = Ebook(title, author, file_size)

        else:
            print("Invalid input")
            return

        self.books.append(book)

        print("Book registered successfully")

    # Search for a book
    def search_book(self):

        title = input("Enter title to search: ")

        for book in self.books:

            if book.title == title:

                print("----- Book Info -----")
                print("Title:", book.title)
                print("Author:", book.author)

                # Only print if it's an Ebook
                if isinstance(book, Ebook):
                    print("File size:", book.file_size, "MB")

                print("Borrowed:", book.is_borrowed)

                return

        print("Book not found.")

    # Edit a book
    def edit_book(self):

        title = input("Enter the title of the book to edit: ")

        for book in self.books:

            if book.title == title:

                new_title = input("Enter new title: ")
                new_author = input("Enter new author: ")

                if not Book.validate_title(new_title):
                    print("Invalid title")
                    return

                book.title = new_title
                book.author = new_author

                print("Book updated successfully")
                return

        print("Book not found.")

    # Delete a book
    def delete_book(self):

        title = input("Enter the title of the book to delete: ")

        for book in self.books:

            if book.title == title:

                self.books.remove(book)

                Book.total_books -= 1

                print("Book deleted successfully")
                return

        print("Book not found.")


# -----------------------------
# Main program
# -----------------------------
library = Library()

# Admin authentication
if library.admin_login():

    while True:

        print("\n===== Admin System =====")
        print("1. Register book")
        print("2. Search book")
        print("3. Edit book")
        print("4. Delete book")
        print("5. Check total book count")
        print("6. Exit program")

        menu = input("Select menu: ")

        # Register
        if menu == "1":
            library.add_book()

        # Search
        elif menu == "2":
            library.search_book()

        # Edit
        elif menu == "3":
            library.edit_book()

        # Delete
        elif menu == "4":
            library.delete_book()

        # Total book count
        elif menu == "5":
            Book.get_total_books()

        # Exit
        elif menu == "6":
            print("Program terminated")
            break

        else:
            print("Invalid input.")

else:
    print("Admin authentication failed")
