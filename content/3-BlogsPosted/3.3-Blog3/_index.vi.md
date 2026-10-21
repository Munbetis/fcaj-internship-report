---
title: "Blog 3: Amazon Bedrock Knowledge Bases - Xây dựng trợ lý AI với RAG"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AMAZON BEDROCK KNOWLEDGE BASES VÀ RAG

## Xây dựng trợ lý AI hỏi đáp nội quy thư viện bằng Amazon Bedrock Knowledge Bases

Trong những năm gần đây, trí tuệ nhân tạo tạo sinh (Generative AI) ngày càng được ứng dụng rộng rãi vào các hệ thống phần mềm, đặc biệt là những ứng dụng cần tìm kiếm thông tin và hỗ trợ người dùng.

Các mô hình ngôn ngữ lớn (Large Language Models - LLMs) có khả năng hiểu câu hỏi và tạo câu trả lời bằng ngôn ngữ tự nhiên. Tuy nhiên, mô hình không phải lúc nào cũng có sẵn những thông tin nội bộ hoặc dữ liệu mới nhất của một tổ chức.

Ví dụ, trong hệ thống quản lý thư viện, độc giả có thể đặt những câu hỏi như:

- Một người được mượn tối đa bao nhiêu cuốn sách?
- Thời hạn mượn sách là bao lâu?
- Có thể gia hạn sách không?
- Sách trả quá hạn sẽ bị phạt như thế nào?
- Quy trình đặt trước sách được thực hiện ra sao?

Nếu chỉ sử dụng một mô hình AI thông thường, câu trả lời có thể không khớp với quy định riêng của thư viện.

Để giải quyết vấn đề này, chúng ta có thể sử dụng **Retrieval-Augmented Generation (RAG)** kết hợp với **Amazon Bedrock Knowledge Bases**.

Giải pháp giúp ứng dụng truy xuất nội dung từ nguồn tài liệu được cung cấp và sử dụng những thông tin đó làm ngữ cảnh để tạo câu trả lời.

Trong bài viết này, chúng ta sẽ tìm hiểu Amazon Bedrock, cơ chế RAG, Amazon Bedrock Knowledge Bases và cách áp dụng những công nghệ này vào dự án **Cloud Library Management System**.

### Các điểm chính cần nắm

- **Generative AI:** Công nghệ AI có khả năng tạo nội dung mới.
- **Large Language Model (LLM):** Mô hình ngôn ngữ lớn có khả năng xử lý và tạo văn bản.
- **Amazon Bedrock:** Dịch vụ AWS hỗ trợ xây dựng ứng dụng Generative AI bằng các foundation models.
- **Amazon Bedrock Knowledge Bases:** Dịch vụ hỗ trợ kết nối, truy xuất và sử dụng dữ liệu riêng của ứng dụng.
- **Retrieval-Augmented Generation (RAG):** Phương pháp kết hợp truy xuất thông tin và sinh câu trả lời.
- **Embeddings:** Biểu diễn nội dung dưới dạng vector số.
- **Vector Store:** Thành phần lưu trữ và truy vấn vector.
- **Semantic Search:** Phương pháp tìm kiếm dựa trên ý nghĩa của nội dung.
- **Chunking:** Quá trình chia tài liệu thành những phần nhỏ.
- **Data Source:** Nguồn dữ liệu được kết nối với Knowledge Base.
- **RetrieveAndGenerate:** API hỗ trợ truy xuất tài liệu và tạo câu trả lời.

### 1. Tổng quan về Amazon Bedrock

#### 1.1. Amazon Bedrock là gì?

Amazon Bedrock là dịch vụ được AWS quản lý, cung cấp khả năng truy cập các foundation models (FMs) từ AWS và những nhà cung cấp mô hình khác thông qua API.

Foundation Models là những mô hình AI được huấn luyện trên lượng dữ liệu lớn và có thể được sử dụng cho nhiều nhiệm vụ khác nhau.

Một số ứng dụng của Amazon Bedrock bao gồm:

- Xây dựng chatbot hỗ trợ người dùng.
- Tóm tắt tài liệu.
- Tạo nội dung văn bản.
- Phân tích và trích xuất thông tin.
- Xây dựng trợ lý AI cho ứng dụng.
- Hỏi đáp dựa trên tài liệu riêng.

