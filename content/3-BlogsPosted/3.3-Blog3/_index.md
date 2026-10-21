---
title: "Blog 3: Amazon Bedrock Knowledge Bases - Building an AI Assistant with RAG"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AMAZON BEDROCK KNOWLEDGE BASES AND RAG

## Building an AI Assistant for Library Policy Q&A Using Amazon Bedrock Knowledge Bases

In recent years, Generative Artificial Intelligence (Generative AI) has been increasingly adopted in software systems, especially applications that involve information retrieval and user assistance.

Large Language Models (LLMs) can understand questions and generate responses in natural language. However, these models do not always have access to an organization's internal information or most up-to-date data.

For example, readers using a library management system may ask questions such as:

- How many books can a reader borrow at the same time?
- How long is the borrowing period?
- Can borrowed books be renewed?
- What happens if a book is returned late?
- How does the book reservation process work?

If only a general-purpose AI model is used, its responses may not match the library's specific policies.

To address this challenge, we can combine **Retrieval-Augmented Generation (RAG)** with **Amazon Bedrock Knowledge Bases**.

This solution enables applications to retrieve information from provided documents and use that information as context when generating responses.

In this article, we will explore Amazon Bedrock, how RAG works, Amazon Bedrock Knowledge Bases, and how these technologies can be applied to the **Cloud Library Management System** project.

### Key Concepts to Understand

- **Generative AI:** AI technology capable of generating new content.
- **Large Language Model (LLM):** A large-scale language model capable of processing and generating text.
- **Amazon Bedrock:** An AWS service that supports building Generative AI applications using foundation models.
- **Amazon Bedrock Knowledge Bases:** A service that supports connecting, retrieving, and using application-specific data.
- **Retrieval-Augmented Generation (RAG):** A method that combines information retrieval with response generation.
- **Embeddings:** Numerical vector representations of content.
- **Vector Store:** A component used to store and query vectors.
- **Semantic Search:** A search method based on the meaning of content.
- **Chunking:** The process of dividing documents into smaller sections.
- **Data Source:** A source of data connected to a Knowledge Base.
- **RetrieveAndGenerate:** An API that supports document retrieval and response generation.

### 1. Overview of Amazon Bedrock

#### 1.1. What Is Amazon Bedrock?

Amazon Bedrock is a managed AWS service that provides access to foundation models (FMs) from AWS and other model providers through APIs.

Foundation Models are AI models trained on large amounts of data and can be used for various tasks.

Common applications of Amazon Bedrock include:

- Building customer support chatbots.
- Summarizing documents.
- Generating text content.
- Analyzing and extracting information.
- Developing AI assistants for applications.
- Answering questions based on private documents.

With Amazon Bedrock, developers can integrate AI models into their systems without having to build and operate the underlying model-training infrastructure from scratch.

#### 1.2. Key Features

**Access to Multiple Foundation Models**

Amazon Bedrock supports different foundation models depending on the AWS Region and service availability.

**API Integration**

Developers can invoke Amazon Bedrock APIs from their backend applications.

**Support for RAG Applications**

Amazon Bedrock Knowledge Bases helps connect data sources and retrieve information for generating responses.

**Integration with the AWS Ecosystem**

Amazon Bedrock can be integrated with Amazon S3, AWS Lambda, IAM, and other AWS services.

**Access Management**

AWS IAM helps control permissions for accessing related resources and APIs.

#### 1.3. Limitations of Using LLMs

Although LLMs can generate natural-sounding responses, using a standalone model has several limitations:

- It does not automatically know a library's internal policies.
- It may not contain recently updated information.
- It may generate inaccurate content.
- It does not automatically have access to an application's database.
- Data sources and access permissions must be controlled.

An important issue is **Hallucination**, which occurs when a model generates information that sounds reasonable but is not supported by reliable data.

RAG is one method that helps reduce this risk by providing additional context from identified data sources.

However, RAG does not completely eliminate hallucinations.

### 2. Retrieval-Augmented Generation (RAG)

#### 2.1. What Is RAG?

Retrieval-Augmented Generation (RAG) is a method that combines two processes:

1. **Retrieval:** Retrieves relevant information from data sources.
2. **Generation:** Uses an AI model to generate a response based on the question and retrieved information.

Instead of relying only on the model's existing knowledge, RAG provides relevant document passages as additional context.

For example, a user asks:

```text
How many books can I borrow at the same time?
```

The system searches the library policy documents and retrieves the following information:

```text
Each reader may borrow a maximum of 3 books.
```

The model can then generate a response:

```text
According to Cloud Library's policies,
each reader may borrow up to 3 books
at the same time.
```

As a result, the response is generated using the library's specific regulations instead of relying only on the model's general knowledge.

#### 2.2. Components of a RAG System

| Component | Function |
| --- | --- |
| **User Query** | The question submitted by the user. |
| **Knowledge Base** | Manages the knowledge retrieval process. |
| **Data Source** | The connected source of documents. |
| **Embedding Model** | Converts content into numerical vectors. |
| **Vector Store** | Stores and searches vector representations. |
| **Retrieval** | Finds relevant document passages. |
| **Foundation Model** | Generates responses using the retrieved context. |
| **Response** | The answer returned to the user. |

#### 2.3. What Are Embeddings?

Embeddings represent content as numerical vectors.

These vectors help systems compare and identify semantic similarities between text passages.

For example, consider the following questions:

```text
How long can I borrow books from the library?
```

and

```text
How many days do I have before returning a book?
```

Although they are phrased differently, both questions refer to the borrowing period.

Using embeddings and Semantic Search, the system can identify documents that are semantically related to the user's question.

#### 2.4. What Is Chunking?

Chunking is the process of dividing documents into smaller sections to support indexing and information retrieval.

For example, a library policy document may contain:

```text
CLOUD LIBRARY POLICIES

1. Reader Registration Policy
2. Book Borrowing Policy
3. Book Return Policy
4. Book Renewal Policy
5. Overdue Book Policy
6. Book Reservation Policy
```

Instead of processing the entire document as one large piece of information, the system can divide it into smaller sections corresponding to different policy categories.

The choice of chunk size and chunking strategy can affect retrieval accuracy.

#### 2.5. How RAG Works

The basic RAG workflow consists of two stages.

**Stage 1: Data Preparation**

1. Documents are uploaded to a Data Source.
2. The system processes and divides the documents into Chunks.
3. An Embedding Model converts the content into vectors.
4. The vectors are stored in a Vector Store.

**Stage 2: Question Answering**

1. The user submits a question.
2. The system represents the question for retrieval.
3. The Vector Store is used to find relevant content.
4. Relevant document passages are provided as context.
5. A Foundation Model generates a response.
6. The system returns the answer to the user.

### 3. Overview of Amazon Bedrock Knowledge Bases

#### 3.1. What Are Amazon Bedrock Knowledge Bases?

Amazon Bedrock Knowledge Bases is a feature of Amazon Bedrock that helps applications connect to data sources and implement Retrieval-Augmented Generation workflows.

The service supports processes such as:

- Connecting document sources.
- Processing data.
- Dividing documents into Chunks.
- Creating Embeddings.
- Storing Embeddings in a supported Vector Store.
- Retrieving relevant content.
- Combining retrieved information with an AI model to generate responses.

As a result, developers do not necessarily need to build the entire RAG pipeline from scratch.

#### 3.2. Data Source

A Data Source provides the information used by a Knowledge Base to build and update its knowledge repository.

One common option is **Amazon S3**.

For example, Cloud Library could store documents using the following structure:

```text
cloud-library-documents/
    library-rules.pdf
    borrowing-policy.pdf
    return-policy.pdf
    reservation-guide.pdf
```

These documents may contain:

- Account registration policies.
- Borrowing limits.
- Book borrowing periods.
- Renewal policies.
- Overdue fine calculations.
- Book reservation procedures.

This is an example document structure for the proposed solution.

#### 3.3. Vector Store

A Vector Store stores vector embeddings to support information retrieval.

Amazon Bedrock Knowledge Bases can integrate with supported Vector Store solutions.

