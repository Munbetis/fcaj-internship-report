---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Library Management System

## An AWS Serverless Library Management Solution Integrated with an AI Assistant

### 1. Executive Summary

**Cloud Library Management System** is a project aimed at developing an online library management system for schools or organizations, using a Serverless architecture on Amazon Web Services (AWS).

The project aims to build a centralized platform for managing book catalogs, individual book copies, reader profiles, and borrowing and returning transactions. The system supports book searches, checking available copies, submitting borrowing requests, reservations, renewals, and tracking due dates and fines.

In addition to library management functions, the system integrates an AI assistant using **Amazon Bedrock** and **Amazon Bedrock Knowledge Bases**. The AI assistant helps readers ask questions about library regulations and find books based on their needs using approved documents.

The solution uses **React** to build the user interface, **Node.js on AWS Lambda** for business logic processing, **Amazon API Gateway** to provide APIs, **Amazon Cognito** for authentication and authorization, and **Amazon DynamoDB** as the primary database.

Applying an AWS Serverless architecture helps reduce server management tasks, supports the automation of business processes, and provides a foundation for future system expansion.

### 2. Problem Statement

#### Current Problems

Library management requires tracking various types of information, such as book catalogs, the number of individual book copies, reader profiles, borrowing and returning status, due dates, and fines.

When this information is managed separately or updated manually, searching for information and processing business operations can become complicated. Librarians need to check book availability, monitor borrowing requests, confirm book handovers and returns, and accurately update data.

For readers, finding suitable books, checking library regulations, tracking due dates, or submitting renewal requests also needs to be more convenient.

In addition, libraries need to ensure data accuracy, prevent borrowing beyond the available number of book copies, and control access permissions for different user groups.

#### The Solution

Cloud Library Management System proposes a centralized web-based library management application that combines AWS Serverless services with an AI assistant.

The main functions include:

- **Book Management:** Add, update, discontinue circulation of books, and manage individual book copies.
- **Reader Management:** Store user profiles and manage information related to library activities.
- **Book Search:** Search the catalog, view book details, and check the number of available copies.
- **Borrowing and Returning Management:** Submit borrowing requests, confirm book handovers and returns, and track borrowing history and due dates.
- **Reservations and Waiting Lists:** Allow readers to reserve books when no copies are available.
- **Online Renewals:** Submit and process renewal requests according to library regulations.
- **Fine Management:** Calculate fines when readers return books after their due dates.
- **Notifications:** Send due-date reminder emails and notifications about reserved books.
- **AI Assistant:** Answer questions about library regulations and find books based on user needs.

The system is designed with four user groups:

| Role | Main Functions | Permission Scope |
| --- | --- | --- |
| **Guest** | View the public catalog, book details, and register an account. | Must log in before submitting borrowing requests or using the AI assistant. |
| **Reader** | Update profiles, search for books, use AI, save favorite books, borrow, reserve, renew, and view borrowing history. | Can only access their own profile and transactions. |
| **Librarian** | Manage books and readers, approve borrowing and renewal requests, confirm returns, and handle waiting lists and fines. | Handles library operations without independently administering the system. |
| **Administrator (Admin)** | Manage accounts, roles, library regulations, AI documents, and summary reports. | Administers the system; requires an additional librarian role to directly process book handovers and returns. |

Newly registered users are assigned the Reader role. Librarian and Admin permissions are managed through groups in Amazon Cognito. A single account may have multiple roles.

#### Benefits and Return on Investment (ROI)

**Centralized Management**

- Manage book, reader, and transaction data on a unified platform.
- Reduce difficulties in searching for and verifying information.
- Help librarians monitor book availability and borrowing and returning requests.

**Improved User Experience**

- Readers can search for books and submit requests online.
- Track due dates, fines, and borrowing history.
- Receive notifications about due dates or reserved books.

**Application of Artificial Intelligence**

- Assist in answering questions about library regulations.
- Search for books that match readers' learning needs.
- Provide reference sources when answering questions based on library documents.

**Operational Optimization**

- Use Serverless architecture to reduce server management tasks.
- Support the automation of due-date checks and notification delivery.
- Establish a foundation for expanding system functions in the future.

**Return on Investment (ROI)**

The project currently does not have quantitative data on implementation costs, time savings, or revenue to calculate ROI.

The team will evaluate operating costs and system benefits after determining AWS configurations, usage workloads, and testing results.