Với Amazon Bedrock, nhà phát triển có thể tích hợp các mô hình AI vào hệ thống mà không cần tự xây dựng và vận hành hạ tầng huấn luyện mô hình từ đầu.

#### 1.2. Những đặc điểm nổi bật

**Truy cập nhiều foundation models**

Amazon Bedrock hỗ trợ nhiều mô hình khác nhau tùy theo AWS Region và khả năng cung cấp của dịch vụ.

**Tích hợp thông qua API**

Nhà phát triển có thể gọi các API Amazon Bedrock từ ứng dụng backend.

**Hỗ trợ xây dựng ứng dụng RAG**

Amazon Bedrock Knowledge Bases giúp kết nối nguồn dữ liệu và hỗ trợ truy xuất thông tin để tạo câu trả lời.

**Tích hợp với hệ sinh thái AWS**

Amazon Bedrock có thể kết hợp với Amazon S3, AWS Lambda, IAM và những dịch vụ khác.

**Quản lý quyền truy cập**

AWS IAM hỗ trợ kiểm soát quyền sử dụng các tài nguyên và API liên quan.

#### 1.3. Những hạn chế cần lưu ý khi sử dụng LLM

Mặc dù LLM có khả năng tạo câu trả lời tự nhiên, việc sử dụng mô hình độc lập vẫn có một số hạn chế:

- Không tự động biết nội quy riêng của thư viện.
- Có thể thiếu thông tin mới được cập nhật.
- Có thể tạo nội dung không chính xác.
- Không tự động truy cập được database của ứng dụng.
- Cần cơ chế kiểm soát nguồn dữ liệu và quyền truy cập.

Một vấn đề quan trọng là **Hallucination**, tức mô hình tạo ra thông tin nghe có vẻ hợp lý nhưng không được hỗ trợ bởi dữ liệu đáng tin cậy.

RAG là một trong những phương pháp giúp giảm rủi ro này bằng cách cung cấp thêm ngữ cảnh từ nguồn dữ liệu đã xác định.

Tuy nhiên, RAG không loại bỏ hoàn toàn hiện tượng Hallucination.

### 2. Retrieval-Augmented Generation (RAG)

#### 2.1. RAG là gì?

Retrieval-Augmented Generation (RAG) là phương pháp kết hợp hai quá trình:

1. **Retrieval:** Truy xuất thông tin liên quan từ nguồn dữ liệu.
2. **Generation:** Sử dụng mô hình AI để tạo câu trả lời dựa trên câu hỏi và thông tin được truy xuất.

Thay vì chỉ dựa vào kiến thức có sẵn của mô hình, RAG cung cấp thêm những đoạn tài liệu phù hợp làm ngữ cảnh.

Ví dụ, người dùng hỏi:

```text
Tôi được mượn tối đa bao nhiêu cuốn sách?
```

Hệ thống tìm trong tài liệu nội quy thư viện và truy xuất nội dung:

```text
Mỗi độc giả được mượn tối đa 3 cuốn sách.
```

Sau đó, mô hình có thể tạo câu trả lời:

```text
Theo nội quy Cloud Library, mỗi độc giả
được mượn tối đa 3 cuốn sách cùng lúc.
```

Nhờ vậy, câu trả lời được xây dựng từ quy định của thư viện thay vì chỉ từ kiến thức chung của mô hình.

#### 2.2. Các thành phần trong hệ thống RAG

| Thành phần | Chức năng |
| --- | --- |
| **User Query** | Câu hỏi được người dùng nhập vào. |
| **Knowledge Base** | Quản lý quá trình truy xuất dữ liệu kiến thức. |
| **Data Source** | Nguồn tài liệu được kết nối. |
| **Embedding Model** | Chuyển nội dung thành vector số. |
| **Vector Store** | Lưu trữ và tìm kiếm vector. |
| **Retrieval** | Tìm những đoạn nội dung liên quan. |
| **Foundation Model** | Tạo câu trả lời dựa trên ngữ cảnh. |
| **Response** | Câu trả lời được trả về cho người dùng. |

#### 2.3. Embeddings là gì?

Embeddings là cách biểu diễn nội dung dưới dạng những vector số.

Những vector này giúp hệ thống so sánh và tìm kiếm sự tương đồng về mặt ngữ nghĩa giữa các đoạn văn bản.

Ví dụ, hai câu hỏi:

```text
Thư viện cho mượn sách trong bao lâu?
```

và

```text
Thời hạn trả sách là mấy ngày?
```

có cách diễn đạt khác nhau nhưng cùng liên quan đến thời hạn mượn sách.

Thông qua embeddings và Semantic Search, hệ thống có thể xác định những tài liệu có ý nghĩa liên quan đến câu hỏi.

#### 2.4. Chunking là gì?

Chunking là quá trình chia tài liệu thành nhiều phần nhỏ để hỗ trợ việc lập chỉ mục và truy xuất.

Ví dụ, tài liệu nội quy thư viện có thể gồm:

```text
NỘI QUY CLOUD LIBRARY

1. Quy định đăng ký độc giả
2. Quy định mượn sách
3. Quy định trả sách
4. Quy định gia hạn
5. Quy định xử lý sách quá hạn
6. Quy định đặt trước
```

Thay vì xử lý toàn bộ tài liệu như một khối thông tin duy nhất, hệ thống có thể chia thành những phần liên quan đến từng nhóm quy định.

Việc lựa chọn kích thước và phương pháp Chunking có thể ảnh hưởng đến độ chính xác khi truy xuất.

#### 2.5. Quy trình hoạt động của RAG

Quy trình RAG cơ bản gồm hai giai đoạn.

**Giai đoạn 1: Chuẩn bị dữ liệu**

1. Tài liệu được đưa vào Data Source.
2. Hệ thống xử lý và chia tài liệu thành các Chunks.
3. Embedding Model chuyển nội dung thành vector.
4. Vector được lưu trong Vector Store.

**Giai đoạn 2: Hỏi đáp**

1. Người dùng đặt câu hỏi.
2. Hệ thống biểu diễn câu hỏi để phục vụ truy xuất.
3. Vector Store được sử dụng để tìm nội dung liên quan.
4. Các đoạn tài liệu phù hợp được cung cấp làm ngữ cảnh.
5. Foundation Model tạo câu trả lời.
6. Hệ thống trả kết quả cho người dùng.

### 3. Tổng quan về Amazon Bedrock Knowledge Bases

#### 3.1. Amazon Bedrock Knowledge Bases là gì?

Amazon Bedrock Knowledge Bases là thành phần trong Amazon Bedrock giúp ứng dụng kết nối với các nguồn dữ liệu và thực hiện quy trình Retrieval-Augmented Generation.

Dịch vụ hỗ trợ những bước như:

- Kết nối nguồn tài liệu.
- Xử lý dữ liệu.
- Chia tài liệu thành Chunks.
- Tạo Embeddings.
- Lưu Embeddings vào Vector Store được hỗ trợ.
- Truy xuất nội dung liên quan.
- Kết hợp dữ liệu truy xuất với mô hình AI để tạo câu trả lời.

Nhờ đó, nhà phát triển không nhất thiết phải tự xây dựng toàn bộ pipeline RAG từ đầu.

#### 3.2. Data Source

Data Source là nguồn dữ liệu mà Knowledge Base sử dụng để xây dựng và cập nhật kho kiến thức.

Một lựa chọn phổ biến là **Amazon S3**.

Ví dụ, Cloud Library có thể lưu các tài liệu:

```text
cloud-library-documents/
    library-rules.pdf
    borrowing-policy.pdf
    return-policy.pdf
    reservation-guide.pdf
```

Các tài liệu này có thể chứa:

- Quy định đăng ký tài khoản.
- Số lượng sách được mượn.
- Thời hạn mượn sách.
- Quy định gia hạn.
- Cách tính tiền phạt.
- Quy trình đặt trước sách.

Đây là cấu trúc tài liệu minh họa cho giải pháp đề xuất.

#### 3.3. Vector Store

Vector Store là nơi lưu trữ vector embeddings để phục vụ truy xuất thông tin.

Amazon Bedrock Knowledge Bases có thể tích hợp với những giải pháp Vector Store được hỗ trợ.

Ví dụ:

- Amazon OpenSearch Serverless.
- Amazon Aurora PostgreSQL với pgvector.
- Amazon S3 Vectors.

Từng lựa chọn có đặc điểm về hiệu năng, tính năng và chi phí khác nhau.

Đối với Cloud Library, Amazon S3 Vectors là một phương án đáng cân nhắc cho bài toán lưu trữ vector kiến thức.