Examples include:

- Amazon OpenSearch Serverless.
- Amazon Aurora PostgreSQL with pgvector.
- Amazon S3 Vectors.

Each option has different characteristics related to performance, features, and costs.

For Cloud Library, Amazon S3 Vectors is an option worth considering for storing knowledge embeddings.

However, model compatibility, AWS Region availability, and retrieval requirements should be checked before selecting a solution.

#### 3.4. Data Synchronization

After documents are updated in a Data Source, the Knowledge Base needs to be synchronized so that the new information can be indexed.

For example, suppose the library changes its borrowing period policy.

When the policy document is updated in Amazon S3, the administrator needs to perform or automate the Knowledge Base synchronization process according to the system design.

Without synchronization, the system may continue retrieving outdated information.

Therefore, document updates and synchronization are important parts of maintaining the AI assistant's response quality.

### 4. RAG System Architecture on AWS

The following components can be used to integrate RAG into Cloud Library:

| Component | Role |
| --- | --- |
| **React Frontend** | Displays the AI assistant interface. |
| **Amazon Cognito** | Supports user authentication. |
| **Amazon API Gateway** | Receives requests from the frontend. |
| **AWS Lambda** | Processes requests and invokes Bedrock APIs. |
| **Amazon Bedrock Knowledge Bases** | Retrieves information from documents. |
| **Amazon S3** | Stores library policy documents. |
| **Vector Store** | Stores Embeddings and supports semantic search. |
| **Foundation Model** | Generates answers using the retrieved context. |
| **AWS IAM** | Controls access permissions. |

#### 4.1. Proposed Architecture Diagram

```text
+-----------------------------+
|           Reader            |
|      Submits an AI Query    |
+-----------------------------+
              |
              v
+-----------------------------+
|       React Frontend        |
+-----------------------------+
              |
              v
+-----------------------------+
|     Amazon API Gateway      |
+-----------------------------+
              |
              v
+-----------------------------+
|         AWS Lambda          |
|     Processes Requests      |
+-----------------------------+
              |
              v
+-----------------------------+
|  Amazon Bedrock Knowledge   |
|            Bases            |
+-----------------------------+
         |             |
         v             v
+----------------+  +----------------+
|  Vector Store  |  | Foundation     |
| Semantic Search|  | Model          |
+----------------+  +----------------+
         ^
         |
+-----------------------------+
|        Amazon S3            |
|   Library Policy Documents  |
+-----------------------------+
    (Sync and Indexing)
```

*This diagram illustrates a simplified architecture. In practice, Amazon Bedrock Knowledge Bases coordinates information retrieval and uses an appropriate model to generate responses.*

#### 4.2. Question Processing Workflow

Suppose a user asks:

```text
How much is the fine for returning a book late?
```

The system can process the question as follows:

1. The user enters a question in the React interface.
2. The frontend sends the request to API Gateway.
3. API Gateway forwards the valid request to Lambda.
4. Lambda invokes Amazon Bedrock Knowledge Bases.
5. The Knowledge Base retrieves the relevant overdue fine policy.
6. The Foundation Model uses the retrieved content to generate an answer.
7. Lambda returns the result to the frontend.
8. The interface displays the answer and source information, if available.

An example of the expected response is:

```text
According to Cloud Library's proposed policies,
the overdue fine is 5,000 VND
for each day a book is returned late.
```

This response should only be displayed when supported by a valid source document.

### 5. Hands-on Guide to Amazon Bedrock Knowledge Bases

This section introduces the proposed process for building a Knowledge Base using documents stored in Amazon S3.

The steps may vary depending on AWS Region, permissions, model types, and the Amazon Bedrock interface at the time of implementation.

#### Step 1: Prepare Knowledge Documents

First, create a sample library policy document for Cloud Library.

For example:

```text
CLOUD LIBRARY - LIBRARY RULES

1. Each reader may borrow a maximum
   of 3 books at the same time.

2. The standard borrowing period
   is 14 days.

3. Readers may request one renewal
   for an additional 7 days if they
   meet the library's conditions.

4. The overdue fine is 5,000 VND
   per day.

5. Reserved books are held for
   48 hours according to policy.
```

