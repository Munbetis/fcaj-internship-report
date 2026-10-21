---
title: "Blog 2: AWS Cost Optimization - Cost Optimization Strategies on AWS"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS COST OPTIMIZATION

## Cost Optimization Strategies for Building Serverless Applications on AWS

When developing and deploying applications on cloud computing platforms, one of the important factors developers need to consider is the cost of operating the system.

Amazon Web Services (AWS) provides various services that allow businesses and developers to build applications without investing in physical server infrastructure. However, inefficient use of AWS resources can result in unexpected costs.

Especially when developing academic projects or experimental applications, users often focus on implementing features without paying sufficient attention to monitoring and optimizing costs.

To address this issue, AWS provides cloud financial management tools such as **AWS Cost Explorer, AWS Budgets, and AWS Pricing Calculator**.

In addition to using cost management tools, developers can optimize system architecture by selecting appropriate services, resource configurations, and pricing models.

In this article, we will explore the fundamental principles of **AWS Cost Optimization**, the tools available for managing cloud expenses, and how these concepts can be applied to the **Cloud Library Management System** project.

### Key Concepts to Understand

- **AWS Cost Optimization:** The process of optimizing the cost of using AWS resources.
- **AWS Well-Architected Framework:** A set of guidelines for designing and operating systems on AWS.
- **Cost Optimization Pillar:** A pillar focused on using resources cost-effectively.
- **AWS Cost Explorer:** A tool for analyzing AWS costs and usage.
- **AWS Budgets:** A service for setting budgets and cost alerts.
- **AWS Pricing Calculator:** A tool for estimating AWS service costs before deployment.
- **Pay-as-you-go:** A pricing model based on actual usage.
- **Right-sizing:** Selecting resources that match actual requirements.
- **Serverless:** A deployment model that reduces the need to manage servers.
- **Cost Monitoring:** Tracking, analyzing, and controlling operational costs.

### 1. Overview of AWS Cost Optimization

#### 1.1. What Is AWS Cost Optimization?

AWS Cost Optimization is the process of analyzing, managing, and adjusting AWS resource usage to meet system requirements at a reasonable cost.

The goal of Cost Optimization is not simply to reduce expenses to the lowest possible level.

Instead, a system needs to maintain a balance among:

- Operating costs.
- Application performance.
- Scalability.
- Availability.
- Security.
- Actual usage requirements.

For example, an application may reduce costs by allocating fewer computing resources. However, if reducing resources causes slow response times or frequent errors, the solution may not be truly effective.

Therefore, cost optimization should be performed based on technical objectives and business requirements.

#### 1.2. Why Is Cost Optimization Important on AWS?

AWS provides flexible pricing models. Users may pay based on usage duration, the number of requests, storage capacity, or configured resources.

This flexibility offers many benefits, but it also requires users to manage resource consumption appropriately.

Some common causes of increased AWS costs include:

- Maintaining resources that are no longer needed.
- Configuring more resources than the application requires.
- Storing unnecessary data or logs for extended periods.
- Making excessive API requests.
- Using inefficient database query methods.
- Failing to monitor incurred costs.
- Not configuring budgets and alerts.

For student projects, understanding cost management helps make AWS learning and experimentation more proactive and manageable.

#### 1.3. Cost Optimization in the AWS Well-Architected Framework

The AWS Well-Architected Framework is a set of guidelines that helps developers evaluate and improve application architectures on AWS.

The framework consists of six pillars:

1. Operational Excellence.
2. Security.
3. Reliability.
4. Performance Efficiency.
5. Cost Optimization.
6. Sustainability.

Among these, the **Cost Optimization Pillar** focuses on selecting appropriate solutions and using resources efficiently to deliver value at an effective cost.

Its important practice areas include:

| Practice Area | Description |
| --- | --- |
| Cloud Financial Management | Establish cloud financial management capabilities. |
| Expenditure and Usage Awareness | Understand resource usage and associated costs. |
| Cost-effective Resources | Select cost-effective resources and services. |
| Manage Demand and Supply | Adjust resources according to usage demand. |
| Optimize Over Time | Continuously evaluate and improve cost efficiency. |

These principles can be applied from the early stages of project design rather than being considered only when AWS bills increase.

### 2. AWS Cost Management Tools

AWS provides various tools to support different cost management requirements.

The three tools introduced in this article are AWS Cost Explorer, AWS Budgets, and AWS Pricing Calculator.

#### 2.1. AWS Cost Explorer