Tuy nhiên, cần kiểm tra khả năng hỗ trợ của mô hình, AWS Region và phương pháp tìm kiếm trước khi lựa chọn.

#### 3.4. Data Synchronization

Sau khi tài liệu được cập nhật trong Data Source, Knowledge Base cần được đồng bộ để lập chỉ mục dữ liệu mới.

Ví dụ, thư viện thay đổi quy định về thời hạn mượn sách.

Khi tài liệu nội quy được cập nhật trên Amazon S3, người quản trị cần thực hiện hoặc tự động hóa quá trình đồng bộ Knowledge Base theo thiết kế.

Nếu không đồng bộ, hệ thống có thể tiếp tục truy xuất nội dung cũ.

Vì vậy, quá trình cập nhật tài liệu là một phần quan trọng trong việc duy trì chất lượng của trợ lý AI.

### 4. Kiến trúc hệ thống RAG trên AWS

Để tích hợp RAG vào Cloud Library, có thể sử dụng các thành phần sau:

| Thành phần | Vai trò |
| --- | --- |
| **React Frontend** | Hiển thị giao diện trợ lý AI. |
| **Amazon Cognito** | Hỗ trợ xác thực người dùng. |
| **Amazon API Gateway** | Tiếp nhận yêu cầu từ frontend. |
| **AWS Lambda** | Xử lý yêu cầu và gọi Bedrock API. |
| **Amazon Bedrock Knowledge Bases** | Truy xuất kiến thức từ tài liệu. |
| **Amazon S3** | Lưu tài liệu nội quy thư viện. |
| **Vector Store** | Lưu Embeddings và hỗ trợ tìm kiếm. |
| **Foundation Model** | Tạo câu trả lời từ ngữ cảnh. |
| **AWS IAM** | Kiểm soát quyền truy cập. |

#### 4.1. Sơ đồ kiến trúc đề xuất

```text
+-----------------------------+
|           Reader            |
|       Đặt câu hỏi AI        |
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
|       Xử lý yêu cầu         |
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
|    Tài liệu nội quy         |
+-----------------------------+
    (Đồng bộ và lập chỉ mục)
```

*Sơ đồ là mô hình khái quát. Trong thực tế, Bedrock Knowledge Bases điều phối việc truy xuất dữ liệu và sử dụng mô hình phù hợp để tạo câu trả lời.*

#### 4.2. Luồng xử lý câu hỏi

Giả sử người dùng hỏi:

```text
Nếu trả sách trễ thì bị phạt bao nhiêu?
```

Hệ thống có thể xử lý như sau:

1. Người dùng nhập câu hỏi vào giao diện React.
2. Frontend gửi yêu cầu đến API Gateway.
3. API Gateway chuyển yêu cầu hợp lệ đến Lambda.
4. Lambda gọi Amazon Bedrock Knowledge Bases.
5. Knowledge Base truy xuất quy định liên quan đến tiền phạt.
6. Foundation Model sử dụng nội dung truy xuất để tạo câu trả lời.
7. Lambda trả kết quả về frontend.
8. Giao diện hiển thị câu trả lời và thông tin nguồn nếu có.

Ví dụ câu trả lời mong muốn:

```text
Theo quy định đề xuất của Cloud Library,
sách trả quá hạn có mức phạt 5.000 VNĐ
cho mỗi ngày quá hạn.
```

Câu trả lời này chỉ nên được hiển thị khi có nguồn tài liệu hợp lệ hỗ trợ thông tin tương ứng.

### 5. Hướng dẫn thực hành Amazon Bedrock Knowledge Bases

Phần này giới thiệu quy trình xây dựng Knowledge Base với tài liệu lưu trên Amazon S3.

Các bước có thể thay đổi tùy AWS Region, quyền truy cập, loại mô hình và giao diện Amazon Bedrock tại thời điểm thực hành.

#### Bước 1: Chuẩn bị tài liệu kiến thức

Đầu tiên, tạo một tài liệu nội quy mẫu cho Cloud Library.

Ví dụ:

```text
CLOUD LIBRARY - LIBRARY RULES

1. Mỗi độc giả được mượn tối đa
   3 cuốn sách cùng lúc.

2. Thời hạn mượn sách là 14 ngày.

3. Độc giả được yêu cầu gia hạn
   một lần thêm 7 ngày nếu đáp ứng
   điều kiện của thư viện.

4. Tiền phạt trả quá hạn là
   5.000 VNĐ cho mỗi ngày.

5. Sách đặt trước được giữ trong
   48 giờ theo quy định.
```