Save the document in a format supported by the Data Source, such as `.txt` or `.pdf`.

These details are examples based on Cloud Library's proposed business rules, not the official policies of an operating library.

#### Step 2: Upload Documents to Amazon S3

1. Sign in to the AWS Management Console.
2. Search for Amazon S3.
3. Create or select an appropriate S3 Bucket.
4. Create a folder for knowledge documents.
5. Upload the prepared library policy documents.
6. Review access permissions and security configurations.

Example data location:

```text
s3://your-cloud-library-bucket/knowledge/
```

The Bucket name is only an example.

Internal documents should not be configured for public access unless the application specifically requires it.

#### Step 3: Access Amazon Bedrock

1. Open Amazon Bedrock in the AWS Management Console.
2. Select an AWS Region that supports the intended features.
3. Check model access requirements for the service.
4. Open the `Knowledge Bases` section.
5. Choose to create a new Knowledge Base.

During implementation, verify the availability of the Embedding Model and Foundation Model in the selected Region.

#### Step 4: Create a Knowledge Base

When configuring the Knowledge Base:

1. Enter a name, such as `cloud-library-knowledge-base`.
2. Select an appropriate Vector Store configuration.
3. Configure an IAM Service Role.
4. Select Amazon S3 as the Data Source.
5. Specify the document storage location.
6. Choose a Chunking strategy.
7. Select a supported Embedding Model.
8. Configure the Vector Store.
9. Review the settings and create the Knowledge Base.

For example, Amazon S3 Vectors may be selected if the environment supports it and it meets the system's requirements.

#### Step 5: Synchronize Data

After creating the Knowledge Base:

1. Open the created Knowledge Base.
2. Select the Data Source.
3. Start the data synchronization process.
4. Monitor the Ingestion Job status.
5. Review the results after synchronization is completed.

During this process, the documents are processed and indexed to support retrieval.

If synchronization fails, check access permissions, document formats, and the model or Vector Store configurations.

#### Step 6: Test the Knowledge Base

After successful synchronization, use the testing functionality provided by Amazon Bedrock Knowledge Bases.

Example questions:

```text
How many books can I borrow?
```

```text
How long is the borrowing period?
```

```text
Can I renew a borrowed book?
```

```text
How are overdue fines calculated?
```

```text
How long are reserved books held?
```

When testing, evaluate the following:

- Does the response match the source documents?
- Does the system retrieve relevant document passages?
- Does the answer include appropriate source citations?
- Does the system generate information that is not supported by the documents?
- Do differently worded questions produce consistent answers?

### 6. Integrating a Knowledge Base with AWS Lambda

To integrate the AI question-answering feature into the Cloud Library website, the backend can invoke Amazon Bedrock through the AWS SDK.

#### 6.1. Prepare the Node.js Library

AWS SDK for JavaScript v3 supports integration with Amazon Bedrock Knowledge Bases.

Install the required package:

```bash
npm install @aws-sdk/client-bedrock-agent-runtime
```

#### 6.2. Example Using RetrieveAndGenerate

The following code demonstrates how to submit a question to a Knowledge Base using Node.js.

```javascript
import {
  BedrockAgentRuntimeClient,
  RetrieveAndGenerateCommand
} from "@aws-sdk/client-bedrock-agent-runtime";

const client = new BedrockAgentRuntimeClient({
  region: "ap-southeast-1"
});

const command = new RetrieveAndGenerateCommand({
  input: {
    text: "How long is the borrowing period?"
  },
  retrieveAndGenerateConfiguration: {
    type: "KNOWLEDGE_BASE",
    knowledgeBaseConfiguration: {
      knowledgeBaseId: process.env.KNOWLEDGE_BASE_ID,
      modelArn: process.env.BEDROCK_MODEL_ARN
    }
  }
});

const response = await client.send(command);

console.log(response.output?.text);
console.log(response.citations);
```

**Explanation:**