AWS Cost Explorer is a tool that allows users to observe, analyze, and understand their AWS expenses.

With Cost Explorer, users can:

- Monitor total costs over selected periods.
- Analyze expenses by individual AWS service.
- Observe increasing or decreasing cost trends.
- Filter data by account, Region, or other supported dimensions.
- View cost forecasts through available features.

For example, if a project uses Amazon DynamoDB, AWS Lambda, and Amazon S3, Cost Explorer can help identify which service contributes the largest portion of the expenses.

Developers can then focus their investigation on services with high usage or costs.

#### 2.2. AWS Budgets

AWS Budgets allows users to set budgets and receive notifications when costs or usage reach configured thresholds.

For example, a learning project may establish the following illustrative budget:

```text
Budget name: CloudLibrary-Monthly-Budget

Budget type: Cost Budget

Period: Monthly

Planned budget: 10 USD
```

In this example, USD 10 is only a hypothetical budget selected by the team. It is not a fixed charge or a forecast of Cloud Library's operating costs.

Users can configure alerts when actual costs reach thresholds such as:

| Threshold | Purpose |
| --- | --- |
| 50% | Monitor initial resource usage. |
| 80% | Review services generating expenses. |
| 100% | Assess the risk of exceeding the budget. |

AWS Budgets can send email notifications based on the configured alert settings.

**Note:** Standard budgets and alerts do not automatically prevent additional charges. Alerts may also be delayed compared with actual resource usage.

Therefore, AWS Budgets is a tool for supporting cost control, not a mechanism that guarantees an AWS account will never exceed its budget.

#### 2.3. AWS Pricing Calculator

AWS Pricing Calculator is a tool that helps users estimate expenses before deploying applications.

Users can select AWS services and enter their expected usage parameters.

For example, when building Cloud Library, the team can prepare cost estimates for:

- AWS Lambda.
- Amazon API Gateway.
- Amazon DynamoDB.
- Amazon S3.
- Amazon CloudFront.
- Other AWS services used in the architecture.

For each service, relevant parameters such as the number of requests, storage capacity, and resource configurations must be determined.

The result generated by AWS Pricing Calculator is an **estimate**, not a guaranteed final bill.

Actual costs may vary depending on AWS Region, usage patterns, configurations, and pricing at the time of deployment.

#### 2.4. Comparison of the Three Tools

| Tool | Main Function | When to Use |
| --- | --- | --- |
| **AWS Cost Explorer** | Analyzes incurred costs and usage trends. | During system operation. |
| **AWS Budgets** | Sets budgets and cost alerts. | Before and during deployment. |
| **AWS Pricing Calculator** | Estimates costs based on planned configurations. | During system design and planning. |

These three tools complement one another throughout the cloud financial management process.

### 3. Cost Optimization Strategies on AWS

#### 3.1. Choosing an Appropriate Pricing Model

AWS provides different pricing models depending on the service.

For example:

- Some services charge according to resource consumption.
- Some services charge based on the number of requests.
- Some services charge according to storage capacity.
- Some services offer commitment-based pricing options under certain conditions.

For academic applications with unpredictable traffic, usage-based pricing may be more convenient than maintaining large resources for extended periods.

However, developers should compare options for each service rather than assuming one pricing model is always cheaper than another.

#### 3.2. Resource Right-sizing

Right-sizing is the process of selecting and adjusting resources to match actual workloads.

For example, if a Lambda Function requires only a small amount of memory to process an API request, configuring excessive memory may create unnecessary expenses.

Conversely, allocating too little memory may increase execution time.

Therefore, measurement and testing are necessary before choosing an appropriate configuration.

#### 3.3. Removing Unused Resources

When learning AWS, users may create various resources for hands-on practice.

After completing an exercise, some resources may remain active or continue to exist.

Examples include:

- Experimental resources that are no longer needed.
- Temporary stored data.
- Unused copies or versions of data.
- Logs that do not need long-term retention.

Regular resource reviews can help reduce the risk of unexpected costs.

However, before deleting resources, developers should check their dependencies and data retention requirements.

#### 3.4. Optimizing Serverless Architecture

Serverless architecture helps developers reduce server administration tasks while supporting scalability based on demand.

Some Serverless services on AWS include:

- AWS Lambda.
- Amazon API Gateway.
- Amazon DynamoDB.
- Amazon EventBridge.
- Amazon S3.

When properly designed, Serverless architecture can be cost-effective for applications with changing workloads.

