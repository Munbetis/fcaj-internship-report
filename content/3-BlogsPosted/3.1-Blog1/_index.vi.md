---
title: "Blog 1: Amazon DynamoDB - Xây dựng cơ sở dữ liệu NoSQL trên AWS"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# AMAZON DYNAMODB

## Xây dựng cơ sở dữ liệu NoSQL với Amazon DynamoDB và ứng dụng trong Cloud Library

Khi phát triển một ứng dụng web, cơ sở dữ liệu là thành phần quan trọng giúp lưu trữ, tổ chức và truy xuất thông tin. Đối với một hệ thống quản lý thư viện, dữ liệu không chỉ bao gồm tên sách và tác giả mà còn liên quan đến hồ sơ độc giả, số lượng bản sách, lịch sử mượn trả và các yêu cầu đặt trước.

Một trong những dịch vụ cơ sở dữ liệu nổi bật của Amazon Web Services (AWS) là **Amazon DynamoDB**. Đây là dịch vụ cơ sở dữ liệu NoSQL được quản lý hoàn toàn, có khả năng hỗ trợ các ứng dụng cần tốc độ truy xuất nhanh và mở rộng linh hoạt.

Điểm đáng chú ý là nhà phát triển không cần tự quản lý máy chủ cơ sở dữ liệu, cài đặt hệ điều hành hay cấu hình các cụm database truyền thống. Thay vào đó, họ có thể tập trung vào thiết kế dữ liệu và phát triển ứng dụng.

Trong bài viết này, chúng ta sẽ tìm hiểu cách DynamoDB hoạt động, các thành phần cơ bản, phương pháp thiết kế khóa, cách thực hiện CRUD, đồng thời liên hệ với bài toán quản lý sách trong dự án **Cloud Library Management System**.

### Các điểm chính cần nắm

- **Fully Managed:** AWS quản lý hạ tầng và việc vận hành dịch vụ cơ sở dữ liệu.
- **NoSQL:** Hỗ trợ mô hình dữ liệu key-value và document.
- **Table, Item, Attribute:** Các thành phần cơ bản để tổ chức dữ liệu.
- **Partition Key và Sort Key:** Xác định cách nhận diện và truy xuất các bản ghi.
- **Global Secondary Index (GSI):** Hỗ trợ những nhu cầu truy vấn bổ sung.
- **CRUD Operations:** Thêm, đọc, cập nhật và xóa dữ liệu.
- **Capacity Modes:** Cho phép lựa chọn On-demand hoặc Provisioned.
- **Conditional Writes:** Chỉ cập nhật dữ liệu khi điều kiện được đáp ứng.
- **Transactions:** Hỗ trợ cập nhật nhiều bản ghi theo nguyên tắc tất cả thành công hoặc cùng thất bại.
- **AWS Integration:** Có thể tích hợp với AWS Lambda, API Gateway, IAM và nhiều dịch vụ khác.

### 1. Tổng quan về Amazon DynamoDB

#### 1.1. Amazon DynamoDB là gì?

Amazon DynamoDB là dịch vụ cơ sở dữ liệu NoSQL do AWS cung cấp, được thiết kế để hỗ trợ các ứng dụng cần khả năng truy xuất dữ liệu với độ trễ thấp và mở rộng theo nhu cầu.

Khác với các cơ sở dữ liệu quan hệ như MySQL hoặc PostgreSQL, DynamoDB không sử dụng mô hình bảng quan hệ cùng những phép JOIN truyền thống để giải quyết mọi nhu cầu truy vấn.

Thay vào đó, DynamoDB khuyến khích nhà phát triển xác định trước các **Access Patterns**, tức những cách ứng dụng sẽ truy vấn dữ liệu, rồi thiết kế khóa và chỉ mục phù hợp.

Ví dụ, trong hệ thống thư viện, những câu hỏi cần được hỗ trợ có thể là:

