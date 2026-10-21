---
title: "Blog 2: AWS Cost Optimization - Chiến lược tối ưu chi phí trên AWS"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# AWS COST OPTIMIZATION

## Chiến lược tối ưu chi phí khi xây dựng ứng dụng Serverless trên AWS

Khi xây dựng và triển khai ứng dụng trên nền tảng điện toán đám mây, một trong những vấn đề quan trọng mà nhà phát triển cần quan tâm là chi phí vận hành hệ thống.

Amazon Web Services (AWS) cung cấp nhiều dịch vụ giúp doanh nghiệp và nhà phát triển xây dựng ứng dụng mà không cần đầu tư vào hạ tầng máy chủ vật lý. Tuy nhiên, việc sử dụng tài nguyên AWS không phù hợp có thể dẫn đến những khoản chi phí phát sinh ngoài dự kiến.

Đặc biệt, khi phát triển các dự án học tập hoặc ứng dụng thử nghiệm, người dùng thường tập trung vào việc triển khai chức năng mà chưa quan tâm đúng mức đến cách theo dõi và tối ưu hóa chi phí.

Để giải quyết vấn đề này, AWS cung cấp các công cụ hỗ trợ quản lý tài chính đám mây như **AWS Cost Explorer, AWS Budgets và AWS Pricing Calculator**.

Bên cạnh việc sử dụng các công cụ quản lý chi phí, nhà phát triển còn có thể tối ưu kiến trúc hệ thống bằng cách lựa chọn dịch vụ, cấu hình tài nguyên và mô hình tính phí phù hợp.

Trong bài viết này, chúng ta sẽ tìm hiểu những nguyên tắc cơ bản của **AWS Cost Optimization**, các công cụ hỗ trợ quản lý chi phí và cách áp dụng những kiến thức này vào dự án **Cloud Library Management System**.

### Các điểm chính cần nắm

- **AWS Cost Optimization:** Quá trình tối ưu chi phí sử dụng tài nguyên AWS.
- **AWS Well-Architected Framework:** Bộ hướng dẫn thiết kế và vận hành hệ thống trên AWS.
- **Cost Optimization Pillar:** Trụ cột tập trung vào việc sử dụng tài nguyên hiệu quả về mặt chi phí.
- **AWS Cost Explorer:** Công cụ phân tích chi phí và mức sử dụng AWS.
- **AWS Budgets:** Dịch vụ thiết lập ngân sách và cảnh báo chi phí.
- **AWS Pricing Calculator:** Công cụ ước tính chi phí dịch vụ AWS trước khi triển khai.
- **Pay-as-you-go:** Mô hình thanh toán dựa trên mức sử dụng.
- **Right-sizing:** Lựa chọn tài nguyên phù hợp với nhu cầu thực tế.
- **Serverless:** Mô hình triển khai giảm nhu cầu quản lý máy chủ.
- **Cost Monitoring:** Theo dõi, phân tích và kiểm soát chi phí trong quá trình vận hành.

### 1. Tổng quan về AWS Cost Optimization

#### 1.1. AWS Cost Optimization là gì?

AWS Cost Optimization là quá trình phân tích, quản lý và điều chỉnh việc sử dụng tài nguyên AWS nhằm đáp ứng yêu cầu của hệ thống với mức chi phí hợp lý.

Mục tiêu của Cost Optimization không đơn giản là giảm chi phí xuống mức thấp nhất.

Thay vào đó, hệ thống cần đạt được sự cân bằng giữa:

- Chi phí vận hành.
- Hiệu năng ứng dụng.
- Khả năng mở rộng.
- Tính sẵn sàng.
- Bảo mật.
- Nhu cầu sử dụng thực tế.

Ví dụ, một ứng dụng có thể tiết kiệm chi phí bằng cách giảm tài nguyên xử lý. Tuy nhiên, nếu việc giảm tài nguyên khiến ứng dụng phản hồi chậm hoặc thường xuyên gặp lỗi thì giải pháp này chưa thực sự hiệu quả.

Vì vậy, tối ưu chi phí cần được thực hiện dựa trên mục tiêu kỹ thuật và nhu cầu nghiệp vụ.

#### 1.2. Tại sao cần tối ưu chi phí trên AWS?

