---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Cloud Library Management System

## Giải pháp quản lý thư viện trên AWS Serverless tích hợp trợ lý AI

### 1. Tóm tắt điều hành

**Cloud Library Management System** là dự án xây dựng hệ thống quản lý thư viện trực tuyến dành cho trường học hoặc tổ chức, sử dụng kiến trúc Serverless trên nền tảng Amazon Web Services (AWS).

Dự án hướng đến việc xây dựng một nền tảng tập trung để quản lý danh mục sách, từng bản sách, hồ sơ độc giả và các giao dịch mượn trả. Hệ thống hỗ trợ tìm kiếm sách, kiểm tra số lượng sách còn sẵn, gửi yêu cầu mượn, đặt trước, gia hạn và theo dõi hạn trả cũng như tiền phạt.

Bên cạnh các chức năng quản lý thư viện, hệ thống tích hợp trợ lý AI sử dụng **Amazon Bedrock** và **Amazon Bedrock Knowledge Bases**. Trợ lý AI hỗ trợ độc giả hỏi đáp nội quy thư viện và tìm kiếm sách theo nhu cầu dựa trên các tài liệu đã được phê duyệt.

Giải pháp sử dụng **React** để xây dựng giao diện, **Node.js trên AWS Lambda** để xử lý nghiệp vụ, **Amazon API Gateway** để cung cấp API, **Amazon Cognito** để xác thực và phân quyền, cùng **Amazon DynamoDB** làm cơ sở dữ liệu chính.

Việc ứng dụng kiến trúc AWS Serverless giúp giảm công việc quản lý máy chủ, hỗ trợ tự động hóa các quy trình nghiệp vụ và tạo nền tảng để mở rộng hệ thống trong tương lai.

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại

Hoạt động quản lý thư viện yêu cầu theo dõi nhiều loại thông tin như danh mục sách, số lượng từng bản sách, hồ sơ độc giả, tình trạng mượn trả, hạn trả và tiền phạt.

Khi các thông tin này được quản lý phân tán hoặc cập nhật thủ công, việc tra cứu và xử lý nghiệp vụ có thể trở nên phức tạp. Thủ thư cần kiểm tra tình trạng sách, theo dõi yêu cầu mượn, xác nhận giao nhận và cập nhật dữ liệu chính xác.

Đối với độc giả, việc tìm kiếm sách phù hợp, tra cứu nội quy, theo dõi hạn trả hoặc gửi yêu cầu gia hạn cũng cần được thực hiện thuận tiện hơn.

Bên cạnh đó, thư viện cần bảo đảm tính chính xác của dữ liệu, tránh cho mượn vượt số lượng sách hiện có và kiểm soát quyền truy cập của từng nhóm người dùng.

#### Giải pháp

Cloud Library Management System đề xuất xây dựng một ứng dụng web quản lý thư viện tập trung, kết hợp các dịch vụ AWS Serverless và trợ lý AI.

Các chức năng chính bao gồm:

- **Quản lý sách:** Thêm, cập nhật, ngưng lưu hành sách và quản lý từng bản sách.
- **Quản lý độc giả:** Lưu trữ hồ sơ người dùng và quản lý thông tin liên quan đến hoạt động thư viện.
- **Tìm kiếm sách:** Tra cứu danh mục, xem chi tiết và kiểm tra số lượng sách còn sẵn.
- **Quản lý mượn trả:** Gửi yêu cầu mượn, xác nhận giao nhận, theo dõi lịch sử và hạn trả.
- **Đặt trước và hàng chờ:** Cho phép độc giả đặt sách khi hết bản còn sẵn.
- **Gia hạn trực tuyến:** Gửi và xử lý yêu cầu gia hạn theo quy định.
- **Quản lý tiền phạt:** Tính tiền phạt khi độc giả trả sách quá hạn.
- **Thông báo:** Gửi email nhắc hạn trả và thông báo về sách đặt trước.
- **Trợ lý AI:** Hỏi đáp nội quy thư viện và tìm sách theo nhu cầu.

Hệ thống được thiết kế với bốn nhóm người dùng:

| Vai trò | Chức năng chính | Phạm vi quyền |
| --- | --- | --- |
| **Khách truy cập** | Xem danh mục công khai, chi tiết sách và đăng ký tài khoản. | Cần đăng nhập trước khi gửi yêu cầu mượn hoặc sử dụng AI. |
| **Độc giả (Reader)** | Cập nhật hồ sơ, tìm sách, sử dụng AI, lưu sách yêu thích, mượn, đặt trước, gia hạn và xem lịch sử. | Chỉ truy cập hồ sơ và các giao dịch của mình. |
| **Thủ thư (Librarian)** | Quản lý sách, độc giả, duyệt mượn và gia hạn, xác nhận trả, xử lý hàng chờ và tiền phạt. | Xử lý nghiệp vụ thư viện, không tự quản trị hệ thống. |
| **Quản trị viên (Admin)** | Quản lý tài khoản, vai trò, quy định thư viện, tài liệu AI và báo cáo tổng hợp. | Quản trị hệ thống; cần thêm vai trò thủ thư để trực tiếp xử lý giao nhận. |

Người dùng đăng ký mới được gán vai trò độc giả. Quyền thủ thư và Admin được quản lý thông qua các nhóm trong Amazon Cognito. Một tài khoản có thể có nhiều vai trò.

#### Lợi ích và hoàn vốn đầu tư (ROI)

**Quản lý tập trung**

- Quản lý dữ liệu sách, độc giả và giao dịch trên một nền tảng thống nhất.
- Giảm khó khăn khi tra cứu và đối chiếu thông tin.
- Hỗ trợ thủ thư theo dõi tình trạng sách và yêu cầu mượn trả.

**Cải thiện trải nghiệm người dùng**

- Độc giả có thể tìm sách và gửi yêu cầu trực tuyến.
- Theo dõi hạn trả, tiền phạt và lịch sử mượn.
- Nhận thông báo về hạn trả hoặc sách đặt trước.

**Ứng dụng trí tuệ nhân tạo**

- Hỗ trợ trả lời các câu hỏi về nội quy.
- Tìm kiếm sách phù hợp với nhu cầu học tập.
- Cung cấp nguồn tham khảo khi trả lời từ tài liệu thư viện.

**Tối ưu vận hành**

- Sử dụng kiến trúc Serverless để giảm công việc quản lý máy chủ.
- Hỗ trợ tự động hóa tác vụ kiểm tra hạn trả và gửi thông báo.
- Tạo nền tảng mở rộng chức năng trong tương lai.

**Hoàn vốn đầu tư (ROI)**

Dự án hiện chưa có số liệu định lượng về chi phí triển khai, thời gian tiết kiệm hoặc doanh thu để tính ROI.

Nhóm sẽ đánh giá chi phí vận hành và lợi ích của hệ thống sau khi xác định cấu hình AWS, khối lượng sử dụng và kết quả thử nghiệm.

### 3. Kiến trúc giải pháp

Cloud Library Management System sử dụng **kiến trúc AWS Serverless**, trong đó frontend, backend, cơ sở dữ liệu và trợ lý AI được kết nối thông qua các dịch vụ AWS.

Ứng dụng frontend được xây dựng bằng React. Sau khi đăng nhập qua Amazon Cognito, người dùng gửi yêu cầu từ giao diện đến Amazon API Gateway.

API Gateway kiểm tra token truy cập và chuyển yêu cầu đến AWS Lambda. Lambda xử lý nghiệp vụ, kiểm tra quyền của người dùng và thực hiện các thao tác dữ liệu trong Amazon DynamoDB.

Đối với các yêu cầu liên quan đến trợ lý AI, Lambda truy vấn Amazon Bedrock Knowledge Bases và gọi mô hình AI trên Amazon Bedrock để tạo câu trả lời.

Knowledge Bases sử dụng những tài liệu đã được phê duyệt lưu trữ trên Amazon S3, đồng thời tạo chỉ mục để hỗ trợ truy xuất thông tin từ kho vector.

