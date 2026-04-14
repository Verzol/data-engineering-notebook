<!-- Gộp nội dung từ: assignment-01-schema-design.md -->
# Assignment 01: Schema Design & Normalization

**Thời lượng dự kiến:** 60 phút
**Mục tiêu:** Áp dụng kiến thức phân tích RDBMS và chuẩn mức 3NF để phác thảo lên bản đồ dữ liệu của một trường đại học thu nhỏ.

## Ngữ cảnh (Business Context)

Bạn được giao nhiệm vụ xây dựng hệ thống quản lý Đào tạo cho trường "Data Engineering University". Business Analyst đưa cho bạn một mớ giấy nháp mô tả yêu cầu như sau:

> *"Một trường học có nhiều **Khoa** (IT, Kinh tế, Ngoại ngữ...). Mỗi khoa quản lý nhiều **Giảng viên**, và một giảng viên chỉ trực thuộc đúng một khoa. Các giảng viên sẽ tiến hành giảng dạy các **Môn học**. Một môn học có thể do nhiều giảng viên dạy (ở các lớp khác nhau), và một giảng viên cũng có thể dạy nhiều môn khác nhau. Cuối cùng, **Sinh viên** đăng ký các môn học. Nhà trường cần lưu được thời gian sinh viên ghi danh và **Điểm số cuối kỳ** của sinh viên đó cho môn học. Cần lưu cả số điện thoại của sinh viên nhé!"*

Mẫu file nháp đang được thư ký trường lưu trên Excel trông một dòng rất thảm họa dị thường (Vi phạm 1NF):
`| Sinh_Vien_A | IT_Dept | GiaoVien_X_Y | MonHoc: DB, AI, Code | DienThoai: 091, 092 | Diem_So: 8.0, 9.5 |`

---

## Yêu cầu Bài tập

### Task 1: Thiết kế ERD (Chuẩn Conceptual & Logical)
1. Hãy liệt kê tất cả các **Thực thể (Entities)** có trong ngữ cảnh trên. (Gợi ý: Dựa vào các danh từ in đậm).
2. Xác định **Mối quan hệ (Relationships)** giữa chúng (1-1, 1-N, N-N). Vẽ lại luồng liên kết này trên giấy nháp hoặc dùng tool [Draw.io / dbdiagram.io].
3. Nếu phát hiện quan hệ Nhiều-Nhiều (N-N), hãy tạo ngay Bảng trung gian (Junction table) để hóa giải nó thành hai quan hệ 1-N.

### Task 2: Áp dụng Chuẩn hóa 3NF
Lên danh sách các Bảng cuối cùng (Dạng Physical Data Model) và chỉ định Primary Key (PK), Foreign Key (FK) cho mỗi bảng. Thiết kế của bạn phải thỏa mãn mức độ **3NF**:
- Không được có cột chứa nhiều giá trị một lúc như cột "Sở thích" hay "Nhiều SĐT" (Phá vỡ 1NF). Nếu sinh viên có nhiều số điện thoại, bạn xử lý ở cấp Table như nào?
- Liệu có thuộc tính phi-khóa nào phụ thuộc vào thuộc tính phi-khóa khác không? Nếu có hãy tách bảng.

*Mẫu nộp bài Task 2 (Kẻ bảng danh sách Cột cho từng Bảng):*
- **Table: Departments**
  - `dept_id` (PK)
  - `dept_name`

### Task 3: Phân tích Denormalization (Câu hỏi Tự luận)
Sau khi thiết kế xong bản 3NF tuyệt đẹp ở Task 2. Giám đốc muốn tạo một "Bảng Dashboard Báo cáo cấp tốc" để ngày nào Giám đốc cũng vào xem **Tổng số Sinh viên của Từng Khoa và Điểm Trung bình Hệ thống** mà không tốn quá nhiều thời gian CPU chờ đợi nối 4, 5 bảng.
- Bạn có đề xuất Phi chuẩn hóa (Denormalization) thiết kế nào không? (Gợi ý: Có nên thêm một cột cắm sẵn nào đó vào bảng cha không?).
- Kỹ thuật phi chuẩn hóa này mang lại ưu điểm/rủi ro gì cho hệ thống mỗi lúc có sinh viên mới nhập học?

---

*Lưu ý: Bạn không cần viết SQL cho bài này. Toàn bộ thiết kế ERD có thể được nộp dưới file Hình ảnh cấu trúc bảng hoặc Note Text.*


---

<!-- Gộp nội dung từ: assignment-02-db-implementation.md -->
# Assignment 02: Database Implementation

**Thời lượng dự kiến:** 90 phút
**Công cụ:** PostgreSQL + DBeaver (Hoặc môi trường tương đương)
**Mục tiêu:** Kiểm chứng năng lực viết mã rành rẽ DDL Constraints (Tạo khung) và bơm dữ liệu mồi DML (Populating).

