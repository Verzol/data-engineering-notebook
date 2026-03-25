# Structured & Unstructured Data

## 1. Dữ liệu có cấu trúc (Structured Data)

### Định nghĩa

Dữ liệu có cấu trúc (Structured Data) là dữ liệu được tổ chức, định dạng và lưu trữ theo một lược đồ (schema) xác định trước. Dữ liệu này tuân theo một định dạng cố định với các hàng (rows) và cột (columns) rõ ràng, trong đó mỗi trường dữ liệu có một loại dữ liệu (data type) và ý nghĩa (semantic) cụ thể.

**Đặc điểm chính:**

- **Có lược đồ (Schema-based)**: Cấu trúc dữ liệu được định nghĩa rõ ràng trước khi nhập dữ liệu.
- **Định dạng cố định**: Mỗi bản ghi phải tuân thủ cấu trúc được định sẵn.
- **Dễ truy vấn**: Có thể truy vấn bằng SQL hoặc các ngôn ngữ truy vấn tiêu chuẩn.
- **Bảng (Tabular)**: Dữ liệu được sắp xếp thành các bảng với hàng và cột rõ ràng.

### Ví dụ về Dữ liệu có cấu trúc

```
Bảng Employee:
| emp_id | emp_name      | emp_salary | hire_date  | department |
|--------|---------------|------------|------------|-----------|
| 1      | Nguyễn Văn A  | 50,000,000 | 2023-01-15 | IT        |
| 2      | Trần Thị B    | 45,000,000 | 2023-03-20 | HR        |
| 3      | Phạm Văn C    | 55,000,000 | 2022-06-10 | Sales     |
```

Các ví dụ khác:

- **Bảng trong cơ sở dữ liệu quan hệ**: MySQL, PostgreSQL, Oracle, SQL Server
- **Dữ liệu CSV**: Dữ liệu bảng tính được lưu dưới dạng văn bản phân tách bằng dấu phẩy
- **Dữ liệu Excel**: Các tệp bảng tính có định dạng cột rõ ràng
- **Dữ liệu thời gian thực từ IoT**: Dữ liệu từ các cảm biến với các trường xác định trước

### Ưu điểm của Dữ liệu có cấu trúc

- **Dễ tìm kiếm và truy vấn**: SQL và các công cụ truy vấn khác có thể dễ dàng truy cập dữ liệu.
- **Tính nhất quán cao**: Dữ liệu tuân theo quy tắc dữ liệu (data validation rules) và ràng buộc.
- **Hiệu suất tốt**: Truy vấn trên dữ liệu có cấu trúc thường nhanh hơn.
- **Quản lý dễ dàng**: Dữ liệu được tổ chức rõ ràng, dễ bảo trì và cập nhật.
- **Tích hợp tốt**: Dễ dàng tích hợp giữa các hệ thống khác nhau.

### Nhược điểm của Dữ liệu có cấu trúc

- **Độ cứng nhắc cao**: Khó thay đổi cấu trúc sau khi đã tạo, thêm cột mới có thể tốn nhiều thời gian.
- **Không phù hợp với dữ liệu đa dạng**: Không phù hợp lưu trữ dữ liệu có cấu trúc khác nhau.
- **Khó mở rộng ngang**: Khó chia sẻ dữ liệu trên nhiều máy chủ.
- **Tốn dung lượng**: Dữ liệu bị ràng buộc bởi lược đồ có thể tốn nhiều không gian lưu trữ.

## 2. Dữ liệu phi cấu trúc (Unstructured Data)

### Định nghĩa

Dữ liệu phi cấu trúc (Unstructured Data) là dữ liệu không tuân theo bất kỳ định dạng, lược đồ hoặc cấu trúc cụ thể nào. Đây là dữ liệu tự do (free-form), không có định dạng cột hay hàng rõ ràng, và thường chứa thông tin phức tạp như văn bản, hình ảnh, âm thanh, và video.