Amazon S3 Vectors là phương án được đề xuất để lưu trữ chỉ mục vector khi dịch vụ được hỗ trợ tại AWS Region triển khai.

Dữ liệu thay đổi thường xuyên, chẳng hạn số bản sách còn sẵn, hạn trả và tiền phạt, phải được truy xuất từ Amazon DynamoDB thay vì chỉ dựa trên câu trả lời của mô hình AI.

#### Sơ đồ kiến trúc hệ thống

*Bổ sung sơ đồ kiến trúc AWS của Cloud Library Management System sau khi nhóm hoàn thiện bản thiết kế.*

#### Dịch vụ AWS sử dụng

| Dịch vụ AWS | Vai trò trong hệ thống |
| --- | --- |
| **Amazon Cognito** | Xác thực người dùng, quản lý tài khoản và nhóm quyền Reader, Librarian, Admin. |
| **Amazon API Gateway** | Cung cấp API và kiểm tra token truy cập. |
| **AWS Lambda** | Xử lý nghiệp vụ, kiểm tra quyền và điều phối yêu cầu AI. |
| **Amazon DynamoDB** | Cơ sở dữ liệu chính, lưu thông tin sách, độc giả, bản sách và giao dịch mượn trả. |
| **Amazon S3** | Lưu trữ ảnh bìa sách và tài liệu nguồn của trợ lý AI. |
| **Amazon CloudFront** | Phân phối ứng dụng frontend React. |
| **Amazon Bedrock** | Cung cấp mô hình AI để tạo câu trả lời cho người dùng. |
| **Amazon Bedrock Knowledge Bases** | Truy xuất nội quy, FAQ và mô tả sách từ nguồn tài liệu đã duyệt. |
| **Amazon S3 Vectors** | Lưu chỉ mục vector cho Knowledge Bases theo phương án đề xuất. |
| **Amazon EventBridge Scheduler** | Kích hoạt các tác vụ kiểm tra hạn trả và hàng chờ theo lịch. |
| **Amazon SES** | Gửi email nhắc hạn và thông báo sách đặt trước đã sẵn sàng. |
| **Amazon CloudWatch** | Theo dõi lỗi và hoạt động của hệ thống. |
| **AWS IAM** | Quản lý quyền truy cập giữa các dịch vụ AWS. |

#### Thiết kế thành phần

**Frontend - React, Node.js**

- Cung cấp giao diện web cho các nhóm người dùng.
- Hiển thị danh mục và thông tin sách.
- Hỗ trợ tìm kiếm, gửi yêu cầu mượn, đặt trước và gia hạn.
- Cung cấp giao diện quản lý dành cho thủ thư và Admin.
- Kết nối với backend thông qua Amazon API Gateway.

**Backend - Node.js, AWS Lambda và API Gateway**

- Tiếp nhận và xử lý các yêu cầu từ frontend.
- Kiểm tra vai trò và quyền truy cập của người dùng.
- Xử lý các nghiệp vụ quản lý sách và độc giả.
- Xử lý quy trình mượn, trả, đặt trước và gia hạn.
- Tính toán hạn trả và tiền phạt.
- Truy xuất và cập nhật dữ liệu trong Amazon DynamoDB.
- Điều phối các yêu cầu đến trợ lý AI.

**Xác thực và phân quyền - Amazon Cognito**

- Quản lý việc đăng ký và đăng nhập tài khoản.
- Sử dụng các nhóm quyền để phân biệt độc giả, thủ thư và Admin.
- Cung cấp token xác thực cho các yêu cầu API.
- Không cho phép người dùng tự chọn quyền Admin hoặc thủ thư khi đăng ký.

**Cơ sở dữ liệu - Amazon DynamoDB**

- Lưu trữ dữ liệu nghiệp vụ của hệ thống thư viện.
- Quản lý thông tin sách và số lượng bản sách.
- Lưu hồ sơ độc giả.
- Theo dõi các phiếu mượn trả.
- Quản lý đặt trước, hàng chờ và các thông báo.
- Hỗ trợ các thao tác cập nhật có điều kiện để đảm bảo tính chính xác của dữ liệu.

