# librarySystemDemo
import java.util.*;

// Author class
class Author {
    private String name;
    private int numberOfBooksWritten;

    public Author(String name, int numberOfBooksWritten) {
        this.name = name;
        this.numberOfBooksWritten = numberOfBooksWritten;
    }

    public String getName() {
        return name;
    }

    public void displayBio() {
        System.out.println("Author: " + name);
        System.out.println("Books Written: " + numberOfBooksWritten);
    }
}

// Book class
class Book {
    private String title;
    private Author author;
    private int publicationYear;
    private boolean isAvailable;

    public Book(String title, Author author, int publicationYear) {
        this.title = title;
        this.author = author;
        this.publicationYear = publicationYear;
        this.isAvailable = true;
    }

    public String getTitle() {
        return title;
    }

    public Author getAuthor() {
        return author;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void displayDetails() {
        System.out.println("Title: " + title);
        System.out.println("Author: " + author.getName());
        System.out.println("Year: " + publicationYear);
        System.out.println("Available: " + (isAvailable ? "Yes" : "No"));
    }

    public void borrow() {
        if (isAvailable) {
            isAvailable = false;
            System.out.println(title + " has been borrowed.");
        } else {
            System.out.println(title + " is currently not available.");
        }
    }

    public void returnBook() {
        isAvailable = true;
        System.out.println(title + " has been returned.");
    }
}

// Library class
class Library {
    private List<Book> books;

    public Library() {
        books = new ArrayList<>();
    }

    public void addBook(Book b) {
        books.add(b);
        System.out.println("Book added: " + b.getTitle());
    }

    public void borrowBook(String title) {
        for (Book b : books) {
            if (b.getTitle().equalsIgnoreCase(title)) {
                b.borrow();
                return;
            }
        }
        System.out.println("Book not found.");
    }

    public void returnBook(String title) {
        for (Book b : books) {
            if (b.getTitle().equalsIgnoreCase(title)) {
                b.returnBook();
                return;
            }
        }
        System.out.println("Book not found.");
    }

    public void searchByTitle(String title) {
        for (Book b : books) {
            if (b.getTitle().toLowerCase().contains(title.toLowerCase())) {
                b.displayDetails();
                return;
            }
        }
        System.out.println("No book found with that title.");
    }

    public void searchByAuthor(String authorName) {
        for (Book b : books) {
            if (b.getAuthor().getName().equalsIgnoreCase(authorName)) {
                b.displayDetails();
            }
        }
    }
}


// Main class
public class LibrarySystemDemo {
    public static void main(String[] args) {
        // Create authors
        Author author1 = new Author("George Orwell", 10);
        Author author2 = new Author("J.K. Rowling", 15);

        // Create books
        Book book1 = new Book("1984", author1, 1949);
        Book book2 = new Book("Harry Potter", author2, 1997);

        // Create library
        Library myLibrary = new Library();

        // Perform operations
        myLibrary.addBook(book1);
        myLibrary.addBook(book2);

        myLibrary.searchByTitle("1984");
        myLibrary.borrowBook("1984");
        myLibrary.borrowBook("1984"); // attempt again
        myLibrary.returnBook("1984");

        System.out.println("\nSearch by Author:");
        myLibrary.searchByAuthor("J.K. Rowling");
    }
}
