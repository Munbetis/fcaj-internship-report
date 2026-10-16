---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Tìm hiểu kiến thức nền tảng về Networking trong AWS và Amazon Virtual Private Cloud (VPC).
* Nắm được các thành phần cơ bản của VPC như CIDR Block, IP Address, Subnet và Route Table.
* Tìm hiểu các cơ chế bảo mật mạng bằng Security Groups và Network ACLs.
* Nghiên cứu cách hoạt động của Internet Gateway và NAT Gateway.
* Tìm hiểu kiến trúc mạng nhiều tầng (Multi-tier Network Architecture) trong AWS.

### Các công việc thực hiện trong tuần

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | **TÌM HIỂU AMAZON VPC** <br> - Bắt đầu tìm hiểu Networking trong AWS theo lộ trình AWS Study Group. <br> - Nghiên cứu khái niệm Amazon Virtual Private Cloud (VPC) và vai trò của VPC trong việc xây dựng môi trường mạng riêng trên AWS. <br> - Tìm hiểu CIDR Block, IP Address, Region, Availability Zone và Subnet. <br> - Xem tài liệu hướng dẫn về cách tổ chức và quản lý tài nguyên mạng trong Cloud. | 05/10/2026 | 05/10/2026 | [Amazon VPC](https://docs.aws.amazon.com/vpc/) |
| 3 | **THIẾT LẬP VPC VÀ SUBNET** <br> - Tìm hiểu quy trình thiết lập VPC trên AWS Management Console. <br> - Nghiên cứu cách phân chia dải địa chỉ IP, tạo Public Subnet và Private Subnet. <br> - Tìm hiểu Route Table và cách định tuyến lưu lượng giữa các Subnet. <br> - Xem hướng dẫn cấu hình VPC cơ bản, ghi chú kiến thức chuẩn bị cho bài thực hành Networking. | 06/10/2026 | 06/10/2026 | [VPC Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/configure-subnets.html) |
| 4 | **SECURITY GROUPS VÀ NACLs** <br> - Tìm hiểu các cơ chế bảo mật mạng trong AWS. <br> - Nghiên cứu Security Groups và Network Access Control Lists (NACLs). <br> - Tìm hiểu Inbound Rules và Outbound Rules để kiểm soát lưu lượng truy cập. <br> - So sánh Security Groups và NACLs về phạm vi áp dụng, Stateful và Stateless. | 07/10/2026 | 07/10/2026 | [VPC Security](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security.html) |
| 5 | **INTERNET GATEWAY VÀ NAT GATEWAY** <br> - Tìm hiểu chức năng và cách hoạt động của Internet Gateway và NAT Gateway. <br> - Nghiên cứu cách Internet Gateway hỗ trợ tài nguyên trong Public Subnet kết nối Internet. <br> - Tìm hiểu cách NAT Gateway cho phép tài nguyên trong Private Subnet truy cập Internet theo chiều đi ra. <br> - Tìm hiểu cách kết hợp Route Table với các thành phần mạng. | 08/10/2026 | 08/10/2026 | [Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html) |
| 6 | **MULTI-TIER NETWORK ARCHITECTURE** <br> - Tìm hiểu kiến trúc mạng nhiều tầng trong AWS. <br> - Nghiên cứu mô hình phân chia hệ thống thành các tầng Web, Application và Database. <br> - Tìm hiểu cách kết hợp VPC, Public Subnet, Private Subnet, Route Table, Security Groups và NAT Gateway. <br> - Xem hướng dẫn bài lab Multi-tier Network Architecture và ghi chú quy trình triển khai. | 09/10/2026 | 09/10/2026 | [AWS VPC](https://docs.aws.amazon.com/vpc/) |
| 7 | **ÔN TẬP KIẾN THỨC NETWORKING** <br> - Tổng hợp kiến thức Networking đã học trong tuần. <br> - Hệ thống lại Amazon VPC, Subnet, Route Table, Security Groups, NACLs, Internet Gateway và NAT Gateway. <br> - Ôn lại mô hình Multi-tier Network Architecture và cách các thành phần mạng kết nối với nhau. <br> - Ghi chú kiến thức quan trọng và chuẩn bị cho các bài thực hành AWS tiếp theo. | 10/10/2026 | 10/10/2026 | [AWS Study Group](https://cloudjourney.awsstudygroup.com/) |

### Kết quả đạt được tuần 3:

* Nắm được kiến thức nền tảng về **Amazon Virtual Private Cloud (VPC)**:
  * Hiểu vai trò của VPC trong việc xây dựng môi trường mạng riêng trên AWS.
  * Tìm hiểu các khái niệm CIDR Block, IP Address, Region và Availability Zone.
  * Hiểu cách sử dụng Subnet để phân chia mạng trong VPC.

* Hiểu cách tổ chức và định tuyến mạng trong **Amazon VPC**:
  * Phân biệt Public Subnet và Private Subnet.
  * Nắm được vai trò của Route Table.
  * Tìm hiểu cách định tuyến lưu lượng giữa các Subnet.

* Có kiến thức cơ bản về **Security Groups và Network ACLs (NACLs)**:
  * Hiểu cách sử dụng Inbound Rules và Outbound Rules.
  * Phân biệt cơ chế Stateful của Security Groups và Stateless của NACLs.
  * Hiểu vai trò của các thành phần này trong việc bảo vệ tài nguyên AWS.

* Tìm hiểu cách kết nối Internet trong môi trường VPC:
  * Hiểu chức năng của Internet Gateway.
  * Nắm được vai trò của NAT Gateway đối với Private Subnet.
  * Hiểu cách kết hợp Gateway và Route Table để tổ chức luồng truy cập mạng.

* Nắm được kiến thức tổng quan về **Multi-tier Network Architecture**:
  * Hiểu mô hình phân chia thành các tầng Web, Application và Database.
  * Tìm hiểu cách kết hợp các thành phần mạng để tăng khả năng quản lý và bảo mật.
  * Nghiên cứu quy trình triển khai mô hình mạng nhiều tầng trên AWS.

* Hoàn thành việc tổng hợp và ôn tập kiến thức Networking trong tuần, tạo nền tảng cho các bài thực hành AWS tiếp theo.