**Trợ lý AI - Amazon Bedrock**

- Hỗ trợ hỏi đáp nội quy thư viện.
- Tìm kiếm sách theo nhu cầu.
- Sử dụng Knowledge Bases để truy xuất nguồn tài liệu.
- Kết hợp dữ liệu hiện tại từ DynamoDB để hiển thị tình trạng sách.

**Lưu trữ - Amazon S3**

- Lưu ảnh bìa sách.
- Lưu nội quy thư viện, FAQ và mô tả sách.
- Cung cấp tài liệu đầu vào cho Knowledge Bases.

**Tự động hóa và thông báo**

- EventBridge Scheduler kích hoạt Lambda theo lịch.
- Lambda kiểm tra các phiếu sắp đến hạn, quá hạn và hàng chờ.
- Amazon SES gửi email thông báo đến người dùng.

#### Thiết kế cơ sở dữ liệu với Amazon DynamoDB

Hệ thống sử dụng **Amazon DynamoDB làm cơ sở dữ liệu chính** để quản lý dữ liệu nghiệp vụ.

DynamoDB là dịch vụ cơ sở dữ liệu NoSQL được AWS quản lý, phù hợp với kiến trúc Serverless của Cloud Library Management System.

Frontend không trực tiếp truy cập DynamoDB. Các thao tác đọc, ghi và cập nhật dữ liệu được thực hiện thông qua API Gateway và AWS Lambda sau khi kiểm tra quyền truy cập.

**Các nhóm dữ liệu chính**

| Nhóm dữ liệu | Các trường dữ liệu đề xuất | Chức năng |
| --- | --- | --- |
| **Books** | bookId, title, author, category, totalCopies, availableCopies, coverImageKey | Quản lý danh mục, thông tin sách và số lượng sách. |
| **Readers** | cognitoSub, fullName, studentId | Quản lý hồ sơ độc giả. |
| **Loans** | loanId, readerId, bookId, copyId, borrowDate, dueDate, returnDate, status, fineAmount, renewalCount | Quản lý phiếu mượn, hạn trả, gia hạn và tiền phạt. |
| **BookCopies** | copyId, bookId, qrCode, status | Theo dõi từng bản sách vật lý. |
| **Reservations** | reservationId, readerId, bookId, queuePosition, holdUntil | Quản lý đặt trước và hàng chờ. |
| **Favorites** | readerId, bookId | Lưu danh sách sách yêu thích. |
| **Notifications** | notificationId, recipientId, type, status | Theo dõi các thông báo gửi đến người dùng. |

*Các tên trường ở bảng trên là cách biểu diễn đề xuất từ nội dung tài liệu. Thiết kế bảng, Partition Key, Sort Key và các chỉ mục truy vấn sẽ được xác định khi hoàn thiện cơ sở dữ liệu.*

**Phân chia trách nhiệm lưu trữ**

- **Amazon DynamoDB:** Lưu thông tin nghiệp vụ của thư viện.
- **Amazon Cognito:** Quản lý thông tin đăng nhập và danh tính người dùng.
- **Amazon S3:** Lưu ảnh bìa và các tài liệu phục vụ AI.
- **Amazon Bedrock Knowledge Bases:** Truy xuất nội dung từ nguồn tài liệu đã được phê duyệt.

**Quy trình lưu trữ dữ liệu khi mượn sách**

1. Độc giả gửi yêu cầu mượn sách trên giao diện React.
2. API Gateway tiếp nhận yêu cầu và xác thực người dùng.
3. AWS Lambda kiểm tra số sách đang mượn, giới hạn mượn và tình trạng còn sẵn.
4. Thủ thư xác nhận việc giao sách.
5. Lambda sử dụng giao dịch có điều kiện trong DynamoDB để tạo hoặc cập nhật phiếu mượn và giảm số lượng sách còn sẵn.
6. Hệ thống cập nhật trạng thái giao dịch để độc giả theo dõi.

**Quy trình cập nhật dữ liệu khi trả sách**

