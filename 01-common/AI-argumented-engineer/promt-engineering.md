# Prompt Engineering

Là quá trình viết hướng dẫn một cách hiệu quả cho một mô hình để tạo ra nội dung phù hợp với yêu cầu của bản thân.

Vì nội dung được tạo ra từ mô hình là không xác định (non-deterministic), việc hướng dẫn chi tiết để có được kết quả mong muốn là rất quan trọng.

---

## 1. Principles of Professional Prompting

### 1.1. Prompt là gì?

Prompt là đầu vào (input) mà người dùng cung cấp cho mô hình AI để yêu cầu thực hiện một tác vụ cụ thể. Prompt có thể là câu hỏi, chỉ dẫn, đoạn văn bản, hoặc sự kết hợp của nhiều thành phần.

### 1.2. Các thành phần của một Prompt hiệu quả

Một prompt chuyên nghiệp thường bao gồm các thành phần sau:

| Thành phần                  | Mô tả                               | Ví dụ                                                |
| --------------------------- | ----------------------------------- | ---------------------------------------------------- |
| **Role (Vai trò)**          | Gán vai trò cụ thể cho AI           | _"Bạn là một kỹ sư dữ liệu cao cấp..."_              |
| **Context (Ngữ cảnh)**      | Cung cấp thông tin nền              | _"Trong dự án ETL pipeline đang xử lý 10TB/ngày..."_ |
| **Task (Nhiệm vụ)**         | Mô tả rõ ràng yêu cầu cần thực hiện | _"Hãy viết script Python để validate schema..."_     |
| **Format (Định dạng)**      | Chỉ định cấu trúc output mong muốn  | _"Trả lời dưới dạng bảng markdown..."_               |
| **Constraints (Ràng buộc)** | Giới hạn phạm vi hoặc điều kiện     | _"Chỉ sử dụng thư viện có sẵn trong Python 3.11..."_ |

### 1.3. Nguyên tắc viết Prompt chuyên nghiệp

**Nguyên tắc 1: Rõ ràng và cụ thể (Be Specific)**

```
Kém: "Giải thích về database"
Tốt: "Giải thích sự khác biệt giữa OLTP và OLAP database,
         bao gồm use case, kiến trúc và ví dụ cụ thể cho từng loại"
```

**Nguyên tắc 2: Cung cấp ngữ cảnh đầy đủ (Provide Context)**

```
Kém: "Code bị lỗi, sửa giúp tôi"
Tốt: "Đoạn code Python dưới đây dùng pandas để đọc file CSV 2GB
         nhưng gặp lỗi MemoryError trên máy 8GB RAM. Hãy tối ưu
         bằng cách sử dụng chunked reading hoặc Dask:
         [đoạn code]"
```

**Nguyên tắc 3: Chia nhỏ tác vụ phức tạp (Decompose Complex Tasks)**

Thay vì yêu cầu AI thực hiện toàn bộ một tác vụ lớn, hãy chia thành các bước nhỏ:

```
Bước 1: "Phân tích yêu cầu business cho pipeline xử lý đơn hàng"
Bước 2: "Thiết kế schema cho staging và warehouse tables"
Bước 3: "Viết transformation logic bằng dbt"
Bước 4: "Viết test cases để validate kết quả"
```

**Nguyên tắc 4: Chỉ định định dạng đầu ra (Specify Output Format)**

```
"Trả lời theo cấu trúc sau:
- Tóm tắt: (2-3 câu)
- Ưu điểm: (danh sách bullet points)
- Nhược điểm: (danh sách bullet points)
- Khuyến nghị: (1 đoạn ngắn)"
```

**Nguyên tắc 5: Sử dụng delimiter để phân tách nội dung**

Dùng các ký hiệu như `"""`, `###`, `---`, `<tag>` để phân tách rõ ràng các phần khác nhau trong prompt:

```
Hãy tóm tắt đoạn văn bản sau:
###
[Nội dung văn bản cần tóm tắt ở đây]
###
Tóm tắt trong 3 bullet points chính.
```

**Nguyên tắc 6: Cung cấp ví dụ mẫu (Provide Examples)**

Cho AI thấy output mong muốn thông qua ví dụ cụ thể

### 1.4. Các lỗi thường gặp khi viết Prompt