- Tìm thông tin sách theo mã sách.
- Hiển thị danh sách các bản của một đầu sách.
- Xem lịch sử mượn của một độc giả.
- Kiểm tra trạng thái một phiếu mượn.
- Tìm những yêu cầu đặt trước đang chờ xử lý.

Mỗi nhu cầu truy vấn có thể ảnh hưởng đến cách thiết kế bảng và chỉ mục DynamoDB.

#### 1.2. Những đặc điểm nổi bật

**Không cần quản lý máy chủ**

DynamoDB là dịch vụ Fully Managed. AWS chịu trách nhiệm vận hành hạ tầng cơ sở dữ liệu, giúp nhà phát triển giảm công việc quản trị hệ thống.

**Khả năng mở rộng**

DynamoDB được thiết kế để hỗ trợ lưu lượng đọc và ghi lớn, đáp ứng nhu cầu của những ứng dụng có số lượng người dùng thay đổi.

**Tính sẵn sàng cao**

Trong một AWS Region, DynamoDB lưu trữ dữ liệu trên nhiều Availability Zones nhằm hỗ trợ khả năng sẵn sàng và độ bền dữ liệu.

**Mô hình dữ liệu linh hoạt**

Các Item trong một Table không bắt buộc phải có toàn bộ Attribute giống nhau, ngoại trừ các yêu cầu liên quan đến khóa chính.

**Tích hợp với AWS**

DynamoDB có thể kết hợp với AWS Lambda để xử lý nghiệp vụ, IAM để quản lý quyền truy cập và CloudWatch để theo dõi hoạt động.

#### 1.3. DynamoDB khác gì cơ sở dữ liệu SQL?

| Tiêu chí | DynamoDB | Cơ sở dữ liệu quan hệ |
| --- | --- | --- |
| Mô hình dữ liệu | NoSQL, key-value và document | Các bảng có quan hệ |
| Truy vấn | Chủ yếu dựa trên khóa và index | SQL |
| JOIN | Không hỗ trợ JOIN như SQL | Hỗ trợ JOIN |
| Thiết kế | Ưu tiên Access Patterns | Thường dựa trên quan hệ dữ liệu |
| Vận hành | Dịch vụ do AWS quản lý | Tùy hệ thống và dịch vụ sử dụng |
| Phù hợp | Truy vấn theo khóa, ứng dụng có nhu cầu mở rộng | Nghiệp vụ quan hệ và truy vấn phức tạp |

Không có loại cơ sở dữ liệu nào phù hợp với mọi hệ thống. Việc lựa chọn phụ thuộc vào cấu trúc dữ liệu, nhu cầu truy vấn và đặc điểm ứng dụng.

### 2. Cấu trúc dữ liệu trong DynamoDB

#### 2.1. Table, Item và Attribute

DynamoDB sử dụng ba thành phần cơ bản:

| Thành phần | Ý nghĩa | Ví dụ |
| --- | --- | --- |
| **Table** | Tập hợp các Item. | Books |
| **Item** | Một bản ghi dữ liệu. | Sách BOOK001 |
| **Attribute** | Thuộc tính của một Item. | title, author, availableCopies |

Ví dụ, một Item trong bảng `Books`:

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

Trong đó:

- `bookId`: Mã định danh của đầu sách.
- `title`: Tên sách.
- `author`: Tác giả.
- `category`: Thể loại.
- `totalCopies`: Tổng số bản sách.
- `availableCopies`: Số bản còn có thể mượn.
- `status`: Trạng thái lưu hành.

#### 2.2. Partition Key

Partition Key là thành phần bắt buộc của Primary Key.

DynamoDB sử dụng giá trị Partition Key để xác định cách phân phối dữ liệu. Khi bảng chỉ sử dụng Partition Key, giá trị khóa phải xác định duy nhất một Item.

Ví dụ, bảng `Books` sử dụng `bookId` làm Partition Key:

| bookId | title | availableCopies |
| --- | --- | --- |
| BOOK001 | AWS Fundamentals | 2 |
| BOOK002 | Learning Python | 5 |
| BOOK003 | Introduction to AI | 3 |

