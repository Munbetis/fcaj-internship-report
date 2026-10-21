
---
title: "Published Blogs"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# AWS KNOWLEDGE SHARING BLOGS

## Overview

During my internship in the **First Cloud AI Journey (FCAJ)** program, I have been researching, summarizing, and preparing technical blog posts to strengthen my knowledge of Amazon Web Services (AWS) and share what I have learned with the community.

According to the program requirements, each participant must complete **at least three technical blog posts** based on the knowledge they have learned or researched and subsequently publish them in the **AWS Study Group** community.

The blog posts may focus on introducing and analyzing AWS services, exploring cost optimization strategies, or explaining how to solve real-world problems using cloud technologies.

Based on these directions, I selected three topics related to NoSQL databases, cost optimization, and Generative AI applications. These topics are also directly related to the **Cloud Library Management System** project that our team is researching and developing.

---

## 1. Blog 1: Amazon DynamoDB

### Building a NoSQL Database on AWS

**[Read Blog 1](3.1-Blog1/)**

The first blog focuses on **Amazon DynamoDB**, a fully managed NoSQL database service provided by AWS.

The article introduces DynamoDB's key features, data organization methods, primary key design, and fundamental database operations.

**Main Topics:**

- Overview of Amazon DynamoDB and its key features.
- Comparison between DynamoDB and relational databases.
- Understanding Tables, Items, Attributes, Partition Keys, and Sort Keys.
- Analyzing Global Secondary Indexes (GSIs) and Access Patterns.
- Performing basic CRUD operations.
- Creating tables and managing data on AWS.
- Integrating DynamoDB with AWS Lambda and API Gateway.
- Exploring Conditional Writes and Transactions.
- Analyzing security, performance, and cost considerations.

**Application to Cloud Library:**

DynamoDB is proposed as the primary operational database for Cloud Library, supporting the management of books, readers, physical book copies, borrowing records, and related data.

The article also explains how conditional updates and transactions can help prevent incorrect book quantities when multiple borrowing or return requests are processed.

**Content Direction:** Introduction and analysis of AWS services.

**AWS Study Group Post:** The link will be added after publication.

---

## 2. Blog 2: AWS Cost Optimization

### Cost Optimization Strategies for Building Serverless Applications on AWS

**[Read Blog 2](3.2-Blog2/)**

The second blog focuses on **AWS Cost Optimization**, one of the six pillars of the AWS Well-Architected Framework.

The article explores budget management, cost analysis, and the selection of AWS resources that match application requirements.

**Main Topics:**

- Introduction to AWS Cost Optimization and its role in cloud architecture.
- Understanding the Cost Optimization Pillar of the AWS Well-Architected Framework.
- Exploring AWS Cost Explorer, AWS Budgets, and AWS Pricing Calculator.
- Studying pricing models and the Pay-as-you-go principle.
- Understanding Right-sizing and unused resource management.
- Analyzing cost optimization methods for AWS Lambda.
- Comparing DynamoDB On-demand and Provisioned Capacity.
- Exploring cost optimization for Amazon S3, API Gateway, and CloudWatch.
- Configuring budgets and monitoring costs.
- Developing a cost control plan for Serverless applications.

**Application to Cloud Library:**

Cost Optimization principles can be applied to evaluate the Cloud Library architecture, including backend processing expenses, database access, book cover image storage, and content delivery.

The article proposes using AWS Pricing Calculator for cost estimation, AWS Budgets for alerts, and Cost Explorer for evaluating expenses during deployment.

The costs discussed in the article are illustrative and intended for analysis. They do not represent measured operating expenses of the actual project.

**Content Direction:** AWS cost optimization strategies.

**AWS Study Group Post:** The link will be added after publication.

---

## 3. Blog 3: Amazon Bedrock Knowledge Bases and RAG

### Building an AI Assistant for Library Policy Q&A

**[Read Blog 3](3.3-Blog3/)**

The third blog explores how **Amazon Bedrock Knowledge Bases** and **Retrieval-Augmented Generation (RAG)** can be used to develop an AI assistant capable of answering questions based on private documents.

This approach aims to help readers understand library policies and usage instructions through natural language interactions.

**Main Topics:**

- Overview of Amazon Bedrock and Generative AI.
- Introduction to Retrieval-Augmented Generation (RAG).
- Understanding Embeddings, Semantic Search, Chunking, and Vector Stores.
- Analyzing the role of Amazon Bedrock Knowledge Bases.
- Exploring Amazon S3 as a document data source.
- Understanding document synchronization and indexing.
- Designing a RAG architecture using API Gateway and AWS Lambda.
- Creating and testing a Knowledge Base.
- Demonstrating the RetrieveAndGenerate API using Node.js.
- Analyzing security, accuracy, and cost optimization considerations.

**Application to Cloud Library:**

Amazon Bedrock Knowledge Bases is proposed for developing an AI assistant that helps readers understand borrowing, returning, renewal, reservation, and overdue book policies.

The knowledge source may include library policy documents stored in Amazon S3, while user transactions remain managed in the operational database.

The RAG solution represents a proposed research and implementation direction. It does not imply that the complete AI assistant functionality has already been deployed in the actual system.

**Content Direction:** Solving real-world problems using AWS services.

**AWS Study Group Post:** The link will be added after publication.

---

## 4. Summary of the Three Blogs

| Blog | Topic | Key Knowledge |
| --- | --- | --- |
| **Blog 1** | Amazon DynamoDB | NoSQL databases, data modeling, and Serverless integration. |
| **Blog 2** | AWS Cost Optimization | Budget management, AWS cost analysis, and optimization. |
| **Blog 3** | Amazon Bedrock Knowledge Bases and RAG | Generative AI, document retrieval, and AI assistant development. |

The three topics were selected to explore different aspects of application development on AWS, ranging from data management and cost control to artificial intelligence integration.

As a result, the research covers not only individual AWS services but also supports architectural planning and future development of the Cloud Library Management System project.

## 5. Learning Objectives and Outcomes

Through researching and developing these three technical blogs, I aim to:

- Strengthen my understanding of AWS services studied during the FCAJ program.
- Improve my ability to research and read technical documentation.
- Understand how to select AWS services based on application requirements.
- Expand my knowledge of NoSQL databases and Serverless architectures.
- Explore AWS cost management and optimization strategies.
- Learn how to develop Generative AI applications using RAG.
- Improve my technical writing and presentation skills.
- Practice creating examples, architecture diagrams, and hands-on tutorials.
- Connect AWS knowledge with real-world problems in the Cloud Library Management System project.
- Share knowledge and exchange experiences with the AWS community.

## 6. Sharing Blog Posts with AWS Study Group

According to FCAJ program requirements, the blog posts will be published and shared in the AWS Study Group Facebook community after completion.

**Community:** [AWS Study Group - Facebook](https://www.facebook.com/groups/awsstudygroupfcj)

Links to individual Facebook posts will be updated after publication.

Sharing these technical articles helps me consolidate the knowledge I have researched while creating opportunities to receive feedback and learn from other AWS community members.