## Mô tả (Scenario)

Từ bản Blueprint ERD bạn phân tích ở Assignment 01. Giờ đây với quyền hạn của một Database Developer, hãy tự tay "Khai thổ xây nhà" và đổ dữ liệu giả (Seed Data) để trường học có thể lấy hệ thống ra chạy thử nghiệm.

---

## Yêu cầu Bài tập

### Task 1: Implement DDL Scripts (Viết lệnh kiến trúc)
Sử dụng câu lệnh `CREATE TABLE`, viết file `init_schema.sql` thỏa mãn các tiêu chí hóc búa sau:

1. Có bảng `Departments`, `Professors`, `Courses`, `Students`, `Enrollments`. (Cách thiết kế tự do theo Assignment 1 của bạn).
2. Quy chuẩn **Primary Key**: Tất cả các bảng phải khai báo khóa chính kiểu tự động tăng (Dùng kiểu `SERIAL` trên Postgres).
3. Quy chuẩn **Foreign Key**: Liên kết bảng đúng đắn. Trong hệ thống Enrollments, nếu lỡ Sinh viên nghỉ học (Tức Bảng Student bị `DELETE` bằng 1 tay ngang), thì bản ghi đăng ký môn học của bé SV đó cũng phải tự động bay màu theo không thắc mắc. (Gợi ý: Chú ý mệnh lệnh nối `ON DELETE CASCADE`).
4. Bọc các **Constraints (Ràng buộc)** xịn xò để gác cổng:
   - Điểm của Sinh viên (Grade) chỉ được phép rơi trong thang từ 0.0 đến 10.0 (Gợi ý: Dùng `CHECK`).
   - Tên môn học không được phép trùng lặp trong toàn trường (Dùng `UNIQUE`).
   - Email hoặc Tên người gõ vào bắt buộc phải có, không được null.
   - Khi một Enrollment mới khai sinh, nếu không kịp trỏ vào cột Ngày Đăng ký, mặc định hệ thống cho lấy Ngày hiệu hành của Database (Dùng `DEFAULT CURRENT_DATE`).

### Task 2: Implement DML Scripts (Phép màu Hồi sinh)
Nhà không thể vô chủ. Viết câu lệnh `INSERT INTO` để bơm vào Database một khối lượng mồi giả định (Seed Data) phục vụ truy vấn. Lệnh này được gọi là `seed_data.sql`.

*Yêu cầu số lượng data:*
- Thêm tối thiểu **3 Departments** (VD: IT, Business, Languages).
- Thêm tối thiểu **5 Professors**.
- Thêm tối thiểu **6 Courses** (Phân bổ rãi rác cho các Giáo sư dạy).
- Thêm tối thiểu **10 Students**.
- Execute đăng ký cho mỗi bé Student ít nhất 2 môn học, trộn lẫn điểm số giả rải đêu từ 4.0 đến 10.0.

> [!CAUTION]
> **Trap (Bẫy sập):** Chú ý thứ tự `INSERT`! Giống hệt như xây nhà, bạn không thể cất nóc (Bơm dữ liệu cho bảng Enrollment - Con) khi mà móng (Bảng Departments/Student - Cha) còn đang rỗng tuyếch. Bơm sai thứ tự RDBMS sẽ ăn vạ ngay lập tức vì không tìm thấy khóa ngoài Foreign Key!

### Task 3: Kịch bản khẩn cấp (Alter & Transaction)
1. Thư ký phòng Đào tạo thông báo: *"Chết! Tôi muốn sinh viên phải có cột Địa chỉ Phường/Xã ở hệ thống"*. Viết 1 lệnh `ALTER TABLE` chêm vô cột mới là `address` kiểu Text cho sinh viên.
2. Nhà trường phát hiện Giáo sư bị lưu nhầm mã lương. Viết 1 kịch bản Transaction sài `BEGIN;` và `UPDATE` tăng lương, nhưng cuối cùng cố tình báo sai hệ thống bắt buộc xài `ROLLBACK;` để thoái nhượng, trả lại mức lương củ.

---

**Cách nộp bài:**
Gom toàn bộ lệnh SQL chạy tốt từ rên xuống dưới vào 1 file `university_init.sql` gửi lên repo. Đảm bảo bất cứ ai mang file này Run thẳng ở nhà họ thì toàn bộ Database và mầm sống Data đều phun ra y hệt.


---

<!-- Gộp nội dung từ: assignment-03-complex-reporting.md -->
# Assignment 03: Complex Reporting & Analysis

**Thời lượng dự kiến:** 120 phút
**Công cụ:** PostgreSQL / MySQL
**Dữ liệu Môi trường:** Tiếp nối hệ thống data bạn vừa xây từ **Assignment 02** (Lược đồ University).