1. Thủ thư xác nhận nhận lại sách.
2. Lambda kiểm tra trạng thái phiếu mượn.
3. Hệ thống tính tiền phạt nếu sách trả quá hạn.
4. DynamoDB cập nhật trạng thái phiếu và tăng số lượng sách còn sẵn.
5. Thao tác xác nhận trả chỉ được xử lý một lần để tránh tăng số lượng sách trùng lặp.

**Đảm bảo tính nhất quán và bảo mật dữ liệu**

- Sử dụng giao dịch và điều kiện trong DynamoDB để tránh cho mượn vượt số lượng.
- Kiểm tra trạng thái giao dịch trước khi cập nhật.
- Không cho phép độc giả truy cập hồ sơ hoặc phiếu mượn của người khác.
- Kiểm tra quyền truy cập ở backend.
- Phân quyền truy cập DynamoDB cho Lambda theo nguyên tắc quyền tối thiểu.

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai

Dự án được tổ chức theo bốn giai đoạn triển khai đề xuất.

**Giai đoạn 1: Nghiên cứu và thiết kế kiến trúc**

- Phân tích yêu cầu và xác định chức năng hệ thống.
- Xác định các nhóm người dùng và quyền truy cập.
- Nghiên cứu các dịch vụ AWS phù hợp.
- Thiết kế kiến trúc Serverless.
- Thiết kế các nhóm dữ liệu sử dụng Amazon DynamoDB.
- Xác định quy tắc quản lý sách, mượn trả, gia hạn và tiền phạt.

**Giai đoạn 2: Xây dựng các chức năng nghiệp vụ**

- Xây dựng giao diện người dùng với React.
- Thiết lập Amazon Cognito.
- Xây dựng API Gateway và các hàm AWS Lambda.
- Thiết lập cơ sở dữ liệu Amazon DynamoDB.
- Phát triển chức năng quản lý sách và độc giả.
- Phát triển quy trình mượn trả và tính tiền phạt.

**Giai đoạn 3: Tích hợp AI và tiện ích**

- Chuẩn bị nội quy, FAQ và mô tả sách.
- Lưu tài liệu nguồn trên Amazon S3.
- Cấu hình Amazon Bedrock Knowledge Bases.
- Tích hợp trợ lý AI hỏi đáp nội quy và tìm sách.
- Phát triển đặt trước, hàng chờ và gia hạn.
- Thiết lập hệ thống nhắc hạn trả.

**Giai đoạn 4: Kiểm thử và triển khai**

- Kiểm thử các chức năng nghiệp vụ.
- Kiểm tra quyền truy cập theo vai trò.
- Kiểm thử tính nhất quán dữ liệu trong DynamoDB.
- Kiểm tra kết quả truy xuất của trợ lý AI.
- Theo dõi lỗi và chi phí AWS.
- Triển khai ứng dụng và chuẩn bị demo.

#### Yêu cầu kỹ thuật

**Giao diện người dùng**

- React.
- Kết nối backend thông qua API Gateway.
- Hỗ trợ giao diện phù hợp với từng nhóm quyền.

**Xử lý nghiệp vụ**

- Node.js.
- AWS Lambda.
- Amazon API Gateway.
- Kiểm tra xác thực và phân quyền thông qua Amazon Cognito.

**Cơ sở dữ liệu**

- Amazon DynamoDB.
- Lưu trữ dữ liệu sách, độc giả và giao dịch thư viện.
- Hỗ trợ truy vấn dữ liệu theo nhu cầu nghiệp vụ.
- Sử dụng giao dịch có điều kiện đối với các thao tác cập nhật quan trọng.

**Trợ lý AI**

- Amazon Bedrock.
- Amazon Bedrock Knowledge Bases.
- Amazon S3.
- Kho vector cho dữ liệu truy xuất.
- Amazon S3 Vectors là phương án đề xuất khi được hỗ trợ tại Region triển khai.

**Thông báo và giám sát**

- Amazon EventBridge Scheduler.
- Amazon SES.
- Amazon CloudWatch.
- AWS IAM.

**Quy tắc nghiệp vụ**