Ứng dụng có thể sử dụng `GetItem` với `bookId = BOOK001` để đọc thông tin sách tương ứng.

#### 2.3. Sort Key

Sort Key là thành phần tùy chọn của Primary Key.

Khi một bảng sử dụng cả Partition Key và Sort Key, hai giá trị kết hợp với nhau sẽ xác định duy nhất một Item.

Ví dụ, bảng `BookCopies` có thể được thiết kế như sau:

| bookId (PK) | copyId (SK) | status |
| --- | --- | --- |
| BOOK001 | COPY001 | AVAILABLE |
| BOOK001 | COPY002 | BORROWED |
| BOOK001 | COPY003 | AVAILABLE |

Với cấu trúc này, ứng dụng có thể sử dụng `Query` để tìm những bản sách thuộc `BOOK001`.

#### 2.4. Global Secondary Index (GSI)

Trong thực tế, không phải mọi truy vấn đều sử dụng khóa chính của bảng.

Ví dụ, bảng `Loans` sử dụng `loanId` làm Partition Key. Thiết kế này thuận tiện khi cần tìm một phiếu mượn theo mã phiếu, nhưng chưa trực tiếp đáp ứng nhu cầu xem toàn bộ lịch sử mượn của một độc giả.

Một giải pháp là tạo Global Secondary Index (GSI), chẳng hạn:

- GSI Partition Key: `readerId`.
- GSI Sort Key: `borrowDate`.

Ứng dụng có thể truy vấn các phiếu mượn của cùng một độc giả thông qua chỉ mục này.

Tuy nhiên, dữ liệu đọc từ GSI sử dụng cơ chế **Eventually Consistent Read**, nên có thể chưa phản ánh ngay một cập nhật vừa được thực hiện.


### 3. Các thao tác CRUD trong DynamoDB

CRUD là bốn nhóm thao tác cơ bản khi làm việc với cơ sở dữ liệu.

| Thao tác | Chức năng | DynamoDB API |
| --- | --- | --- |
| **Create** | Thêm bản ghi mới | PutItem |
| **Read** | Đọc dữ liệu | GetItem, Query, Scan |
| **Update** | Cập nhật bản ghi | UpdateItem |
| **Delete** | Xóa bản ghi | DeleteItem |

#### 3.1. Create - Thêm dữ liệu

Khi thủ thư thêm một đầu sách mới, ứng dụng cần tạo bản ghi tương ứng trong DynamoDB.

Ví dụ:

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

DynamoDB hỗ trợ `PutItem` để ghi Item vào bảng.

Cần lưu ý rằng PutItem có thể ghi đè một Item đã tồn tại với cùng khóa chính. Vì vậy, ứng dụng có thể sử dụng Condition Expression để chỉ cho phép tạo khi Item chưa tồn tại.

#### 3.2. Read - Đọc dữ liệu

DynamoDB hỗ trợ nhiều phương pháp đọc dữ liệu:

**GetItem**

Dùng để đọc một Item dựa trên đầy đủ Primary Key.

Ví dụ: tìm sách có mã `BOOK001`.

**Query**

Dùng để truy vấn các Item dựa trên điều kiện khóa chính hoặc khóa của một chỉ mục.

Ví dụ: xem các bản sách có cùng `bookId`.

**Scan**

Dùng để đọc dữ liệu trong Table hoặc Index. Với bảng lớn, Scan có thể tốn tài nguyên vì phải đọc nhiều Item.

Khi thiết kế ứng dụng thực tế, nên ưu tiên các Access Patterns có thể đáp ứng bằng GetItem và Query.

#### 3.3. Update - Cập nhật dữ liệu

Giả sử một đầu sách có 3 bản còn sẵn.

Sau khi thủ thư xác nhận cho mượn một bản, hệ thống cần giảm số lượng từ 3 xuống 2.