| Lỗi                    | Hậu quả                              | Cách khắc phục                               |
| ---------------------- | ------------------------------------ | -------------------------------------------- |
| Quá mơ hồ              | Output lan man, không đúng trọng tâm | Thêm chi tiết cụ thể, ràng buộc              |
| Quá dài và phức tạp    | AI bỏ sót yêu cầu                    | Chia nhỏ thành nhiều prompt                  |
| Không có ngữ cảnh      | Output không phù hợp thực tế         | Cung cấp background, tech stack, constraints |
| Thiếu định dạng output | Phải format lại thủ công             | Chỉ định rõ format mong muốn                 |

---

## 2. Chain-of-Thought và Few-shot Prompting

### 2.1. Zero-shot Prompting

Là kỹ thuật đơn giản nhất — hỏi trực tiếp mà **không cung cấp ví dụ** nào. Mô hình dựa hoàn toàn vào kiến thức đã được huấn luyện để trả lời.

```
Prompt: "Phân loại sentiment của câu sau: 'Sản phẩm này tuyệt vời!' → "
Output: "Tích cực (Positive)"
```

**Khi nào dùng:** Tác vụ đơn giản, phổ biến mà mô hình đã quen thuộc.

### 2.2. Few-shot Prompting

Cung cấp **một vài ví dụ mẫu** (thường 2-5) trước khi đưa ra yêu cầu thực tế, giúp mô hình hiểu rõ pattern mong muốn.

**Cấu trúc:**

```
Ví dụ 1: Input → Output
Ví dụ 2: Input → Output
...
Yêu cầu thực tế: Input → ?
```

**Ví dụ thực tế — Chuẩn hóa tên cột trong dataset:**

```
Chuyển tên cột về dạng snake_case và viết thường:

"OrderDate" → "order_date"
"CustomerID" → "customer_id"
"Total Amount" → "total_amount"

"ProductCategoryName" →
```

Output mong đợi: `"product_category_name"`

**Ví dụ thực tế — Trích xuất thông tin từ log:**

```
Trích xuất thông tin lỗi từ log entry theo format JSON:

Log: "2024-03-15 14:23:01 ERROR [DataLoader] Failed to connect to PostgreSQL at host:5432 - timeout after 30s"
Output: {"timestamp": "2024-03-15 14:23:01", "level": "ERROR", "component": "DataLoader", "message": "Failed to connect to PostgreSQL", "details": "timeout after 30s"}

Log: "2024-03-15 14:25:33 WARN [Scheduler] Job etl_daily_sales delayed by 300s due to resource contention"
Output: {"timestamp": "2024-03-15 14:25:33", "level": "WARN", "component": "Scheduler", "message": "Job etl_daily_sales delayed", "details": "300s due to resource contention"}

Log: "2024-03-15 15:01:12 ERROR [Transformer] Schema mismatch in table dim_product - expected 12 columns, got 15"
Output:
```

**Mẹo sử dụng Few-shot hiệu quả:**

- Chọn ví dụ **đa dạng**, đại diện cho các trường hợp khác nhau
- Giữ format **nhất quán** giữa các ví dụ
- Số lượng ví dụ tối ưu thường là **2-5** (quá nhiều sẽ tốn token mà không tăng chất lượng)
- Đặt ví dụ **tương tự nhất** với yêu cầu thực tế ở cuối danh sách

### 2.3. Chain-of-Thought (CoT) Prompting

Chain-of-Thought yêu cầu mô hình **trình bày quá trình suy luận từng bước** trước khi đưa ra kết luận cuối cùng. Kỹ thuật này đặc biệt hiệu quả cho các bài toán cần logic, tính toán, hoặc phân tích nhiều bước.

**So sánh có và không có CoT:**

```
Không có CoT:
Prompt: "Một pipeline xử lý 1000 records/phút. Nếu có 5 triệu records
         và 3 worker nodes chạy song song, mất bao lâu để hoàn thành?"
Output: "1667 phút" (có thể sai, không thể kiểm chứng logic)

Có CoT:
Prompt: "Một pipeline xử lý 1000 records/phút. Nếu có 5 triệu records
         và 3 worker nodes chạy song song, mất bao lâu để hoàn thành?
         Hãy giải thích từng bước suy luận."
Output:
  "Bước 1: Tổng throughput = 1000 records/phút × 3 workers = 3000 records/phút
   Bước 2: Thời gian = 5,000,000 / 3,000 = 1,666.67 phút
   Bước 3: Quy đổi = 1,666.67 / 60 ≈ 27.8 giờ
   Kết luận: Khoảng 27.8 giờ (xấp xỉ 1 ngày 4 giờ)"
```

**Các cách kích hoạt CoT:**