| Quy định | Giá trị áp dụng cho bản demo |
| --- | --- |
| Số sách mượn tối đa | 3 cuốn/độc giả |
| Thời hạn mượn | 14 ngày |
| Tiền phạt quá hạn | 5.000 VNĐ/ngày |
| Số lần gia hạn tối đa | 1 lần |
| Thời gian gia hạn | Thêm 7 ngày |
| Thời gian giữ sách đặt trước | 48 giờ |
| Múi giờ tính hạn trả | Việt Nam |

Độc giả chỉ được gia hạn khi phiếu chưa quá hạn và không có người đặt trước.

Tiền phạt được backend tính dựa trên số ngày trả trễ. Trường hợp sách chưa trả, số tiền phạt được hiển thị dưới dạng tạm tính.

### 5. Lộ trình & Mốc triển khai

#### Lộ trình dự án

Dự án được đề xuất triển khai theo các mốc sau:

| Giai đoạn | Nội dung | Kết quả dự kiến |
| --- | --- | --- |
| **1. Phân tích và thiết kế** | Xác định yêu cầu, thiết kế kiến trúc AWS và dữ liệu DynamoDB. | Tài liệu yêu cầu, sơ đồ kiến trúc và thiết kế dữ liệu. |
| **2. Phát triển chức năng cốt lõi** | Xây dựng React, Cognito, API Gateway, Lambda và DynamoDB. | Hệ thống quản lý sách, độc giả và mượn trả. |
| **3. Tích hợp AI và tiện ích** | Tích hợp Bedrock, Knowledge Bases, đặt trước, gia hạn và thông báo. | Các chức năng AI và tiện ích ưu tiên. |
| **4. Kiểm thử và triển khai** | Kiểm thử nghiệp vụ, phân quyền và triển khai ứng dụng. | Website hoạt động và kịch bản demo. |

*Thời gian cụ thể của từng giai đoạn sẽ được bổ sung sau khi nhóm hoàn thiện kế hoạch thực hiện.*

**Chức năng ưu tiên triển khai**

- Đăng nhập và phân quyền.
- Quản lý sách và độc giả.
- Tìm kiếm sách.
- Quản lý yêu cầu mượn trả.
- Theo dõi lịch sử và tính tiền phạt.
- AI hỏi đáp nội quy.
- AI tìm sách theo nhu cầu.
- Đặt trước và hàng chờ.
- Gia hạn trực tuyến.
- Nhắc hạn trả.

**Chức năng mở rộng**

- AI giới thiệu và tóm tắt sách.
- AI gợi ý lộ trình đọc.
- Quét QR hoặc mã vạch.
- Danh sách sách yêu thích.
- Dashboard thống kê nâng cao.
- Thanh toán tiền phạt trực tuyến.

### 6. Ước tính ngân sách

Dự án sử dụng các dịch vụ AWS Serverless, do đó chi phí vận hành phụ thuộc vào khối lượng sử dụng thực tế.