Lưu tài liệu thành định dạng được Data Source hỗ trợ, chẳng hạn `.txt` hoặc `.pdf`.

Các thông tin trên là ví dụ từ quy tắc nghiệp vụ dự kiến của Cloud Library, không phải nội quy của một thư viện đang vận hành thực tế.

#### Bước 2: Tải tài liệu lên Amazon S3

1. Đăng nhập AWS Management Console.
2. Tìm kiếm Amazon S3.
3. Tạo hoặc chọn một S3 Bucket phù hợp.
4. Tạo thư mục lưu tài liệu kiến thức.
5. Upload tài liệu nội quy đã chuẩn bị.
6. Kiểm tra quyền truy cập và cấu hình bảo mật.

Ví dụ đường dẫn dữ liệu:

```text
s3://your-cloud-library-bucket/knowledge/
```

Tên Bucket trên chỉ là ví dụ.

Không nên cấu hình dữ liệu nội bộ ở chế độ công khai nếu ứng dụng không yêu cầu.

#### Bước 3: Truy cập Amazon Bedrock

1. Mở Amazon Bedrock trong AWS Management Console.
2. Chọn AWS Region hỗ trợ các tính năng dự định sử dụng.
3. Kiểm tra quyền truy cập mô hình theo yêu cầu của dịch vụ.
4. Mở mục `Knowledge Bases`.
5. Chọn tạo Knowledge Base mới.

Trong quá trình thực hành, cần kiểm tra khả năng sử dụng Embedding Model và Foundation Model tại Region đã chọn.

#### Bước 4: Tạo Knowledge Base

Khi cấu hình Knowledge Base:

1. Đặt tên, ví dụ `cloud-library-knowledge-base`.
2. Chọn phương thức sử dụng Vector Store phù hợp.
3. Cấu hình IAM Service Role.
4. Chọn Amazon S3 làm Data Source.
5. Chỉ định vị trí chứa tài liệu.
6. Lựa chọn phương pháp Chunking.
7. Chọn Embedding Model được hỗ trợ.
8. Cấu hình Vector Store.
9. Xem lại cấu hình và tạo Knowledge Base.

Ví dụ có thể lựa chọn Amazon S3 Vectors nếu môi trường hỗ trợ và phù hợp với mục tiêu hệ thống.

#### Bước 5: Đồng bộ dữ liệu

Sau khi tạo Knowledge Base:

1. Mở Knowledge Base đã tạo.
2. Chọn Data Source.
3. Chạy quá trình đồng bộ dữ liệu.
4. Theo dõi trạng thái Ingestion Job.
5. Kiểm tra kết quả sau khi đồng bộ hoàn tất.

Trong quá trình này, tài liệu được xử lý và lập chỉ mục để phục vụ tìm kiếm.

Nếu quá trình đồng bộ xảy ra lỗi, cần kiểm tra quyền truy cập, định dạng tài liệu và cấu hình mô hình hoặc Vector Store.

#### Bước 6: Kiểm thử Knowledge Base

Sau khi đồng bộ thành công, sử dụng tính năng kiểm thử của Amazon Bedrock Knowledge Bases.

Ví dụ các câu hỏi:

```text
Tôi được mượn bao nhiêu cuốn sách?
```

```text
Thời hạn mượn sách của tôi là bao lâu?
```

```text
Tôi có thể gia hạn sách không?
```

```text
Sách trả quá hạn được tính phí thế nào?
```

```text
Sách đặt trước được giữ trong bao lâu?
```

Khi kiểm thử, cần đánh giá:

- Câu trả lời có đúng nội dung tài liệu không?
- Hệ thống có tìm được đoạn tài liệu liên quan không?
- Câu trả lời có trích dẫn nguồn phù hợp không?
- Hệ thống có tạo thông tin không xuất hiện trong tài liệu không?
- Câu hỏi diễn đạt khác nhau có trả về kết quả nhất quán không?

### 6. Tích hợp Knowledge Base với AWS Lambda

Để đưa chức năng hỏi đáp AI vào website Cloud Library, backend có thể gọi Amazon Bedrock thông qua AWS SDK.