## Ngữ cảnh (Business Context)
Kỳ kiểm tra chất lượng kết thúc, Ban Cán sự trường "Data Engineering University" ập tới bàn làm việc của bạn và xả ra hàng loạt yêu cầu xuất Báo cáo phức tạp (Data Reporting). Có những dữ liệu ẩn quá sâu vào nhiều bảng, đòi hỏi kỹ năng lồng ghép Joins hoặc Subqueries nâng cao của bạn.

---

## Yêu cầu Báo cáo (Reporting Tasks)

*Viết duy nhất lệnh `SELECT` để trả ra kết quả cho các câu hỏi sau:*

### Task 1: Master of JOINs (Kỹ thuật ráp bảng mạnh mẽ)

**Report 1.1: Danh sách Đăng ký (Overview)**
Viết câu truy vấn xuất tên Đầu đủ của Sinh viên, Tên môn học họ đã đăng ký, và Tên của Vị Giáo sư đang dạy môn đó. Yêu cầu đổi tên cột trả ra (Alias) sao cho thật thân thiện, ví dụ: `student_name`, `course_title`, `professor_name`.
*(Gợi ý: Bạn sẽ phải Join xuyên qua 4 bảng xếp nối đuôi nhau).*

**Report 1.2: Kẻ Bỏ Cuộc (Orphan Tracker bằng OUTER JOIN)**
Ban Đào tạo cần lùng ra những môn học nào đang vắng bóng không có nổi 1 sinh viên nào đăng ký để cắt lớp, HOẶC lùng ra những sinh viên "ma" có nick trên DB nhưng không hề nhập học môn nào.
- Yêu cầu 1: In ra các Môn học (Courses) chưa có ai Enroll.
- Yêu cầu 2: In ra các Sinh viên (Students) rỗng lịch môn học. 
*(Bắt buộc dùng `LEFT JOIN` hoặc `RIGHT JOIN` kèm điều kiện `IS NULL` để lùng).*

### Task 2: Luyện công Thống kê (Aggregations & Grouping)

**Report 2.1: Phân bổ tín dụng**
Hiện ra Mỗi một Bộ phận/Khoa (Department) đang triển khai dạy bao nhiêu Lớp Môn Học. Nhóm lại và sắp xếp Khoa nào dạy nhiều môn nhất lên đầu danh sách.

**Report 2.2: Bảng Xếp hạng Học giả**
Chỉ tính riêng những sinh viên nào đã có Điểm (Grade không bị Null) ở môn học, hãy chiếu ra Danh sách Tính Điểm Trung Bình (Average Grade) của tất cả môn học của cậu Sinh viên đó, bắt buộc điểm TB làm tròn 2 chữ số (`ROUND`). 
**Đặc biệt:** Chặn lại! Đừng in hết cả cái trường. Ban Giám Hiệu chỉ muốn vinh danh Top 3 bạn Sinh viên có điểm Trung Bình này là cao nhất hệ thống. *(Dùng `LIMIT`).*

### Task 3: Thuật Toán Subquery (Truy vấn lồng)

**Report 3.1: So kè với trung bình Ngành (Uncorrelated Subquery)**
Hiển thị Tên Giáo sư và số lượng Môn học mà giáo sư này đang ôm. **Hạn mức:** Chỉ cần quan tâm và in ra tên những vị Giáo sư nào chịu khó dạy ra số Môn nhiều hơn cái số lượng dạy trung bình của tất cả giáo sư trên toàn hệ thống.

**Report 3.2: Khúc xương ác mộng khó nhai nhất (Subquery IN / Correlated tùy sở thích)**
Ban Giám Hiệu nổi giận rà soát: "Xuất ra cho tôi tên những **Sinh viên** nào dám đăng ký từ 2 môn trở lên **MÀ CẢ 2 MÔN ĐÓ ĐỀU DO CHUNG 1 GIÁO SƯ DUY NHẤT BAO THẦU THI ĐẬU**!". (Sợ có đi đêm).
*(Gợi ý: Câu này cực kì hóc học búa. Đẳng cấp Master SQL. Bạn hãy đếm tổng số Giáo sư khác biệt (Count distinct professor) dạy cho 1 mã học sinh, làm sao cho số Giáo sư dạy = 1 nhưng số Môn của học sinh > 1).*

---

**Cách nộp bài:**
Copy nội dung 6 câu SQL script thẳng hàng lối, dán vào 1 file `complex_analysis_reports.sql`. Chạy thử trên máy bạn thấy ra bảng Data tức là thành công rực rỡ! Ngôn ngữ chỉ có học qua việc ăn hành bằng code thôi. Chúc các Data Engineer xuất sắc may mắn!


---

