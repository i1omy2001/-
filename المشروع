# LIBRARY MANAGEMENT SYSTEM

class Book:

    library_name = "المكتبة المركزية"
    total_books = 0

    def __init__(self, book_id, title, author):
        self.__book_id = book_id
        self.__title = title
        self.__author = author
        self.__is_borrowed = False

        Book.total_books += 1

    def get_id(self):
        return self.__book_id

    def get_title(self):
        return self.__title

    def get_author(self):
        return self.__author

    @property
    def title(self):
        return self.__title

    @title.setter
    def title(self, new_title):
        if new_title.strip():
            self.__title = new_title

    def set_title(self, new_title):
        self.title = new_title

    @classmethod
    def change_library_name(cls, new_name):
        cls.library_name = new_name

    @staticmethod
    def valid_id(book_id):
        return book_id.isdigit()

    def borrow_book(self):
        if self.__is_borrowed:
            print("الكتاب مستعار حالياً")
        else:
            self.__is_borrowed = True
            print("تمت استعارة الكتاب بنجاح")

    def return_book(self, days_late):
        if not self.__is_borrowed:
            print("الكتاب موجود في المكتبة أصلاً")
        else:
            self.__is_borrowed = False
            fine = days_late * 1000
            print("تم إرجاع الكتاب. الغرامة:", fine, "دينار")

    def show_info(self):
        status = "مستعار" if self.__is_borrowed else "متاح"

        print("رقم الكتاب:", self.__book_id)
        print("العنوان:", self.__title)
        print("المؤلف:", self.__author)
        print("الحالة:", status)

    def __str__(self):
        return f"{self.title} - {self.__author}"


class PaperBook(Book):

    def __init__(self, book_id, title, author, shelf):
        super().__init__(book_id, title, author)
        self.shelf = shelf

    def show_paper_info(self):
        self.show_info()
        print("النوع: كتاب ورقي")
        print("رقم الرف:", self.shelf)


class EBook(Book):

    def __init__(self, book_id, title, author, file_size):
        super().__init__(book_id, title, author)
        self.file_size = file_size

    def show_ebook_info(self):
        self.show_info()
        print("النوع: كتاب إلكتروني")
        print("حجم الملف:", self.file_size, "MB")


class Library:

    def __init__(self):
        self.books = []

    def add_book(self):
        print("\n1. كتاب ورقي")
        print("2. كتاب إلكتروني")

        book_type = input("اختر النوع: ")
        book_id = input("رقم الكتاب: ")

        if not Book.valid_id(book_id):
            print("رقم الكتاب يجب أن يحتوي على أرقام فقط")
            return

        if self.find_book(book_id):
            print("رقم الكتاب موجود مسبقاً")
            return

        title = input("عنوان الكتاب: ")
        author = input("اسم المؤلف: ")

        if book_type == "1":
            shelf = input("رقم الرف: ")
            book = PaperBook(book_id, title, author, shelf)
        elif book_type == "2":
            size = input("حجم الملف MB: ")
            book = EBook(book_id, title, author, size)

        else:
            print("اختيار غير صحيح")
            return

        self.books.append(book)
        print("تمت إضافة الكتاب بنجاح")

    def find_book(self, book_id):
        for book in self.books:
            if book.get_id() == book_id:
                return book
        return None

    def borrow(self):
        book_id = input("رقم الكتاب للاستعارة: ")
        book = self.find_book(book_id)

        if book:
            book.borrow_book()
        else:
            print("الكتاب غير موجود")

    def return_book(self):
        book_id = input("رقم الكتاب للإرجاع: ")
        book = self.find_book(book_id)

        if book:
            try:
                days = int(input("عدد أيام التأخير: "))

                if days < 0:
                    print("عدد الأيام غير صحيح")
                    return

                book.return_book(days)

            except ValueError:
                print("أدخل رقماً صحيحاً")

        else:
            print("الكتاب غير موجود")

    def display_all(self):
        if not self.books:
            print("لا توجد كتب")

        for book in self.books:
            print("-------------------")
            if isinstance(book, PaperBook):
                book.show_paper_info()
            elif isinstance(book, EBook):
                book.show_ebook_info()

    def search(self):
        title = input("أدخل عنوان الكتاب: ")

        for book in self.books:
            if book.title == title:
                print(book)
                if isinstance(book, PaperBook):
                    book.show_paper_info()
                elif isinstance(book, EBook):
                    book.show_ebook_info()
                return

        print("لم يتم العثور على الكتاب")

    def menu(self):
        while True:
            print("\n======", Book.library_name, "======")
            print("1. إضافة كتاب")
            print("2. استعارة كتاب")
            print("3. إرجاع كتاب")
            print("4. عرض الكتب")
            print("5. البحث عن كتاب")
            print("6. عدد الكتب")
            print("7. تغيير اسم المكتبة")
            print("8. خروج")

            choice = input("اختر العملية: ")

            if choice == "1":
                self.add_book()

            elif choice == "2":
                self.borrow()

            elif choice == "3":
                self.return_book()

            elif choice == "4":
                self.display_all()

            elif choice == "5":
                self.search()

            elif choice == "6":
                print("عدد الكتب:", Book.total_books)

            elif choice == "7":
                name = input("اسم المكتبة الجديد: ")
                Book.change_library_name(name)
                print("تم تغيير الاسم")

            elif choice == "8":
                print("مع السلامة!")
                break

            else:
                print("اختيار غير صحيح")

my_library = Library()
my_library.menu()