#### 6.1. Chuẩn bị thư viện Node.js

AWS SDK for JavaScript v3 hỗ trợ làm việc với Amazon Bedrock Knowledge Bases.

Cài đặt thư viện:

```bash
npm install @aws-sdk/client-bedrock-agent-runtime
```

#### 6.2. Ví dụ gọi RetrieveAndGenerate

Đoạn code sau minh họa cách đặt câu hỏi tới Knowledge Base từ Node.js.

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
    text: "Thời hạn mượn sách là bao lâu?"
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

**Giải thích:**

- `BedrockAgentRuntimeClient`: Khởi tạo client cho Bedrock Agent Runtime.
- `RetrieveAndGenerateCommand`: Gửi yêu cầu truy xuất và tạo câu trả lời.
- `input.text`: Câu hỏi của người dùng.
- `knowledgeBaseId`: Mã Knowledge Base.
- `modelArn`: Định danh mô hình tạo câu trả lời được hỗ trợ.
- `response.output`: Chứa văn bản câu trả lời.
- `response.citations`: Chứa thông tin trích dẫn nếu được trả về.

Ví dụ sử dụng các Environment Variables:

```text
KNOWLEDGE_BASE_ID=YOUR_KNOWLEDGE_BASE_ID
BEDROCK_MODEL_ARN=YOUR_SUPPORTED_MODEL_IDENTIFIER
```

Những giá trị trên phải được thay bằng cấu hình thực tế.

Đoạn code giả định Knowledge Base đã được tạo, đồng bộ thành công, Region hỗ trợ và môi trường thực thi có quyền IAM thích hợp.

Đây là ví dụ tích hợp kỹ thuật, không có nghĩa chức năng trợ lý AI đã được triển khai hoàn chỉnh trong dự án.

#### 6.3. Vai trò của AWS IAM

Để sử dụng Amazon Bedrock Knowledge Bases, hệ thống cần kiểm soát quyền truy cập.

Ví dụ:

- Knowledge Base Service Role cần quyền truy cập nguồn dữ liệu.
- Service Role cần quyền đối với Vector Store và những mô hình liên quan.
- Lambda Execution Role cần quyền gọi API Amazon Bedrock cần thiết.
- API của ứng dụng cần kiểm tra quyền của người dùng.

Không nên lưu thông tin xác thực AWS trực tiếp trong frontend React hoặc mã nguồn công khai.

### 7. Ứng dụng RAG vào Cloud Library Management System

#### 7.1. Giới thiệu bài toán

Cloud Library Management System được đề xuất tích hợp trợ lý AI để giúp độc giả nhanh chóng tìm hiểu những quy định và hướng dẫn sử dụng thư viện.

Thông thường, người dùng phải tự tìm kiếm thông tin trong nhiều trang hoặc tài liệu.

Ví dụ:

- Trang hướng dẫn mượn sách.
- Trang chính sách gia hạn.
- Trang nội quy.
- Trang quy định tiền phạt.
- Trang hướng dẫn đặt trước.

Trợ lý AI sử dụng RAG có thể hỗ trợ trả lời các câu hỏi dựa trên những tài liệu đó.

#### 7.2. Ví dụ hỏi đáp nội quy

Giả sử người dùng hỏi:

**Câu hỏi 1:**

```text
Tôi có thể mượn tối đa bao nhiêu cuốn?
```

**Câu trả lời mong muốn:**

```text
Theo quy định Cloud Library,
mỗi độc giả có thể mượn tối đa
3 cuốn sách cùng lúc.
```

**Câu hỏi 2:**

```text
Sách được mượn trong bao nhiêu ngày?
```

**Câu trả lời mong muốn:**

```text
Thời hạn mượn sách tiêu chuẩn
là 14 ngày.
```

**Câu hỏi 3:**

```text
Tôi có thể gia hạn thêm không?
```

**Câu trả lời mong muốn:**

```text
Theo quy định đề xuất,
độc giả có thể yêu cầu gia hạn
một lần thêm 7 ngày nếu đáp ứng
điều kiện của thư viện.
```

Các ví dụ này thể hiện cách hệ thống có thể trả lời dựa trên nội dung tài liệu được cung cấp.

#### 7.3. Phân biệt dữ liệu kiến thức và dữ liệu giao dịch

Trong Cloud Library, cần phân biệt hai nhóm dữ liệu quan trọng.