Có thể lập bảng dự toán bằng [AWS Pricing Calculator](https://calculator.aws/).

#### Chi phí hạ tầng

| Dịch vụ AWS | Yếu tố ảnh hưởng đến chi phí |
| --- | --- |
| **Amazon Cognito** | Số lượng người dùng và hoạt động xác thực. |
| **Amazon API Gateway** | Số lượng yêu cầu API. |
| **AWS Lambda** | Số lần thực thi, thời gian chạy và bộ nhớ. |
| **Amazon DynamoDB** | Dung lượng dữ liệu, thao tác đọc/ghi và cấu hình sử dụng. |
| **Amazon S3** | Dung lượng ảnh bìa và tài liệu AI. |
| **Amazon CloudFront** | Lưu lượng phân phối nội dung. |
| **Amazon Bedrock** | Mô hình AI được chọn và mức sử dụng. |
| **Bedrock Knowledge Bases** | Hoạt động truy xuất và đồng bộ dữ liệu. |
| **Amazon S3 Vectors** | Dung lượng vector và hoạt động truy vấn. |
| **EventBridge Scheduler** | Số lượng tác vụ theo lịch. |
| **Amazon SES** | Số lượng email được gửi. |
| **Amazon CloudWatch** | Dung lượng log và hoạt động giám sát. |

**Tổng chi phí dự kiến:** Chưa xác định.

Nhóm sẽ cần lựa chọn AWS Region, cấu hình dịch vụ và ước lượng số người dùng, sách, yêu cầu API và yêu cầu AI để lập bảng chi phí.

#### Các biện pháp kiểm soát chi phí

- Thiết lập cảnh báo ngân sách trên AWS.
- Theo dõi chi phí phát sinh từ Amazon Bedrock.
- Giới hạn tần suất gửi yêu cầu đến trợ lý AI.
- Giới hạn độ dài đầu ra của mô hình.
- Theo dõi mức sử dụng của các dịch vụ ứng dụng.
- Cấu hình thời hạn lưu log trong CloudWatch.

### 7. Đánh giá rủi ro

#### Ma trận rủi ro

| Rủi ro | Ảnh hưởng có thể xảy ra | Biện pháp giảm thiểu |
| --- | --- | --- |
| **Vượt ngân sách AWS** | Chi phí vận hành tăng ngoài dự kiến. | Theo dõi chi phí và thiết lập cảnh báo ngân sách. |
| **Truy cập trái phép** | Người dùng xem hoặc thay đổi dữ liệu không được phép. | Sử dụng Cognito, IAM và kiểm tra quyền trong Lambda. |
| **Sai lệch số lượng sách** | Cho mượn vượt số lượng bản sách còn sẵn. | Sử dụng giao dịch và điều kiện trong DynamoDB. |
| **Cập nhật giao dịch trùng lặp** | Sai số lượng sách hoặc trạng thái phiếu mượn. | Đảm bảo thao tác xác nhận trả chỉ được xử lý một lần. |
| **AI trả lời thiếu chính xác** | Độc giả nhận thông tin không phù hợp. | Sử dụng tài liệu được duyệt và đối chiếu dữ liệu nghiệp vụ. |
| **Thông báo bị gửi trùng** | Người dùng nhận nhiều thông báo giống nhau. | Lưu trạng thái gửi và kiểm tra trước khi gửi. |
| **Dịch vụ AWS gặp lỗi** | Một số chức năng không thể xử lý yêu cầu. | Theo dõi lỗi bằng CloudWatch và xây dựng phương án xử lý. |

#### Chiến lược giảm thiểu

**Bảo mật và phân quyền**

- Áp dụng nguyên tắc Least Privilege trong AWS IAM.
- Kiểm tra vai trò và quyền sở hữu dữ liệu đối với mỗi API.
- Giới hạn quyền truy cập vào Amazon S3.
- Ghi nhật ký khi thay đổi vai trò hoặc quy định hệ thống.

**Đảm bảo tính chính xác của dữ liệu**

- Sử dụng DynamoDB transactions và condition expressions đối với các cập nhật quan trọng.
- Kiểm tra số bản còn sẵn trước khi xác nhận mượn.
- Không cho phép mượn vượt giới hạn.
- Kiểm tra trạng thái phiếu trước khi xác nhận trả.
- Đảm bảo thao tác trả sách không được xử lý lặp.

**Kiểm soát trợ lý AI**

- Chỉ sử dụng tài liệu đã được phê duyệt.
- Đồng bộ lại Knowledge Bases khi nguồn thay đổi.
- Cung cấp nguồn tham khảo cho câu trả lời về nội quy.
- Lấy dữ liệu tình trạng sách và tiền phạt từ hệ thống nghiệp vụ.
- Thông báo chưa đủ thông tin khi không có nguồn phù hợp.

**Theo dõi vận hành**

- Sử dụng CloudWatch để theo dõi lỗi và thời gian xử lý.
- Kiểm soát chi phí sử dụng dịch vụ AWS.
- Cấu hình thời hạn lưu trữ log.

#### Kế hoạch dự phòng

Các phương án dự phòng cần được nhóm tiếp tục hoàn thiện trong quá trình triển khai và kiểm thử.

Những tình huống cần xem xét gồm:

- Gián đoạn kết nối hoặc lỗi API.
- Thao tác cập nhật dữ liệu không thành công.
- Hệ thống không gửi được thông báo.
- Trợ lý AI không tìm thấy tài liệu phù hợp.
- Chi phí AWS vượt mức dự kiến.

Đối với các giao dịch quan trọng, hệ thống cần trả trạng thái lỗi rõ ràng và tránh cập nhật dữ liệu một phần khi thao tác không thành công.

### 8. Kết quả kỳ vọng

#### Cải tiến kỹ thuật

Dự án hướng đến việc xây dựng ứng dụng web quản lý thư viện trên nền tảng AWS, tích hợp các chức năng quản lý nghiệp vụ và trợ lý AI.

**Các kết quả kỹ thuật dự kiến:**

- Xây dựng hệ thống quản lý thư viện trực tuyến.
- Sử dụng Amazon Cognito để xác thực và phân quyền người dùng.
- Xây dựng backend Serverless với Amazon API Gateway và AWS Lambda.
- Sử dụng Amazon DynamoDB làm cơ sở dữ liệu chính.
- Quản lý danh mục sách, từng bản sách và hồ sơ độc giả.
- Xử lý giao dịch mượn trả và tính tiền phạt.
- Hỗ trợ đặt trước, hàng chờ và gia hạn.
- Gửi thông báo nhắc hạn trả.
- Tích hợp trợ lý AI hỏi đáp nội quy và tìm kiếm sách.
- Sử dụng Amazon CloudWatch để theo dõi hoạt động hệ thống.

#### Kịch bản demo dự kiến

**Bước 1: Quản lý tài khoản và sách**

Admin cấp vai trò thủ thư và cấu hình quy định thư viện.

Thủ thư thêm một đầu sách gồm 3 bản, ảnh bìa và mô tả phục vụ trợ lý AI.

**Bước 2: Tìm kiếm sách bằng AI**

Độc giả hỏi trợ lý AI về các sách phù hợp để học AWS và nội quy thư viện.

Hệ thống hiển thị kết quả dựa trên danh mục sách, nguồn tham khảo và số bản còn sẵn.

**Bước 3: Mượn sách**

Độc giả gửi yêu cầu mượn.

Thủ thư giao sách và xác nhận giao dịch.

Số bản còn sẵn trong DynamoDB giảm từ 3 xuống 2. Độc giả có thể theo dõi hạn trả và lịch sử mượn.

**Bước 4: Đặt trước, gia hạn và tiền phạt**

Hệ thống minh họa chức năng đặt trước hoặc gia hạn.

Email nhắc hạn được gửi theo quy trình.

Sử dụng một phiếu mượn quá hạn 4 ngày để minh họa tiền phạt:

**4 ngày × 5.000 VNĐ = 20.000 VNĐ.**

**Bước 5: Trả sách và kiểm tra bảo mật**

Thủ thư xác nhận trả sách.

DynamoDB cập nhật trạng thái phiếu và tăng số lượng sách còn sẵn từ 2 lên 3.

Kiểm tra nhật ký hệ thống và thử sử dụng tài khoản độc giả truy cập API quản trị để xác nhận yêu cầu bị từ chối.

#### Giá trị dài hạn

Cloud Library Management System có thể được mở rộng để đáp ứng thêm nhu cầu quản lý thư viện trong tương lai.

Các hướng phát triển bao gồm:

- AI tóm tắt mô tả sách và tài liệu được cung cấp.
- AI gợi ý lộ trình đọc theo mục tiêu học tập.
- Quản lý bản sách bằng QR hoặc mã vạch.
- Danh sách sách yêu thích.
- Dashboard thống kê nâng cao.
- Thanh toán tiền phạt trực tuyến.

**Sản phẩm bàn giao dự kiến:**

- Ứng dụng web quản lý thư viện triển khai trên AWS.
- Mã nguồn của dự án.
- Sơ đồ kiến trúc hệ thống.
- Báo cáo nghiệp vụ.
- Tài liệu và hướng dẫn demo.
