
---
title: "Các bài blog đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

# CÁC BÀI VIẾT CHIA SẺ KIẾN THỨC AWS

## Tổng quan

Trong quá trình tham gia chương trình thực tập **First Cloud AI Journey (FCAJ)**, em thực hiện nghiên cứu, tổng hợp và xây dựng các bài viết kỹ thuật nhằm củng cố kiến thức đã học về Amazon Web Services (AWS), đồng thời chia sẻ những kiến thức này với cộng đồng.

Theo yêu cầu của chương trình, mỗi cá nhân cần hoàn thành **tối thiểu 3 bài blog kỹ thuật** dựa trên những kiến thức đã học hoặc tìm hiểu, sau đó đăng tải lên cộng đồng **AWS Study Group**.

Các bài viết có thể tập trung vào việc giới thiệu và phân tích dịch vụ AWS, nghiên cứu các chiến lược tối ưu chi phí hoặc hướng dẫn giải quyết những bài toán thực tế bằng công nghệ điện toán đám mây.

Dựa trên những định hướng đó, em lựa chọn ba chủ đề liên quan đến cơ sở dữ liệu NoSQL, tối ưu chi phí và ứng dụng Generative AI. Những chủ đề này cũng có thể liên hệ trực tiếp với dự án **Cloud Library Management System** mà nhóm đang nghiên cứu và phát triển.

---

## 1. Blog 1: Amazon DynamoDB

### Xây dựng cơ sở dữ liệu NoSQL trên AWS

**[Xem chi tiết Blog 1](3.1-Blog1/)**

Bài viết đầu tiên tập trung tìm hiểu **Amazon DynamoDB**, dịch vụ cơ sở dữ liệu NoSQL được quản lý hoàn toàn bởi AWS.

Nội dung bài viết giới thiệu những đặc điểm quan trọng của DynamoDB, phương pháp tổ chức dữ liệu, thiết kế khóa và các thao tác làm việc với cơ sở dữ liệu.

**Nội dung chính:**

- Tổng quan về Amazon DynamoDB và những đặc điểm nổi bật.
- Phân biệt DynamoDB với cơ sở dữ liệu quan hệ.
- Tìm hiểu Table, Item, Attribute, Partition Key và Sort Key.
- Phân tích Global Secondary Index (GSI) và Access Patterns.
- Thực hiện các thao tác CRUD cơ bản.
- Hướng dẫn tạo bảng và thao tác dữ liệu trên AWS.
- Tìm hiểu cách tích hợp DynamoDB với AWS Lambda và API Gateway.
- Nghiên cứu Conditional Writes và Transactions.
- Phân tích bảo mật, hiệu năng và chi phí khi sử dụng DynamoDB.

**Liên hệ với Cloud Library:**

DynamoDB được đề xuất sử dụng làm cơ sở dữ liệu nghiệp vụ chính cho Cloud Library, hỗ trợ quản lý sách, độc giả, bản sách vật lý, phiếu mượn trả và những dữ liệu liên quan.

Bài viết cũng phân tích cách sử dụng các thao tác cập nhật có điều kiện và giao dịch để hạn chế sai lệch số lượng sách khi nhiều yêu cầu mượn trả được xử lý.

**Hướng nội dung:** Giới thiệu và phân tích dịch vụ AWS.

**Bài đăng AWS Study Group:** Sẽ bổ sung đường dẫn sau khi đăng tải.

---

## 2. Blog 2: AWS Cost Optimization

### Chiến lược tối ưu chi phí khi xây dựng ứng dụng Serverless trên AWS

**[Xem chi tiết Blog 2](3.2-Blog2/)**

Bài viết thứ hai tập trung nghiên cứu **AWS Cost Optimization**, một trong sáu trụ cột của AWS Well-Architected Framework.

Nội dung hướng đến việc tìm hiểu cách quản lý ngân sách, phân tích chi phí và lựa chọn tài nguyên AWS phù hợp với nhu cầu của hệ thống.

**Nội dung chính:**

- Giới thiệu AWS Cost Optimization và vai trò trong kiến trúc đám mây.
- Tìm hiểu Cost Optimization Pillar thuộc AWS Well-Architected Framework.
- Phân tích AWS Cost Explorer, AWS Budgets và AWS Pricing Calculator.
- Nghiên cứu các mô hình tính phí và nguyên tắc Pay-as-you-go.
- Tìm hiểu Right-sizing và cách quản lý tài nguyên không còn sử dụng.
- Phân tích phương pháp tối ưu chi phí cho AWS Lambda.
- So sánh DynamoDB On-demand và Provisioned Capacity.
- Tìm hiểu cách tối ưu Amazon S3, API Gateway và CloudWatch.
- Hướng dẫn thiết lập ngân sách và theo dõi chi phí.
- Xây dựng kế hoạch kiểm soát chi phí cho ứng dụng Serverless.

**Liên hệ với Cloud Library:**

Các nguyên tắc Cost Optimization có thể được áp dụng để đánh giá kiến trúc Cloud Library, bao gồm chi phí xử lý backend, truy xuất database, lưu trữ ảnh bìa sách và phân phối nội dung.

Bài viết đề xuất sử dụng AWS Pricing Calculator để lập dự toán, AWS Budgets để thiết lập cảnh báo và Cost Explorer để đánh giá chi phí trong quá trình triển khai.

Các khoản chi phí được đề cập trong bài chỉ phục vụ phân tích và minh họa, không đại diện cho chi phí vận hành thực tế đã đo đạc của dự án.

**Hướng nội dung:** Chiến lược tối ưu chi phí trên AWS.

