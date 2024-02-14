# Machine-learning-Akbank-Bootcamp
Library Management System
class Library:
    def __init__(self):
        self.file = open("books.txt", "a+")

    def listing(self):
        self.file.seek(0)  # Dosyayı başa al
        lines = self.file.read().splitlines()

        eachbook = []
        for line in lines:
            book_info = line.split(",")
            eachbook.append(book_info)

        for book in eachbook:
            print(f"Book: {book[0]}, Author: {book[1]}")


    def add_book(self):
      book_title= input("What is the name of the book that you want to add?")
      book_author= input("What is the author of the  book that you want to add?")
      book_releasedate= input("What is the release date of the  book that you want to add?")
      book_numberofpages= input("What is the number of pages of the  book that you want to add?")
      new_add = f"{book_title},{book_author},{book_releasedate},{book_numberofpages}\n"
      self.file.write(new_add)

    def remove_book(self):
        print("Remove a Book:")
        title_to_remove = input("Enter the title of the book to remove: ")

        self.file.seek(0)
        book_lines = self.file.read().splitlines()

        found = False
        for i, book_line in enumerate(book_lines):
            if title_to_remove in book_line:
                found = True
                del book_lines[i]
                break

        if found:
            self.file.truncate(0)
            self.file.seek(0)

            for book_line in book_lines:
                self.file.write(book_line + "\n")

    def dosyayi_kapat(self):
        self.file.close()

    def __del__(self):
        self.dosyayi_kapat()


lib = Library()

while True:
  print("*** MENU***")
  print("1) List Books")
  print("2) Add Book")
  print("3) Remove Book")
  print("q)Q1uit")


  answer = (input("enter your choice (1-3)"))
  if answer.lower() == 'q':
        break
  if answer == '1':
      lib.listing()
  elif answer == '2':
      lib.add_book()
  elif answer == '3':
      lib.remove_book()
  else:
     print("Invalid choice. Please enter a number between 1 and 3.")
