<!-- Gộp nội dung từ: ddl-dml-core.md -->
# Concept: DDL Mastery & DML Core

Sau khi nắm vững lý thuyết, đây là lúc bạn giao tiếp thực tế với cơ sở dữ liệu qua cú pháp SQL chuẩn hoá, phân chia làm hai mặt trận lõi: **Xây nhà (DDL)** và **Sắp xếp đồ đạc (DML)**. (Lưu ý: Bạn chỉ cần chèn lệnh `COMMIT;` tùy thuộc cấu hình Auto-commit của tool).

## 1. DDL: Lõi ngôn ngữ Định nghĩa Dữ liệu (Data Definition Language)

DDL bao gồm mệnh lệnh chỉ định **thao tác với cấu trúc hạ tầng** của CSDL: Các thao tác Tạo, Sửa, Xóa bảng/schema. Các lệnh này mang tính biểu tượng vĩnh viễn (auto-commit), không thể dễ dàng Ctrl+Z (Rollback).

### 1.1 Lệnh `CREATE`: Tạo mới cấu trúc
Giúp vạch ra cái khung cho dữ liệu (Bảng, Index, View...):
```sql
CREATE TABLE employees (
    emp_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    salary DECIMAL(10, 2),
    hire_date DATE
);
```

### 1.2 Lệnh `ALTER`: Sửa đổi cấu trúc (Không làm mất dữ liệu)
Đã sinh bảng nhưng sếp yêu cầu thêm cột "Số điện thoại"? Không cần xóa bảng đi làm lại, ta dùng `ALTER`:
```sql
-- Thêm một cột mới
ALTER TABLE employees ADD COLUMN phone_number VARCHAR(15);

-- Đổi kiểu dữ liệu của một cột đang có (VD: varchar sang text lớn hơn)
ALTER TABLE employees ALTER COLUMN phone_number TYPE TEXT;

-- Xoá bỏ một cột không dùng đến nữa
ALTER TABLE employees DROP COLUMN phone_number;
```

### 1.3 Lệnh `DROP` và `TRUNCATE`: Tiêu hủy cấu trúc
- **`DROP TABLE`:** Hủy diệt hoàn toàn thực thể. Đập sập cả "nhà" lẫn "đồ đạc" bên trong không để lại dấu vết.
```sql
DROP TABLE employees;
```
- **`TRUNCATE TABLE`:** Phép lai. Giữ nguyên cái "nhà" (cấu trúc rỗng của bàng), nhưng quét dọn hút sạch hoàn toàn "đồ đạc" ngay lập tức (Xóa siêu nhanh, nhanh hơn DELETE).
```sql
TRUNCATE TABLE employees;
```

---

## 2. Constraints (Ràng buộc Dữ liệu)

Để đảm bảo các quy tắc toàn vẹn (Data integrity) không bị phá hỏng bởi sự bất cẩn của con người, mọi DDL phải đi kèm với hệ thống **Constraints**. Không có rào chắn này, Data Engineer sẽ khóc thét lúc dọn dẹp data rác!

| Loại Constraint | Vai trò tác dụng | Ví dụ Cú pháp |
|---|---|---|
| **NOT NULL** | Giá trị của cột không được rỗng/trống. | `email VARCHAR(50) NOT NULL` |
| **UNIQUE** | Đảm bảo tính duy nhất không đụng hàng (dù được phép NULL). Có thể cho sđt, email. | `email VARCHAR(50) UNIQUE` |
| **PRIMARY KEY** | Chìa khóa chính (Sự pha trộn quyền lực của cả `NOT NULL` và `UNIQUE`). Định danh bản ghi. | `id INT PRIMARY KEY` |
| **FOREIGN KEY** | Buộc cột này tham chiếu đến `PRIMARY KEY` của một bảng khác. (Mối nối toàn vẹn) | `FOREIGN KEY (dept_id) REFERENCES departments(id)` |
| **CHECK** | Áp đặt một quy tắc logic bất kỳ (Ví dụ lương phải luôn > 0). Hễ ai nhập số âm DB sẽ chửi cự tuyệt. | `CHECK (salary > 0)` |
| **DEFAULT** | Gán mặc định nếu người xài bỏ trống không nhập gì vào trường đó. | `created_at DATE DEFAULT CURRENT_DATE` |

---

## 3. DML: Lõi ngôn ngữ Thao tác Dữ liệu (Data Manipulation Language)

Một cái bảng vô tri không có ý nghĩa nếu thiếu dữ liệu (Rows/Records). DML được sử dụng để thao tác nội dung thông qua thao tác "Thêm, Sửa, Xóa" dữ liệu thuần túy (CRUD - Create, Read, Update, Delete). Lệnh `SELECT` thực tế cũng thuộc dòng máu DML nhưng mang phong cách riêng là DQL (Data Query Language). 

### 3.1 `INSERT`: Bơm dữ liệu
**Cách 1:** Cấp phát giá trị từng cột theo thứ tự định nghĩa
```sql
INSERT INTO employees (first_name, last_name, salary, hire_date)
VALUES ('John', 'Doe', 5000.00, '2023-01-15');
```
**Cách 2:** Bơm hàng loạt (Bulk Insert - Chuẩn mực ngành Data Engineer)
```sql
INSERT INTO employees (first_name, last_name, salary, hire_date)
VALUES 
    ('Alice', 'Smith', 6000.00, '2022-11-01'),
    ('Bob', 'Johnson', 4500.00, '2023-02-20');
```

### 3.2 `UPDATE`: Chỉnh sửa dữ liệu
> [!CAUTION]
> **Tử huyệt của DML:** Lệnh `UPDATE` và `DELETE` TUYỆT ĐỐI luôn đi kèm dính chặt với mệnh đề `WHERE` (Điều kiện). Nếu bạn quên `WHERE`, bạn vừa vô tình update cho tất cả mọi dòng trong database thành 1 giá trị. Chúc mừng bạn đã phá hỏng cả kho DB.

```sql
-- Chỉ sửa lương cho nhân viên có id = 2
UPDATE employees
SET salary = 5500.00
WHERE emp_id = 2;
```

### 3.3 `DELETE`: Xóa dữ liệu có kiểm soát
Rút tỉa mảng bỏ đi những file lưu trữ bản ghi không con phù hợp (bị khóa, lỗi).
```sql
-- Xóa những ai vào làm chưa qua thử việc hoặc bỏ việc (Giả sử id là 3)
DELETE FROM employees
WHERE emp_id = 3;
```
Sự khác biệt cực lớn giữa `DELETE` và `TRUNCATE` là `DELETE` quét qua từng dòng (log lại toàn bộ lịch sử tốn thời gian nhưng cứu được) và có thể bắn điều kiện `WHERE` nhỏ lẻ. `TRUNCATE` thì dọn toàn bộ cái bảng không hối lỗi.


---

<!-- Gộp nội dung từ: querying-aggregation.md -->
# Concept: Querying & Aggregation Fundamentals

Từ thời điểm này, chúng ta bước vào vương quốc của `SELECT` (Câu lệnh phân vùng truy tìm dữ liệu - DQL). SQL là loại ngôn ngữ Khai báo (Declarative): Bạn nói **những gì bạn muốn lấy** (kết quả mong muốn), chứ không cần quan tâm hệ thống lấy ra bằng các bước mảng xử lý thuật toán nào.

## 1. Nền tảng SELECT (The Core Basics)

Lệnh `SELECT` đơn giản nhất là trỏ thẳng tới một bảng và bóc tách dữ liệu từ các cột.

```sql
-- Lấy tất tần tật (*) các cột
SELECT * FROM employees;

-- Chỉ lấy đích danh một số cột để tiết kiệm RAM/Băng thông
SELECT first_name, salary FROM employees;

-- Nối cột, tính toán trực tiếp và đặt tên giả Alias (AS) cực kì hữu ích
SELECT 
    first_name || ' ' || last_name AS full_name,  -- Phép nối chuỗi kí tự (Postgres)
    salary * 12 AS annual_salary
FROM employees;
```

### Filtering Dữ Liệu (Mệnh đề WHERE)
Data Engineer không bao lấy toàn bộ DB ra ngoài, chúng phải bị thanh lọc khắt khe thông qua lưới lọc điều kiện logic `WHERE`.

```sql
SELECT first_name, salary 
FROM employees
WHERE salary > 5000 AND hire_date > '2022-01-01';
```

**Bộ Toán tử xài chung cực gắt trong WHERE:**
- So sánh: `=`, `<`, `>`, `<=`, `>=`, `<>` (hoặc `!=`)
- Logic AND/OR: `(salary > 5k OR dept = 'IT') AND status = 'Active'`
- So sánh chuỗi (Pattern matching): `WHERE first_name LIKE 'A%'` (Tìm ai lấy tên chữ A đầu) hoặc `%son%` (Chứa chữ 'son'). (Chú ý `ILIKE` dùng k phân biệt hoa/thường ở Postgres).
- Nằm trong list: `WHERE dept IN ('IT', 'HR', 'Sales')` (Tương đương nhiều OR)
- Khoảng giá trị: `WHERE salary BETWEEN 4000 AND 6000`
- Kiểm tra Rỗng: `WHERE email IS NULL` (Không được dùng dấu `=` với NULL)

### Phân trang và Sắp xếp (ORDER BY, LIMIT)
```sql
SELECT first_name, salary 
FROM employees
ORDER BY salary DESC, first_name ASC -- Xếp lương cao nhất trước (DESC), sau đó ưu tiên xếp bảng chữ cái (ASC)
LIMIT 10 OFFSET 20; -- Cắt khúc: Bỏ qua 20 dòng đầu, xin 10 dòng sau (Dùng cho ứng dụng Next/Prev Page)
```

## 2. Các Phép tính Tổng Quát (Aggregations)

Thay vì trả về hàng ngàn dòng chi tiết, tính năng Aggregate tổng hợp tất cả dữ liệu lại theo dạng đo lường "Quy mô", cho ra duy nhất một dòng tổng kết số liệu. Rất tuyệt vời cho Report Data!

* **COUNT()**: Đếm số dòng (rất phổ biến). `COUNT(*)` đếm hết kể cả NULL, `COUNT(cột)` đếm những dòng không bị NULL ở cột đó, `COUNT(DISTINCT cột)` đếm những dòng giá trị khác biệt nhau không trùng ở cột đó.
* **SUM()**: Lấy tổng tích lũy (Sum doanh thu).
* **AVG()**: Giá trị trung bình của toàn kho.
* **MIN() / MAX()**: Sinh giá trị thấp nhất và cao nhất cực đại.

```sql
SELECT 
    COUNT(*) AS total_employees,
    AVG(salary) AS average_salary,
    MAX(hire_date) AS newest_hire_date
FROM employees;
```

## 3. Nhóm Dữ Liệu Học Thuật (GROUP BY & HAVING)

Aggregations phía trên gộp toàn bộ công ty làm một cục. Nhưng sếp cần biết **"Trung bình lương của TỪNG phòng ban là bao nhiêu?"**. Đây là lúc sinh ra vua của Data Analytics SQL: `GROUP BY`.

### Mệnh đề GROUP BY
Nó tạo ra mảng các "Hộp/thùng nhóm" (Buckets) khác biệt nhau (phòng IT, phòng HR...). Sau đó nó bỏ mọi báo cáo Aggregate (cộng trừ nhân chia) vào độc lập từng rổ nhóm.

```sql
SELECT 
    department_id,
    COUNT(emp_id) AS number_of_staffs,
    AVG(salary) AS avg_dept_salary
FROM employees
GROUP BY department_id
ORDER BY avg_dept_salary DESC;
```
> [!IMPORTANT]
> **Quy tắc Thép của GROUP BY:** Bất kì thuộc tính cột nào được viết lòi ra ở phía sau lệnh `SELECT` (mà không bị bọc bởi một hàm Aggregate như SUM/COUNT) **BẮT BUỘC** bạn phải liệt kê đích danh nó ở trong mệnh đề `GROUP BY`. Nếu không bộ xử lý máy tính sẽ báo lỗi đỏ vì không hiểu cách chia nhóm.

### Điều kiện Nhóm (Mệnh đề HAVING)
Mọi người hay nhầm `HAVING` và `WHERE`. 
- `WHERE`: Bạn cầm rây lọc Lọc dòng dữ liệu thô **TRƯỚC KHI** đem chúng gom tụ nhóm lại. Không được phép đặt `SUM()`, `COUNT()` vào trong `WHERE`.
- `HAVING`: Bạn dùng màng lọc chặn rào dữ liệu **SAU KHI** chúng đã được nhồi nhét xử lý vào nhóm. Được quyền kiểm tra hàm Aggregate ở bước duyệt cuối.

Ví dụ: Báo cáo cho tôi biết những **Phòng ban** nào có **sĩ quân vượt quá 10 người**.

```sql
SELECT 
    department_id,
    COUNT(emp_id) AS total_staff
FROM employees
WHERE status = 'Active'         -- Bước 1: Lọc bỏ người nghỉ việc (Row-level)
GROUP BY department_id          -- Bước 2: Chia đống data thành các cụm Phòng Ban
HAVING COUNT(emp_id) > 10       -- Bước 3: Đập bỏ nhóm nào lưa thưa dưới 10 người ra khỏi rổ (Group-level)
ORDER BY total_staff DESC;      -- Bước 4: Sắp xếp
```
Thứ tự não bộ hệ thống Database tuân thủ trình tự xử lý (Order of Execution): `FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY -> LIMIT`. Lắm lúc não bộ của Data Engineer hiểu sai luật này đẫn đến chọc câu SQL báo lỗi tung tóe!


---

<!-- Gộp nội dung từ: joins-subqueries.md -->
# Concept: Joins Mastery & Subqueries

Sau khi cắt xẻ dữ liệu để thỏa mãn chuẩn hóa 3NF, chúng ta cần một siêu quyền lực để chắp và "khâu" chúng lại trong những bản báo cáo. Khả năng làm chủ **Tiên đề Lắp ráp (JOIN)** và **Truy vấn lồng (Subquery)** đánh dấu ranh giới giữa một học viên nhập môn và một SQL Developer cứng cựa. 

## 1. Bộ công cụ Joins Mastery

`JOIN` là phép toán liên kết các cột ngang hàng từ một hay nhiều bảng dựa trên các giá trị tương đồng (thường là sự đối sánh giữa Khóa chính PK và Khóa ngoại FK).

### 1.1 INNER JOIN (Giao nhau)
Lấy về những bản ghi thỏa mãn điệu kiện khớp 100% ở CẢ HAI bảng. Giống như phép Giao mảng lõi.
```sql
SELECT s.first_name, c.course_name
FROM students s
INNER JOIN enrollments e ON s.student_id = e.student_id
INNER JOIN courses c ON e.course_id = c.course_id;
-- Chỉ những sinh viên có đi đăng ký học mới xuất hiện. SV nợ môn hoặc chưa đăng ký sẽ tàng hình.
```
*(Ghi chú: Ta thường dùng bí danh - alias `s`, `e`, `c` để rút gọn câu lệnh đục khoét sâu).*

### 1.2 OUTER JOINS (LEFT, RIGHT, FULL)
Dùng để gộp bảng mà **vẫn giữ lại nhứng dòng không thể ghép cặp** (unmatched rows). Nơi nào bên kia không có dữ liệu đối chiếu thì thay thế bằng `NULL`.

- **LEFT JOIN:** Lấy 100% dữ liệu từ Bảng Trái (Bảng đặt ngay sau chỉ dẫn `FROM`), kể cả khi nó vắng bóng ở Bảng Phải. 
```sql
-- Xem tất cả sinh viên, kế bên là mã môn học đăng ký. 
-- Nếu sinh viên đó lười biếng chưa đăng ký môn nào, ta vẫn muốn thấy tên họ với mã môn là NULL
SELECT s.first_name, e.course_id
FROM students s
LEFT JOIN enrollments e ON s.student_id = e.student_id;
```
- **RIGHT JOIN:** Ngược lại với LEFT JOIN. (Ít thấy trong thực tế do người ta thường đảo `FROM` và xài LEFT JOIN cho thuận chiều tư duy từ trái qua).
- **FULL OUTER JOIN:** Bê 100% dữ liệu cả bên trái lẫn bên phải lên mâm, khớp được thì ghép, không khớp thì rải `NULL` về hai phía. Dùng khi đối chiếu/Kiểm toán kho (Reconciliation).

### 1.3 CROSS JOIN (Tích Đề-Các)
Không cần điều kiện `ON`. Nó bê mỗi một dòng bên Bảng A ghép với TOÀN BỘ dòng bên Bảng B. Kết quả là 1 tổ hợp bùng nổ `Row(A) * Row(B)`. Gần như chả ai xài trừ phi làm Data Mockup hoặc cần trải ma trận.

### 1.4 SELF JOIN (Tự kỷ)
Join một bảng với chính CÁI BẢNG ĐÓ. Rất vi diệu dành cho kiểu cấu trúc Nhân viên - Quản lý nằm chung 1 Table.
```sql
SELECT 
    emp.name AS Employee_Name, 
    mgr.name AS Manager_Name
FROM employees emp
LEFT JOIN employees mgr 
    ON emp.manager_id = mgr.id; -- So sánh mã quản lý của em này với mã ID của nhân viên khác trong cùng bảng
```

---

## 2. Truy vấn Lồng (Subqueries)

Sẽ có thứ tự yêu cầu logic móc nối gối đầu nhau, bắt buộc bạn phải lấy mảng kết quả của Bước 1 đem làm Input (đầu vào) nhét thẳng vào làm tham số lọc của Bước 2. Đó gọi là Truy vấn lồng (Subqueries). Subquery bọc trong dấu ngoặc tròn `()`.

### 2.1 Nested/Uncorrelated Subqueries (Dạng độc lập hoàn toàn)
Lệnh con chạy hoàn tất xong độc lập trước từ lõi, cho ra MỘT giá trị hay Một list hằng số, ném lên cho lệnh mẹ ở ngoài ăn. Lệnh mẹ chả cần biết lệnh con đã cực khổ lọc ra kiểu gì.

*Tuyệt chiêu: Lấy ra những sinh viên có tuổi đời cao tuổi hơn độ tuổi Trung bình toàn trường:*
```sql
SELECT first_name, age 
FROM students
WHERE age > (
    SELECT AVG(age) FROM students  -- Câu lệnh Subquery trả ra 1 số thực duy nhất (Ví dụ 21.5).
);
```

*Tuyệt chiêu: Dùng với toán tử `IN` (Subquery trả ra nguyên 1 cái cột Array List):*
```sql
SELECT first_name
FROM students
WHERE dept_id IN (
    SELECT dept_id FROM departments WHERE location = 'Building A'
);
```

### 2.2 Correlated Subqueries (Phụ thuộc rễ đan xen - Nặng nề bậc nhất)
Lỗi sợ của mọi cơ sở dữ liệu. Mệnh đề truy vấn lệnh Con bên trong lại phải vay mượn/chọt tham chiếu một cột từ mệnh đề lệnh Mẹ bên ngoài. 
Nguyên tắc hoạt động của nó: Lệnh mẹ cứ quét mỗi một Row, thì lệnh Con bên trong bụng bị lôi ra dập chạy (Execute) toàn bộ chu trình 1 lượt. Mẹ quét 1 triệu dòng thì Con chạy 1 triệu lần. Tốc độ cực thảm họa.

*VD: Lấy ra những nhân viên nào có lương cao hơn lương trung bình CỦA CHÍNH phòng ban người đó đang làm.*
```sql
SELECT e1.first_name, e1.salary, e1.dept_id
FROM employees e1
WHERE e1.salary > (
    -- Đây là Correlated Subquery vì nó chui ra ngoài lấy cái dept_id của hàng e1 chèn vào WHERE bên trong
    SELECT AVG(salary) 
    FROM employees e2
    WHERE e2.dept_id = e1.dept_id
);
```
> [!TIP]
> **Performance Tip:** Khi đối mặt với thuật toán Correlated Subqueries, các Data Engineer đẳng cấp thường đập đi xây lại bằng cách biến nó thành các hàm `JOIN` hoặc dùng **Window Functions** (`OVER (PARTITION BY ...)`). Hãy hạn chế xài Correlated Subquery tối đa.


---

<!-- Gộp nội dung từ: transactions-security.md -->
# Concept: Transactions (ACID) & Security (DCL)

Trong một dự án nhỏ ở Đại học, việc ghi lỡ thiếu hay gõ nhầm vài dòng dữ liệu thì không thành vấn đề. Thế nhưng, trong hệ thống Ngân hàng (Ví dụ: Chuyển khoản trừ tiền 1 bên rồi, đang cộng tiền sang bên kia mà tự nhiên... máy chủ cúp điện đột ngột), hậu quả sẽ là thảm họa sai lệch hàng tỷ tỷ đồng!
Đây là lúc chúng ta phải nắm chặt sức mạnh gác cổng khổng lồ đằng sau của RDBMS: **Transactions** & **Access Control**.

## 1. Bản chất của Transaction (Giao dịch)

Một Transaction (Giao dịch) không phải là 1 lệnh SQL. Nó là **một chùm/một chuỗi (sequence)** gồm một hoặc rất nhiều các câu lệnh SQL nhỏ gộp lại để tạo thành **MỘT (1) đơn vị logic duy nhất (A Single Logical Unit of Work)**.

Nguyên tắc chốt hạ của Transaction: RDBMS đảm bảo rằng toàn bộ chuỗi lệnh này phải thành công viên mãn tất cả (All), hoặc thất bại sụp đổ toàn bộ, ném data về trạng thái cũ như chưa có gì xảy ra (Nothing). Tuyệt đối không có chuyện dở dang nửa chừng.

### Kiểm soát Giao dịch với ngôn ngữ TCL (Transaction Control Language)
1. Bắt đầu: Mở cờ lệnh `BEGIN` hoặc `START TRANSACTION;`
2. Viết hàng mớ code `INSERT`, `UPDATE`, `DELETE` (Lúc này data mới chỉ tạm thay đổi trong Cache RAM rỗng, thế giới thực bên ngoài bảng chưa thấy).
3. Ra lệnh phán quyết cuối cùng:
   - `COMMIT;` (Ấn định vĩnh viễn, lưu mạnh mẽ vào ổ cứng dính chết rễ. Đã Commit là không hối hận quay đầu).
   - `ROLLBACK;` (Thôi dẹp đi, bỏ hết mọi thay đổi từ nãy giờ, reload data lúc trước BEGIN).
4. `SAVEPOINT name;` Tạo điểm cắm cờ checkpoint nhỏ bên trong một cái Transaction quá bự. Để nếu lỗi chỉ Back lại điểm này (Rollback to) thay vì quay đi gõ cả cõi từ đầu.

```sql
BEGIN;

UPDATE accounts SET balance = balance - 1000 WHERE id = 'A';
UPDATE accounts SET balance = balance + 1000 WHERE id = 'B';

-- Kiểm tra xem số dư tài khoản A có bị âm không?
-- Nếu âm -> ROLLBACK; (Sợ sai)
-- Nếu đủ tiền -> COMMIT; (Kết sổ ngon lành)
```

## 2. Tính chất ACID siêu phòng thủ

Để được vinh danh là hệ thống an toàn ở cấp Enterprise, mọi RDBMS (như PostgreSQL, Oracle) đều phải vượt qua bài kiểm tra đáp ứng trọn vẹn 4 tiêu chuẩn thép gọi là **ACID**:

- **[A]tomicity (Tính nguyên tử):** Đặc tính "All or Nothing". Chuỗi hạt Transaction không thể chẻ tách làm hai nửa. Hoặc lệnh chạy trọn vẹn, hoặc chẳng có lệnh nào trong cục gộp đó được chạy. Lỡ có 1 SQL bị Crash, toàn bộ cục đó hủy diệt theo (Rollback hoàn toàn).
- **[C]onsistency (Tính nhất quán):** Database lúc trước khi tiến hành giao dịch đang tuân tủ Constraints đúng chuẩn mực. Giao dịch xong, DB vẫn ở trạng thái hoàn hảo 100% tuân thủ toàn bộ Constraints, Foreign Keys, rào cản CHECK. Nếu Data nhập nhằng xé rào, cự tuyệt ngay lập tức (Trigger Rollback).
- **[I]solation (Tính cô lập):** Rất nhiều Users ở ngoài đời có thể lao vào sửa cùng 1 cái Database tại 1 mili-giây. Isolation đảm bảo các chùm Transaction của anh A chạy hoàn toàn cách ly, không nhìn thấy "Dữ liệu đang sửa lỡ dở" của bộ hồ sơ chị B đang làm mà chưa COMMIT. Tránh hiện tượng Đọc bùn dơ (Dirty Read).
- **[D]urability (Tính bền bỉ):** Tính kháng bom. Một khi Transaction đã được gõ mộc báo cáo thành công (COMMIT), dữ liệu đó phải được tạc vào ổ cứng HDD vĩnh viễn không bao giờ hoại diệt, bất chấp ngay giây tiếp theo cơ sở dữ liệu bị rút điện, sập Server, hay nổ cầu gãy nhánh mạng. Khi Server bật lại lên, Data vẫn còn nguyên vẹn ở đó (hệ lưu log đền nền phục hồi).

## 3. Mạng lưới Phân quyền Bảo mật (DCL - Data Control Language)

Là một Database Admin, bạn không đời nào giao password `postgres` root quyền hành tối cao cho đám Junior Developer của Team Website chọc ngoáy vào DB. Rửa tay dơ trên máy tính khác là chém chết hệ thống. Bạn cần tạo User/Role và ghim giấy rào chặn cấm cung họ bằng **DCL (Data Control Language)**.

DCL sinh ra để cấp hay thu hồi vũ khí (chiếu chỉ, quyền lực phép):

### 3.1 Cấp Mộc (GRANT)
Giúp chia quyền (Privilege) cho tài khoản/User hay 1 Role group.

```sql
-- Chỉ cho xài lệnh lôi 데이터 lên nhìn, KHÔNG cho đụng dao kéo gạch đá sờ vào (Read-Only)
GRANT SELECT ON employees TO readonly_user;

-- Cho phép cả Sửa, Thêm, Nhìn chỉ trên đúng 1 bảng nhất định
GRANT SELECT, INSERT, UPDATE ON departments TO content_developer;

-- Set full toàn quyền trên toàn bộ cục Database (Admin cấp cao)
GRANT ALL PRIVILEGES ON DATABASE university_db TO super_dba;
```

### 3.2 Tước Quyền (REVOKE)
Thu lại đặc ân đã phát, dĩ nhiên chém đi khả năng truy sát dữ liệu nhạy cảm mà hôm qua ta cho lỡ tay.
```sql
-- Cấm User này k đc phép Thêm và Cập nhật bảng
REVOKE INSERT, UPDATE ON departments FROM content_developer;

-- Cút luôn, tịch thu hết
REVOKE ALL PRIVILEGES ON employees FROM readonly_user;
```

Việc am hiểu TCL đảm bảo dữ liệu chạy đúng quy chuẩn không méo mó, còn thấu đáo DCL bảo vệ vững trãi hệ thống khỏi bàn tay tò mò hay những query tai hại của kẻ cắp giấu mặt.


---


# Concept: Phân tích Dữ liệu Chuyên sâu với SQL (Data Analysis Focus)

*(Được truyền cảm hứng từ Series SQL From Zero to Hero - Phù hợp cho Data Analysts và Data Engineers).*

Khi làm việc thực tế với dữ liệu, bạn sẽ không dừng lại ở Joins và Group By. Bạn cần làm chủ những tính năng cực thâm hậu của SQL: **CTE (Bảng tạm chung)** và **Window Functions (Hàm cửa sổ)**.

## 1. Mệnh đề `WITH` hay còn gọi là CTE (Common Table Expressions)

Subquery kẹp trong lệnh mẹ rất khó đọc (spaghetti code). Thay vì thế, CTE giúp ta nhúng câu truy vấn lồng vào một "Biến bảng tạm" cực kỳ gọn gàng nằm ở đầu file, trước khi thực hiện câu lện chính.

**Cú pháp:**
```sql
WITH HighestSalaryCTE AS (
    SELECT dept_id, MAX(salary) AS max_salary 
    FROM employees 
    GROUP BY dept_id
)
SELECT e.first_name, e.salary, c.max_salary
FROM employees e
JOIN HighestSalaryCTE c ON e.dept_id = c.dept_id
WHERE e.salary = c.max_salary;
```

**Ưu điểm của CTE so với Subquery:**
- Dễ đọc như một cuốn sách (từ trên xuống dưới).
- Tái sử dụng được nhiều lần trong cùng 1 câu Select Mother ở dưới. Gõ 1 lần xài được N lần thay vì paste đoạn subquery liên tục.
- Hỗ trợ RECURSIVE (Gọi đệ quy) để vẽ vòng lặp quản trị nhân sự (Sếp -> Nhân viên -> Cháu nhánh).

## 2. Window Functions (Hàm Cứa Sổ Tuyệt Kỹ)

Nếu `GROUP BY` đập bẹp đống dữ liệu của bạn, gom các hàng trùng lại thành 1 rổ (giữ 1 kết quả báo cáo duy nhất). Thì **Window Function** có khả năng chèn một cái "Cửa sổ trượt" (Window) mang sức mạnh tính toán Lướt qua từng hàng mà **KHÔNG HỀ LÀM BIẾN MẤT SỐ DÒNG HIỆN CÓ CỦA BẠN**.

*Ví dụ kinh điển: Tính cột Rank Xếp Hạng hoặc Doanh thu luỹ kế Running Total.*

**Cú pháp:**
```sql
SELECT 
    emp_name, 
    department, 
    salary,
    -- Điểm nhấn: Hàm Window Function
    RANK() OVER (PARTITION BY department ORDER BY salary DESC) as rank_in_dept,
    SUM(salary) OVER(PARTITION BY department) as total_dept_salary
FROM employees;
```

**Bộ phận tạo nên sự sống của Window Function:**
- Lệnh `OVER()`: Kích hoạt màng bọc Window Function thay vì Aggregate binh thường.
- Lệnh `PARTITION BY`: Nén cửa sổ trượt lại trong khuôn khổ nhóm (Giống Group By nhưng k xoá bớt dòng), ví dụ "bộ đếm chỉ trượt tính nhẩm trong vòng phòng IT, nhảy sang phòng HR thì bộ đếm reset về 0".
- Lệnh `ORDER BY`: Xác định con chuột cửa sổ cuộn từ trên xuống dưới theo thứ tự lương DESC (Đứa lương top 1 đếm trước).

**Các hàm Cửa sổ đắt giá của phân tích Dữ liệu:**
- `ROW_NUMBER()`: Đánh số thứ tự 1,2,3,4 bất chấp bạn có giá trị trùng lặp.
- `RANK()` và `DENSE_RANK()`: Đánh số xếp hạng cuộc thi. Nếu 2 người đồng hạng Lương như nhau, cả hai đứng hạng 1. Khác nhau ở chỗ (Người tiếp theo hạng 3 đối với Rank, và hạng 2 ở Dense Rank).
- `LEAD()` và `LAG()`: Nhòm sang tương lai dòng phía dưới hoặc Móc lấy giá trị của dòng ở quá khứ dán vào ngay bên cạnh dòng hiện tại. Siêu việt trong báo cáo Phân tích Trượt doanh số Sales tháng Này với Tháng Trước (MoM).