However, as the number of requests or processing time increases, Serverless costs may also increase.

Therefore, choosing Serverless does not automatically mean that a system will always have the lowest operating cost.

### 4. Optimizing Costs for Services in a Serverless Architecture

#### 4.1. AWS Lambda

AWS Lambda allows developers to run code without managing servers.

Lambda costs depend on factors such as:

- Number of requests.
- Execution duration.
- Configured memory.
- Processor architecture and other applicable billable features.

**Optimization strategies:**

- Avoid unnecessary Lambda invocations.
- Optimize source code to reduce execution time.
- Review memory configurations.
- Minimize redundant database queries.
- Monitor Duration, Errors, and Invocations through CloudWatch.

For example, in Cloud Library, an API that retrieves book information should fetch only the required data instead of processing the entire catalog for every request.

#### 4.2. Amazon DynamoDB

Amazon DynamoDB is a Serverless NoSQL database that can scale according to demand.

An important cost optimization decision is choosing the appropriate Capacity Mode.

| Capacity Mode | Characteristics | When to Consider |
| --- | --- | --- |
| **On-demand** | Charges based on read/write usage without requiring manual configuration of basic throughput. | Unpredictable or fluctuating traffic. |
| **Provisioned** | Allows read/write throughput to be configured and can be combined with Auto Scaling. | Stable and predictable traffic. |

For Cloud Library during the experimental stage, On-demand is an option worth considering because sufficient usage data is not yet available to predict throughput.

In addition to Capacity Mode, query design also affects costs.

**Optimization methods include:**

- Design appropriate Partition Keys and Sort Keys.
- Use GetItem or Query for common Access Patterns.
- Avoid unnecessary Scan operations on large tables.
- Create Global Secondary Indexes only when clear query requirements exist.
- Monitor data and index storage.
- Use pagination when retrieving large result sets.

For example, when a reader views information about a book using its `bookId`, the application can use GetItem instead of scanning the entire Books table.

It is important to note that Scan and Query have different resource consumption characteristics. A Filter Expression is not a substitute for proper key design.

#### 4.3. Amazon S3

Amazon Simple Storage Service (Amazon S3) is an object storage service.

In Cloud Library, S3 can be used to store:

- Book cover images.
- Documents required by the application.
- Other data objects based on system requirements.

Factors that may affect costs include:

- Storage capacity.
- Storage Class.
- Number of access requests.
- Data transfer.
- Enabled features.

**Optimization strategies:**

- Select an appropriate Storage Class.
- Avoid storing unnecessary objects.
- Optimize image sizes before uploading.
- Manage object versions if S3 Versioning is enabled.
- Use Lifecycle Rules for data groups with clearly defined retention policies.

For example, reducing the size of book cover images can help decrease storage requirements and the amount of data transferred to users.

#### 4.4. Amazon API Gateway

Amazon API Gateway supports building, deploying, and managing APIs.

In the Cloud Library architecture, the frontend sends requests through API Gateway to access backend functions.

API Gateway costs depend on the API type, number of requests, and other factors related to the service's pricing model.

**Optimization strategies:**

- Design endpoints according to application functionality.
- Reduce unnecessary API requests from the frontend.
- Use pagination for large data lists.
- Consider HTTP APIs or REST APIs based on feature requirements.
- Evaluate caching solutions when appropriate for the data characteristics and costs.

The API type should not be selected solely based on price while ignoring authentication, integration, and application requirements.

#### 4.5. Amazon CloudWatch

Amazon CloudWatch supports monitoring system metrics, logs, and alerts.

In Cloud Library, CloudWatch can be used to monitor:

- Lambda execution duration.
- Number of API requests.
- Execution errors.
- Unusual system activity.

However, excessive logging or keeping logs for extended periods may increase costs.

Therefore, the team should:

- Configure appropriate log retention periods.
- Avoid logging unnecessary sensitive information.
- Collect only logs required for monitoring and troubleshooting.
- Monitor expenses associated with monitoring features.

### 5. Hands-on Guide to AWS Cost Management

This section presents a proposed workflow for beginners to monitor and control AWS expenses.

The steps may vary depending on access permissions and the AWS Management Console interface at the time of practice.

#### Step 1: Check Billing Information

1. Sign in to the AWS Management Console.
2. Open `Billing and Cost Management`.
3. Review the overall cost information.
4. Identify services currently generating charges.
5. Review applicable Free Tier information or available account benefits, if any.

This helps users understand their current usage before creating additional resources.