AWS cung cấp nhiều mô hình tính phí linh hoạt. Người dùng có thể trả tiền dựa trên thời gian sử dụng, số lượng yêu cầu, dung lượng lưu trữ hoặc các tài nguyên đã cấu hình.

Điều này mang lại nhiều lợi ích nhưng cũng đòi hỏi người dùng phải quản lý mức sử dụng một cách hợp lý.

Một số nguyên nhân có thể làm tăng chi phí AWS:

- Duy trì những tài nguyên không còn sử dụng.
- Cấu hình tài nguyên lớn hơn nhu cầu thực tế.
- Lưu trữ dữ liệu hoặc log không cần thiết trong thời gian dài.
- Thực hiện nhiều yêu cầu API không cần thiết.
- Sử dụng phương thức truy vấn database chưa hiệu quả.
- Không theo dõi chi phí phát sinh.
- Không thiết lập ngân sách và cảnh báo.

Đối với các dự án sinh viên, việc hiểu cách kiểm soát chi phí giúp quá trình học tập và thử nghiệm dịch vụ AWS được chủ động hơn.

#### 1.3. Cost Optimization trong AWS Well-Architected Framework

AWS Well-Architected Framework là bộ hướng dẫn giúp nhà phát triển đánh giá và cải thiện kiến trúc ứng dụng trên AWS.

Framework bao gồm sáu trụ cột:

1. Operational Excellence.
2. Security.
3. Reliability.
4. Performance Efficiency.
5. Cost Optimization.
6. Sustainability.

Trong đó, **Cost Optimization Pillar** tập trung vào việc sử dụng tài nguyên và lựa chọn giải pháp phù hợp để tạo ra giá trị với chi phí hiệu quả.

Các lĩnh vực thực hành quan trọng bao gồm:

| Lĩnh vực | Ý nghĩa |
| --- | --- |
| Cloud Financial Management | Xây dựng khả năng quản lý tài chính đám mây. |
| Expenditure and Usage Awareness | Hiểu rõ chi phí và mức sử dụng tài nguyên. |
| Cost-effective Resources | Lựa chọn tài nguyên và dịch vụ hiệu quả về chi phí. |
| Manage Demand and Supply | Điều chỉnh tài nguyên theo nhu cầu sử dụng. |
| Optimize Over Time | Liên tục đánh giá và cải thiện chi phí. |

Những nguyên tắc này có thể được áp dụng ngay từ giai đoạn thiết kế dự án, thay vì chỉ xem xét khi hóa đơn AWS tăng lên.

### 2. Các công cụ hỗ trợ quản lý chi phí AWS

AWS cung cấp nhiều công cụ phục vụ các nhu cầu khác nhau trong quản lý chi phí.

Ba công cụ được giới thiệu trong bài viết là AWS Cost Explorer, AWS Budgets và AWS Pricing Calculator.

#### 2.1. AWS Cost Explorer

AWS Cost Explorer là công cụ giúp người dùng quan sát, phân tích và tìm hiểu chi phí sử dụng AWS.

Thông qua Cost Explorer, người dùng có thể:

- Theo dõi tổng chi phí theo khoảng thời gian.
- Phân tích chi phí theo từng dịch vụ AWS.
- Quan sát xu hướng tăng hoặc giảm chi phí.
- Lọc dữ liệu theo tài khoản, Region hoặc những chiều dữ liệu được hỗ trợ.
- Xem thông tin dự báo chi phí theo chức năng có sẵn.

Ví dụ, nếu một dự án sử dụng Amazon DynamoDB, AWS Lambda và Amazon S3, Cost Explorer có thể hỗ trợ xác định dịch vụ nào đang tạo ra phần lớn chi phí.

Từ đó, nhà phát triển có thể tập trung kiểm tra những dịch vụ có mức sử dụng cao.

#### 2.2. AWS Budgets

AWS Budgets cho phép người dùng thiết lập ngân sách và nhận thông báo khi chi phí hoặc mức sử dụng đạt các ngưỡng đã cấu hình.

Ví dụ, một dự án học tập có thể thiết lập ngân sách minh họa:

```text
Tên ngân sách: CloudLibrary-Monthly-Budget

Loại ngân sách: Cost Budget

Khoảng thời gian: Monthly

Ngân sách dự kiến: 10 USD
```

Trong ví dụ trên, 10 USD chỉ là mức ngân sách giả định do nhóm tự lựa chọn, không phải mức phí cố định hoặc chi phí dự báo của Cloud Library.

Người dùng có thể thiết lập cảnh báo khi chi phí thực tế đạt các ngưỡng như:

| Ngưỡng | Mục đích |
| --- | --- |
| 50% | Theo dõi mức sử dụng ban đầu. |
| 80% | Kiểm tra các dịch vụ đang phát sinh chi phí. |
| 100% | Đánh giá nguy cơ vượt ngân sách. |

AWS Budgets có thể gửi thông báo qua email dựa trên cấu hình cảnh báo.

**Lưu ý:** Ngân sách và cảnh báo thông thường không tự động ngăn phát sinh chi phí. Cảnh báo cũng có thể có độ trễ so với mức sử dụng thực tế.

Vì vậy, AWS Budgets là công cụ hỗ trợ kiểm soát chi phí, không phải cơ chế bảo đảm tài khoản không bao giờ vượt ngân sách.

#### 2.3. AWS Pricing Calculator

AWS Pricing Calculator là công cụ giúp người dùng xây dựng ước tính chi phí trước khi triển khai ứng dụng.

Người dùng có thể lựa chọn dịch vụ AWS và nhập các thông số sử dụng dự kiến.

Ví dụ, khi xây dựng Cloud Library, nhóm có thể lập dự toán cho:

- AWS Lambda.
- Amazon API Gateway.
- Amazon DynamoDB.
- Amazon S3.
- Amazon CloudFront.
- Những dịch vụ AWS khác được sử dụng trong kiến trúc.

Đối với từng dịch vụ, cần xác định những thông số phù hợp như số lượng yêu cầu, dung lượng lưu trữ hoặc cấu hình tài nguyên.

Kết quả từ AWS Pricing Calculator là **ước tính**, không phải hóa đơn chắc chắn của hệ thống.

Chi phí thực tế có thể thay đổi tùy AWS Region, cách sử dụng dịch vụ, cấu hình và bảng giá tại thời điểm triển khai.

#### 2.4. So sánh ba công cụ

| Công cụ | Chức năng chính | Thời điểm sử dụng |
| --- | --- | --- |
| **AWS Cost Explorer** | Phân tích chi phí đã phát sinh và xu hướng sử dụng. | Trong quá trình vận hành. |
| **AWS Budgets** | Thiết lập ngân sách và cảnh báo. | Trước và trong khi triển khai. |
| **AWS Pricing Calculator** | Ước tính chi phí theo cấu hình dự kiến. | Khi thiết kế và lập kế hoạch. |

Ba công cụ bổ trợ cho nhau trong quá trình quản lý tài chính đám mây.

### 3. Các chiến lược tối ưu chi phí trên AWS

#### 3.1. Lựa chọn mô hình tính phí phù hợp

AWS cung cấp những mô hình tính phí khác nhau tùy từng dịch vụ.

Ví dụ:

- Một số dịch vụ tính phí theo lượng tài nguyên sử dụng.
- Một số dịch vụ tính phí theo số lượng yêu cầu.
- Một số dịch vụ tính phí theo dung lượng lưu trữ.
- Một số dịch vụ có những hình thức cam kết sử dụng để được hưởng mức giá phù hợp.

Đối với ứng dụng học tập có lưu lượng không ổn định, mô hình thanh toán theo mức sử dụng có thể thuận tiện hơn việc duy trì tài nguyên lớn trong thời gian dài.

Tuy nhiên, cần so sánh cụ thể theo từng dịch vụ thay vì cho rằng một mô hình luôn rẻ hơn mọi mô hình khác.

#### 3.2. Right-sizing tài nguyên

Right-sizing là quá trình lựa chọn và điều chỉnh tài nguyên để phù hợp với khối lượng công việc thực tế.

Ví dụ, nếu một Lambda Function chỉ cần một lượng bộ nhớ nhỏ để xử lý yêu cầu API, việc cấu hình bộ nhớ quá lớn có thể tạo ra chi phí không cần thiết.

Ngược lại, cấp quá ít bộ nhớ có thể khiến thời gian thực thi tăng lên.

Do đó, cần đo đạc và thử nghiệm trước khi lựa chọn cấu hình.

#### 3.3. Loại bỏ tài nguyên không còn sử dụng

Trong quá trình học AWS, người dùng có thể tạo nhiều tài nguyên để thực hành.

Sau khi hoàn tất bài thực hành, một số tài nguyên có thể vẫn tiếp tục tồn tại.

Ví dụ:

- Những tài nguyên thử nghiệm không còn cần thiết.
- Dữ liệu lưu trữ tạm thời.
- Bản sao hoặc phiên bản dữ liệu không còn sử dụng.
- Các log không cần giữ lâu dài.

Việc thường xuyên rà soát tài nguyên giúp giảm nguy cơ phát sinh chi phí ngoài dự kiến.

Tuy nhiên, trước khi xóa cần kiểm tra các quan hệ phụ thuộc và yêu cầu lưu giữ dữ liệu.

#### 3.4. Tối ưu kiến trúc Serverless

Kiến trúc Serverless giúp nhà phát triển giảm công việc quản trị máy chủ và hỗ trợ khả năng mở rộng theo nhu cầu.

Một số dịch vụ Serverless trên AWS gồm:

- AWS Lambda.
- Amazon API Gateway.
- Amazon DynamoDB.
- Amazon EventBridge.
- Amazon S3.

Khi được thiết kế phù hợp, kiến trúc Serverless có thể tiết kiệm chi phí đối với những ứng dụng có lưu lượng thay đổi.

Tuy nhiên, nếu số lượng yêu cầu hoặc thời gian xử lý tăng cao, chi phí Serverless cũng có thể tăng tương ứng.

Vì vậy, lựa chọn Serverless không đồng nghĩa với việc hệ thống luôn có chi phí thấp nhất.

### 4. Tối ưu chi phí các dịch vụ trong kiến trúc Serverless

#### 4.1. AWS Lambda

AWS Lambda cho phép chạy mã mà không cần quản lý máy chủ.

Chi phí Lambda phụ thuộc vào những yếu tố như:

- Số lượng yêu cầu.
- Thời gian thực thi.
- Bộ nhớ được cấu hình.
- Kiến trúc bộ xử lý và các tính năng tính phí liên quan.

**Chiến lược tối ưu:**

- Tránh gọi Lambda khi không cần thiết.
- Tối ưu mã nguồn để giảm thời gian xử lý.
- Kiểm tra cấu hình bộ nhớ.
- Hạn chế thực hiện các truy vấn database dư thừa.
- Theo dõi Duration, Errors và Invocations bằng CloudWatch.

Ví dụ, trong Cloud Library, API lấy thông tin sách nên chỉ truy xuất những dữ liệu cần thiết thay vì xử lý toàn bộ danh mục trong mỗi yêu cầu.

#### 4.2. Amazon DynamoDB

Amazon DynamoDB là cơ sở dữ liệu NoSQL Serverless có khả năng mở rộng theo nhu cầu.

Một trong những quyết định quan trọng khi tối ưu chi phí là lựa chọn Capacity Mode.

| Capacity Mode | Đặc điểm | Trường hợp cân nhắc |
| --- | --- | --- |
| **On-demand** | Tính phí theo mức sử dụng đọc/ghi, không cần tự cấu hình thông lượng cơ bản. | Lưu lượng chưa ổn định hoặc khó dự đoán. |
| **Provisioned** | Cấu hình thông lượng đọc/ghi và có thể kết hợp Auto Scaling. | Lưu lượng ổn định, có thể dự đoán. |

Đối với Cloud Library ở giai đoạn thử nghiệm, On-demand là một lựa chọn đáng cân nhắc vì chưa có dữ liệu sử dụng thực tế để dự đoán thông lượng.

Ngoài Capacity Mode, thiết kế truy vấn cũng ảnh hưởng đến chi phí.

**Một số phương pháp tối ưu:**

- Thiết kế Partition Key và Sort Key phù hợp.
- Sử dụng GetItem hoặc Query cho những Access Patterns phổ biến.
- Tránh Scan không cần thiết trên bảng lớn.
- Chỉ tạo Global Secondary Index khi có nhu cầu truy vấn rõ ràng.
- Theo dõi dung lượng dữ liệu và chỉ mục.
- Sử dụng cơ chế phân trang khi truy vấn nhiều kết quả.

Ví dụ, khi độc giả xem thông tin một cuốn sách theo `bookId`, ứng dụng có thể sử dụng GetItem thay vì Scan toàn bộ bảng Books.

Lưu ý rằng Scan và Query có cơ chế tiêu thụ tài nguyên riêng; Filter Expression không phải giải pháp thay thế cho việc thiết kế khóa hợp lý.

#### 4.3. Amazon S3

Amazon Simple Storage Service (Amazon S3) là dịch vụ lưu trữ đối tượng.

Trong Cloud Library, S3 có thể được sử dụng để lưu:

- Hình ảnh bìa sách.
- Tài liệu phục vụ ứng dụng.
- Những đối tượng dữ liệu khác theo yêu cầu của hệ thống.

Các yếu tố ảnh hưởng đến chi phí có thể bao gồm:

- Dung lượng lưu trữ.
- Storage Class.
- Số lượng yêu cầu truy cập.
- Truyền dữ liệu.
- Những tính năng được bật.

**Chiến lược tối ưu:**

- Lựa chọn Storage Class phù hợp.
- Hạn chế lưu trữ những đối tượng không cần thiết.
- Tối ưu kích thước hình ảnh trước khi tải lên.
- Quản lý phiên bản đối tượng nếu bật S3 Versioning.
- Sử dụng Lifecycle Rules cho các nhóm dữ liệu có chính sách lưu giữ rõ ràng.

Ví dụ, việc giảm kích thước ảnh bìa sách có thể giúp giảm dung lượng lưu trữ và dữ liệu cần truyền đến người dùng.

#### 4.4. Amazon API Gateway

Amazon API Gateway hỗ trợ xây dựng, triển khai và quản lý API.

Trong kiến trúc Cloud Library, frontend gửi yêu cầu qua API Gateway để truy cập các chức năng backend.

Chi phí API Gateway phụ thuộc vào loại API, số lượng yêu cầu và những yếu tố liên quan theo mô hình tính phí của dịch vụ.

**Chiến lược tối ưu:**

- Thiết kế endpoint phù hợp với chức năng.
- Hạn chế những yêu cầu API không cần thiết từ frontend.
- Sử dụng phân trang cho danh sách dữ liệu lớn.
- Cân nhắc HTTP API hoặc REST API theo yêu cầu tính năng.
- Đánh giá giải pháp caching khi phù hợp với đặc điểm dữ liệu và chi phí.

Không nên lựa chọn loại API chỉ dựa trên mức giá mà bỏ qua yêu cầu xác thực, tích hợp và tính năng ứng dụng.

#### 4.5. Amazon CloudWatch

Amazon CloudWatch hỗ trợ theo dõi chỉ số, log và cảnh báo hoạt động của hệ thống.

Trong Cloud Library, CloudWatch có thể được sử dụng để giám sát:

- Thời gian xử lý Lambda.
- Số lượng yêu cầu API.
- Lỗi thực thi.
- Hoạt động bất thường.

Tuy nhiên, việc lưu log quá nhiều hoặc giữ log trong thời gian dài có thể ảnh hưởng đến chi phí.

Do đó, nhóm cần:

- Cấu hình thời gian lưu giữ log hợp lý.
- Không ghi dữ liệu nhạy cảm không cần thiết.
- Chỉ thu thập những log phục vụ việc giám sát và khắc phục lỗi.
- Theo dõi chi phí phát sinh từ tính năng giám sát.

### 5. Hướng dẫn thực hành quản lý chi phí AWS

Phần này trình bày quy trình đề xuất để người mới bắt đầu theo dõi và kiểm soát chi phí AWS.

Các thao tác có thể khác nhau tùy quyền truy cập và giao diện AWS Management Console tại thời điểm thực hành.

#### Bước 1: Kiểm tra thông tin Billing

1. Đăng nhập AWS Management Console.
2. Mở `Billing and Cost Management`.
3. Kiểm tra khu vực tổng quan chi phí.
4. Xem các dịch vụ đang phát sinh phí.
5. Kiểm tra thông tin Free Tier hoặc ưu đãi hiện có của tài khoản nếu áp dụng.

Việc này giúp người dùng hiểu tình trạng sử dụng trước khi tạo thêm tài nguyên.

#### Bước 2: Sử dụng AWS Cost Explorer

1. Mở `Billing and Cost Management`.
2. Chọn `Cost Explorer`.
3. Bật hoặc mở Cost Explorer tùy trạng thái tài khoản.
4. Chọn khoảng thời gian cần phân tích.
5. Chọn cách nhóm chi phí theo `Service`.
6. Quan sát các dịch vụ có mức chi phí cao.
7. Điều chỉnh bộ lọc để kiểm tra chi tiết.

Ví dụ, nếu DynamoDB phát sinh phần lớn chi phí, nhóm có thể kiểm tra:

- Số lượng thao tác đọc và ghi.
- Capacity Mode của bảng.
- Mức sử dụng các GSI.
- Dung lượng lưu trữ.
- Những tính năng bổ sung được bật.

Cần lưu ý dữ liệu chi phí có thể không cập nhật tức thời.

#### Bước 3: Tạo ngân sách bằng AWS Budgets

1. Trong `Billing and Cost Management`, chọn `Budgets`.
2. Chọn `Create budget`.
3. Chọn loại ngân sách `Cost budget`.
4. Đặt tên ngân sách, ví dụ `CloudLibrary-Monthly-Budget`.
5. Chọn chu kỳ `Monthly`.
6. Nhập mức ngân sách phù hợp với kế hoạch.
7. Thiết lập những ngưỡng cảnh báo.
8. Nhập địa chỉ email nhận thông báo.
9. Kiểm tra cấu hình và tạo ngân sách.

Ví dụ ngân sách minh họa:

```text
Budget name: CloudLibrary-Monthly-Budget
Period: Monthly
Budget amount: 10 USD

Alert 1: 50% actual cost
Alert 2: 80% actual cost
Alert 3: 100% actual cost
```

Các ngưỡng này có thể được điều chỉnh theo điều kiện tài chính thực tế.

Lưu ý rằng không phải mọi tính năng nâng cao của AWS Budgets đều có cùng mô hình tính phí. Nên kiểm tra bảng giá nếu sử dụng những chức năng như Budget Actions hoặc Reports.

#### Bước 4: Ước tính chi phí bằng AWS Pricing Calculator

1. Truy cập AWS Pricing Calculator.
2. Chọn tạo một Estimate mới.
3. Thêm dịch vụ cần ước tính.
4. Chọn AWS Region phù hợp.
5. Nhập thông số sử dụng dự kiến.
6. Kiểm tra chi phí ước tính.
7. Lưu hoặc xuất kết quả theo tính năng được hỗ trợ.

Ví dụ, đối với Cloud Library, các thông số cần dự kiến có thể gồm:

| Dịch vụ | Thông số cần ước tính |
| --- | --- |
| AWS Lambda | Số lượt gọi, bộ nhớ, thời gian xử lý. |
| Amazon API Gateway | Số yêu cầu API mỗi tháng. |
| Amazon DynamoDB | Lượt đọc/ghi, dung lượng và chỉ mục. |
| Amazon S3 | Dung lượng đối tượng, số request và truyền dữ liệu. |
| Amazon CloudFront | Lưu lượng truyền dữ liệu và số yêu cầu. |

Vì các thông số thực tế của Cloud Library chưa được đo đạc đầy đủ, không nên khẳng định một mức chi phí cố định cho toàn bộ hệ thống.

#### Bước 5: Đánh giá và tối ưu

Sau khi có dữ liệu chi phí, nhóm cần:

1. Xác định dịch vụ phát sinh nhiều chi phí.
2. Kiểm tra mức sử dụng thực tế.
3. Xác định tài nguyên dư thừa.
4. Đề xuất phương án tối ưu.
5. Đánh giá ảnh hưởng đến hiệu năng và bảo mật.
6. Thực hiện thay đổi trong phạm vi an toàn.
7. Theo dõi lại chi phí sau khi thay đổi.

Quá trình này cần được thực hiện định kỳ vì mức sử dụng ứng dụng có thể thay đổi theo thời gian.

### 6. Ứng dụng Cost Optimization vào Cloud Library Management System

#### 6.1. Tổng quan dự án

Cloud Library Management System là dự án xây dựng hệ thống quản lý thư viện trên AWS.

Kiến trúc đề xuất sử dụng các dịch vụ như:

- React cho giao diện người dùng.
- Amazon Cognito để xác thực.
- Amazon API Gateway để tiếp nhận yêu cầu API.
- AWS Lambda để xử lý nghiệp vụ.
- Amazon DynamoDB để lưu dữ liệu thư viện.
- Amazon S3 và CloudFront phục vụ lưu trữ, phân phối nội dung.
- Những dịch vụ AI được đề xuất cho các chức năng thông minh.

Trong quá trình triển khai, nhóm cần cân nhắc cả yêu cầu kỹ thuật và chi phí vận hành.

#### 6.2. Những nguồn chi phí cần quan tâm

| Thành phần | Nguồn chi phí cần theo dõi |
| --- | --- |
| AWS Lambda | Số lượt gọi và tài nguyên thực thi. |
| API Gateway | Số lượng API Requests. |
| DynamoDB | Lượt đọc/ghi, dung lượng, GSI và các tính năng liên quan. |
| Amazon S3 | Dung lượng lưu trữ và hoạt động truy cập. |
| Amazon CloudFront | Lưu lượng phân phối nội dung. |
| Amazon Cognito | Mức sử dụng và các tính năng thuộc gói dịch vụ. |
| Dịch vụ AI | Số lượng yêu cầu, lượng dữ liệu xử lý và cách tính phí của từng dịch vụ. |
| CloudWatch | Log, metrics và những tính năng giám sát sử dụng. |

Danh sách trên là các nguồn chi phí cần đánh giá theo kiến trúc dự kiến, không phải bảng chi phí đã phát sinh thực tế của nhóm.

#### 6.3. Ví dụ tối ưu chức năng tìm kiếm sách

Giả sử người dùng tìm kiếm thông tin một cuốn sách theo mã `BOOK001`.

Một cách thiết kế chưa hiệu quả là đọc nhiều bản ghi trong bảng Books rồi lọc kết quả tại backend.

Nếu hệ thống đã có `bookId` làm khóa chính và chỉ cần tìm một Item cụ thể, việc sử dụng GetItem có thể phù hợp hơn.

Quy trình đề xuất:

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

Việc truy vấn theo khóa phù hợp giúp hạn chế đọc dữ liệu không cần thiết.

Đối với những chức năng tìm kiếm phức tạp như tìm theo tên sách hoặc từ khóa, nhóm cần đánh giá thêm Access Patterns và giải pháp truy vấn tương ứng.

#### 6.4. Ví dụ tối ưu hình ảnh bìa sách

Cloud Library có thể lưu ảnh bìa sách trên Amazon S3.

Nếu mỗi ảnh có dung lượng lớn hơn nhu cầu hiển thị, việc tải ảnh có thể tiêu tốn nhiều băng thông và ảnh hưởng đến thời gian tải trang.

Một số phương pháp cải thiện:

- Nén ảnh trước khi tải lên S3.
- Sử dụng định dạng ảnh phù hợp.
- Tạo kích thước ảnh phù hợp cho danh sách sách.
- Sử dụng CloudFront để hỗ trợ phân phối nội dung.
- Áp dụng cấu hình cache phù hợp.

Những thay đổi này có thể giúp giảm lượng dữ liệu được truyền và cải thiện trải nghiệm người dùng.

Tuy nhiên, chi phí CloudFront và S3 vẫn cần được kiểm tra theo mức sử dụng thực tế.

#### 6.5. Ví dụ tối ưu backend Lambda

Trong Cloud Library, các chức năng backend có thể bao gồm:

- Lấy danh sách sách.
- Xem chi tiết sách.
- Xử lý mượn và trả sách.
- Quản lý hồ sơ độc giả.
- Xử lý đặt trước.

Nhóm có thể tối ưu Lambda bằng cách:

1. Giảm các thao tác xử lý dư thừa.
2. Hạn chế gọi database nhiều lần không cần thiết.
3. Tách hoặc tổ chức chức năng theo yêu cầu triển khai.
4. Đo thời gian thực thi để điều chỉnh bộ nhớ.
5. Theo dõi lỗi và số lần gọi.
6. Kiểm thử sau khi thay đổi cấu hình.

Mục tiêu là sử dụng tài nguyên hợp lý mà vẫn bảo đảm tính chính xác của nghiệp vụ.

### 7. Lập kế hoạch kiểm soát chi phí cho Cloud Library

Để quản lý chi phí hiệu quả, nhóm có thể chia hoạt động theo từng giai đoạn.