### 3. Solution Architecture

Cloud Library Management System uses an **AWS Serverless architecture**, in which the frontend, backend, database, and AI assistant are connected through AWS services.

The frontend application is built with React. After logging in through Amazon Cognito, users send requests from the interface to Amazon API Gateway.

API Gateway validates access tokens and forwards requests to AWS Lambda. Lambda processes business logic, checks user permissions, and performs data operations in Amazon DynamoDB.

For requests related to the AI assistant, Lambda queries Amazon Bedrock Knowledge Bases and invokes an AI model on Amazon Bedrock to generate responses.

Knowledge Bases uses approved documents stored in Amazon S3 and creates indexes to support information retrieval from a vector store.

Amazon S3 Vectors is the proposed solution for storing vector indexes when the service is supported in the deployment AWS Region.

Frequently changing data, such as the number of available book copies, due dates, and fines, must be retrieved from Amazon DynamoDB rather than relying solely on the AI model's responses.

#### System Architecture Diagram

*Add the AWS architecture diagram of Cloud Library Management System after the team completes the design.*

#### AWS Services Used

| AWS Service | Role in the System |
| --- | --- |
| **Amazon Cognito** | Authenticates users and manages accounts and permission groups for Readers, Librarians, and Admins. |
| **Amazon API Gateway** | Provides APIs and validates access tokens. |
| **AWS Lambda** | Processes business logic, checks permissions, and coordinates AI requests. |
| **Amazon DynamoDB** | Serves as the primary database, storing books, readers, book copies, and borrowing and returning transactions. |
| **Amazon S3** | Stores book cover images and source documents for the AI assistant. |
| **Amazon CloudFront** | Distributes the React frontend application. |
| **Amazon Bedrock** | Provides AI models to generate responses for users. |
| **Amazon Bedrock Knowledge Bases** | Retrieves library regulations, FAQs, and book descriptions from approved source documents. |
| **Amazon S3 Vectors** | Stores vector indexes for Knowledge Bases as part of the proposed solution. |
| **Amazon EventBridge Scheduler** | Triggers scheduled tasks to check due dates and waiting lists. |
| **Amazon SES** | Sends due-date reminder emails and notifications when reserved books become available. |
| **Amazon CloudWatch** | Monitors errors and system activities. |
| **AWS IAM** | Manages access permissions between AWS services. |

#### Component Design

**Frontend - React, Node.js**

- Provides web interfaces for different user groups.
- Displays book catalogs and information.
- Supports searching, submitting borrowing requests, reservations, and renewals.
- Provides management interfaces for Librarians and Admins.
- Connects to the backend through Amazon API Gateway.

**Backend - Node.js, AWS Lambda, and API Gateway**

- Receives and processes requests from the frontend.
- Checks user roles and access permissions.
- Handles book and reader management operations.
- Processes borrowing, returning, reservation, and renewal workflows.
- Calculates due dates and fines.
- Retrieves and updates data in Amazon DynamoDB.
- Coordinates requests to the AI assistant.

**Authentication and Authorization - Amazon Cognito**

- Manages account registration and login.
- Uses permission groups to distinguish Readers, Librarians, and Admins.
- Provides authentication tokens for API requests.
- Prevents users from assigning themselves Admin or Librarian permissions during registration.

**Database - Amazon DynamoDB**

- Stores the library system's business data.
- Manages book information and the number of book copies.
- Stores reader profiles.
- Tracks borrowing and returning records.
- Manages reservations, waiting lists, and notifications.
- Supports conditional updates to ensure data accuracy.

**AI Assistant - Amazon Bedrock**

- Supports answering questions about library regulations.
- Searches for books based on user needs.
- Uses Knowledge Bases to retrieve source documents.
- Combines current data from DynamoDB to display book availability.

**Storage - Amazon S3**

- Stores book cover images.
- Stores library regulations, FAQs, and book descriptions.
- Provides input documents for Knowledge Bases.

**Automation and Notifications**

- EventBridge Scheduler triggers Lambda on a schedule.
- Lambda checks upcoming due dates, overdue loans, and waiting lists.
- Amazon SES sends notification emails to users.

#### Database Design with Amazon DynamoDB

The system uses **Amazon DynamoDB as the primary database** to manage business data.

DynamoDB is an AWS-managed NoSQL database service suitable for the Serverless architecture of Cloud Library Management System.