#### Step 2: Use AWS Cost Explorer

1. Open `Billing and Cost Management`.
2. Select `Cost Explorer`.
3. Enable or open Cost Explorer depending on the account's current status.
4. Select the period to analyze.
5. Group costs by `Service`.
6. Observe which services have the highest expenses.
7. Adjust filters to investigate the details.

For example, if DynamoDB accounts for most of the costs, the team can examine:

- Number of read and write operations.
- Table Capacity Mode.
- Usage of Global Secondary Indexes.
- Storage capacity.
- Additional features that have been enabled.

Cost data may not be updated in real time.

#### Step 3: Create a Budget with AWS Budgets

1. In `Billing and Cost Management`, select `Budgets`.
2. Click `Create budget`.
3. Choose the `Cost budget` type.
4. Enter a budget name, such as `CloudLibrary-Monthly-Budget`.
5. Select the `Monthly` period.
6. Enter a budget amount appropriate for the project.
7. Configure alert thresholds.
8. Enter the email address that will receive notifications.
9. Review the configuration and create the budget.

Example budget configuration:

```text
Budget name: CloudLibrary-Monthly-Budget
Period: Monthly
Budget amount: 10 USD

Alert 1: 50% actual cost
Alert 2: 80% actual cost
Alert 3: 100% actual cost
```

These thresholds can be adjusted according to the project's actual financial conditions.

Note that not all advanced AWS Budgets features follow the same pricing model. Users should review the applicable pricing when using features such as Budget Actions or Reports.

#### Step 4: Estimate Costs Using AWS Pricing Calculator

1. Open AWS Pricing Calculator.
2. Create a new Estimate.
3. Add the AWS services to be estimated.
4. Select the appropriate AWS Region.
5. Enter the expected usage parameters.
6. Review the estimated costs.
7. Save or export the results using the supported features.

For Cloud Library, parameters to estimate may include:

| Service | Parameters to Estimate |
| --- | --- |
| AWS Lambda | Number of invocations, memory, and execution duration. |
| Amazon API Gateway | Number of API requests per month. |
| Amazon DynamoDB | Read/write usage, storage, and indexes. |
| Amazon S3 | Object storage, number of requests, and data transfer. |
| Amazon CloudFront | Data transfer volume and number of requests. |

Because Cloud Library's actual usage parameters have not yet been fully measured, a fixed operating cost should not be claimed for the entire system.

#### Step 5: Evaluate and Optimize

After collecting cost data, the team should:

1. Identify services generating high expenses.
2. Review actual resource usage.
3. Detect redundant resources.
4. Propose optimization solutions.
5. Evaluate the impact on performance and security.
6. Implement changes within a safe scope.
7. Monitor costs again after making changes.

This process should be performed periodically because application usage may change over time.

### 6. Applying Cost Optimization to Cloud Library Management System

#### 6.1. Project Overview

Cloud Library Management System is a project aimed at building a library management system on AWS.

The proposed architecture uses services such as:

- React for the user interface.
- Amazon Cognito for authentication.
- Amazon API Gateway for handling API requests.
- AWS Lambda for business logic processing.
- Amazon DynamoDB for storing library data.
- Amazon S3 and CloudFront for storage and content delivery.
- Proposed AI services for intelligent application features.

During implementation, the team needs to consider both technical requirements and operating costs.

#### 6.2. Cost Sources to Monitor

| Component | Cost Sources to Monitor |
| --- | --- |
| AWS Lambda | Invocations and execution resources. |
| API Gateway | Number of API requests. |
| DynamoDB | Read/write operations, storage, GSIs, and related features. |
| Amazon S3 | Storage capacity and access activity. |
| Amazon CloudFront | Content delivery traffic. |
| Amazon Cognito | Usage levels and features included in service tiers. |
| AI Services | Number of requests, amount of processed data, and each service's pricing model. |
| CloudWatch | Logs, metrics, and monitoring features used. |

This list represents cost sources that should be evaluated for the proposed architecture, not actual expenses already incurred by the team.

#### 6.3. Example: Optimizing the Book Search Function

Suppose a user searches for information about a book using the ID `BOOK001`.

An inefficient approach would be to read many records from the Books table and filter the results in the backend.

If the system uses `bookId` as its primary key and only needs to retrieve one specific Item, using GetItem may be more appropriate.

The proposed workflow is:

```text
React Frontend
      |
      v
Amazon API Gateway
      |
      v
AWS Lambda
      |
      v
Amazon DynamoDB
(GetItem by bookId)
      |
      v
Return book information
```

