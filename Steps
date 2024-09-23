# Library-Management-System
CREATE DATABASE library;

USE library;

CREATE TABLE Branch (
    Branch_no INT PRIMARY KEY,
    Manager_Id INT,
    Branch_address VARCHAR(255),
    Contact_no VARCHAR(15)
);

INSERT INTO Branch ( Branch_no, Manager_Id, Branch_address, Contact_no) VALUES
(1, 201, '123 Main St, Downtown, New Delhi, 110001', '9876543210'),
(2, 202, '456 Oak St, Central Park, Mumbai, 400001', '9876543222'),
(3, 203, '789 Pine St, MG Road, Bengaluru, 560001', '9876543233'),
(4, 204, '987 Cedar St, Whitefield, Hyderabad, 500001', '9876543244'),
(5, 205, '654 Maple St, Anna Nagar, Chennai, 600040', '9876543255');

SELECT * FROM Branch;

CREATE TABLE Employee (
    Emp_Id INT PRIMARY KEY,
    Emp_name VARCHAR(100),
    Position VARCHAR(100),
    Salary DECIMAL(10, 2),
    Branch_no INT,
    FOREIGN KEY (Branch_no) REFERENCES Branch (Branch_no)
);

INSERT INTO Employee (Emp_Id, Emp_name, Position, Salary, Branch_no) VALUES
(201, 'Alice Smith', 'Manager', 80000, 1),
(202, 'Bob Johnson', 'Assistant Manager', 60000, 2),
(203, 'Charlie Davis', 'Manager', 75000, 3),
(204, 'Eve Thompson', 'Clerk', 30000, 1),
(205, 'Frank White', 'Clerk', 55000, 2),
(206, 'Grace Lee', 'Clerk', 45000, 3),
(207, 'Henry Walker', 'Clerk', 52000, 4),
(208, 'Ivy Adams', 'Manager', 90000, 4),
(209, 'Jack Evans', 'Assistant Manager', 70000, 5);

SELECT * FROM Employee;

CREATE TABLE Books (
    ISBN VARCHAR(13) PRIMARY KEY,
    Book_title VARCHAR(255),
    Category VARCHAR(100),
    Rental_Price DECIMAL(10, 2),
    Status VARCHAR(3),
    Author VARCHAR(100),
    Publisher VARCHAR(100)
);

INSERT INTO Books (ISBN, Book_title, Category, Rental_Price, Status, Author, Publisher) VALUES
('1234567890', 'The History of Time', 'History', 40, 'Yes', 'Stephen Hawking', 'Penguin'),
('1234567891', 'Science Revolution', 'Science', 50, 'Yes', 'Isaac Newton', 'HarperCollins'),
('1234567892', 'The Art of War', 'History', 30, 'No', 'Sun Tzu', 'Random House'),
('1234567893', 'Quantum Physics', 'Science', 60, 'Yes', 'Niels Bohr', 'Springer'),
('1234567894', 'World War II', 'History', 45, 'No', 'John Keegan', 'Oxford Press'),
('1234567895', 'The History of Ancient Rome', 'History', 35, 'Yes', 'Mary Beard', 'Penguin'),
('1234567896', 'Astrophysics Explained', 'Science', 70, 'No', 'Neil deGrasse Tyson', 'Random House');

SELECT * FROM Books ;

CREATE TABLE Customer (
    Customer_Id INT PRIMARY KEY,
    Customer_name VARCHAR(100),
    Customer_address VARCHAR(255),
    Reg_date DATE
);

INSERT INTO Customer ( Customer_Id, Customer_name, Customer_address, Reg_date) VALUES
(301, 'Emily Brown', '12 Willow St, City A', '2021-12-15'),
(302, 'Michael Green', '98 Elm St, City B', '2022-01-20'),
(303, 'Sophia Miller', '56 Maple St, City C', '2020-10-05'),
(304, 'James Harris', '77 Cedar St, City A', '2021-07-22'),
(305, 'Olivia Lewis', '22 Birch St, City B', '2022-06-18');

SELECT *FROM Customer;