| Cách                                      | Ví dụ trigger                                       |
| ----------------------------------------- | --------------------------------------------------- |
| **Explicit** — Yêu cầu trực tiếp          | _"Hãy suy nghĩ từng bước"_ / _"Think step by step"_ |
| **Structured** — Chỉ định cấu trúc        | _"Trình bày theo: Phân tích → Lập luận → Kết luận"_ |
| **Few-shot CoT** — Cho ví dụ có reasoning | Cung cấp ví dụ mẫu bao gồm cả quá trình suy luận    |

**Ví dụ Few-shot CoT — Debug lỗi data pipeline:**

```
Phân tích nguyên nhân gốc (root cause) của các lỗi data pipeline:

Lỗi: "Row count mismatch: source has 1M rows, target has 999,500 rows"
Phân tích:
1. Chênh lệch 500 rows (0.05%) cho thấy dữ liệu bị mất trong quá trình ETL
2. Nguyên nhân có thể: NULL values bị filter, duplicate removal quá mức,
   hoặc transformation logic loại bỏ rows không hợp lệ
3. Kiểm tra: So sánh row count ở từng stage (extract → transform → load)
   để xác định stage nào mất dữ liệu
Root cause likely: Transformation step đang DROP rows có NULL trong required fields

Lỗi: "Job completed but avg processing time increased from 2min to 45min"
Phân tích:
```

**Khi nào nên dùng CoT:**

- Bài toán nhiều bước (tính toán, lập kế hoạch)
- Cần giải thích logic cho người khác review
- Debug và troubleshooting
- So sánh và đánh giá nhiều phương án

### 2.4. Kết hợp các kỹ thuật

Trong thực tế, các kỹ thuật prompting thường được **kết hợp** với nhau:

```
[Role]
Bạn là một Senior Data Engineer với 10 năm kinh nghiệm về AWS.

[Few-shot + CoT]
Ví dụ phân tích kiến trúc pipeline:

Yêu cầu: "Pipeline ingest real-time clickstream data, 100K events/sec"
Phân tích:
1. Volume: 100K events/sec = ~8.6B events/ngày → cần hệ thống streaming
2. Ingestion: Kafka hoặc Kinesis (Kinesis phù hợp hệ sinh thái AWS)
3. Processing: Flink trên Kinesis Data Analytics cho real-time
4. Storage: S3 (raw) + Redshift (aggregated) cho phân tích
Đề xuất: Kinesis → KDA (Flink) → S3 + Redshift

[Task thực tế]
Yêu cầu: "Pipeline xử lý IoT sensor data từ 10,000 thiết bị,
          mỗi thiết bị gửi data mỗi 5 giây, cần anomaly detection real-time"
Phân tích:
```

---

## 3. AI for Technical Document Summarization

### 3.1. Tại sao cần AI để tóm tắt tài liệu kỹ thuật?

Trong công việc Data Engineering, lượng tài liệu kỹ thuật cần đọc rất lớn:

- Documentation của các công cụ (Spark, Airflow, dbt, Kafka...)
- Design documents và Architecture Decision Records (ADR)
- Research papers về phương pháp xử lý dữ liệu mới
- Release notes và changelog của các phiên bản mới
- Incident reports và postmortem documents

AI giúp **rút ngắn thời gian tiếp thu** bằng cách tóm tắt và trích xuất thông tin quan trọng.

### 3.2. Các chiến lược tóm tắt tài liệu

**Chiến lược 1: Tóm tắt tổng quan (Executive Summary)**

```
Prompt:
"Tóm tắt tài liệu kỹ thuật sau trong 5 bullet points chính.
Tập trung vào: mục tiêu, giải pháp đề xuất, và điểm cần lưu ý.
Đối tượng đọc: Data Engineer cần đánh giá nhanh để quyết định
có nên áp dụng không.

###
[Nội dung tài liệu]
###"
```

**Chiến lược 2: Tóm tắt có cấu trúc (Structured Summary)**

```
Prompt:
"Đọc tài liệu kỹ thuật sau và tóm tắt theo cấu trúc:

1. Vấn đề (Problem): Tài liệu giải quyết vấn đề gì?
2. Giải pháp (Solution): Cách tiếp cận được đề xuất?
3. Kiến trúc (Architecture): Các thành phần chính?
4. Trade-offs: Ưu điểm và hạn chế?
5. Áp dụng (Applicability): Phù hợp với trường hợp nào?

###
[Nội dung tài liệu]
###"
```

**Chiến lược 3: Tóm tắt so sánh (Comparative Summary)**

Hữu ích khi cần so sánh nhiều công nghệ hoặc phương án:

```
Prompt:
"Đọc 2 tài liệu sau và tạo bảng so sánh gồm các tiêu chí:
Performance, Scalability, Cost, Learning curve, Community support.

Tài liệu 1 (Apache Spark):
###
[Nội dung]
###

Tài liệu 2 (Apache Flink):
###
[Nội dung]
###"
```

### 3.3. Kỹ thuật nâng cao

**Tóm tắt theo tầng (Hierarchical Summarization)**

Với tài liệu dài, chia thành nhiều phần và tóm tắt từng phần trước, sau đó tóm tắt lại từ các bản tóm tắt:

```
Bước 1: Tóm tắt Chapter 1 → Summary 1
Bước 2: Tóm tắt Chapter 2 → Summary 2
...
Bước N: Tóm tắt [Summary 1 + Summary 2 + ...] → Final Summary
```

Kỹ thuật này giúp giải quyết giới hạn context window của mô hình khi tài liệu quá dài.

**Trích xuất thông tin có mục tiêu (Targeted Extraction)**

Thay vì tóm tắt toàn bộ, chỉ trích xuất thông tin liên quan đến mục tiêu cụ thể:

```
Prompt:
"Từ tài liệu Spark 4.0 release notes bên dưới,
chỉ trích xuất các thay đổi liên quan đến:
1. Structured Streaming improvements
2. Breaking changes ảnh hưởng đến PySpark API
3. Performance improvements cho DataFrame operations

Bỏ qua các thay đổi về Spark ML, GraphX, và R API.

###
[Release notes]
###"
```

**Tạo Q&A từ tài liệu (Document-based Q&A)**

```
Prompt:
"Dựa trên tài liệu sau, hãy trả lời các câu hỏi:
1. Cần config gì để chạy trong production environment?
2. Công cụ này handle failure/retry như thế nào?
3. Có giới hạn nào về scale mà cần lưu ý?

Nếu tài liệu không đề cập đến câu hỏi nào, hãy ghi rõ
'Không tìm thấy trong tài liệu'.

###
[Nội dung tài liệu]
###"
```

### 3.4. Quy trình tóm tắt tài liệu hiệu quả

```
┌─────────────────────────────────────────────────────────────┐
│  1. XÁC ĐỊNH MỤC TIÊU                                      │
│     Tôi cần biết gì từ tài liệu này?                       │
│     ↓                                                        │
│  2. CHỌN CHIẾN LƯỢC                                         │
│     Tổng quan / Có cấu trúc / So sánh / Có mục tiêu?       │
│     ↓                                                        │
│  3. VIẾT PROMPT                                              │
│     Áp dụng nguyên tắc: Role + Context + Task + Format      │
│     ↓                                                        │
│  4. REVIEW VÀ ITERATE                                        │
│     Kết quả đã đủ chính xác và hữu ích chưa?               │
│     Cần điều chỉnh prompt hoặc hỏi thêm chi tiết?          │
│     ↓                                                        │
│  5. LƯU TRỮ VÀ CHIA SẺ                                     │
│     Lưu bản tóm tắt vào knowledge base của team             │
└─────────────────────────────────────────────────────────────┘
```

### 3.5. Lưu ý quan trọng

- **Luôn verify thông tin quan trọng** — AI có thể hiểu sai hoặc bỏ sót chi tiết kỹ thuật
- **Không thay thế hoàn toàn việc đọc** — Với tài liệu quan trọng (security, compliance), cần đọc kỹ bản gốc
- **Cập nhật prompt template** — Lưu lại các prompt hiệu quả để tái sử dụng
- **Chú ý giới hạn context window** — Với tài liệu dài, sử dụng kỹ thuật tóm tắt theo tầng

---

## Nguồn tham khảo

> Nội dung tài liệu này được tổng hợp và biên soạn dựa trên kiến thức chung về Prompt Engineering, kết hợp các nguồn tham khảo chính sau:
>
> 1. **OpenAI — Prompt Engineering Guide**: https://platform.openai.com/docs/guides/prompt-engineering
> 2. **Google — Prompt Engineering for Generative AI**: https://cloud.google.com/vertex-ai/docs/generative-ai/learn/introduction-prompt-design
> 3. **Wei et al. (2022)** — _"Chain-of-Thought Prompting Elicits Reasoning in Large Language Models"_: https://arxiv.org/abs/2201.11903
> 4. **Brown et al. (2020)** — _"Language Models are Few-Shot Learners"_ (GPT-3 paper): https://arxiv.org/abs/2005.14165
> 5. **Anthropic — Prompt Engineering Documentation**: https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering
