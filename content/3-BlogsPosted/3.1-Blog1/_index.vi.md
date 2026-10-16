---
title: "Blog 1: Amazon DynamoDB"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AMAZON DYNAMODB

Amazon DynamoDB là dịch vụ cơ sở dữ liệu NoSQL Serverless được quản lý hoàn toàn bởi AWS. Dịch vụ cho phép các nhà phát triển lưu trữ và truy xuất dữ liệu với độ trễ thấp, hỗ trợ mở rộng theo nhu cầu mà không cần tự quản lý máy chủ cơ sở dữ liệu.

Trong các ứng dụng web hiện đại, DynamoDB thường được kết hợp với AWS Lambda và Amazon API Gateway để xây dựng backend theo kiến trúc Serverless.

Đối với dự án Cloud Library Management System, DynamoDB được đề xuất làm cơ sở dữ liệu chính để quản lý sách, thông tin độc giả và các giao dịch mượn trả.

### Các điểm chính cần nắm

- **Fully Managed:** AWS quản lý hạ tầng, việc sao chép dữ liệu và khả năng sẵn sàng của dịch vụ.
- **NoSQL Database:** Lưu dữ liệu theo mô hình key-value và document, không yêu cầu các item có cùng toàn bộ thuộc tính.
- **Table, Item, Attribute:** Ba thành phần cơ bản để tổ chức dữ liệu trong DynamoDB.
- **Partition Key:** Thành phần khóa chính dùng để xác định cách phân phối và truy xuất dữ liệu.
- **Sort Key:** Khóa tùy chọn, kết hợp với Partition Key để tổ chức nhiều item có chung Partition Key.
- **CRUD Operations:** Hỗ trợ thêm, đọc, cập nhật và xóa dữ liệu thông qua các API.
- **Global Secondary Index (GSI):** Hỗ trợ truy vấn dữ liệu theo những khóa khác với khóa chính của bảng.
- **Conditional Writes và Transactions:** Giúp kiểm soát các thao tác cập nhật và hỗ trợ tính nhất quán dữ liệu trong nghiệp vụ.

### Các thành phần cơ bản của DynamoDB

Một bảng DynamoDB gồm nhiều Item, mỗi Item chứa các Attribute.

Ví dụ với bảng Books:

| bookId | title | category | availableCopies |
| --- | --- | --- | --- |
| BOOK001 | AWS Fundamentals | Cloud Computing | 3 |
| BOOK002 | Learning Python | Programming | 5 |
| BOOK003 | Introduction to AI | Artificial Intelligence | 2 |

Trong ví dụ này, `bookId` được sử dụng làm Partition Key nhằm xác định duy nhất từng cuốn sách trong bảng Books.

Ngoài Partition Key, DynamoDB còn hỗ trợ Composite Primary Key gồm Partition Key và Sort Key, phù hợp với những dữ liệu cần tổ chức theo nhóm.

### Các thao tác CRUD trong DynamoDB

DynamoDB cung cấp những thao tác cơ bản:

- **PutItem:** Tạo hoặc ghi một Item vào bảng.
- **GetItem:** Lấy thông tin một Item bằng khóa chính.
- **UpdateItem:** Cập nhật các thuộc tính của Item.
- **DeleteItem:** Xóa một Item.
- **Query:** Truy vấn dữ liệu dựa trên điều kiện khóa.
- **Scan:** Đọc các Item trong bảng hoặc Index.

Việc lựa chọn khóa và thiết kế cách truy vấn phù hợp giúp ứng dụng hạn chế sử dụng Scan không cần thiết.

### DynamoDB trong kiến trúc AWS Serverless

Một kiến trúc phổ biến sử dụng DynamoDB bao gồm:

1. Người dùng thao tác trên giao diện web.
2. Amazon API Gateway tiếp nhận yêu cầu API.
3. AWS Lambda xử lý nghiệp vụ và kiểm tra quyền truy cập.
4. Lambda truy xuất hoặc cập nhật dữ liệu trong DynamoDB.
5. Kết quả được trả về cho giao diện người dùng.

![Sơ đồ kiến trúc DynamoDB trong Cloud Library](/images/blogs/blog-1/dynamodb-architecture.svg)

### Ứng dụng thực tế vào Cloud Library

Cloud Library Management System là dự án xây dựng ứng dụng quản lý thư viện trên AWS.

DynamoDB được đề xuất sử dụng để quản lý các nhóm dữ liệu như Books, Readers, Loans, BookCopies và Reservations.

Ví dụ khi độc giả mượn một cuốn sách:

- Hệ thống kiểm tra số sách còn sẵn.
- Thủ thư xác nhận việc giao sách.
- AWS Lambda cập nhật phiếu mượn trong DynamoDB.
- Số lượng sách còn sẵn được giảm tương ứng.

Để hạn chế sai lệch dữ liệu khi có nhiều yêu cầu đồng thời, hệ thống có thể sử dụng DynamoDB Transactions kết hợp Condition Expressions.

Ví dụ, khi có 3 bản sách còn sẵn và một bản được cho mượn thành công, số lượng sẽ giảm còn 2.

Nhờ đó, DynamoDB không chỉ lưu thông tin danh mục mà còn hỗ trợ quản lý các giao dịch nghiệp vụ quan trọng.

### Kết luận

Amazon DynamoDB là một lựa chọn đáng cân nhắc khi phát triển các ứng dụng NoSQL trên AWS, đặc biệt là hệ thống sử dụng kiến trúc Serverless.

Thông qua việc tìm hiểu DynamoDB, em nắm được những khái niệm về Table, Item, Attribute, Primary Key, các thao tác CRUD và cách phối hợp DynamoDB với AWS Lambda.

Những kiến thức này là nền tảng để thiết kế cơ sở dữ liệu và xử lý nghiệp vụ trong dự án Cloud Library Management System.

### Hình ảnh

*Có thể bổ sung thêm hình ảnh thực hành DynamoDB trên AWS Management Console tại đây.*