DynamoDB hỗ trợ `UpdateItem` để thay đổi những thuộc tính cần thiết mà không phải ghi lại toàn bộ Item.

Đối với các thao tác cập nhật số lượng, nên kết hợp điều kiện kiểm tra để tránh giảm số bản sách xuống dưới 0.

#### 3.4. Delete - Xóa dữ liệu

`DeleteItem` cho phép xóa Item theo khóa chính.

Tuy nhiên, trong hệ thống thư viện, không phải lúc nào ngưng lưu hành sách cũng nên xóa bản ghi.

Ví dụ, một đầu sách đã có lịch sử mượn trả có thể được chuyển sang trạng thái `INACTIVE` để tiếp tục phục vụ công tác quản lý và tra cứu lịch sử.

### 4. Hướng dẫn thực hành DynamoDB

Phần này minh họa quy trình tạo bảng, thêm dữ liệu và thực hiện các thao tác cơ bản bằng AWS Management Console.

#### Bước 1: Truy cập Amazon DynamoDB

1. Đăng nhập AWS Management Console.
2. Tìm kiếm dịch vụ `DynamoDB`.
3. Chọn `Tables`.
4. Nhấn `Create table`.

#### Bước 2: Tạo bảng Books

Thiết lập những thông tin minh họa:

| Cấu hình | Giá trị |
| --- | --- |
| Table name | Books |
| Partition key | bookId |
| Key type | String |
| Sort key | Không sử dụng |
| Capacity mode | On-demand |

Với On-demand mode, DynamoDB quản lý thông lượng theo nhu cầu sử dụng và tính phí theo hoạt động đọc, ghi cùng các thành phần tính phí liên quan.

Đây là lựa chọn phù hợp để thử nghiệm khi lưu lượng chưa ổn định, nhưng không đồng nghĩa với việc sử dụng hoàn toàn miễn phí.

Sau khi kiểm tra cấu hình, chọn `Create table` và chờ bảng chuyển sang trạng thái `Active`.

#### Bước 3: Thêm dữ liệu mẫu

Trong trang quản lý bảng `Books`:

1. Chọn `Explore table items`.
2. Chọn `Create item`.
3. Nhập `bookId = BOOK001`.
4. Thêm các thuộc tính như `title`, `category`, `totalCopies` và `availableCopies`.
5. Lưu Item.

Ví dụ:

```json
{
  "bookId": "BOOK001",
  "title": "AWS Fundamentals",
  "category": "Cloud Computing",
  "totalCopies": 3,
  "availableCopies": 3
}
```

#### Bước 4: Đọc và cập nhật dữ liệu

Sau khi tạo Item, có thể sử dụng giao diện DynamoDB để tìm bản ghi theo khóa.

Tiếp theo, thử cập nhật `availableCopies` từ 3 xuống 2 và kiểm tra lại kết quả.

Trong ứng dụng thực tế, những thao tác này thường được thực hiện thông qua AWS SDK thay vì chỉnh sửa thủ công trên Console.

#### Bước 5: Ví dụ sử dụng AWS SDK với Node.js

AWS SDK for JavaScript v3 hỗ trợ thao tác DynamoDB trong ứng dụng Node.js.

Cài đặt các thư viện cần thiết:

```bash
npm install @aws-sdk/client-dynamodb @aws-sdk/lib-dynamodb
```

Ví dụ sử dụng `UpdateCommand` để giảm số bản sách còn sẵn:

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

**Giải thích:**

- `TableName`: Bảng cần cập nhật.
- `Key`: Xác định Item thông qua Primary Key.
- `UpdateExpression`: Giảm số bản còn sẵn đi một đơn vị.
- `ConditionExpression`: Chỉ cập nhật khi Item tồn tại và còn ít nhất một bản.
- `ExpressionAttributeValues`: Cung cấp giá trị cho biểu thức.
- `ReturnValues`: Trả về dữ liệu sau khi cập nhật thành công.

Đoạn code giả định bảng Books đã tồn tại, AWS Region phù hợp và môi trường thực thi đã có thông tin xác thực cùng quyền truy cập cần thiết.

**Lưu ý:** Ví dụ này chỉ minh họa cập nhật một Item. Nó chưa phải toàn bộ quy trình mượn sách vì hệ thống còn cần tạo phiếu mượn và cập nhật trạng thái từng bản sách.

Khi thực hành xong, cần kiểm tra và xóa những tài nguyên thử nghiệm không còn sử dụng để tránh phát sinh chi phí không cần thiết.

### 5. Tích hợp DynamoDB với AWS Serverless

Một trong những cách ứng dụng DynamoDB là kết hợp với Amazon API Gateway và AWS Lambda để xây dựng backend Serverless.

Trong mô hình này, frontend không trực tiếp sử dụng thông tin xác thực AWS để đọc hoặc chỉnh sửa database.

Thay vào đó, các yêu cầu được gửi đến backend để kiểm tra quyền và xử lý nghiệp vụ.

#### Sơ đồ kiến trúc đề xuất

![Sơ đồ kiến trúc AWS Serverless và DynamoDB trong Cloud Library](/images/3-Blogs/Blogs1/dynamodb-data-model.png)

#### Luồng hoạt động

1. Người dùng đăng nhập thông qua Amazon Cognito.
2. Giao diện React gửi yêu cầu đến Amazon API Gateway.
3. API Gateway xác thực token theo cấu hình.
4. AWS Lambda tiếp nhận và xử lý yêu cầu.
5. Lambda kiểm tra quyền nghiệp vụ của người dùng.
6. Lambda đọc hoặc cập nhật dữ liệu trong Amazon DynamoDB.
7. Kết quả xử lý được trả về cho frontend.

#### Vai trò của từng dịch vụ

| Dịch vụ | Vai trò |
| --- | --- |
| **React** | Xây dựng giao diện web. |
| **Amazon Cognito** | Xác thực và quản lý danh tính người dùng. |
| **Amazon API Gateway** | Tiếp nhận yêu cầu API và hỗ trợ xác thực. |
| **AWS Lambda** | Xử lý nghiệp vụ và kiểm tra quyền truy cập. |
| **Amazon DynamoDB** | Lưu và truy xuất dữ liệu nghiệp vụ. |
| **AWS IAM** | Cấp quyền truy cập DynamoDB cho Lambda. |

Để truy cập DynamoDB, Lambda có thể sử dụng IAM Execution Role với những quyền cần thiết.

Cách tiếp cận này giúp tránh phải lưu AWS Access Keys trực tiếp trong mã nguồn ứng dụng.

### 6. Ứng dụng DynamoDB trong Cloud Library Management System

#### 6.1. Giới thiệu bài toán

Cloud Library Management System là dự án xây dựng ứng dụng quản lý thư viện trên AWS, kết hợp các chức năng quản lý sách, độc giả, giao dịch mượn trả và trợ lý AI.

Trong kiến trúc đề xuất, DynamoDB đóng vai trò cơ sở dữ liệu nghiệp vụ chính.

Hệ thống cần quản lý các nhóm dữ liệu sau:

| Nhóm dữ liệu | Chức năng |
| --- | --- |
| **Books** | Lưu thông tin đầu sách và số lượng. |
| **Readers** | Quản lý hồ sơ độc giả. |
| **Loans** | Lưu phiếu mượn trả, hạn trả và tiền phạt. |
| **BookCopies** | Theo dõi từng bản sách vật lý. |
| **Reservations** | Quản lý đặt trước và hàng chờ. |
| **Favorites** | Lưu danh sách sách yêu thích. |
| **Notifications** | Quản lý thông báo. |

Đây là những nhóm dữ liệu nghiệp vụ từ đề cương dự án, không nhất thiết tương ứng với bảy bảng DynamoDB vật lý.

Nhóm có thể lựa chọn mô hình nhiều bảng hoặc Single-table Design tùy theo Access Patterns thực tế.