- `BedrockAgentRuntimeClient`: Initializes the Bedrock Agent Runtime client.
- `RetrieveAndGenerateCommand`: Sends a retrieval and response generation request.
- `input.text`: Contains the user's question.
- `knowledgeBaseId`: Identifies the Knowledge Base.
- `modelArn`: Identifies the supported model used to generate responses.
- `response.output`: Contains the generated answer text.
- `response.citations`: Contains citation information when returned by the service.

The example uses the following environment variables:

```text
KNOWLEDGE_BASE_ID=YOUR_KNOWLEDGE_BASE_ID
BEDROCK_MODEL_ARN=YOUR_SUPPORTED_MODEL_IDENTIFIER
```

These values must be replaced with actual configuration values.

The code assumes that the Knowledge Base has been created and synchronized successfully, the Region is supported, and the execution environment has the appropriate IAM permissions.

This is a technical integration example and does not mean that the AI assistant feature has already been fully deployed in the project.

#### 6.3. The Role of AWS IAM

Access permissions must be controlled when using Amazon Bedrock Knowledge Bases.

For example:

- The Knowledge Base Service Role requires permission to access the data source.
- The Service Role requires appropriate permissions for the Vector Store and related models.
- The Lambda Execution Role requires permission to invoke the necessary Amazon Bedrock APIs.
- The application's APIs must verify user permissions.

AWS credentials should not be stored directly in the React frontend or public source code.

### 7. Applying RAG to Cloud Library Management System

#### 7.1. Problem Overview

Cloud Library Management System proposes integrating an AI assistant to help readers quickly access library policies and usage instructions.

Normally, users need to manually search for information across multiple pages or documents.

Examples include:

- Book borrowing instructions.
- Renewal policy pages.
- Library regulations.
- Overdue fine policies.
- Reservation instructions.

An AI assistant using RAG can help answer questions based on these documents.

#### 7.2. Examples of Library Policy Q&A

Suppose a user asks:

**Question 1:**

```text
What is the maximum number of books I can borrow?
```

**Expected Answer:**

```text
According to Cloud Library's policies,
each reader may borrow a maximum of
3 books at the same time.
```

**Question 2:**

```text
How many days can I borrow a book?
```

**Expected Answer:**

```text
The standard borrowing period
is 14 days.
```

**Question 3:**

```text
Can I extend the borrowing period?
```

**Expected Answer:**

```text
According to the proposed policy,
readers may request one renewal
for an additional 7 days if they
meet the library's requirements.
```

These examples demonstrate how the system can generate responses based on provided documents.

#### 7.3. Distinguishing Knowledge Data from Transactional Data

In Cloud Library, it is important to distinguish between two main data categories.

**Knowledge Data**

This includes:

- Library regulations.
- Borrowing and returning instructions.
- Renewal policies.
- Reservation policies.
- Website usage instructions.

These documents can be added to a Knowledge Base for RAG.

**Transactional Data**

This includes:

- A user's borrowing records.
- The status of currently borrowed books.
- Current overdue fines.
- Personal reservation information.
- Reader profiles.

This information is managed in the application's operational database, such as Amazon DynamoDB.

RAG based on static documents should not be used to make definitive claims about frequently changing transactional information.

For example, when a user asks:

```text
How many books am I currently borrowing?
```

The application must authenticate the user and query transactional data that the user is authorized to access rather than relying entirely on documents in the Knowledge Base.

#### 7.4. Expanding the Book Search Feature

In addition to answering library policy questions, Cloud Library may explore using AI to support book discovery.

For example:

```text
Recommend some books for beginners
who want to learn Cloud Computing.
```

This is a potential future enhancement.

However, to ensure that recommendations accurately reflect the available catalog, the system needs a suitable book data source and a mechanism for keeping information updated.

Creating a Knowledge Base containing library policies does not automatically enable accurate searches across the entire book catalog managed in DynamoDB.

### 8. Security, Accuracy, and Cost Optimization

#### 8.1. Data Source Security

When building an AI application using private documents, important considerations include:

- Grant access only to appropriate documents.
- Avoid including sensitive personal information in publicly accessible knowledge sources.
- Use IAM to control access permissions.
- Verify user permissions before processing personal information.
- Do not expose AWS Access Keys in the frontend.
- Manage documents and updated versions securely.

#### 8.2. Controlling Response Accuracy

A RAG system should be evaluated based on both retrieval performance and answer quality.

Some improvement methods include:

- Prepare clear and well-structured documents.
- Divide documents into appropriate Chunks.
- Test different ways of phrasing questions.
- Review the retrieved document content.
- Display source references when possible.
- Instruct the model not to generate unsupported answers when the documents do not contain sufficient information.
- Synchronize the Knowledge Base after updating library policies.

It is important to remember that providing documents to an AI model does not guarantee completely accurate responses.

#### 8.3. Cost Optimization

The cost of implementing RAG on AWS depends on the components used.

For example:

| Component | Cost Factors to Consider |
| --- | --- |
| **Amazon S3** | Document storage and related requests. |
| **Embedding Model** | Processing data to generate Embeddings. |
| **Vector Store** | Vector storage and retrieval operations. |
| **Foundation Model** | Processing input data and generating responses. |
| **AWS Lambda** | Number of invocations and execution resources. |
| **Amazon API Gateway** | Number of API requests. |
| **CloudWatch** | Logs and monitoring features. |

Possible optimization approaches include:

- Add only necessary documents to the Knowledge Base.
- Remove unnecessary duplicate content.
- Choose models that match application requirements.
- Select a Vector Store based on performance needs and budget.
- Monitor the number of questions and the amount of processed data.
- Evaluate Chunking configurations.
- Remove unused experimental resources after checking which data needs to be retained.

For academic projects, AWS Pricing Calculator and current service pricing should be used to estimate costs before deployment.

RAG should not be considered a completely free solution simply because the application uses a Serverless architecture.

### 9. Benefits and Considerations of Using RAG

#### 9.1. Benefits

Combining Amazon Bedrock Knowledge Bases with RAG provides several benefits:

- Supports answering questions based on application-specific documents.
- Reduces the need to manually search through multiple documents.
- Helps users access information more quickly.
- Supports updates to the knowledge repository.
- Takes advantage of the natural language capabilities of LLMs.
- Can be integrated into Serverless architectures on AWS.
- Supports providing source references for generated answers.

#### 9.2. Important Considerations

**RAG Does Not Completely Eliminate Hallucinations**

Responses still need to be reviewed, especially when the information may affect users.

**Document Quality Affects Results**

If the knowledge source is inaccurate or outdated, the generated responses may also be inappropriate.

**RAG Does Not Replace Operational Databases**

A Knowledge Base is not a complete replacement for transaction management systems such as DynamoDB.

**Access Permissions Must Be Managed**

Applications must ensure that users can only access information appropriate to their permissions.

**Costs Must Be Evaluated**

Expenses related to AI models, Vector Stores, and other services need to be monitored.

**Real-world Testing Is Necessary**

System quality should not be evaluated based on only a few illustrative questions.

### 10. Conclusion

Amazon Bedrock Knowledge Bases is a solution that supports the development of Generative AI applications using private data sources.

Through studying Retrieval-Augmented Generation, I have gained a clearer understanding of how document retrieval can be combined with the response generation capabilities of Large Language Models.

Additionally, concepts such as Embeddings, Vector Stores, Semantic Search, and Chunking have helped me understand how data can be organized for AI-powered question-answering systems.

For the **Cloud Library Management System** project, RAG is a suitable proposed approach for developing an AI assistant that helps readers understand library policies, borrowing and returning procedures, and other library regulations.

However, implementation must clearly distinguish between knowledge data and transactional data while maintaining proper access control, response accuracy, and operating cost management.

The most important lesson is that **building a useful AI assistant requires not only a powerful AI model but also reliable data sources, appropriate retrieval mechanisms, and a secure system architecture**.

### 11. Illustrative and Hands-on Images

![AMAZON BEDROCK KNOWLEDGE BASES AND RAG](/images/3-Blogs/Blogs3/bedrock_knowledge.png)