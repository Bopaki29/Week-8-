# Week-8-

-- Library Management System SQL Schema
--
-- Author: [Your Name]
-- Date: [Insert Date]

-- ===============================
--  DROP existing tables if they exist (for reset purposes)

DROP TABLE IF EXISTS BookAuthors;
DROP TABLE IF EXISTS Borrowings;
DROP TABLE IF EXISTS Books;
DROP TABLE IF EXISTS Authors;
DROP TABLE IF EXISTS Members;


--  Table: Members

CREATE TABLE Members (
    memberID INT PRIMARY KEY AUTO_INCREMENT,
    fullName VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    phone VARCHAR(15),
    membershipDate DATE DEFAULT CURRENT_DATE
);


--  Table: Books

CREATE TABLE Books (
    bookID INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(150) NOT NULL,
    isbn VARCHAR(20) UNIQUE NOT NULL,
    publishedYear INT,
    availableCopies INT DEFAULT 1 CHECK (availableCopies >= 0)
);


--  Table: Authors

CREATE TABLE Authors (
    authorID INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL
);


--  Table: BookAuthors (Many-to-Many between Books and Authors)

CREATE TABLE BookAuthors (
    bookID INT,
    authorID INT,
    PRIMARY KEY (bookID, authorID),
    FOREIGN KEY (bookID) REFERENCES Books(bookID),
    FOREIGN KEY (authorID) REFERENCES Authors(authorID)
);


--Table: Borrowings (Many Members can borrow Many Books)

CREATE TABLE Borrowings (
    borrowingID INT PRIMARY KEY AUTO_INCREMENT,
    memberID INT,
    bookID INT,
    borrowDate DATE NOT NULL DEFAULT CURRENT_DATE,
    returnDate DATE,
    FOREIGN KEY (memberID) REFERENCES Members(memberID),
    FOREIGN KEY (bookID) REFERENCES Books(bookID)
);