**Đặc điểm chính:**

- **Không có lược đồ (Schema-less)**: Dữ liệu không cần tuân thủ một cấu trúc được định sẵn.
- **Định dạng tự do**: Mỗi bản ghi có thể có cấu trúc khác nhau.
- **Khó truy vấn**: Truy vấn yêu cầu các kỹ thuật xử lý dữ liệu phức tạp hơn (NLP, Computer Vision).
- **Đa dạng loại dữ liệu**: Bao gồm văn bản, hình ảnh, âm thanh, video, và các định dạng khác.

### Ví dụ về Dữ liệu phi cấu trúc

```
Tài liệu văn bản (Text):
"Hôm nay là một ngày đẹp trời. Tôi đã đi học và học được rất nhiều điều hay.
Sự học tập là rất quan trọng cho sự phát triển của con người."

Dữ liệu JSON (bán cấu trúc):
{
  "user_id": 123,
  "name": "Nguyễn Văn A",
  "posts": [
    {
      "id": 1,
      "title": "Bài viết đầu tiên",
      "comments_count": 5,
      "tags": ["tech", "ai"]
    }
  ],
  "profile": {
    "bio": "Data Engineer",
    "followers": 1500
  }
}

Hình ảnh (Image): photo.jpg, logo.png
Âm thanh (Audio): podcast.mp3, voice_message.wav
Video (Video): tutorial.mp4, presentation.mkv
```

Các ví dụ khác:

- **Email và tin nhắn**: Không có cấu trúc cố định
- **Bài đăng trên mạng xã hội**: Văn bản, hình ảnh, video, emoji được trộn lẫn
- **Tài liệu PDF**: Có định dạng phức tạp
- **Dữ liệu từ cảm biến (sensor data)**: Có thể có khoảng trống hoặc dữ liệu bị thiếu
- **Log từ ứng dụng**: Không có cấu trúc nhất quán

### Ưu điểm của Dữ liệu phi cấu trúc

- **Linh hoạt cao**: Dễ thêm, xóa, hoặc thay đổi các trường dữ liệu.
- **Phù hợp với nhiều loại dữ liệu**: Có thể lưu trữ bất kỳ loại dữ liệu nào.
- **Phát triển nhanh**: Không cần định nghĩa lược đồ trước, có thể bắt đầu lưu trữ dữ liệu ngay lập tức.
- **Mở rộng tốt**: Dễ mở rộng theo chiều ngang trên nhiều máy chủ (horizontal scaling).
- **Phù hợp với Big Data**: Có thể xử lý lượng dữ liệu khổng lồ hiệu quả.

### Nhược điểm của Dữ liệu phi cấu trúc

- **Khó truy vấn**: Yêu cầu các kỹ thuật xử lý dữ liệu tiên tiến để trích xuất thông tin hữu ích.
- **Tính nhất quán thấp**: Dữ liệu có thể không đồng nhất, gây khó khăn trong phân tích.
- **Khó quản lý**: Không có quy tắc dữ liệu, dễ dẫn đến chất lượng dữ liệu kém.
- **Tiêu tốn dung lượng**: Dữ liệu phi cấu trúc thường chiếm nhiều không gian lưu trữ hơn.
- **Hiệu suất truy vấn thấp**: Truy vấn trên dữ liệu phi cấu trúc thường chậm hơn dữ liệu có cấu trúc.

## 3. So sánh giữa Dữ liệu có cấu trúc và Dữ liệu phi cấu trúc