#### 6.2. Bài toán quản lý số lượng sách

Giả sử thư viện có một đầu sách với:

- Mã sách: `BOOK001`.
- Tổng số bản: 3.
- Số bản còn sẵn: 3.
- Một độc giả gửi yêu cầu mượn.

Khi thủ thư xác nhận giao sách, hệ thống cần:

1. Kiểm tra giới hạn mượn của độc giả.
2. Kiểm tra sách còn bản có thể mượn.
3. Xác định bản sách được giao.
4. Tạo hoặc cập nhật phiếu mượn.
5. Cập nhật trạng thái bản sách.
6. Giảm số lượng sách còn sẵn từ 3 xuống 2.

Nếu các thao tác cập nhật không được phối hợp đúng cách, hệ thống có thể xuất hiện tình trạng sai lệch dữ liệu.

Ví dụ, hai yêu cầu đồng thời đều đọc được số lượng còn sẵn là 1. Nếu ứng dụng không kiểm soát điều kiện ghi, cả hai yêu cầu có thể cùng được chấp nhận dù chỉ còn một bản sách.

#### 6.3. Sử dụng Conditional Writes và Transactions

DynamoDB cung cấp Condition Expressions để kiểm tra điều kiện trước khi cập nhật Item.

Ví dụ:

```text
availableCopies >= 1
```

Điều kiện này có thể được dùng để ngăn thao tác giảm số lượng khi không còn sách.

Tuy nhiên, một giao dịch mượn sách có thể liên quan đến nhiều Item, chẳng hạn:

- Item trong Books.
- Item trong BookCopies.
- Item trong Loans.

Để phối hợp các cập nhật này, DynamoDB hỗ trợ `TransactWriteItems`.

Các thao tác trong một giao dịch được xử lý theo nguyên tắc:

**Tất cả cùng thành công hoặc tất cả cùng thất bại.**

Đối với Cloud Library, một giao dịch đề xuất có thể gồm:

1. Kiểm tra và giảm `availableCopies` với điều kiện còn sách.
2. Cập nhật trạng thái bản sách từ `AVAILABLE` sang `BORROWED`.
3. Tạo phiếu mượn trong `Loans`, với điều kiện mã phiếu chưa tồn tại.

Nếu một điều kiện không được đáp ứng, giao dịch không được hoàn tất.

Ngoài ra, backend cần thiết kế cơ chế chống xử lý trùng và kiểm tra giới hạn mượn để bảo đảm đúng quy tắc nghiệp vụ.

#### 6.4. Quy trình trả sách

Khi độc giả trả sách, thủ thư thực hiện xác nhận trên hệ thống.

Backend cần:

1. Kiểm tra phiếu mượn còn ở trạng thái `BORROWED`.
2. Xác định ngày trả thực tế.
3. Tính tiền phạt nếu quá hạn.
4. Cập nhật trạng thái phiếu thành `RETURNED`.
5. Cập nhật bản sách thành `AVAILABLE`.
6. Tăng số bản còn sẵn.

Ví dụ, khi số lượng còn sẵn là 2 và một bản được trả thành công, số lượng tăng thành 3.

Cần sử dụng điều kiện phù hợp để cùng một phiếu trả sách không bị xử lý nhiều lần.

#### 6.5. Vì sao thiết kế database quan trọng?

Trong Cloud Library, chỉ lưu dữ liệu thành công là chưa đủ.

Hệ thống còn phải bảo đảm:

- Không cho mượn vượt số lượng sách thực tế.
- Không cập nhật phiếu mượn sai trạng thái.
- Không tăng số lượng sách nhiều lần khi một thao tác trả bị lặp.
- Không cho phép độc giả xem giao dịch của người khác.
- Hỗ trợ tìm kiếm và truy vấn theo những nhu cầu thực tế.

Do đó, thiết kế DynamoDB cần đi cùng với thiết kế nghiệp vụ và phân quyền ứng dụng.

