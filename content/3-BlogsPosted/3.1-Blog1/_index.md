---
title: "Blog 1: Amazon DynamoDB - Building a NoSQL Database on AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AMAZON DYNAMODB

## Building a NoSQL Database with Amazon DynamoDB and Its Application in Cloud Library

When developing a web application, the database is an essential component for storing, organizing, and retrieving information. In a library management system, data includes not only book titles and authors but also reader profiles, available book copies, borrowing and returning histories, and reservation requests.

One of the prominent database services offered by Amazon Web Services (AWS) is **Amazon DynamoDB**. It is a fully managed NoSQL database service designed to support applications that require fast data access and flexible scalability.

An important advantage is that developers do not need to manage database servers, install operating systems, or configure traditional database clusters. Instead, they can focus on data modeling and application development.

In this article, we will explore how DynamoDB works, its fundamental components, key design methods, CRUD operations, and its application to book management in the **Cloud Library Management System** project.

### Key Concepts to Understand

- **Fully Managed:** AWS manages the infrastructure and database service operations.
- **NoSQL:** Supports key-value and document data models.
- **Table, Item, Attribute:** Fundamental components for organizing data.
- **Partition Key and Sort Key:** Determine how records are identified and retrieved.
- **Global Secondary Index (GSI):** Supports additional query requirements.
- **CRUD Operations:** Create, read, update, and delete data.
- **Capacity Modes:** Allow users to choose between On-demand and Provisioned capacity.
- **Conditional Writes:** Update data only when specified conditions are satisfied.
- **Transactions:** Support updating multiple records using an all-or-nothing approach.
- **AWS Integration:** Can integrate with AWS Lambda, API Gateway, IAM, and many other AWS services.

### 1. Overview of Amazon DynamoDB

#### 1.1. What Is Amazon DynamoDB?

Amazon DynamoDB is a NoSQL database service provided by AWS, designed to support applications requiring low-latency data access and on-demand scalability.

Unlike relational databases such as MySQL or PostgreSQL, DynamoDB does not rely on relational table structures and traditional JOIN operations to handle every query requirement.

Instead, DynamoDB encourages developers to identify **Access Patterns**, which describe how an application needs to retrieve data, before designing appropriate keys and indexes.

For example, a library management system may need to support the following operations:

- Find book information using a book ID.
- Display all physical copies of a particular book.
- View a reader's borrowing history.
- Check the status of a borrowing record.
- Find pending reservation requests.

Each query requirement can influence the design of DynamoDB tables and indexes.

#### 1.2. Key Features

**No Server Management Required**

DynamoDB is a fully managed service. AWS is responsible for operating the database infrastructure, helping developers reduce system administration tasks.

**Scalability**

DynamoDB is designed to support large volumes of read and write operations, meeting the requirements of applications with changing numbers of users.

**High Availability**

Within an AWS Region, DynamoDB stores data across multiple Availability Zones to support availability and data durability.

**Flexible Data Model**

Items in the same table do not need to contain identical attributes, except for requirements related to the primary key.

**AWS Integration**

DynamoDB can be integrated with AWS Lambda for business logic processing, IAM for access management, and CloudWatch for operational monitoring.

#### 1.3. How Does DynamoDB Differ from SQL Databases?

| Criteria | DynamoDB | Relational Database |
| --- | --- | --- |
| Data model | NoSQL, key-value and document | Relational tables |
| Querying | Primarily based on keys and indexes | SQL |
| JOIN operations | Does not support SQL-style JOINs | Supports JOINs |
| Design approach | Prioritizes Access Patterns | Typically based on data relationships |
| Operations | Fully managed by AWS | Depends on the system and service used |
| Suitable for | Key-based queries and scalable applications | Relational business logic and complex queries |

No database type is suitable for every system. The choice depends on data structure, query requirements, and application characteristics.

### 2. Data Structure in DynamoDB

#### 2.1. Table, Item, and Attribute

DynamoDB uses three fundamental components:

| Component | Description | Example |
| --- | --- | --- |
| **Table** | A collection of Items. | Books |
| **Item** | An individual data record. | Book BOOK001 |
| **Attribute** | A property of an Item. | title, author, availableCopies |

For example, an Item in the `Books` table:

```json
{
  "bookId": "BOOK001",
  "title": "AWS Fundamentals",
  "author": "Example Author",
  "category": "Cloud Computing",
  "totalCopies": 3,
  "availableCopies": 2,
  "status": "ACTIVE"
}
```

In this example:

- `bookId`: Unique identifier of a book title.
- `title`: Book title.
- `author`: Author's name.
- `category`: Book category.
- `totalCopies`: Total number of physical copies.
- `availableCopies`: Number of copies currently available for borrowing.
- `status`: Availability or circulation status.

*The data above is only an example illustrating how an Item can be organized in DynamoDB.*

#### 2.2. Partition Key

A Partition Key is a required component of a Primary Key.

DynamoDB uses the Partition Key value to determine how data is distributed. When a table uses only a Partition Key, the key value must uniquely identify an Item.

For example, the `Books` table uses `bookId` as its Partition Key:

| bookId | title | availableCopies |
| --- | --- | --- |
| BOOK001 | AWS Fundamentals | 2 |
| BOOK002 | Learning Python | 5 |
| BOOK003 | Introduction to AI | 3 |

The application can use `GetItem` with `bookId = BOOK001` to retrieve the corresponding book information.

#### 2.3. Sort Key

A Sort Key is an optional component of a Primary Key.

When a table uses both a Partition Key and a Sort Key, the combination of these two values uniquely identifies an Item.

For example, the `BookCopies` table can be designed as follows:

| bookId (PK) | copyId (SK) | status |
| --- | --- | --- |
| BOOK001 | COPY001 | AVAILABLE |
| BOOK001 | COPY002 | BORROWED |
| BOOK001 | COPY003 | AVAILABLE |

With this structure, the application can use `Query` to retrieve all physical copies associated with `BOOK001`.

#### 2.4. Global Secondary Index (GSI)

In real-world applications, not every query uses a table's primary key.

For example, suppose the `Loans` table uses `loanId` as its Partition Key. This design makes it convenient to retrieve a borrowing record by its ID, but it does not directly support viewing a reader's entire borrowing history.

One solution is to create a Global Secondary Index (GSI), such as:

- GSI Partition Key: `readerId`.
- GSI Sort Key: `borrowDate`.

The application can then query borrowing records belonging to the same reader through this index.

However, data read from a GSI uses **Eventually Consistent Reads**, meaning it may not immediately reflect a recently completed update.

#### 2.5. Example Data Model

![Example DynamoDB data model for Books and Loans](/images/blogs/blog-1/dynamodb-data-model.svg)

The diagram illustrates two data groups in Cloud Library:

- `Books`: Manages book information and copy quantities.
- `Loans`: Tracks borrowing and returning transactions.

The keys and indexes shown in the diagram are design examples and do not represent the final database structure of the project.

### 3. CRUD Operations in DynamoDB

CRUD refers to four fundamental groups of database operations.

| Operation | Function | DynamoDB API |
| --- | --- | --- |
| **Create** | Add a new record | PutItem |
| **Read** | Retrieve data | GetItem, Query, Scan |
| **Update** | Modify a record | UpdateItem |
| **Delete** | Remove a record | DeleteItem |

#### 3.1. Create - Adding Data

When a librarian adds a new book title, the application needs to create a corresponding record in DynamoDB.

For example:

```json
{
  "bookId": "BOOK004",
  "title": "Cloud Computing Basics",
  "author": "Example Author",
  "category": "Cloud Computing",
  "totalCopies": 5,
  "availableCopies": 5
}
```

DynamoDB provides the `PutItem` operation to write an Item to a table.

It is important to note that PutItem can overwrite an existing Item with the same primary key. Therefore, the application can use a Condition Expression to allow creation only when the Item does not already exist.

#### 3.2. Read - Retrieving Data

DynamoDB provides several methods for reading data:

**GetItem**