**Dữ liệu kiến thức**

Bao gồm:

- Nội quy thư viện.
- Hướng dẫn mượn và trả sách.
- Chính sách gia hạn.
- Quy định đặt trước.
- Hướng dẫn sử dụng website.

Những dữ liệu này có thể được đưa vào Knowledge Base để phục vụ RAG.

**Dữ liệu giao dịch**

Bao gồm:

- Phiếu mượn của người dùng.
- Trạng thái sách đang mượn.
- Số tiền phạt hiện tại.
- Thông tin đặt trước cá nhân.
- Hồ sơ độc giả.

Những dữ liệu này được quản lý trong database nghiệp vụ, chẳng hạn Amazon DynamoDB.

RAG trên tài liệu tĩnh không nên được sử dụng để khẳng định những thông tin giao dịch đang thay đổi liên tục.

Ví dụ, khi người dùng hỏi:

```text
Tôi đang mượn bao nhiêu cuốn sách?
```

Ứng dụng cần kiểm tra danh tính và truy vấn dữ liệu giao dịch được phép truy cập thay vì dựa hoàn toàn vào tài liệu trong Knowledge Base.

#### 7.4. Mở rộng chức năng tìm kiếm sách

Bên cạnh hỏi đáp nội quy, Cloud Library còn có thể nghiên cứu cách ứng dụng AI để hỗ trợ tìm kiếm sách.

Ví dụ:

```text
Gợi ý cho tôi những cuốn sách
dành cho người mới học Cloud Computing.
```

Đây là hướng mở rộng tiềm năng.

Tuy nhiên, để bảo đảm kết quả phản ánh đúng danh mục hiện có, hệ thống cần thiết kế nguồn dữ liệu sách phù hợp và cơ chế cập nhật thông tin.

Không nên mặc định rằng chỉ cần tạo Knowledge Base nội quy là ứng dụng đã có khả năng tìm kiếm chính xác toàn bộ sách đang được quản lý trong DynamoDB.

### 8. Bảo mật, độ chính xác và tối ưu chi phí

#### 8.1. Bảo mật nguồn dữ liệu

Khi xây dựng ứng dụng AI sử dụng tài liệu riêng, cần chú ý:

- Chỉ cho phép truy cập những tài liệu phù hợp.
- Không đưa dữ liệu cá nhân nhạy cảm vào nguồn kiến thức công khai.
- Sử dụng IAM để kiểm soát quyền truy cập.
- Kiểm tra quyền người dùng trước khi xử lý dữ liệu cá nhân.
- Không đưa AWS Access Keys vào frontend.
- Quản lý tài liệu và những phiên bản cập nhật một cách an toàn.

#### 8.2. Kiểm soát độ chính xác của câu trả lời

Một hệ thống RAG cần được đánh giá dựa trên cả khả năng truy xuất thông tin và chất lượng câu trả lời.

Một số phương pháp cải thiện:

- Chuẩn bị tài liệu rõ ràng và có cấu trúc.
- Chia tài liệu thành những Chunks phù hợp.
- Kiểm thử với nhiều cách diễn đạt câu hỏi.
- Kiểm tra nội dung tài liệu được truy xuất.
- Hiển thị nguồn tham khảo khi có thể.
- Hướng dẫn mô hình không tự tạo câu trả lời khi tài liệu không đủ thông tin.
- Đồng bộ Knowledge Base sau khi cập nhật quy định.

Cần lưu ý rằng việc cung cấp tài liệu cho mô hình không bảo đảm mọi câu trả lời đều chính xác tuyệt đối.

#### 8.3. Tối ưu chi phí

Chi phí triển khai RAG trên AWS phụ thuộc vào các thành phần được sử dụng.

Ví dụ:

| Thành phần | Nguồn chi phí cần xem xét |
| --- | --- |
| **Amazon S3** | Lưu trữ tài liệu và những yêu cầu liên quan. |
| **Embedding Model** | Xử lý dữ liệu để tạo Embeddings. |
| **Vector Store** | Lưu trữ và truy vấn vector. |
| **Foundation Model** | Xử lý dữ liệu đầu vào và tạo nội dung trả lời. |
| **AWS Lambda** | Số lần gọi và tài nguyên thực thi. |
| **Amazon API Gateway** | Số lượng yêu cầu API. |
| **CloudWatch** | Log và những tính năng giám sát. |