The frontend does not access DynamoDB directly. Data reading, writing, and updating operations are performed through API Gateway and AWS Lambda after access permissions have been verified.

**Main Data Groups**

| Data Group | Proposed Data Fields | Function |
| --- | --- | --- |
| **Books** | bookId, title, author, category, totalCopies, availableCopies, coverImageKey | Manages the book catalog, book information, and quantities. |
| **Readers** | cognitoSub, fullName, studentId | Manages reader profiles. |
| **Loans** | loanId, readerId, bookId, copyId, borrowDate, dueDate, returnDate, status, fineAmount, renewalCount | Manages borrowing records, due dates, renewals, and fines. |
| **BookCopies** | copyId, bookId, qrCode, status | Tracks individual physical book copies. |
| **Reservations** | reservationId, readerId, bookId, queuePosition, holdUntil | Manages reservations and waiting lists. |
| **Favorites** | readerId, bookId | Stores readers' favorite book lists. |
| **Notifications** | notificationId, recipientId, type, status | Tracks notifications sent to users. |

*The field names in the table above are proposed representations based on the project documentation. Table design, Partition Keys, Sort Keys, and query indexes will be determined when the database design is finalized.*

**Division of Data Storage Responsibilities**

- **Amazon DynamoDB:** Stores the library's business data.
- **Amazon Cognito:** Manages login information and user identities.
- **Amazon S3:** Stores book cover images and documents used by the AI assistant.
- **Amazon Bedrock Knowledge Bases:** Retrieves content from approved source documents.

**Data Storage Workflow When Borrowing Books**

1. A reader submits a borrowing request through the React interface.
2. API Gateway receives the request and authenticates the user.
3. AWS Lambda checks the number of books currently borrowed, borrowing limits, and book availability.
4. The librarian confirms the book handover.
5. Lambda uses a conditional transaction in DynamoDB to create or update the borrowing record and decrease the number of available copies.
6. The system updates the transaction status so the reader can track it.

**Data Update Workflow When Returning Books**

1. The librarian confirms receipt of the returned book.
2. Lambda checks the borrowing record's status.
3. The system calculates the fine if the book is returned after its due date.
4. DynamoDB updates the borrowing record's status and increases the number of available copies.
5. The return confirmation operation is processed only once to prevent duplicate increases in book quantities.

**Ensuring Data Consistency and Security**

- Use transactions and conditions in DynamoDB to prevent borrowing beyond the available quantity.
- Check transaction status before updating data.
- Prevent readers from accessing other users' profiles or borrowing records.
- Verify access permissions in the backend.
- Grant DynamoDB access permissions to Lambda according to the principle of least privilege.

### 4. Technical Implementation

#### Implementation Phases

The project is organized into four proposed implementation phases.

**Phase 1: Research and Architecture Design**

- Analyze requirements and identify system functions.
- Identify user groups and access permissions.
- Research suitable AWS services.
- Design the Serverless architecture.
- Design data groups using Amazon DynamoDB.
- Define business rules for book management, borrowing, returning, renewals, and fines.

**Phase 2: Developing Business Functions**

- Build the user interface with React.
- Set up Amazon Cognito.
- Develop API Gateway and AWS Lambda functions.
- Set up the Amazon DynamoDB database.
- Develop book and reader management functions.
- Develop borrowing and returning workflows and fine calculations.

**Phase 3: Integrating AI and Additional Features**

- Prepare library regulations, FAQs, and book descriptions.
- Store source documents in Amazon S3.
- Configure Amazon Bedrock Knowledge Bases.
- Integrate the AI assistant for answering regulation-related questions and finding books.
- Develop reservations, waiting lists, and renewals.
- Set up the due-date reminder system.

**Phase 4: Testing and Deployment**

- Test business functions.
- Verify access permissions by user role.
- Test data consistency in DynamoDB.
- Verify the AI assistant's retrieval results.
- Monitor AWS errors and costs.
- Deploy the application and prepare the demo.

#### Technical Requirements

**User Interface**

- React.
- Connect to the backend through API Gateway.
- Support interfaces appropriate for each permission group.

**Business Logic Processing**

- Node.js.
- AWS Lambda.
- Amazon API Gateway.
- Authentication and authorization checks through Amazon Cognito.

**Database**

- Amazon DynamoDB.
- Store book, reader, and library transaction data.
- Support data queries according to business requirements.
- Use conditional transactions for important update operations.

