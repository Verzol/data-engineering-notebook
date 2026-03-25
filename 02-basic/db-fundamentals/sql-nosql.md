# SQL & NoSQL Fundamentals

## SQL (Structured Query Language)

SQL là ngôn ngữ tiêu chuẩn được sử dụng để tương tác, quản lý và truy vấn dữ liệu từ cơ sở dữ liệu quan hệ (Relational Database Management System - RDBMS). SQL hỗ trợ các hoạt động CRUD (Create, Read, Update, Delete) và được hỗ trợ rộng rãi trên nhiều hệ thống CSDL khác nhau như MySQL, Oracle, PostgreSQL, SQL Server, MariaDB, và các hệ thống khác. SQL primary hoạt động với dữ liệu được sắp xếp theo cấu trúc bảng (table-structured data) trong cơ sở dữ liệu quan hệ.

![alt text](how-sql-works.png)

### 1. Một vài thao tác đặc trưng trong SQL.

![alt text](basic-operation.png)

### 2. Các bước chi tiết liên quan đến truy vấn SQL

Quy trình xử lý một truy vấn SQL diễn ra theo các bước sau:

- **Input (Tiếp nhận)**: Người dùng gửi truy vấn SQL (SELECT, INSERT, UPDATE, DELETE, v.v.).
- **Phân tích cú pháp (Parsing)**: Hệ thống kiểm tra xem truy vấn có tuân theo cấu trúc cú pháp SQL chính xác hay không.
- **Xác thực ngữ cảnh (Validation)**: Kiểm tra sự tồn tại của các bảng, cột và các quyền truy cập của người dùng.
- **Tối ưu hóa (Optimization)**: Query Optimizer phân tích các cách khác nhau để thực hiện truy vấn và chọn ra kế hoạch thực hiện hiệu quả nhất.
- **Biên dịch (Compilation)**: Chuyển đổi truy vấn đã tối ưu thành mã máy.
- **Thực thi (Execution)**: CSDL chạy truy vấn theo kế hoạch thực hiện đã được chọn.
- **Đầu ra (Output)**: Kết quả hoặc xác nhận gửi lại cho người dùng.

### 3. Quy tắc viết truy vấn SQL

**Cú pháp cơ bản:**

- **Dấu chấm phẩy ";"**: Kết thúc một câu lệnh SQL.
- **Không phân biệt chữ hoa chữ thường**: Các từ khóa SQL như SELECT, INSERT, UPDATE, DELETE không phân biệt chữ hoa hay chữ thường, tuy nhiên thường được viết in hoa để dễ nhận diện.
- **Khoảng trắng**: Khoảng trắng và dòng mới được phép để tăng tính dễ đọc của mã.
- **Bình luận (Comment)**:
  - Một dòng: `-- comment`
  - Nhiều dòng: `/* comment */`

**Định danh (Identifiers - Tên đối tượng):**

- Bắt đầu bằng một chữ cái (A-Z, a-z)
- Chứa chữ cái, số (0-9) hoặc dấu gạch dưới (\_)
- Độ dài tối đa tùy thuộc vào từng CSDL (thường từ 64 đến 300 ký tự)
- Để sử dụng từ khóa SQL làm tên đối tượng, phải đặt trong dấu ngoặc kép hoặc backtick: `SELECT`, `"user"`, `table`

**Giá trị dữ liệu:**

- **Chuỗi ký tự (String)**: Đặt trong dấu ngoặc kép đơn: `'Hello World'`
- **Số (Number)**: Không cần dấu ngoặc: `123`, `45.67`
- **NULL**: Biểu thị giá trị không tồn tại

**Ràng buộc (Constraints):**

- Sử dụng các ràng buộc như `NOT NULL`, `UNIQUE`, `PRIMARY KEY`, `FOREIGN KEY`, `CHECK` để đảm bảo tính toàn vẹn và nhất quán của dữ liệu.

### 4. Các lệnh truy vấn SQL

Các lệnh SQL được phân loại thành năm danh mục chính dựa trên chức năng cụ thể của chúng. Mỗi danh mục có những lệnh riêng để quản lý, truy vấn, và bảo vệ dữ liệu trong cơ sở dữ liệu:

![alt text](sql-commands.png)

**1. Data Definition Language (DDL)**

DDL bao gồm các lệnh được sử dụng để định nghĩa, tạo, thay đổi hoặc xóa cấu trúc của các đối tượng trong cơ sở dữ liệu (bảng, view, index, schema, v.v.).

| Command  | Description                                                                        |
| :------: | :--------------------------------------------------------------------------------- |
|  CREATE  | Tạo các đối tượng CSDL mới như bảng, view, index, schema, hoặc stored procedure.   |
|  ALTER   | Sửa đổi cấu trúc của các đối tượng có sẵn (thêm/xóa cột, thay đổi kiểu dữ liệu).   |
|   DROP   | Xóa hoàn toàn một đối tượng CSDL (bảng, view, index) cùng dữ liệu của nó.          |
| TRUNCATE | Xóa toàn bộ dữ liệu từ một bảng nhưng giữ nguyên cấu trúc bảng (nhanh hơn DELETE). |
|  RENAME  | Đổi tên cho một đối tượng CSDL (bảng, cột, view).                                  |

**2. Data Manipulation Language (DML)**

DML bao gồm các lệnh được sử dụng để thêm, cập nhật, xóa, và truy xuất dữ liệu từ các bảng trong cơ sở dữ liệu quan hệ.

| Command | Description                                                              |
| :-----: | :----------------------------------------------------------------------- |
| INSERT  | Thêm một hoặc nhiều bản ghi mới vào bảng.                                |
| UPDATE  | Cập nhật giá trị của một hoặc nhiều cột trong bản ghi hiện có.           |
| DELETE  | Xóa một hoặc nhiều bản ghi từ bảng dựa trên điều kiện WHERE.             |
| SELECT  | Truy vấn và lấy dữ liệu từ một hoặc nhiều bảng (có thể được coi là DQL). |

**3. Data Query Language (DQL)**

DQL là một thành phần của SQL tập trung vào việc truy xuất dữ liệu từ cơ sở dữ liệu bằng lệnh **SELECT**. DQL cho phép người dùng chỉ định chính xác dữ liệu nào cần lấy, từ bảng nào, và dữ liệu đó sẽ được lọc, sắp xếp, và nhóm như thế nào.

**Đặc điểm chính:**

- **Truy vấn dữ liệu**: DQL được sử dụng độc quyền để truy xuất dữ liệu, không thay đổi nội dung CSDL.
- **Điều kiện lọc**: Sử dụng mệnh đề `WHERE` để áp dụng các điều kiện cụ thể khi truy vấn.
- **Sắp xếp và nhóm**: Sử dụng `ORDER BY`, `GROUP BY` để sắp xếp và nhóm kết quả.
- **Toán tử quan hệ**: Hỗ trợ các toán tử so sánh (=, <>, <, >, <=, >=), logic (AND, OR, NOT), v.v.

**Ví dụ cơ bản:**

```SQL
-- Truy vấn tất cả bản ghi từ bảng employee
SELECT * FROM employee;

-- Truy vấn các cột cụ thể với điều kiện
SELECT emp_name, emp_salary FROM employee WHERE emp_salary > 5000;

-- Truy vấn với sắp xếp
SELECT * FROM employee ORDER BY emp_salary DESC;
```

Dấu `*` trong SELECT cho biết rằng tất cả các cột được truy vấn từ bảng.

**4. Data Control Language (DCL)**

DCL bao gồm các lệnh được sử dụng để quản lý quyền truy cập của người dùng đối với các đối tượng CSDL. DCL đảm bảo an toàn và bảo mật dữ liệu bằng cách kiểm soát ai có thể làm gì với dữ liệu.

| Command | Description                                                      |
| :-----: | :--------------------------------------------------------------- |
|  GRANT  | Cấp quyền (SELECT, INSERT, UPDATE, DELETE, v.v.) cho người dùng. |
| REVOKE  | Thu hồi quyền đã cấp từ người dùng.                              |

**Ví dụ:**

```sql
GRANT SELECT, INSERT ON table_name TO user_name;
REVOKE DELETE ON table_name FROM user_name;
```

**5. Transaction Control Language (TCL)**

TCL bao gồm các lệnh được sử dụng để quản lý các transaction trong CSDL quan hệ. Transaction là một chuỗi các hoạt động (một hoặc nhiều lệnh SQL) được thực hiện như một đơn vị logic duy nhất, tuân theo nguyên tắc ACID (Atomicity, Consistency, Isolation, Durability) để đảm bảo tính toàn vẹn và nhất quán của dữ liệu.