Một số hướng tối ưu gồm:

- Chỉ đưa những tài liệu cần thiết vào Knowledge Base.
- Loại bỏ nội dung trùng lặp không cần thiết.
- Lựa chọn mô hình phù hợp với yêu cầu.
- Chọn Vector Store theo nhu cầu hiệu năng và ngân sách.
- Theo dõi số lượng câu hỏi và lượng dữ liệu xử lý.
- Đánh giá cấu hình Chunking.
- Xóa tài nguyên thử nghiệm không còn sử dụng sau khi kiểm tra các dữ liệu cần giữ lại.

Đối với dự án học tập, cần sử dụng AWS Pricing Calculator và bảng giá hiện hành để ước tính chi phí trước khi triển khai.

Không nên xem RAG là một giải pháp hoàn toàn miễn phí chỉ vì ứng dụng sử dụng kiến trúc Serverless.

### 9. Lợi ích và những lưu ý khi sử dụng RAG

#### 9.1. Lợi ích

Việc kết hợp Amazon Bedrock Knowledge Bases và RAG mang lại nhiều lợi ích:

- Hỗ trợ trả lời câu hỏi dựa trên tài liệu của ứng dụng.
- Giảm nhu cầu tìm kiếm thủ công trong nhiều tài liệu.
- Giúp người dùng tiếp cận thông tin nhanh hơn.
- Hỗ trợ cập nhật kho kiến thức.
- Tận dụng khả năng xử lý ngôn ngữ tự nhiên của LLM.
- Có thể tích hợp vào kiến trúc Serverless trên AWS.
- Hỗ trợ cung cấp nguồn tham khảo cho câu trả lời.

#### 9.2. Những lưu ý quan trọng

**Không loại bỏ hoàn toàn Hallucination**

Câu trả lời vẫn cần được kiểm tra, đặc biệt với những thông tin có ảnh hưởng đến người dùng.

**Chất lượng tài liệu ảnh hưởng đến kết quả**

Nếu nguồn kiến thức thiếu chính xác hoặc chưa được cập nhật, câu trả lời có thể không phù hợp.

**Không thay thế database nghiệp vụ**

Knowledge Base không phải giải pháp thay thế toàn bộ những hệ thống quản lý giao dịch như DynamoDB.

**Cần quản lý quyền truy cập**

Ứng dụng phải bảo đảm người dùng chỉ tiếp cận dữ liệu phù hợp với quyền của mình.

**Cần đánh giá chi phí**

Chi phí mô hình AI, Vector Store và những dịch vụ liên quan cần được theo dõi.

**Cần kiểm thử thực tế**

Không nên đánh giá chất lượng chỉ dựa trên một vài câu hỏi minh họa.

### 10. Kết luận

Amazon Bedrock Knowledge Bases là một giải pháp hỗ trợ xây dựng ứng dụng Generative AI dựa trên nguồn dữ liệu riêng.

Thông qua việc nghiên cứu Retrieval-Augmented Generation, em hiểu rõ hơn cách kết hợp quá trình truy xuất tài liệu với khả năng tạo câu trả lời của mô hình ngôn ngữ lớn.

Bên cạnh đó, các khái niệm như Embeddings, Vector Store, Semantic Search và Chunking giúp em có thêm kiến thức về cách tổ chức dữ liệu cho hệ thống hỏi đáp AI.

Đối với dự án **Cloud Library Management System**, RAG là một hướng triển khai phù hợp để xây dựng trợ lý AI hỗ trợ độc giả tìm hiểu nội quy, quy trình mượn trả và những chính sách của thư viện.

Tuy nhiên, quá trình triển khai cần phân biệt rõ dữ liệu kiến thức và dữ liệu giao dịch, đồng thời bảo đảm quyền truy cập, độ chính xác của câu trả lời và chi phí vận hành.

Bài học quan trọng nhất là **để xây dựng một trợ lý AI hữu ích, không chỉ cần mô hình AI mạnh mà còn phải có nguồn dữ liệu đáng tin cậy, cơ chế truy xuất phù hợp và kiến trúc hệ thống an toàn**.

### 11. Hình ảnh minh họa và thực hành

![AMAZON BEDROCK KNOWLEDGE BASES AND RAG](/images/3-Blogs/Blogs3/bedrock_knowledge.png)