**Bài đăng AWS Study Group:** Sẽ bổ sung đường dẫn sau khi đăng tải.

---

## 3. Blog 3: Amazon Bedrock Knowledge Bases và RAG

### Xây dựng trợ lý AI hỏi đáp nội quy thư viện

**[Xem chi tiết Blog 3](3.3-Blog3/)**

Bài viết thứ ba nghiên cứu cách ứng dụng **Amazon Bedrock Knowledge Bases** và **Retrieval-Augmented Generation (RAG)** để xây dựng trợ lý AI có khả năng trả lời câu hỏi dựa trên nguồn tài liệu riêng.

Đây là hướng tiếp cận nhằm giải quyết bài toán hỗ trợ độc giả tìm hiểu nội quy và hướng dẫn sử dụng thư viện thông qua ngôn ngữ tự nhiên.

**Nội dung chính:**

- Tổng quan về Amazon Bedrock và Generative AI.
- Giới thiệu Retrieval-Augmented Generation (RAG).
- Tìm hiểu Embeddings, Semantic Search, Chunking và Vector Store.
- Phân tích vai trò của Amazon Bedrock Knowledge Bases.
- Nghiên cứu cách sử dụng Amazon S3 làm nguồn tài liệu.
- Tìm hiểu quy trình đồng bộ và lập chỉ mục tài liệu.
- Thiết kế kiến trúc RAG kết hợp API Gateway và AWS Lambda.
- Hướng dẫn tạo và kiểm thử Knowledge Base.
- Minh họa cách sử dụng API RetrieveAndGenerate bằng Node.js.
- Phân tích các yêu cầu về bảo mật, độ chính xác và tối ưu chi phí.

**Liên hệ với Cloud Library:**

Amazon Bedrock Knowledge Bases được đề xuất sử dụng để xây dựng trợ lý AI hỗ trợ độc giả tìm hiểu quy định mượn trả, gia hạn, đặt trước và xử lý sách quá hạn.

Nguồn kiến thức có thể bao gồm các tài liệu nội quy được lưu trên Amazon S3, trong khi dữ liệu giao dịch của người dùng vẫn được quản lý trong database nghiệp vụ.

Giải pháp RAG là một hướng nghiên cứu và triển khai đề xuất, không đồng nghĩa với việc toàn bộ chức năng AI đã được hoàn thiện trong hệ thống thực tế.

**Hướng nội dung:** Hướng dẫn giải quyết bài toán thực tế bằng dịch vụ AWS.

**Bài đăng AWS Study Group:** Sẽ bổ sung đường dẫn sau khi đăng tải.

---

## 4. Tổng kết ba bài blog

| Blog | Chủ đề | Kiến thức trọng tâm |
| --- | --- | --- |
| **Blog 1** | Amazon DynamoDB | Cơ sở dữ liệu NoSQL, thiết kế dữ liệu và tích hợp Serverless. |
| **Blog 2** | AWS Cost Optimization | Quản lý ngân sách, phân tích và tối ưu chi phí dịch vụ AWS. |
| **Blog 3** | Amazon Bedrock Knowledge Bases và RAG | Generative AI, truy xuất tài liệu và xây dựng trợ lý AI. |

Ba bài viết được lựa chọn để tìm hiểu những khía cạnh khác nhau của việc phát triển ứng dụng trên AWS, từ quản lý dữ liệu, kiểm soát chi phí đến tích hợp trí tuệ nhân tạo.

Nhờ đó, nội dung nghiên cứu không chỉ tập trung vào từng dịch vụ riêng lẻ mà còn hỗ trợ việc xây dựng kiến trúc và định hướng phát triển dự án Cloud Library Management System.

## 5. Mục tiêu và kiến thức đạt được

Thông qua quá trình nghiên cứu và xây dựng ba bài blog, em hướng đến những mục tiêu:

- Củng cố kiến thức về các dịch vụ AWS đã học trong chương trình FCAJ.
- Rèn luyện khả năng nghiên cứu và đọc tài liệu kỹ thuật.
- Hiểu rõ cách lựa chọn dịch vụ phù hợp với yêu cầu ứng dụng.
- Nâng cao kiến thức về cơ sở dữ liệu NoSQL và kiến trúc Serverless.
- Tìm hiểu các phương pháp quản lý và tối ưu chi phí AWS.
- Tiếp cận cách xây dựng ứng dụng Generative AI với RAG.
- Phát triển kỹ năng viết bài kỹ thuật và trình bày kiến thức.
- Rèn luyện khả năng xây dựng ví dụ, sơ đồ kiến trúc và hướng dẫn thực hành.
- Liên hệ kiến thức đã học với bài toán thực tế trong Cloud Library Management System.
- Chia sẻ kiến thức và trao đổi kinh nghiệm cùng cộng đồng AWS.

## 6. Chia sẻ bài viết lên AWS Study Group

Theo yêu cầu của chương trình FCAJ, các bài blog sau khi hoàn thiện sẽ được đăng tải và chia sẻ tại cộng đồng AWS Study Group trên Facebook.

**Cộng đồng:** [AWS Study Group - Facebook](https://www.facebook.com/groups/awsstudygroupfcj)

Các đường dẫn đến từng bài đăng sẽ được cập nhật sau khi bài viết được công bố.

Việc chia sẻ bài viết giúp em tổng hợp lại những kiến thức đã nghiên cứu, đồng thời tạo cơ hội tiếp nhận ý kiến đóng góp và học hỏi thêm kinh nghiệm từ cộng đồng AWS.