|  Command  | Description                                                                                          |
| :-------: | :--------------------------------------------------------------------------------------------------- |
|  COMMIT   | Xác nhận và lưu vĩnh viễn tất cả những thay đổi trong transaction hiện tại.                          |
| ROLLBACK  | Hủy bỏ tất cả những thay đổi trong transaction hiện tại và khôi phục dữ liệu về trạng thái trước đó. |
| SAVEPOINT | Tạo một điểm lưu giữa trong transaction để có thể rollback về điểm đó mà không ảnh hưởng toàn bộ.    |

**Ví dụ:**

```sql
BEGIN TRANSACTION;
    INSERT INTO account VALUES (1, 'John', 1000);
    UPDATE account SET balance = balance - 500 WHERE id = 1;
    SAVEPOINT sp1;
    UPDATE account SET balance = balance + 500 WHERE id = 2;
COMMIT;  -- Lưu tất cả thay đổi

-- Nếu có lỗi
ROLLBACK TO SAVEPOINT sp1;  -- Quay lại điểm sp1
ROLLBACK;  -- Quay lại trước khi BEGIN
```

### 5. Ưu điểm và nhược điểm của SQL

**a. Ưu điểm**

- **Hiệu suất cao**: SQL được tối ưu hóa tốt cho các truy vấn phức tạp trên dữ liệu có cấu trúc.
- **Tính khả dụng rộng**: Được hỗ trợ trên hầu hết các hệ thống RDBMS, giúp dễ dàng chuyển đổi giữa các nền tảng khác nhau.
- **Tính mở rộng**: SQL có thể làm việc hiệu quả từ dữ liệu nhỏ đến dữ liệu rất lớn (Big Data).
- **Hỗ trợ xử lý logic phức tạp**: Có các tiện ích mở rộng như PL/SQL (Oracle), T-SQL (SQL Server), PL/pgSQL (PostgreSQL) để viết các logic phức tạp.
- **Tính toàn vẹn dữ liệu**: Ràng buộc (constraints), transactions, và khóa (locking) đảm bảo dữ liệu luôn nhất quán.

**b. Nhược điểm**

- **Cấu trúc cứng nhắc**: Dữ liệu phải tuân thủ lược đồ (schema) được định sẵn, khó thích nghi với các thay đổi.
- **Không phù hợp với dữ liệu phi cấu trúc**: SQL không tối ưu cho dữ liệu không có cấu trúc hoặc bán cấu trúc (hình ảnh, video, tài liệu JSON).
- **Độ trễ xử lý**: Các hoạt động phức tạp như tối ưu hóa và xác thực có thể tạo độ trễ.
- **Khó mở rộng theo chiều ngang (Horizontal Scaling)**: Các RDBMS truyền thống khó chia sẻ dữ liệu trên nhiều máy chủ.
- **Không hỗ trợ Real-time Analytics tốt**: SQL truyền thống không được thiết kế cho phân tích dữ liệu thời gian thực với khối lượng dữ liệu cực lớn.

### 6. Ứng dụng của SQL

SQL được sử dụng rộng rãi trong nhiều lĩnh vực khác nhau:

- **Data Analytics (Phân tích dữ liệu)**: Truy vấn, phân tích, và báo cáo dữ liệu lớn từ nhiều nguồn khác nhau.
- **E-Commerce (Thương mại điện tử)**: Quản lý hồ sơ khách hàng, danh mục sản phẩm, đơn hàng, thanh toán, và hàng tồn kho.
- **Backend Development (Phát triển Backend)**: Lưu trữ và quản lý dữ liệu ứng dụng web, API, và các dịch vụ.
- **Business Intelligence (Thông tin kinh doanh)**: Tạo báo cáo, dashboard, và insight từ dữ liệu kinh doanh.
- **Finance (Tài chính)**: Quản lý tài khoản, giao dịch, phân tích lịch sử tài chính, báo cáo thuế, và kiểm soán rủi ro.
- **Healthcare (Sức khỏe)**: Quản lý hồ sơ bệnh án điện tử (EHR), lịch hẹn, kết quả xét nghiệm, và lịch sử điều trị.

## Tài liệu tham khảo

- GeeksforGeeks. (2024). _What is SQL?_ Truy cập từ https://www.geeksforgeeks.org/sql/what-is-sql/