**AI Assistant**

- Amazon Bedrock.
- Amazon Bedrock Knowledge Bases.
- Amazon S3.
- A vector store for retrieval data.
- Amazon S3 Vectors as the proposed solution when supported in the deployment Region.

**Notifications and Monitoring**

- Amazon EventBridge Scheduler.
- Amazon SES.
- Amazon CloudWatch.
- AWS IAM.

**Business Rules**

| Rule | Value Applied to the Demo |
| --- | --- |
| Maximum number of borrowed books | 3 books per reader |
| Borrowing period | 14 days |
| Overdue fine | 5,000 VND/day |
| Maximum number of renewals | 1 time |
| Renewal period | Additional 7 days |
| Reservation holding period | 48 hours |
| Time zone for due-date calculations | Vietnam |

Readers may only renew a loan if it is not overdue and no one else has reserved the book.

Fines are calculated by the backend based on the number of overdue days. For books that have not yet been returned, the fine amount is displayed as a provisional calculation.

### 5. Timeline & Milestones

#### Project Timeline

The project is proposed to be implemented according to the following milestones:

| Phase | Activities | Expected Results |
| --- | --- | --- |
| **1. Analysis and Design** | Define requirements, design the AWS architecture, and design DynamoDB data structures. | Requirements documentation, architecture diagram, and data design. |
| **2. Core Function Development** | Develop React, Cognito, API Gateway, Lambda, and DynamoDB components. | Basic book, reader, and borrowing and returning management system. |
| **3. AI and Feature Integration** | Integrate Bedrock, Knowledge Bases, reservations, renewals, and notifications. | Priority AI functions and additional features. |
| **4. Testing and Deployment** | Test business operations, access permissions, and deploy the application. | Functional website and demo scenarios. |

*The specific timeline for each phase will be added after the team finalizes the implementation plan.*

**Priority Features**

- Login and authorization.
- Book and reader management.
- Book search.
- Borrowing and returning request management.
- History tracking and fine calculation.
- AI-based answers to library regulation questions.
- AI-powered book search based on user needs.
- Reservations and waiting lists.
- Online renewals.
- Due-date reminders.

**Extended Features**

- AI-generated book introductions and summaries.
- AI-powered reading path recommendations.
- QR code or barcode scanning.
- Favorite book lists.
- Advanced statistics dashboard.
- Online fine payments.

### 6. Budget Estimation

The project uses AWS Serverless services; therefore, operating costs depend on actual usage workloads.