### 7. Bảo mật, hiệu năng và tối ưu chi phí

#### 7.1. Bảo mật dữ liệu

Một số nguyên tắc quan trọng khi sử dụng DynamoDB:

- Sử dụng AWS IAM để kiểm soát quyền truy cập.
- Áp dụng nguyên tắc Least Privilege.
- Không lưu AWS Access Keys trực tiếp trong mã nguồn.
- Chỉ cấp quyền Lambda đối với những bảng và hành động cần thiết.
- Kiểm tra quyền sở hữu dữ liệu tại backend.
- Sử dụng Amazon Cognito để hỗ trợ xác thực người dùng ứng dụng.

#### 7.2. Thiết kế truy vấn hiệu quả

Cần xác định rõ những Access Patterns như:

- Tìm sách theo `bookId`.
- Xem phiếu mượn theo `loanId`.
- Xem lịch sử mượn theo `readerId`.
- Tìm bản sách thuộc một đầu sách.

Sau đó lựa chọn khóa chính và GSI phù hợp.

Việc thiết kế đúng các truy vấn thường dùng giúp giảm những thao tác đọc không cần thiết.

#### 7.3. On-demand và Provisioned Capacity

DynamoDB hỗ trợ hai chế độ thông lượng chính:

| Chế độ | Đặc điểm |
| --- | --- |
| **On-demand** | Tự điều chỉnh thông lượng theo nhu cầu, tính phí dựa trên hoạt động sử dụng. |
| **Provisioned** | Cấu hình thông lượng đọc/ghi, phù hợp khi có thể dự đoán khối lượng sử dụng. |

Đối với ứng dụng thử nghiệm có lưu lượng chưa ổn định, On-demand thường là lựa chọn thuận tiện.

Với những ứng dụng có lưu lượng ổn định và dự đoán được, Provisioned có thể phù hợp để tối ưu chi phí.

Chi phí thực tế còn phụ thuộc vào dung lượng lưu trữ, chỉ mục, giao dịch và các tính năng bổ sung được sử dụng.

#### 7.4. Những lưu ý khi triển khai

- Tránh lạm dụng Scan đối với bảng lớn.
- Xem xét mức tiêu thụ đọc/ghi của các GSI.
- Sử dụng Conditional Writes cho những cập nhật quan trọng.
- Sử dụng Transactions khi cần phối hợp cập nhật nhiều Item.
- Theo dõi lỗi và mức sử dụng bằng Amazon CloudWatch.
- Thiết lập cảnh báo ngân sách AWS.
- Kiểm thử với các yêu cầu đồng thời.
- Kiểm tra hành vi của ứng dụng khi truy vấn chưa phản ánh ngay cập nhật mới.

### 8. Kết luận

Amazon DynamoDB là một dịch vụ cơ sở dữ liệu NoSQL quan trọng trong hệ sinh thái AWS, phù hợp với nhiều ứng dụng được xây dựng theo kiến trúc Serverless.

Thông qua việc tìm hiểu DynamoDB, em có thêm kiến thức về các thành phần Table, Item, Attribute, Partition Key, Sort Key, Global Secondary Index và những thao tác CRUD cơ bản.

Bên cạnh việc lưu trữ dữ liệu, DynamoDB còn cung cấp Conditional Writes và Transactions để hỗ trợ xử lý những nghiệp vụ cần bảo đảm tính chính xác.

Đối với dự án **Cloud Library Management System**, các kiến thức này có thể được áp dụng để thiết kế dữ liệu sách, độc giả và giao dịch mượn trả, đồng thời giảm nguy cơ sai lệch số lượng sách khi nhiều yêu cầu được xử lý.

Bài học quan trọng nhất là khi xây dựng cơ sở dữ liệu NoSQL, nhà phát triển cần quan tâm đến cả cấu trúc dữ liệu, nhu cầu truy vấn, quy tắc nghiệp vụ, bảo mật và chi phí vận hành.