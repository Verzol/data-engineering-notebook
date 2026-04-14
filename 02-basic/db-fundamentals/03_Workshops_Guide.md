<!-- Gộp nội dung từ: workshop-01-environment-setup.md -->
# Workshop 01: Course Kick-off & DB Environment Setup

## 1. Tổng quan khóa học và Mục tiêu (Course Overview and Objectives)

Chào mừng bạn đến với khóa học **Database Fundamentals**. Khóa học này được thiết kế nhằm cung cấp các kiến thức nền tảng và kỹ năng cốt lõi nhất về Cơ sở dữ liệu, đặc biệt là Hệ quản trị CSDL Quan hệ (RDBMS). 

**Mục tiêu chính của khóa học:**
- Hiểu rõ sự khác biệt giữa Data có cấu trúc, phi cấu trúc và mô hình dữ liệu quan hệ.
- Nắm vững phương pháp thiết kế CSDL từ ERD (Entity Relationship Diagram) và các kỹ thuật Chuẩn hóa (Normalization).
- Có khả năng cấu trúc hệ thống bảng qua các lệnh DDL (Data Definition Language) và cấp quyền bảo mật DCL.
- Thành thạo ngôn ngữ truy vấn SQL từ cơ bản (SELECT, WHERE) đến nâng cao (JOINs, Subqueries, Aggregations).
- Hiểu sâu về Transactions, tính chất ACID để làm việc thực tế với dữ liệu cấp doanh nghiệp.

## 2. Cài đặt và Cấu hình Môi trường (Install & Configure Environment)

Để có thể thực hành các tác vụ SQL xuyên suốt khóa học, chúng ta sẽ sử dụng **PostgreSQL** (hoặc MySQL) làm CSDL chính. PostgreSQL là một hệ quản trị CSDL mã nguồn mở mãnh mẽ, phổ biến hàng đầu trong giới Data Engineering.