Retrieves an Item using its complete Primary Key.

Example: Find a book with the ID `BOOK001`.

**Query**

Retrieves Items based on key conditions defined on a table or index.

Example: View all physical copies associated with a particular `bookId`.

**Scan**

Reads Items from a table or index. For large tables, Scan can consume significant resources because it may need to read many Items.

When designing real applications, developers should prioritize Access Patterns that can be served by GetItem and Query.

#### 3.3. Update - Modifying Data

Suppose a book title has 3 available copies.

After a librarian confirms that one copy has been borrowed, the system needs to reduce the available quantity from 3 to 2.

DynamoDB provides `UpdateItem` to modify specific attributes without rewriting the entire Item.

For quantity updates, conditional checks should be used to prevent the number of available copies from becoming negative.

#### 3.4. Delete - Removing Data

`DeleteItem` allows an Item to be deleted using its primary key.

However, in a library management system, removing a book from circulation does not always mean its database record should be permanently deleted.

For example, a book with an existing borrowing history can be marked as `INACTIVE` so that its information remains available for management and historical reference.

### 4. Hands-on Guide to DynamoDB

This section illustrates how to create a table, add data, and perform basic operations using the AWS Management Console.

#### Step 1: Access Amazon DynamoDB

1. Sign in to the AWS Management Console.
2. Search for the `DynamoDB` service.
3. Select `Tables`.
4. Click `Create table`.

#### Step 2: Create the Books Table

Use the following example configuration:

| Setting | Value |
| --- | --- |
| Table name | Books |
| Partition key | bookId |
| Key type | String |
| Sort key | Not used |
| Capacity mode | On-demand |

With On-demand mode, DynamoDB manages throughput according to demand and charges based on read and write activity, along with other applicable billing components.

This mode is convenient for experimentation when traffic is unpredictable, but it does not mean the service is completely free.

After reviewing the configuration, select `Create table` and wait until the table reaches the `Active` status.

#### Step 3: Add Sample Data

On the `Books` table management page:

1. Select `Explore table items`.
2. Select `Create item`.
3. Enter `bookId = BOOK001`.
4. Add attributes such as `title`, `category`, `totalCopies`, and `availableCopies`.
5. Save the Item.

Example:

```json
{
  "bookId": "BOOK001",
  "title": "AWS Fundamentals",
  "category": "Cloud Computing",
  "totalCopies": 3,
  "availableCopies": 3
}
```

#### Step 4: Read and Update Data

After creating the Item, use the DynamoDB interface to retrieve the record using its key.

Next, try updating `availableCopies` from 3 to 2 and check the result.

In real applications, these operations are usually performed using an AWS SDK rather than manually editing records in the AWS Console.

#### Step 5: Example Using AWS SDK with Node.js

AWS SDK for JavaScript v3 supports DynamoDB operations in Node.js applications.

Install the required packages:

```bash
npm install @aws-sdk/client-dynamodb @aws-sdk/lib-dynamodb
```

The following example uses `UpdateCommand` to decrease the number of available book copies:

```javascript
import { DynamoDBClient } from "@aws-sdk/client-dynamodb";
import {
  DynamoDBDocumentClient,
  UpdateCommand
} from "@aws-sdk/lib-dynamodb";

const client = new DynamoDBClient({
  region: "ap-southeast-1"
});

const db = DynamoDBDocumentClient.from(client);

const result = await db.send(
  new UpdateCommand({
    TableName: "Books",
    Key: {
      bookId: "BOOK001"
    },
    UpdateExpression:
      "SET availableCopies = availableCopies - :one",
    ConditionExpression:
      "attribute_exists(bookId) AND availableCopies >= :one",
    ExpressionAttributeValues: {
      ":one": 1
    },
    ReturnValues: "ALL_NEW"
  })
);

console.log(result.Attributes);
```

**Explanation:**

- `TableName`: Specifies the table to update.
- `Key`: Identifies the Item using its Primary Key.
- `UpdateExpression`: Decreases the number of available copies by one.
- `ConditionExpression`: Allows the update only when the Item exists and at least one copy is available.
- `ExpressionAttributeValues`: Provides values for the expression.
- `ReturnValues`: Returns the updated data after a successful operation.

This example assumes that the Books table already exists, the AWS Region is correct, and the execution environment has the required credentials and access permissions.

**Note:** This example only demonstrates updating one Item. It does not represent the complete borrowing process because the system must also create a borrowing record and update the status of individual book copies.

After completing the hands-on exercise, review and remove unnecessary test resources to avoid unexpected charges.

### 5. Integrating DynamoDB with AWS Serverless

One approach to using DynamoDB is to combine it with Amazon API Gateway and AWS Lambda to build a Serverless backend.

In this architecture, the frontend does not directly use AWS credentials to read or modify the database.

Instead, requests are sent to the backend for authorization checks and business logic processing.

#### Proposed Architecture Diagram

![AWS Serverless and DynamoDB architecture in Cloud Library](/images/3-Blogs/Blogs1/dynamodb-data-model.png)

#### Workflow

1. The user signs in through Amazon Cognito.
2. The React frontend sends a request to Amazon API Gateway.
3. API Gateway validates the authentication token according to its configuration.
4. AWS Lambda receives and processes the request.
5. Lambda checks the user's business-level permissions.
6. Lambda reads or updates data in Amazon DynamoDB.
7. The result is returned to the frontend.

#### Roles of Each Service

| Service | Role |
| --- | --- |
| **React** | Builds the web interface. |
| **Amazon Cognito** | Authenticates users and manages user identities. |
| **Amazon API Gateway** | Receives API requests and supports authentication. |
| **AWS Lambda** | Processes business logic and checks access permissions. |
| **Amazon DynamoDB** | Stores and retrieves business data. |
| **AWS IAM** | Grants Lambda permission to access DynamoDB. |

To access DynamoDB, Lambda can use an IAM Execution Role with the required permissions.

This approach helps avoid storing AWS Access Keys directly in the application's source code.

### 6. Applying DynamoDB to Cloud Library Management System

#### 6.1. Problem Overview

Cloud Library Management System is a project that aims to build a library management application on AWS, combining book management, reader management, borrowing and returning transactions, and an AI assistant.

In the proposed architecture, DynamoDB serves as the primary business database.

The system needs to manage the following data groups:

| Data Group | Function |
| --- | --- |
| **Books** | Stores book information and quantities. |
| **Readers** | Manages reader profiles. |
| **Loans** | Stores borrowing records, due dates, and fines. |
| **BookCopies** | Tracks individual physical book copies. |
| **Reservations** | Manages reservations and waiting queues. |
| **Favorites** | Stores readers' favorite book lists. |
| **Notifications** | Manages notifications. |

These are business data groups from the project proposal and do not necessarily correspond to seven physical DynamoDB tables.

The team can choose either a multi-table model or Single-table Design depending on actual Access Patterns.

#### 6.2. Book Quantity Management Problem

Suppose the library has a book title with:

- Book ID: `BOOK001`.
- Total copies: 3.
- Available copies: 3.
- A reader submits a borrowing request.

When the librarian confirms the handover of a book, the system needs to:

1. Check the reader's borrowing limit.
2. Verify that a copy is available.
3. Identify the physical copy being borrowed.
4. Create or update the borrowing record.
5. Update the book copy's status.
6. Decrease the number of available copies from 3 to 2.

If these updates are not coordinated correctly, data inconsistencies may occur.

For example, two simultaneous requests might both read an available quantity of 1. Without proper write conditions, both requests could be accepted even though only one copy remains.

#### 6.3. Using Conditional Writes and Transactions

DynamoDB provides Condition Expressions to evaluate conditions before updating an Item.

For example:

```text
availableCopies >= 1
```

This condition can help prevent the available quantity from decreasing when no copies remain.

However, a borrowing transaction may involve multiple Items, such as:

- An Item in Books.
- An Item in BookCopies.
- An Item in Loans.

To coordinate these updates, DynamoDB supports `TransactWriteItems`.

Operations within a transaction follow an important principle:

**Either all operations succeed, or none of them are applied.**

For Cloud Library, a proposed transaction may include:

1. Check and decrease `availableCopies`, provided at least one copy remains.
2. Update the physical book copy's status from `AVAILABLE` to `BORROWED`.
3. Create a borrowing record in `Loans`, provided the loan ID does not already exist.

If any condition is not satisfied, the transaction is not completed.

In addition, the backend needs to implement duplicate-processing prevention and borrowing-limit checks to enforce business rules correctly.

#### 6.4. Book Return Process

When a reader returns a book, the librarian confirms the return through the system.

The backend needs to:

1. Check that the borrowing record is still in the `BORROWED` status.
2. Determine the actual return date.
3. Calculate a fine if the book is overdue.
4. Update the borrowing record's status to `RETURNED`.
5. Update the physical book copy's status to `AVAILABLE`.
6. Increase the number of available copies.

For example, if the available quantity is 2 and one book copy is successfully returned, the available quantity increases to 3.

Appropriate conditions should be used to prevent the same return transaction from being processed multiple times.

#### 6.5. Why Is Database Design Important?

In Cloud Library, successfully storing data is not enough.

The system must also ensure that:

- Books cannot be borrowed beyond the actual available quantity.
- Borrowing records are not updated to incorrect statuses.
- Book quantities are not increased multiple times when a return operation is repeated.
- Readers cannot access other readers' borrowing transactions.
- Search and query operations support actual application requirements.

Therefore, DynamoDB database design must be developed alongside business logic and application authorization.

### 7. Security, Performance, and Cost Optimization

#### 7.1. Data Security

Important security practices when using DynamoDB include:

- Use AWS IAM to control access permissions.
- Apply the Principle of Least Privilege.
- Do not store AWS Access Keys directly in source code.
- Grant Lambda access only to the required tables and actions.
- Verify data ownership in the backend.
- Use Amazon Cognito to support application user authentication.

#### 7.2. Efficient Query Design

Important Access Patterns should be clearly identified, such as:

- Find a book using `bookId`.
- Retrieve a borrowing record using `loanId`.
- View borrowing history using `readerId`.
- Find physical copies belonging to a particular book.

Appropriate primary keys and GSIs can then be selected.

Designing for frequently used queries helps reduce unnecessary read operations.

#### 7.3. On-demand and Provisioned Capacity

DynamoDB supports two main throughput capacity modes:

| Mode | Description |
| --- | --- |
| **On-demand** | Automatically adjusts throughput to demand and charges based on usage. |
| **Provisioned** | Allows read and write throughput to be configured, which is suitable when workloads can be predicted. |

For experimental applications with unpredictable traffic, On-demand is often a convenient choice.

For applications with stable and predictable workloads, Provisioned capacity may be suitable for cost optimization.

Actual costs also depend on data storage, indexes, transactions, and additional features being used.

#### 7.4. Implementation Considerations

- Avoid excessive use of Scan on large tables.
- Consider the read/write capacity consumption of GSIs.
- Use Conditional Writes for important updates.
- Use Transactions when coordinating changes to multiple Items.
- Monitor errors and usage with Amazon CloudWatch.
- Set up AWS budget alerts.
- Test the application with concurrent requests.
- Check application behavior when queries do not immediately reflect recent updates.

### 8. Conclusion

Amazon DynamoDB is an important NoSQL database service within the AWS ecosystem and is suitable for many applications built using Serverless architectures.

Through studying DynamoDB, I have gained a better understanding of Table, Item, Attribute, Partition Key, Sort Key, Global Secondary Index, and basic CRUD operations.

Beyond data storage, DynamoDB also provides Conditional Writes and Transactions to support business operations that require data accuracy.

For the **Cloud Library Management System** project, these concepts can be applied to designing book, reader, and borrowing data while reducing the risk of incorrect book quantities when multiple requests are processed.

The most important lesson is that when building a NoSQL database, developers must consider not only data structures but also query requirements, business rules, security, and operating costs.