Using appropriate key-based queries helps reduce unnecessary data reads.

For more complex search functions, such as searching by book title or keyword, the team needs to evaluate additional Access Patterns and corresponding query solutions.

#### 6.4. Example: Optimizing Book Cover Images

Cloud Library can store book cover images in Amazon S3.

If each image is larger than necessary for display, loading images may consume excessive bandwidth and increase page loading times.

Some improvement methods include:

- Compress images before uploading them to S3.
- Use appropriate image formats.
- Create suitable image sizes for book lists.
- Use CloudFront to support content delivery.
- Apply appropriate cache configurations.

These changes can help reduce transferred data and improve the user experience.

However, CloudFront and S3 costs still need to be evaluated based on actual usage.

#### 6.5. Example: Optimizing the Lambda Backend

In Cloud Library, backend functions may include:

- Retrieving book lists.
- Viewing book details.
- Processing book borrowing and returns.
- Managing reader profiles.
- Handling reservations.

The team can optimize Lambda by:

1. Reducing redundant processing operations.
2. Avoiding unnecessary database calls.
3. Separating or organizing functions according to deployment requirements.
4. Measuring execution time to adjust memory configurations.
5. Monitoring errors and invocation counts.
6. Testing after configuration changes.

The goal is to use resources efficiently while maintaining the accuracy of business operations.

### 7. Cost Control Plan for Cloud Library

To manage costs effectively, the team can divide activities into several stages.

| Stage | Activities |
| --- | --- |
| **Design** | Identify services, Regions, and expected usage parameters. |
| **Cost Estimation** | Use AWS Pricing Calculator to estimate expenses. |
| **Before Deployment** | Configure AWS Budgets and alerts. |
| **Hands-on Practice** | Create only necessary resources and review them after use. |
| **Testing** | Monitor request counts, storage capacity, and processing duration. |
| **Evaluation** | Use Cost Explorer to analyze expenses. |
| **Optimization** | Adjust architecture or configurations based on usage data. |

A good cost control plan should assign responsibility for periodic checks and define a procedure for responding to unusual expenses.

### 8. Benefits and Considerations of Cost Optimization

#### 8.1. Benefits

Applying AWS Cost Optimization provides several benefits:

- Helps use budgets more efficiently.
- Reduces the risk of unnecessary expenses.
- Improves visibility into AWS resource usage.
- Supports better service and configuration decisions.
- Helps build architectures that match actual requirements.
- Increases awareness of cloud financial management.
- Allows teams to be more proactive when developing and testing applications.

#### 8.2. Important Considerations

**Do Not Sacrifice All Performance to Reduce Costs**

Resource reductions must be evaluated alongside response times and application stability.

**Do Not Ignore Security Requirements**

Changes intended to reduce costs must still maintain security and access control requirements.

**Do Not Assume the Free Tier Covers Every Cost**

AWS Free Tier coverage and eligibility depend on the account, service, and applicable program.

**Do Not Treat AWS Budgets as an Absolute Cost Prevention Mechanism**

Budget alerts help monitor expenses but do not automatically stop all billable activities.

**Do Not Apply the Same Pricing to Every Region**

Prices and billing factors may vary between Regions and service configurations.

**Cost Optimization Is a Continuous Process**

Developers need to regularly evaluate usage and update management practices as their applications evolve.

### 9. Conclusion

AWS Cost Optimization is an important part of designing, deploying, and operating applications on cloud computing platforms.

Through studying the Cost Optimization Pillar of the AWS Well-Architected Framework, I have gained a better understanding of the importance of selecting appropriate resources, managing usage, and evaluating costs periodically.

Additionally, tools such as AWS Cost Explorer, AWS Budgets, and AWS Pricing Calculator support cost analysis, budget configuration, and cost estimation before deployment.

For the **Cloud Library Management System** project, these concepts can be applied to evaluate the costs of Serverless services such as AWS Lambda, Amazon API Gateway, Amazon DynamoDB, and Amazon S3.

The most important lesson is that **cost optimization is not only about reducing AWS expenses but also about building systems that meet technical requirements while using resources and budgets efficiently**.

Combining cost management with architectural design helps make the project more practical and promotes more efficient use of cloud resources.

### 10. Illustrative and Hands-on Images

![Illustration of AWS architecture and cost optimization tools for Cloud Library](/images/3-Blogs/Blogs2/aws-cost-optimization.png)