CREATE TABLE IssueStatus (
    Issue_Id INT PRIMARY KEY,
    Issued_cust INT,
    Issued_book_name VARCHAR(255),
    Issue_date DATE,
    Isbn_book VARCHAR(13),
    FOREIGN KEY (Issued_cust) REFERENCES Customer(Customer_Id),
    FOREIGN KEY (Isbn_book) REFERENCES Books(ISBN)
);

INSERT INTO IssueStatus (Issue_Id, Issued_cust, Issued_book_name, Issue_date, Isbn_book) VALUES 
(401, 301, 'The History of Time', '2023-06-10', '1234567890'),
(402, 302, 'Science Revolution', '2023-06-15', '1234567891'),
(403, 305, 'Quantum Physics', '2023-07-05', '1234567893');

SELECT * FROM IssueStatus ;

CREATE TABLE ReturnStatus (
    Return_Id INT PRIMARY KEY,
    Return_cust INT,
    Return_book_name VARCHAR(255),
    Return_date DATE,
    Isbn_book2 VARCHAR(13),
    FOREIGN KEY (Return_cust) REFERENCES Customer(Customer_Id),
    FOREIGN KEY (Isbn_book2) REFERENCES Books(ISBN)
);

INSERT INTO ReturnStatus ( Return_Id, Return_cust, Return_book_name, Return_date, Isbn_book2 ) VALUES 
(501, 301, 'The History of Time', '2023-06-15', '1234567890'),
(502, 302, 'Science Revolution', '2023-06-20', '1234567891'),
(503, 305, 'Quantum Physics', '2023-07-10', '1234567893'),
(504, 303, 'The Art of War', '2023-07-12', '1234567892'),
(505, 304, 'World War II', '2023-08-05', '1234567894');

SELECT * FROM ReturnStatus ;

# 1) Retrieve the book title, category, and rental price of all available books.

SELECT Book_title, Category, Rental_Price FROM Books
WHERE Status = 'Yes';

# 2) List the employee names and their respective salaries in descending order of salary.

SELECT Emp_Id, Emp_name, Salary FROM Employee
ORDER BY Salary DESC;

# 3) Retrieve the book titles and the corresponding customers who have issued those books.

SELECT i.Issued_book_name , c.Customer_name FROM IssueStatus i
JOIN Customer C ON i.Issued_cust = c.Customer_Id ;

# 4) Display the total count of books in each category.

SELECT Category, COUNT(*) AS total_count FROM Books
GROUP BY Category;

# 5) Retrieve the employee names and their positions for the employees whose salaries are above Rs.50,000.

SELECT Emp_Id, Emp_name, Position FROM Employee
WHERE Salary > 50000 ;

# 6) List the customer names who registered before 2022-01-01 and have not issued any books yet.

SELECT c.Customer_name FROM Customer c
LEFT JOIN IssueStatus i ON c.Customer_Id = i.Issued_cust
WHERE c.Reg_date < '2022-01-01' AND i.Issued_cust IS NULL;

# 7) Display the branch numbers and the total count of employees in each branch

SELECT Branch_no, COUNT(*) AS Total_count FROM Employee
GROUP BY Branch_no;

# 8)  Display the names of customers who have issued books in the month of June 2023. 

SELECT c.Customer_name FROM Customer c
JOIN IssueStatus i ON c.Customer_Id = i.Issued_cust
WHERE MONTH(i.Issue_date) =6 AND YEAR(i.Issue_date) = 2023;

# 9) Retrieve book_title from book table containing history. 

SELECT Book_title FROM Books 
WHERE Category = 'History';

# 10) Retrieve the branch numbers along with the count of employees for branches having more than 5 employees 

SELECT Branch_no, COUNT(*) AS Employee_Count FROM Employee
GROUP BY Branch_no
HAVING COUNT(*) > 5;

# 11)  Retrieve the names of employees who manage branches and their respective branch addresses

SELECT e.Emp_name, b.Branch_address FROM Employee e 
JOIN Branch b ON e.Branch_no = b.Branch_no
WHERE e. Position= 'Manager';

# 12) Display the names of customers who have issued books with a rental price higher than Rs. 25.

SELECT c.Customer_name FROM Customer c
JOIN IssueStatus i ON c.Customer_Id = i.Issued_cust
JOIN Books b ON i.Isbn_book = b.ISBN
WHERE b.Rental_Price > 25;