| Tiêu chí           | Structured Data            | Unstructured Data                      |
| :----------------- | :------------------------- | :------------------------------------- |
| **Lược đồ**        | Có lược đồ xác định trước  | Không có lược đồ (schema-less)         |
| **Định dạng**      | Cố định, tuân thủ cấu trúc | Tự do, không có cấu trúc nhất quán     |
| **Tổ chức**        | Bảng, hàng, cột rõ ràng    | Không có tổ chức hình thức             |
| **Kích thước**     | Thường nhỏ hơn             | Thường lớn hơn (chiếm ~80-90% dữ liệu) |
| **Truy vấn**       | Dễ truy vấn bằng SQL       | Khó truy vấn, cần kỹ thuật tiên tiến   |
| **Hiệu suất**      | Truy vấn nhanh             | Truy vấn chậm                          |
| **Tính nhất quán** | Cao                        | Thấp                                   |
| **Linh hoạt**      | Thấp, khó thay đổi         | Cao, dễ thay đổi                       |
| **Mở rộng**        | Khó mở rộng ngang          | Dễ mở rộng ngang                       |
| **Công cụ**        | SQL, RDBMS                 | NoSQL, MongoDB, Hadoop, Spark          |
| **Ứng dụng**       | ERP, CRM, Banking          | Social Media, Images, Videos           |

## 4. Dữ liệu bán cấu trúc (Semi-structured Data)

### Định nghĩa

Dữ liệu bán cấu trúc (Semi-structured Data) là dữ liệu nằm giữa dữ liệu có cấu trúc và dữ liệu phi cấu trúc. Dữ liệu này không tuân theo lược đồ RDBMS cố định nhưng có các thẻ (tags) hoặc nhãn (labels) để tổ chức thông tin.

## 5. Các định dạng tệp phổ biến (Common File Formats)

### 5.1 JSON (JavaScript Object Notation)

#### Định nghĩa

JSON là một định dạng trao đổi dữ liệu văn bản nhẹ (lightweight), dễ đọc bởi con người và máy tính. JSON được phát triển vào năm 2002 và trở thành tiêu chuẩn phổ biến cho việc truyền dữ liệu giữa các máy chủ web và trình duyệt, cũng như giữa các API.

#### Cấu trúc

JSON sử dụng hai cấu trúc chính:

**1. Object (Đối tượng)** - Bắt đầu bằng `{` và kết thúc bằng `}`

```json
{
  "key1": "value1",
  "key2": 123,
  "key3": true,
  "key4": null
}
```

**2. Array (Mảng)** - Bắt đầu bằng `[` và kết thúc bằng `]`

```json
["item1", "item2", 123, true]
```

**Kiểu dữ liệu trong JSON:**

- **String**: `"hello"` - Chuỗi ký tự bọc trong dấu ngoặc kép
- **Number**: `123`, `45.67` - Số nguyên hoặc số thập phân
- **Boolean**: `true`, `false` - Giá trị logic
- **Null**: `null` - Giá trị không tồn tại
- **Object**: `{}` - Tập hợp các key-value pairs
- **Array**: `[]` - Danh sách các giá trị

#### Ví dụ thực tế

```json
{
  "customer_id": "C001",
  "name": "Nguyễn Văn A",
  "email": "nguyenvana@example.com",
  "phone": "0901234567",
  "is_active": true,
  "registration_date": "2023-01-15",
  "orders": [
    {
      "order_id": "O001",
      "date": "2024-01-15",
      "items": [
        {
          "product_id": "P001",
          "product_name": "Laptop",
          "quantity": 1,
          "price": 20000000
        },
        {
          "product_id": "P002",
          "product_name": "Mouse",
          "quantity": 2,
          "price": 500000
        }
      ],
      "total": 21000000,
      "status": "completed"
    }
  ],
  "address": {
    "street": "123 Đường Nguyễn Huệ",
    "city": "Hồ Chí Minh",
    "district": "Quận 1",
    "postal_code": "70000",
    "country": "Vietnam"
  }
}
```

#### Ưu điểm

- **Nhẹ và nhanh**: Kích thước tệp nhỏ, xử lý nhanh
- **Dễ đọc**: Con người dễ hiểu cấu trúc
- **Hỗ trợ rộng rãi**: Hầu hết ngôn ngữ lập trình đều hỗ trợ
- **Linh hoạt**: Có thể lồng các object và array vô hạn
- **Chuẩn công nghiệp**: Được sử dụng rộng rãi trong web APIs