### 2.1 Cài đặt PostgreSQL trên hệ điều hành của bạn
- **Windows / macOS:**
  1. Tải bản cài đặt từ trang chủ [PostgreSQL Downloads](https://www.postgresql.org/download/).
  2. Chạy file installer. Trong quá trình cài đặt, ghi nhớ **Password** cho user mặc định là `postgres` và **Port** (thường là `5432`).
  3. Chọn cài đặt kèm theo `pgAdmin` và `Command Line Tools`.
- **Linux (Ubuntu/Debian):**
  ```bash
  sudo apt update
  sudo apt install postgresql postgresql-contrib
  ```

### 2.2 Kiểm tra kết nối
Mở terminal hoặc command prompt và gõ thử lệnh kết nối bằng công cụ dòng lệnh `psql`:
```bash
psql -U postgres
```
Nếu được hỏi mật khẩu, hãy nhập mật khẩu lúc cài đặt. Khi con trỏ chuột chuyển sang `postgres=#`, chúc mừng bạn đã cài đặt thành công! Gõ `\q` để thoát.

> [!TIP]
> **Docker Alternative:** Nếu không muốn cài DB trực tiếp lên máy tính, bạn có thể chạy PostgreSQL dễ dàng qua Docker: 
> `docker run --name my-postgres -e POSTGRES_PASSWORD=mysecretpassword -p 5432:5432 -d postgres`

## 3. Giới thiệu về SQL GUI Tools (Introduction to SQL GUI Tools)

Thay vì chỉ tương tác bằng Command Line, các kỹ sư thường dùng GUI tools để quản trị, viết lệnh, format và hiển thị dữ liệu dạng bảng đồ họa trực quan.

Dưới đây là các phần mềm SQL GUI phổ biến nhất:

1. **DBeaver (Khuyên dùng)**
   - **Đặc điểm:** Miễn phí, mã nguồn mở, hỗ trợ hầu hết mọi loại cơ sở dữ liệu (PostgreSQL, MySQL, SQL Server, Oracle, MongoDB...).
   - **Tải về:** [dbeaver.io](https://dbeaver.io)
   - **Cách kết nối tới Postgres:** Chọn biểu tượng "New Database Connection" -> Trỏ vào PostgreSQL -> Nhập Host (`localhost`), Database (`postgres`), User (`postgres`) và Password.

2. **pgAdmin 4**
   - **Đặc điểm:** Công cụ chính thức đi kèm PostgreSQL, chạy trên nền web (web-based) siêu nhẹ và đầy đủ các tính năng quản lý nội bộ hệ thống chuyên biệt cho Postgres.

3. **DataGrip (JetBrains)**
   - **Đặc điểm:** Chuyên nghiệp, siêu mạnh về Auto-complete, kiểm tra lỗi cú pháp (IDE xịn xò). Tuy nhiên, đây là phần mềm trả phí (Trial 30 ngày hoặc dùng bản Student miễn phí).

4. **TablePlus**
   - **Đặc điểm:** Nhẹ, nhanh, giao diện màu tối cá tính và hiện đại, sinh ra để dùng trên macOS (nay đã có Windows/Linux). Có bản miễn phí cấu hình thấp.

**Kết luận Workshop 01:**
Sau bài học này, bạn cần chắc chắn hệ thống PostgreSQL đã được chạy sẵn sàng và DBeaver đã thiết lập kết nối thành công tới Database cục bộ. Chúng ta sẽ dùng môi trường này để thiết kế bảng và viết Query trong các bài tiếp theo!


---

<!-- Gộp nội dung từ: workshop-02-intro-to-sql.md -->
# Workshop 02: Review Design & Intro to SQL

Trong Workshop này, chúng ta sẽ bắt đầu làm việc trực tiếp với mã SQL (Structured Query Language) sau khi đã làm quen với các bản phác thảo thiết kế Database (ERD). Đồng thời, chúng ta sẽ xem xét cách chuyển đổi từ "Bản vẽ trên giấy" thành "Bảng thật trong Database" qua quá trình Live Coding, và học cách giải cứu một số rắc rối thường gặp (Troubleshooting) về môi trường kết nối.

## 1. ERD Design Review & Feedback

Trước khi cắm đầu vào gõ code tạo bảng, hãy dành 5 phút nhìn lại thiết kế ERD (Entity-Relationship Diagram) của bạn. Quá trình Review này giúp giảm thiểu việc đập đi xây lại khi hệ thống đã có dữ liệu thực (lúc đó việc sửa bảng rất đau đớn).

**Các câu hỏi Review cơ bản (Trường hợp Quản lý Sinh viên - University):**
- *Tính đầy đủ:* Chúng ta có bảng `Student`, `Course`, `Enrollment`, `Professor` chưa?
- *Nguyên tắc Khóa chính (Primary Key - PK):* Mỗi bảng có một trường định danh duy nhất ID chưa? (Ví dụ: `student_id`).
- *Nguyên tắc Khóa ngoại (Foreign Key - FK):* Bảng `Enrollment` (Đăng ký môn học) đã bắt mối nối FK tới `student_id` và `course_id` để biết sinh viên nào đăng ký môn nào chưa?
- *Chuẩn hóa:* Có sinh viên nào bị lưu thêm thuộc tính như "Sở thích 1, Sở thích 2" cùng một dòng không? (Vi phạm 1NF). Độ chuẩn hóa đã đạt 3NF hay chưa?

## 2. Live Coding: ERD to DDL (Data Definition Language)

Khi ERD đã hoàn chỉnh, nó là bản Blueprint (thiết kế gốc). Công việc tiếp theo là dùng lệnh **SQL DDL (CREATE, ALTER, DROP)** để ra lệnh cho máy tính xây phòng chứa dữ liệu cho Blueprint này.

*(Bạn bật DBeaver/pgAdmin lên, kết nối vào DB PostgreSQL đã cài ở Workshop 01 và làm theo nhé!)*

### Bước 2.1: Khởi tạo Database và Bảng Độc lập (Không chứa FK)
Những bảng độc lập là những bảng không phụ thuộc vào dữ liệu của bảng khác. Ví dụ bảng `departments` (Khoa):
```sql
-- Tạo Database mới (Có thể tạo qua giao diện Graphic của DBeaver cũng được)
CREATE DATABASE university_db;

-- Chuyển connection vào database vừa tạo và chạy lệnh sau:
CREATE TABLE departments (
    dept_id SERIAL PRIMARY KEY,    -- SERIAL là kiểu tự động tăng ID của Postgres
    dept_name VARCHAR(100) NOT NULL UNIQUE
);
```

### Bước 2.2: Khởi tạo Bảng Phụ thuộc (Chứa FK)
Bảng `students` (Sinh viên) sẽ thuộc về 1 `department` (Khoa), do đó nó cần tham chiếu Khóa ngoại (FK) từ bảng `departments`.
```sql
CREATE TABLE students (
    student_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE,
    dept_id INT,                   -- Cột sẽ làm Khóa ngoại
    
    -- Khai báo ràng buộc Khóa ngoại
    CONSTRAINT fk_department
        FOREIGN KEY (dept_id) 
        REFERENCES departments(dept_id)
        ON DELETE SET NULL         -- Khi Khoa bị xóa, sinh viên thuộc Khoa đó sẽ trở thành NULL (Không bị xóa theo vạch trần bộ)
);
```

### Bước 2.3: Bảng Liên kết (Nhiều-Nhiều)
Giữa Sinh viên (`students`) và Khóa học (`courses`), một sinh viên học nhiều khóa, một khóa có nhiều sinh viên. Ta bắt buộc phải tạo **Bảng Trung Gian (Junction table)** `enrollments`.

*Giả định đã có bảng `courses(course_id)`*
```sql
CREATE TABLE enrollments (
    enrollment_id SERIAL PRIMARY KEY,
    student_id INT NOT NULL,
    course_id INT NOT NULL,
    enrollment_date DATE DEFAULT CURRENT_DATE,

    CONSTRAINT fk_student FOREIGN KEY (student_id) REFERENCES students(student_id),
    CONSTRAINT fk_course FOREIGN KEY (course_id) REFERENCES courses(course_id),
    
    -- Một sinh viên không thể đăng ký 1 môn học nguyên xi 2 lần cùng lúc
    CONSTRAINT uq_student_course UNIQUE(student_id, course_id)
);
```
Chỉ qua 3 lệnh `CREATE` này, bạn đã thực tế biến Data Model trên giấy thành schema trong Database của mình.

## 3. Environment Troubleshooting (Xử lý sự cố môi trường)

Trong thực tế đi làm hoặc thực hành, rất hiếm khi bạn ấn nút chạy là code xanh mượt ngay. Lỗi môi trường hay lỗi cú pháp rất phổ biến. Dưới đây là phác đồ sơ cứu:

1. **Lỗi `Connection refused` (Từ chối kết nối):**
   - *Nguyên nhân:* PostgreSQL service (dịch vụ chạy ngầm) trên máy bạn chưa được bật, hoặc bạn gõ sai Port (thường là 5432).
   - *Cách sửa:* Trên Windows, mở phần mềm `Services` -> Tìm `postgresql-x64-XX` -> Chuột phải chọn `Start`. Trên Linux gõ `sudo systemctl start postgresql`.
2. **Lỗi `relation "XYZ" does not exist`:**
   - *Nguyên nhân:* Bạn đang cố truy vấn vào một bảng/cột bị gõ sai chính tả, hoặc bảng đó... chưa bao giờ được tạo bằng lệnh `CREATE`.
   - *Cách sửa:* Mở bảng cây thư mục (Tree menu) của DBeaver ra check xem bảng đó có thực sự nằm trong danh sách không. Nhớ ấn *Refresh* (F5).
3. **Lỗi `Key (XYZ)=(value) is not present in table (ABC)`:**
   - *Nguyên nhân:* Lỗi kinh điển của Foreign Key bóp cò. Bạn insert `dept_id = 99` vào bảng `students` nhưng cái ID 99 lại chưa hề tồn tại trong bảng `departments` mẹ.
   - *Cách sửa:* Phải `INSERT` cha/mẹ trước, rồi mới được thả dữ liệu nối con vào sau. 
4. **Lỗi lệnh kẹt chạy không xong (Running forever):**
   - *Nguyên nhân:* Bị block (khóa vòng) nội bộ do bạn hoặc ai đó đang `UPDATE` bảng mở transaction mà không thèm `COMMIT`.
   - *Cách sửa:* Kill phiên làm việc (Session), hoặc Rollback. (Sẽ học ở bài Transactions).


---

<!-- Gộp nội dung từ: workshop-03-advanced-querying.md -->
# Workshop 03: Advanced Querying Techniques

Chào mừng bạn đến với Workshop 03! Tại đây, chúng ta sẽ bắt đầu ráp nối nhiều kỹ thuật lại cùng nhau: Chữa bài tập Query cũ, Luyện tập Live Coding với dữ liệu thực tế mang tính tổng hợp (Aggregation), và một phần cực kỳ quan trọng là Trực quan hóa (Visualizing) lại cách mà các lệnh `JOIN` thực sự hoạt động dưới nền DB để tránh các lỗi nhân đôi số liệu chết người.

## 1. Review Query Assignment (Chữa bài tập Query cơ bản)

(Học viên mở file hoặc repo chứa các câu `SELECT`, `WHERE`, `GROUP BY` của bài trước lên màn hình).
**Những điểm chết (Pitfalls) thường gặp khi review bài:**
- Dùng sai `COUNT(cột)` và `COUNT(*)`: Gây thiếu hụt kết quả nếu cột đó có dữ liệu `NULL`. Tối ưu nhất để đếm số lượng dòng là `COUNT(1)` hoặc `COUNT(*)`.
- Quên đặt `Alias` (dùng `AS`): Ra báo cáo cột có tên là `sum` hay `count` thay vì tên nghiệp vụ như `total_revenue`, khiến Frontend Dev hay Data Analyst không hiểu cột đó là gì.
- Lầm lẫn thứ tự `WHERE` và `HAVING`: Vẫn cố gắng ép điều kiện `HAVING SUM(salary) > 5000` vào mệnh đề `WHERE`. (Nhắc lại: Lọc điều kiện nhóm phải nằm ở `HAVING`).

## 2. Aggregations Live Practice (Thực hành tổng hợp dữ liệu)

Chúng ta sẽ chạy một số Sample Data (do Mentor cung cấp) để phân tích "Thống kê tình hình hoạt động của Sinh viên/Khoa học".

*Đề bài Thực hành Live 1:* Tìm ra Khoa (Department) có đông sinh viên nhất.
```sql
SELECT 
    dept_id,
    COUNT(student_id) AS student_count
FROM students
GROUP BY dept_id
ORDER BY student_count DESC
LIMIT 1;
```

*Đề bài Thực hành Live 2:* Có bao nhiêu sinh viên đăng ký môn học trong tháng hiện tại? (Áp dụng Data/Time Filtering)
```sql
SELECT 
    COUNT(DISTINCT student_id) AS unique_students -- Cực kì lưu ý chữ DISTINCT để loại trừ sinh viên đăng ký 2 môn bị đếm 2 lần
FROM enrollments
WHERE EXTRACT(MONTH FROM enrollment_date) = EXTRACT(MONTH FROM CURRENT_DATE)
  AND EXTRACT(YEAR FROM enrollment_date) = EXTRACT(YEAR FROM CURRENT_DATE);
```

## 3. Visualizing Joins (Trực quan hóa Phép nối Bảng)

Khi thiết kế Database ở chuẩn **3NF**, dữ liệu bị chém ra làm rất nhiều mảnh (nhiều Bảng). Để đọc được một báo cáo có nghĩa (Ví dụ muốn xem Tên sinh viên và Tên Khoa học đăng kí), bạn bắt buộc phải may (Join) các mảnh đó lại thông qua Khóa chính (PK) và Khóa ngoại (FK).

Bạn có thể chạy thử lệnh rác (Cartesian Product) để xem hậu quả của việc quên gõ điều kiện `ON` trong Join:
```sql
SELECT * FROM students CROSS JOIN courses;
```
*(Nếu bạn có 1000 sinh viên và 50 khóa học, lệnh này trả ra 1000 x 50 = 50,000 dòng rác).*

### Cách trực quan để hiểu JOIN
Mentor sẽ vẽ sơ đồ Venn Diagram (2 vòng tròn giao nhau) lên bảng hoặc màn hình:
1. **[Vùng giao giữa - Vùng chung]:** Đại diện cho `INNER JOIN`. Phải có rễ cắm ở cả 2 bên mới được lên sóng.
2. **[Toàn bộ Vòng tròn Trái]:** Đại diện cho `LEFT JOIN`. Lấy MỌI THỨ bên trái, bên phải không có thì để `NULL`.
3. **[Toàn bộ Vòng tròn Phải]:** `RIGHT JOIN` (Ngược lại).
4. **[Quét sạch 2 Vòng tròn]:** `FULL OUTER JOIN` (Gom hết, thiếu đâu chèn NULL đó).

**Lời khuyên từ Mentor trong quy trình suy luận:**
- *"Mình muốn chọn bảng nào làm Gốc (bảng chính cầm trịch)?"* -> Đặt nó ngay sau `FROM`.
- *"Mình muốn giữ lại toàn bộ Bảng Gốc và chỉ nạp thêm thông tin từ Bảng Phụ?"* -> Sử dụng `LEFT JOIN Bảng_Phụ ON ...`.
- *"Mình chỉ muốn kết quả trả ra phải Khớp dính hoàn toàn 100% hai bên (ai cũng phải có đôi có cặp)?"* -> Sử dụng `INNER JOIN`.

(Mở code IDE lên và chạy đan xen thay đổi `LEFT JOIN` và `INNER JOIN` để thấy số lượng bản ghi trả về thay đổi ntn trên màn hình). Đón xem chi tiết hơn ở Concept Joins Mastery sắp tới!


---