A budget estimate can be prepared using the [AWS Pricing Calculator](https://calculator.aws/).

#### Infrastructure Costs

| AWS Service | Factors Affecting Costs |
| --- | --- |
| **Amazon Cognito** | Number of users and authentication activities. |
| **Amazon API Gateway** | Number of API requests. |
| **AWS Lambda** | Number of executions, execution duration, and memory allocation. |
| **Amazon DynamoDB** | Data storage capacity, read/write operations, and usage configuration. |
| **Amazon S3** | Storage capacity for book cover images and AI documents. |
| **Amazon CloudFront** | Content delivery traffic. |
| **Amazon Bedrock** | Selected AI model and usage volume. |
| **Bedrock Knowledge Bases** | Data retrieval and synchronization activities. |
| **Amazon S3 Vectors** | Vector storage capacity and query activities. |
| **EventBridge Scheduler** | Number of scheduled tasks. |
| **Amazon SES** | Number of emails sent. |
| **Amazon CloudWatch** | Log storage capacity and monitoring activities. |

**Estimated Total Cost:** Not yet determined.

The team will need to select an AWS Region, configure services, and estimate the number of users, books, API requests, and AI requests to prepare a cost estimate.

#### Cost Control Measures

- Set up budget alerts on AWS.
- Monitor costs generated by Amazon Bedrock.
- Limit the frequency of requests sent to the AI assistant.
- Limit the model's output length.
- Monitor the usage of application services.
- Configure log retention periods in CloudWatch.

### 7. Risk Assessment

#### Risk Matrix

| Risk | Potential Impact | Mitigation Measures |
| --- | --- | --- |
| **AWS Budget Overruns** | Operating costs increase beyond expectations. | Monitor costs and configure budget alerts. |
| **Unauthorized Access** | Users view or modify data without permission. | Use Cognito, IAM, and permission checks in Lambda. |
| **Incorrect Book Quantities** | More books may be borrowed than the number of available copies. | Use transactions and conditions in DynamoDB. |
| **Duplicate Transaction Updates** | Incorrect book quantities or borrowing record statuses. | Ensure return confirmation operations are processed only once. |
| **Inaccurate AI Responses** | Readers receive inappropriate or incorrect information. | Use approved documents and verify business data. |
| **Duplicate Notifications** | Users receive multiple identical notifications. | Store notification statuses and check before sending. |
| **AWS Service Failures** | Some functions cannot process requests. | Monitor errors using CloudWatch and develop recovery procedures. |

#### Mitigation Strategies

**Security and Authorization**

- Apply the Least Privilege principle in AWS IAM.
- Verify user roles and data ownership for each API.
- Restrict access to Amazon S3.
- Record logs when roles or system regulations are changed.

**Ensuring Data Accuracy**

- Use DynamoDB transactions and condition expressions for important updates.
- Check the number of available copies before confirming a loan.
- Prevent borrowing beyond the allowed limit.
- Verify borrowing record status before confirming a return.
- Ensure return operations are not processed repeatedly.

**AI Assistant Control**

- Use only approved documents.
- Resynchronize Knowledge Bases when source documents change.
- Provide reference sources for responses about library regulations.
- Retrieve book availability and fine information from the business system.
- Indicate when insufficient information is available if no suitable source is found.

**Operational Monitoring**

- Use CloudWatch to monitor errors and processing times.
- Control AWS service usage costs.
- Configure log retention periods.

#### Contingency Plans

The team needs to further develop contingency procedures during implementation and testing.

Situations to consider include:

- Connection interruptions or API failures.
- Unsuccessful data update operations.
- Failure to send system notifications.
- The AI assistant being unable to find suitable documents.
- AWS costs exceeding the expected budget.

For important transactions, the system must return clear error statuses and prevent partial data updates when operations fail.

### 8. Expected Outcomes

#### Technical Improvements

The project aims to develop a web-based library management application on AWS, integrating business management functions and an AI assistant.

**Expected Technical Outcomes:**

- Build an online library management system.
- Use Amazon Cognito for user authentication and authorization.
- Develop a Serverless backend with Amazon API Gateway and AWS Lambda.
- Use Amazon DynamoDB as the primary database.
- Manage book catalogs, individual book copies, and reader profiles.
- Process borrowing and returning transactions and calculate fines.
- Support reservations, waiting lists, and renewals.
- Send due-date reminder notifications.
- Integrate an AI assistant for answering library regulation questions and searching for books.
- Use Amazon CloudWatch to monitor system activities.

#### Proposed Demo Scenarios

**Step 1: Account and Book Management**

The Admin assigns the Librarian role and configures library regulations.

The Librarian adds a book title with 3 copies, a cover image, and a description for the AI assistant.

**Step 2: AI-Powered Book Search**

A reader asks the AI assistant about suitable books for learning AWS and about library regulations.

The system displays results based on the book catalog, reference sources, and the number of available copies.

**Step 3: Borrowing Books**

The reader submits a borrowing request.

The Librarian hands over the book and confirms the transaction.

The number of available copies in DynamoDB decreases from 3 to 2. The reader can track the due date and borrowing history.

**Step 4: Reservations, Renewals, and Fines**

The system demonstrates the reservation or renewal function.

Due-date reminder emails are sent according to the workflow.

A borrowing record that is 4 days overdue is used to demonstrate the fine:

**4 days × 5,000 VND = 20,000 VND.**

**Step 5: Returning Books and Security Verification**

The Librarian confirms the book return.

DynamoDB updates the borrowing record's status and increases the number of available copies from 2 to 3.

The system logs are checked, and a Reader account is used to attempt access to an administrative API to verify that the request is denied.

#### Long-term Value

Cloud Library Management System can be expanded to meet additional library management needs in the future.

Potential development directions include:

- AI-generated summaries of book descriptions and provided documents.
- AI-powered reading path recommendations based on learning objectives.
- Book copy management using QR codes or barcodes.
- Favorite book lists.
- Advanced statistics dashboards.
- Online fine payments.

**Expected Deliverables:**

- A library management web application deployed on AWS.
- Project source code.
- System architecture diagram.
- Business process documentation.
- Demo documentation and instructions.