#### Nhược điểm

- **Không hỗ trợ comment**: Không thể thêm ghi chú trong JSON
- **Không hỗ trợ ngày tháng**: Phải lưu ngày tháng dưới dạng string
- **Không có schema mặc định**: Cần xác định schema riêng (JSON Schema)

#### Ứng dụng

- **REST APIs**: Trao đổi dữ liệu giữa client và server
- **Cấu hình ứng dụng**: package.json (Node.js), config.json
- **NoSQL Databases**: MongoDB lưu trữ dữ liệu dạng JSON
- **Real-time Data**: WebSocket, Server-Sent Events
- **Web Scraping**: Lưu trữ dữ liệu từ trang web

---

### 5.2 CSV (Comma-Separated Values)

#### Định nghĩa

CSV là định dạng tệp văn bản đơn giản để lưu trữ dữ liệu bảng tính (tabular data). Mỗi dòng trong tệp CSV đại diện cho một hàng, và các giá trị được phân tách bằng dấu phẩy. CSV là định dạng phổ biến nhất để trao đổi dữ liệu giữa các ứng dụng khác nhau.

#### Cấu trúc

```csv
column1,column2,column3,column4
value1,value2,value3,value4
value5,value6,value7,value8
```

**Các quy tắc:**

- **Hàng đầu tiên (Header)**: Chứa tên cột (không bắt buộc nhưng được khuyến cáo)
- **Các hàng tiếp theo**: Chứa dữ liệu bảng tính
- **Dấu phân tách mặc định**: Dấu phẩy (`,`), nhưng có thể là `;` hoặc `\t` (tab)
- **Trích dẫn (Quoting)**: Nếu giá trị chứa dấu phẩy, cần bọc trong ngoặc kép: `"value, with comma"`

#### Ví dụ thực tế

```csv
emp_id,emp_name,email,phone,department,salary,hire_date
E001,Nguyễn Văn A,nguyenvana@example.com,0901234567,IT,50000000,2023-01-15
E002,Trần Thị B,tranthib@example.com,0909876543,HR,45000000,2023-03-20
E003,Phạm Văn C,phamvanc@example.com,0912345678,Sales,55000000,2022-06-10
E004,"Lê Thị D (Team Lead)",leqthid@example.com,0913579246,IT,60000000,2021-11-05
```

**Cách xử lý giá trị phức tạp:**

Nếu giá trị chứa dấu phẩy hoặc dòng mới, phải bọc trong ngoặc kép:

```csv
customer_id,name,address
C001,Nguyễn Văn A,"123 Đường Nguyễn Huệ, Quận 1"
C002,Trần Thị B,"456 Đường Lê Lợi, Quận 1"
C003,Phạm Văn C,"789 Đường Trần Hưng Đạo
Quận 5"
```

#### Ưu điểm

- **Đơn giản và nhẹ**: Kích thước tệp nhỏ, dễ xử lý
- **Hỗ trợ phổ quát**: Mọi ứng dụng bảng tính đều hỗ trợ (Excel, Google Sheets, v.v.)
- **Dễ đọc**: Con người có thể mở và dọc trực tiếp
- **Không phụ thuộc công cụ**: Có thể xử lý bằng bất kỳ ngôn ngữ lập trình nào
- **Hỗ trợ big data**: Có thể xử lý tệp lớn giống như Hadoop, Spark

#### Nhược điểm

- **Không có schema**: Không có định dạng chuẩn để định nghĩa kiểu dữ liệu
- **Khó xử lý dữ liệu phức tạp**: Không thể lồng cấu trúc
- **Không hỗ trợ metadata**: Chỉ là bảng phẳng
- **Ambiguity**: Cần thỏa thuận về dấu phân tách, quoting, và encoding
- **Không an toàn khi có dấu phẩy**: Cần escape cẩn thận

