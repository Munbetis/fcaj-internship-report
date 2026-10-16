---
title: "Blog 1: Amazon DynamoDB"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AMAZON DYNAMODB

Amazon DynamoDB is a fully managed, serverless NoSQL database service provided by AWS. The service allows developers to store and retrieve data with low latency and supports scaling based on demand without requiring them to manage database servers.

In modern web applications, DynamoDB is often combined with AWS Lambda and Amazon API Gateway to build backends using a Serverless architecture.

For the Cloud Library Management System project, DynamoDB is proposed as the primary database for managing books, reader information, and borrowing and returning transactions.

### Key Points to Understand

- **Fully Managed:** AWS manages the infrastructure, data replication, and service availability.
- **NoSQL Database:** Stores data using key-value and document models without requiring all items to have identical attributes.
- **Table, Item, Attribute:** The three basic components used to organize data in DynamoDB.
- **Partition Key:** A primary key component used to determine how data is distributed and retrieved.
- **Sort Key:** An optional key combined with the Partition Key to organize multiple items sharing the same Partition Key.
- **CRUD Operations:** Supports creating, reading, updating, and deleting data through APIs.
- **Global Secondary Index (GSI):** Supports querying data using keys different from the table's primary key.
- **Conditional Writes and Transactions:** Help control update operations and support data consistency in business processes.

### Basic Components of DynamoDB

A DynamoDB table consists of multiple Items, and each Item contains Attributes.

For example, a Books table:

| bookId | title | category | availableCopies |
| --- | --- | --- | --- |
| BOOK001 | AWS Fundamentals | Cloud Computing | 3 |
| BOOK002 | Learning Python | Programming | 5 |
| BOOK003 | Introduction to AI | Artificial Intelligence | 2 |

In this example, `bookId` is used as the Partition Key to uniquely identify each book in the Books table.

In addition to a Partition Key, DynamoDB supports a Composite Primary Key consisting of a Partition Key and a Sort Key, which is suitable for organizing related data into groups.

### CRUD Operations in DynamoDB

DynamoDB provides the following basic operations:

- **PutItem:** Creates or writes an Item to a table.
- **GetItem:** Retrieves an Item using its primary key.
- **UpdateItem:** Updates the attributes of an Item.
- **DeleteItem:** Deletes an Item.
- **Query:** Retrieves data based on key conditions.
- **Scan:** Reads Items from a table or Index.

Choosing appropriate keys and designing efficient access patterns helps applications avoid unnecessary Scan operations.

### DynamoDB in an AWS Serverless Architecture

A common architecture using DynamoDB includes the following workflow:

1. Users interact with the web interface.
2. Amazon API Gateway receives API requests.
3. AWS Lambda processes business logic and checks access permissions.
4. Lambda retrieves or updates data in DynamoDB.
5. The results are returned to the user interface.

![DynamoDB Architecture in Cloud Library](/images/blogs/blog-1/dynamodb-architecture.svg)

### Practical Application in Cloud Library

Cloud Library Management System is a project aimed at developing a library management application on AWS.

DynamoDB is proposed for managing data groups such as Books, Readers, Loans, BookCopies, and Reservations.

For example, when a reader borrows a book:

- The system checks the number of available copies.
- The librarian confirms the book handover.
- AWS Lambda updates the borrowing record in DynamoDB.
- The number of available copies is reduced accordingly.

To minimize data inconsistencies when multiple requests occur simultaneously, the system can use DynamoDB Transactions combined with Condition Expressions.

For example, if 3 copies are available and one is successfully borrowed, the available quantity decreases to 2.

Therefore, DynamoDB not only stores catalog information but also supports the management of important business transactions.

### Conclusion

Amazon DynamoDB is a database service worth considering when developing NoSQL applications on AWS, especially systems using a Serverless architecture.

By learning about DynamoDB, I have gained an understanding of Tables, Items, Attributes, Primary Keys, CRUD operations, and how DynamoDB works together with AWS Lambda.

This knowledge provides a foundation for database design and business logic processing in the Cloud Library Management System project.

### Images