| Giai đoạn | Hoạt động |
| --- | --- |
| **Thiết kế** | Xác định dịch vụ, Region và thông số sử dụng dự kiến. |
| **Lập dự toán** | Sử dụng AWS Pricing Calculator để ước tính chi phí. |
| **Trước triển khai** | Thiết lập AWS Budgets và cảnh báo. |
| **Thực hành** | Chỉ tạo tài nguyên cần thiết và kiểm tra tài nguyên sau khi sử dụng. |
| **Kiểm thử** | Theo dõi số lượng request, dung lượng và thời gian xử lý. |
| **Đánh giá** | Sử dụng Cost Explorer để phân tích các khoản chi phí. |
| **Tối ưu** | Điều chỉnh kiến trúc hoặc cấu hình dựa trên dữ liệu. |

Một kế hoạch kiểm soát chi phí tốt cần có người phụ trách kiểm tra định kỳ và quy trình xử lý khi xuất hiện khoản phí bất thường.

### 8. Lợi ích và những lưu ý khi tối ưu chi phí

#### 8.1. Lợi ích

Việc áp dụng AWS Cost Optimization mang lại nhiều lợi ích:

- Hỗ trợ sử dụng ngân sách hiệu quả hơn.
- Giảm nguy cơ phát sinh chi phí không cần thiết.
- Nâng cao khả năng theo dõi tài nguyên AWS.
- Cải thiện việc lựa chọn dịch vụ và cấu hình.
- Hỗ trợ xây dựng kiến trúc phù hợp với nhu cầu thực tế.
- Tăng nhận thức về quản lý tài chính đám mây.
- Giúp nhóm chủ động hơn khi phát triển và thử nghiệm ứng dụng.

#### 8.2. Những lưu ý quan trọng

**Không đánh đổi toàn bộ hiệu năng để giảm chi phí**

Việc giảm tài nguyên cần được đánh giá cùng với thời gian phản hồi và tính ổn định của ứng dụng.

**Không bỏ qua yêu cầu bảo mật**

Những thay đổi giúp giảm chi phí vẫn phải duy trì các yêu cầu bảo mật và kiểm soát truy cập.

**Không mặc định Free Tier bao phủ mọi chi phí**

Phạm vi và điều kiện ưu đãi của AWS phụ thuộc vào tài khoản, dịch vụ và chương trình áp dụng.

**Không xem AWS Budgets là cơ chế chặn chi phí tuyệt đối**

Cảnh báo ngân sách giúp theo dõi tình trạng chi phí nhưng không tự động dừng toàn bộ hoạt động tính phí.

**Không sử dụng một mức giá chung cho mọi Region**

Giá và các yếu tố tính phí có thể khác nhau giữa các Region và cấu hình dịch vụ.

**Tối ưu chi phí là quá trình liên tục**

Nhà phát triển cần thường xuyên đánh giá mức sử dụng và cập nhật phương pháp quản lý khi ứng dụng thay đổi.

### 9. Kết luận

AWS Cost Optimization là một phần quan trọng trong quá trình thiết kế, triển khai và vận hành ứng dụng trên nền tảng điện toán đám mây.

Thông qua việc tìm hiểu Cost Optimization Pillar thuộc AWS Well-Architected Framework, em hiểu rõ hơn tầm quan trọng của việc lựa chọn tài nguyên phù hợp, quản lý mức sử dụng và đánh giá chi phí định kỳ.

Bên cạnh đó, các công cụ như AWS Cost Explorer, AWS Budgets và AWS Pricing Calculator giúp hỗ trợ việc phân tích chi phí, thiết lập ngân sách và xây dựng dự toán trước khi triển khai.

Đối với dự án **Cloud Library Management System**, những kiến thức này có thể được áp dụng để xem xét chi phí của các dịch vụ Serverless như AWS Lambda, Amazon API Gateway, Amazon DynamoDB và Amazon S3.

Bài học quan trọng nhất là **tối ưu chi phí không chỉ nhằm giảm số tiền sử dụng AWS, mà còn hướng đến việc xây dựng hệ thống đáp ứng yêu cầu kỹ thuật với mức tài nguyên và chi phí hợp lý**.

Việc kết hợp quản lý chi phí với thiết kế kiến trúc giúp dự án có định hướng triển khai thực tế và sử dụng tài nguyên đám mây hiệu quả hơn.

### 10. Hình ảnh minh họa và thực hành

![Minh họa kiến trúc và các công cụ tối ưu chi phí AWS cho Cloud Library](/images/3-Blogs/Blogs2/aws-cost-optimization.png)