#### Ứng dụng

- **Nhập/xuất dữ liệu**: Từ Excel, Google Sheets, Airtable
- **Data Analytics**: Tệp dữ liệu đầu vào cho Pandas (Python), R
- **ETL Processes**: Tệp trung gian trong quy trình xử lý dữ liệu
- **Trao đổi dữ liệu B2B**: Các phần mềm quản lý khác nhau
- **Machine Learning Datasets**: Tập dữ liệu huấn luyện mô hình
- **Log files**: Một số ứng dụng xuất log dưới dạng CSV

### 5.3 So sánh JSON, XML, CSV

| Tiêu chí                  | JSON                               | XML                     | CSV                    |
| :------------------------ | :--------------------------------- | :---------------------- | :--------------------- |
| **Kích thước tệp**        | Nhỏ                                | Lớn                     | Rất nhỏ                |
| **Khả năng đọc**          | Tốt                                | Tốt                     | Rất tốt                |
| **Hỗ trợ lồng (Nesting)** | Có (Object/Array)                  | Có (Elements)           | Không                  |
| **Schema**                | JSON Schema (optional)             | XML Schema (XSD)        | Không có               |
| **Kiểu dữ liệu**          | Có (string, number, boolean, null) | Tất cả đều string       | Tất cả đều string      |
| **Comment**               | Không                              | Có (`<!-- comment -->`) | Không                  |
| **Namespace**             | Không                              | Có                      | Không                  |
| **Tốc độ xử lý**          | Nhanh                              | Chậm                    | Rất nhanh              |
| **Sử dụng phổ biến**      | APIs, NoSQL                        | SOAP, Enterprise        | Excel, Data Import     |
| **Ví dụ use case**        | REST API response                  | SOAP Web Service        | CSV export từ database |

### 5.4 Lựa chọn định dạng nào?

**Chọn JSON khi:**

- Xây dựng REST API
- Làm việc với Node.js, Python, JavaScript
- Cần tốc độ xử lý nhanh
- Dữ liệu có cấu trúc phức tạp (nested)

**Chọn XML khi:**

- Xây dựng SOAP Web Services
- Cần schema chặt chẽ (XML Schema)
- Làm việc với các hệ thống enterprise
- Cần namespace để tránh xung đột
- Cần hỗ trợ công cụ chuẩn (XSLT, XPath)

**Chọn CSV khi:**

- Trao đổi dữ liệu với Excel/Google Sheets
- Dữ liệu bảng tính đơn giản
- Cần kích thước tệp nhỏ nhất có thể
- Dễ dàng import/export
- Thực hiện phân tích dữ liệu

## 6. Ứng dụng trong Data Engineering

### Dữ liệu có cấu trúc (Structured Data)

- **Hệ thống quản lý**: ERP, CRM, HRM
- **Giao dịch tài chính**: Banking, Payment systems
- **Báo cáo kinh doanh**: Analytics, Business Intelligence
- **Quản lý kho dữ liệu**: Data Warehouse, Data Mart
- **IoT có định dạng cố định**: Dữ liệu cảm biến với các trường xác định

### Dữ liệu phi cấu trúc (Unstructured Data)

- **Mạng xã hội**: Facebook, Instagram, TikTok - chứa hình ảnh, video, văn bản
- **Nội dung kỹ thuật số**: Blog, News, Wikipedia
- **Multimedia**: Thư viện hình ảnh, video
- **Email và tin nhắn**: Giao tiếp trong tổ chức
- **Log và Monitoring**: System logs, Application logs, Sensor logs

### Dữ liệu bán cấu trúc (Semi-structured Data)

- **API responses**: Dữ liệu JSON từ các API web
- **Web scraping**: Dữ liệu HTML được lấy từ trang web
- **Dữ liệu IoT**: Thường ở định dạng JSON hoặc CSV
- **Document databases**: MongoDB, Elasticsearch lưu trữ dữ liệu bán cấu trúc

## 7. Công cụ và Công nghệ

### Cho Dữ liệu có cấu trúc

| Công cụ            | Mô tả                                                             |
| :----------------- | :---------------------------------------------------------------- |
| **RDBMS**          | MySQL, PostgreSQL, Oracle, SQL Server - Cơ sở dữ liệu quan hệ     |
| **SQL**            | Ngôn ngữ chuẩn để truy vấn dữ liệu có cấu trúc                    |
| **ETL Tools**      | Talend, Informatica, Apache NiFi - để xử lý và chuyển đổi dữ liệu |
| **Data Warehouse** | Snowflake, Amazon Redshift, Google BigQuery                       |
| **BI Tools**       | Tableau, Power BI, Looker - để tạo báo cáo và dashboard           |

### Cho Dữ liệu phi cấu trúc

| Công cụ                | Mô tả                                                |
| :--------------------- | :--------------------------------------------------- |
| **NoSQL Databases**    | MongoDB, Cassandra, HBase - Cơ sở dữ liệu NoSQL      |
| **Big Data Platforms** | Hadoop, Apache Spark - Xử lý dữ liệu lớn             |
| **Cloud Storage**      | Amazon S3, Azure Blob, Google Cloud Storage          |
| **Machine Learning**   | TensorFlow, PyTorch - Xử lý hình ảnh, video, văn bản |
| **Text Processing**    | NLP, Elasticsearch - Tìm kiếm toàn văn bản           |

### Cho Dữ liệu bán cấu trúc

| Công cụ                | Mô tả                             |
| :--------------------- | :-------------------------------- |
| **Document Databases** | MongoDB, CouchDB, Elasticsearch   |
| **Data Serialization** | JSON, XML, Protocol Buffers       |
| **ETL Platforms**      | Apache NiFi, Talend, Apache Beam  |
| **Data Lakes**         | Cloud storage với xử lý tùy chỉnh |

## 8. Thách thức và Giải pháp

### Thách thức

**Dữ liệu có cấu trúc:**

- Khó thích nghi với thay đổi yêu cầu kinh doanh
- Giới hạn trong lưu trữ dữ liệu đa dạng

**Dữ liệu phi cấu trúc:**

- Khó xử lý và phân tích
- Yêu cầu công nghệ tiên tiến và kỹ năng chuyên môn cao
- Chất lượng dữ liệu không ổn định

### Giải pháp

- **Data Lake**: Lưu trữ cả dữ liệu có cấu trúc, bán cấu trúc, và phi cấu trúc ở một nơi
- **Hybrid Approach**: Sử dụng kết hợp RDBMS và NoSQL tùy theo nhu cầu
- **Data Governance**: Thiết lập quy tắc, tiêu chuẩn, và quy trình quản lý dữ liệu
- **Master Data Management (MDM)**: Quản lý dữ liệu chính một cách tập trung

## 9. Xu hướng trong Data Engineering

- **Data Mesh**: Phân tán quản lý dữ liệu cho các đội riêng lẻ
- **Real-time Streaming**: Xử lý dữ liệu thời gian thực từ các nguồn không cấu trúc
- **AI/ML Integration**: Sử dụng AI/ML để xử lý và phân tích dữ liệu phi cấu trúc
- **Data Lakehouse**: Kết hợp tốt nhất của Data Lake và Data Warehouse
- **GraphQL APIs**: Truy cập dữ liệu bán cấu trúc một cách linh hoạt

---

## Tài liệu tham khảo

- GeeksforGeeks. (2024). _Structured vs Unstructured Data_. Truy cập từ https://www.geeksforgeeks.org
- IBM. (2024). _Structured vs Unstructured Data_. IBM Cloud Education.
- Databricks. (2024). _Lakehouse Architecture_. Truy cập từ https://databricks.com
