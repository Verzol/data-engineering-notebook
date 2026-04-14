<!-- Gộp nội dung từ: quiz-01-db-concepts.md -->
# Quiz 01: Database Concepts & Design

**Thời gian:** 30 phút
**Số lượng:** 20 câu hỏi Trắc nghiệm (Multiple Choice Questions)

Đây là bài kiểm tra lý thuyết trắc nghiệm nhằm đánh giá sự thấu hiểu của bạn về Kiến trúc Cơ sở Dữ liệu, Mô hình ERD và các mức Chuẩn hóa Dữ liệu (Normalization). Hãy chọn ĐÁP ÁN ĐÚNG NHẤT cho mỗi câu hỏi.

---

1. **RDBMS đứng viết tắt cho từ gì?**
   A. Relational Data Backup Management System
   B. Relational Database Management System
   C. Regional Database Manipulation System
   D. Real-time Database Management System

2. **Dữ liệu nào sau đây được xem là "Dữ liệu phi cấu trúc" (Unstructured Data)?**
   A. Dữ liệu bảng tài chính lưu trên Excel.
   B. Cấu trúc tổ chức Bảng Nhân viên trong Hệ thống Postgres.
   C. File video `.mp4`, hình ảnh, và nội dung dòng trạng thái trên Facebook.
   D. Dữ liệu thời tiết lấy qua định dạng JSON.

3. **Mô hình kiến trúc Dữ liệu Quan hệ (Relational Model) tổ chức dữ liệu chủ yếu dưới hình thức nào?**
   A. Biểu đồ cây phân cấp (Tree structure).
   B. Các node mạng lưới phức hợp (Graph structure).
   C. Các bảng 2 chiều gồm Cột và Hàng (Tables).
   D. Cặp Key-Value dưới dạng văn bản (JSON).

4. **Đâu Nằm trong hệ lý thuyết CAP Theorem của cơ sở dữ liệu phân tán?**
   A. Consistency, Availability, Partition Tolerance
   B. Capability, Availability, Performance
   C. Consistency, Accuracy, Partition Tolerance
   D. Cloud, Automation, Portability

5. **Trong ngữ cảnh RDBMS, Khóa chính (Primary Key) có hai ràng buộc bắt buộc nào?**
   A. Phải là Số nguyên (Integer) và Tự động tăng.
   B. Được phép NULL, nhưng các giá trị khác phải KHÔNG lặp lại (UNIQUE).
   C. KHÔNG được phép NULL (NOT NULL) và Giá trị KHÔNG được lặp lại (UNIQUE).
   D. Là một cột Text duy nhất.

6. **Đâu là chức năng chính yếu của Khóa ngoại (Foreign Key)?**
   A. Giúp cho câu lệnh SELECT chạy nhanh hơn.
   B. Giải cứu bộ nhớ ổ cứng máy chủ lưu trữ.
   C. Tạo và bảo toàn tính toàn vẹn sự liên kết tham chiếu (Referential Integrity) giữa hai bảng.
   D. Tăng tính bảo mật mã hóa cho Dữ liệu nhạy cảm của Cột.

7. **Bảng A và B có mối quan hệ N:M (Nhiều - Nhiều). Cách tiêu chuẩn tốt nhất trong thiết kế để giải quyết mối quan hệ này là gì?**
   A. Cắm Foreign Key của bảng A vào bảng B.
   B. Gộp hai bảng lại thành 1 siêu bản.
   C. Nhồi một danh sách mảng dữ liệu (Array List) vào một trong hai bảng.
   D. Tạo ra một bảng trung gian (Junction table) chứa Khóa chính của bảng A và Khóa chính của bảng B.

8. **Trong quá trình thiết kế ERD, Mô hình nào chứa các thực thể chung chung, KHÔNG BẬN TÂM ĐẾN kiểu dữ liệu cột, rào cản và độc lập với Engine Database (MySQL hay PostgreSQL..)?**
   A. Physical Data Model
   B. Conceptual Data Model
   C. Logical Data Model
   D. DWH Data Model

9. **Dạng chuẩn số 1 (1NF) quy định hệ giá trị phải thỏa mãn điều kiện cốt lõi nào?**
   A. Dữ liệu các Cột phải lưu dưới dạng Văn bản thuần.
   B. Các cột không khóa phải phụ thuộc vào nhau.
   C. Mỗi Ô dữ liệu giao điểm Hàng-Cột chỉ lưu 1 trị nguyên thủy (Atomic value).
   D. Mỗi bảng phải có 2 Primary Keys.

10. **Bảng "Sản phẩm" chứa cột (Mã Loa, Tên Loa, Hãng Loa, Số điện thoại hỗ trợ của Hãng Loa). Bạn nhận thấy cột [Số điện thoại hãng] thay vì phụ thuộc vào Mã Loa, nó lại đi phụ thuộc gián tiếp qua cột [Hãng Loa]. Việc này chứng minh Bảng Sản phẩm đang VI PHẠM Dạng chuẩn nào?**
    A. Dạng Chuẩn 1NF
    B. Dạng Chuẩn 2NF
    C. Dạng Chuẩn 3NF
    D. Bảng chuẩn thiết kế hoàn hảo.

11. **Khi muốn thiết kế Data Warehouse cho truy xuất báo cáo (OLAP) chạy siêu tốc, người ta hay NGƯỢC LỐI đập bỏ sự chuẩn hóa, rải dữ liệu dư thừa vào một cục lớn. Nó được gọi là thuật ngữ?**
    A. Fragmentation
    B. Sharding
    C. Normalization
    D. Denormalization (Phi chuẩn hóa)

12. **Mô hình kiến trúc rất phổ biến trong Data Warehouse với 1 Bảng Sự thật (Fact Table) trồi lên ở giữa, và dăm ba Bảng Ngữ cảnh (Dimension Tables) bâu xung quanh, được gọi tên là gì?**
    A. Snow-flake Schema
    B. Star Schema (Lược đồ ánh sao)
    C. Galaxy Schema
    D. Cube Schema

13. **Tuples (trong toán học thiết kế Dữ liệu quan hệ) thực chất nhằm chỉ thuật ngữ Database nào ngoài thực tế?**
    A. Table
    B. Column / Field
    C. Row / Record
    D. Constraint

14. **SQL là ngôn ngữ Khai báo (Declarative Query Language), có nghĩa là gì?**
    A. Yêu cầu Lập trình viên thiết lập từng bước vòng lặp dòng (For loop) thì dữ liệu mới ra được.
    B. Yêu cầu Lập trình viên truyền đạt "KẾT QUẢ MÌNH MUỐN" bằng chỉ định mô tả, Database tự tìm giải thuật đem xôi về.
    C. Chỉ xài được trên Cloud Database.
    D. Dùng để làm Frontend Website giao diện người dùng.

15. **Toán tử lấy một Dòng dữ liệu của Table A đem gán đôi với toàn bộ Tất cả các Dòng của Table B (Tạo ra tích chéo Cartesian Product bùng nổ hàng triệu dòng hỏa mù) là loại kết nối Join nào?**
    A. LEFT JOIN
    B. INNER JOIN
    C. SELF JOIN
    D. CROSS JOIN

16. **Thuộc tính "Ngày sinh học sinh" được tính hợp lệ nếu lưu vào định dạng Date, thuộc mảng Kiến trúc nào trong RDBMS chịu trách nhiệm gác cổng?**
    A. Query Optimizer
    B. Domain Constraint (Miền Giá Trị Type)
    C. Transaction Manager
    D. File System

17. **Cột A không mang đặc quyền Primary Key, nhưng ban Thiết kế vẫn chỉ định cho nó là DUY NHẤT để tránh bị đụng hàng dữ liệu, Cột A lúc đó sẽ mang constraint gì?**
    A. UNIQUE
    B. DEFAULT
    C. CHECK
    D. IDENTITY

18. **Một RDBMS xử lý lệnh Query theo dòng chảy các khối nào?**
    A. Client -> Storage -> Parser -> Optimizer.
    B. Client -> Parser -> Query Optimizer -> Storage Engine -> Lấy xôi.
    C. Xử lý lưu điện -> Optimizer -> Storage Engine -> Client.
    D. DBM -> Optimizer -> API Rest.

19. **Bảng "Logs" chuyên chứa lưu vết nhật ký sự kiện có thể có đến tỷ bản ghi. Thuật ngữ miêu tả số lượng bản ghi/Hàng (Row count) của bảng này gọi là?**
    A. Bậc (Degree)
    B. Kích cỡ (Size bytes)
    C. Bản số (Cardinality)
    D. Lực dồn (Density)

20. **Trong DDL, để gỡ bỏ triết để một cột không sử dụng ra khỏi khuôn bảng "Users", ta dùng lệnh (cú pháp lõi) nào sau đây?**
    A. `DELETE Cột FROM Users`
    B. `REMOVE COLUMN Cột FROM Users`
    C. `ALTER TABLE Users DROP COLUMN Cột`
    D. `DE-ATTACH Cột FROM Users` 

---
**ĐÁP ÁN THAM KHẢO**
1. B | 2. C | 3. C | 4. A | 5. C | 6. C | 7. D | 8. C (hoặc B tuỳ độ trừu tượng, B đúng nhất cho mức cao nhất) | 9. C | 10. C | 11. D | 12. B | 13. C | 14. B | 15. D | 16. B | 17. A | 18. B | 19. C | 20. C


---

<!-- Gộp nội dung từ: quiz-02-transaction-access-control.md -->
# Quiz 02: Transaction & Access Control

**Thời gian:** 30 phút
**Số lượng:** 20 câu hỏi Trắc nghiệm (Multiple Choice Questions)

Bài kiểm tra xoay quanh hai nội hàm sức mạnh duy trì trật tự của RDBMS: Vòng đời dòng Giao dịch (Transactions & ACID) và Cấp quyền quản lý hệ thống (DCL Bảo mật). Chọn đáp án đúng nhất.

---

1. **Transaction (Giao dịch) trong cơ sở dữ liệu là gì?**
   A. Là một dòng lệnh SELECT đơn độc dùng để lấy dữ liệu.
   B. Là hành động Hacker ăn trộm dữ liệu hệ thống.
   C. Là chùm một chuỗi tác vụ tác động mặt dữ liệu gộp lại như một khối (Unit of work) phải chạy là trọn vẹn sống cùng tịnh, chết cùng chết.
   D. Là thao tác tải máy chủ Data lên đĩa Cloud.

2. **Dãy 4 hệ triết lý vĩ đại bảo vệ giao dịch doanh nghiệp, viết tắt là ACID, bao gồm các từ ngữ nào?**
   A. Accuracy, Completeness, Isolation, Database.
   B. Atomicity, Consistency, Isolation, Durability.
   C. Atomicity, Concurrent, Interface, Durable.
   D. Advanced, Control, Internal, Defense.

3. **Chữ "A" (Atomicity) trong ACID đảm bảo rào luật nào?**
   A. Đọc và Ghi tốc độ ánh sáng (nguyên tử).
   B. Khóa các thao tác User đang giành xé.
   C. All-or-Nothing (Cả cụm lệnh chạy thành công hoặc bị bóp nát hủy bỏ quay đầu toàn bộ nếu một lệnh con bị lỗi).
   D. Data bị xóa thì mãi mãi không thể khép lại.

4. **Trạng thái Database đột nhiên nổ cầu mạng sập vạch 100% khi vừa kịp bấm xác nhận gửi giao dịch. Khi mở máy chủ lại lên điện, con số giao dịch vừa nãy VẪN ĐƯỢC LƯU MÃI MÃI. Tính chất này thuộc chữ cái nào trong ACID?**
   A. Tính A
   B. Tính C
   C. Tính I
   D. Tính D (Durability - Bền bỉ) 

5. **Để mở đầu tạo dấu cắm một Vòng giao dịch Transaction trước khi xả lệnh sửa dữ liệu, ta dùng mệnh lệnh gì trong SQL?**
   A. `OPEN;`
   B. `START TRANSACTION;` (hoặc `BEGIN;`)
   C. `INIT;`
   D. `FIRE;`

6. **Giám đốc duyệt báo cáo sai và la hét bạn phải HỦY BỎ hết đống lệnh sửa Lương vừa mới gõ nãy lỡ sai số (Chưa kịp save cứng). Mệnh lệnh "Thuốc hối hận" này trong TCL SQL là gì?**
   A. `BACKUP;`
   B. `REVOKE;`
   C. `ROLLBACK;`
   D. `CTRL_Z;`

7. **Để "CHỐT ĐƠN" đóng ghim vĩnh viễn mảng đổi giao dịch đè lên Dữ liệu thật, bạn phải gõ Cú pháp gì chốt cửa sổ TCL?**
   A. `DONE;`
   B. `FINISH;`
   C. `END TRAN;`
   D. `COMMIT;`

8. **Trạng thái "Dirty Read" (Đọc Dữ liệu Bẩn) diễn ra khi:**
   A. Server bị bụi bấm hư HDD.
   B. Dữ liệu đang chứa quá nhiều kí tự rác đặc biệt bị SQL bóc phải.
   C. User A lấy và đọc phải cục dữ liệu mà User B đang tiến thành `UPDATE` dở dang chưa kịp `COMMIT`. Lỡ như User B Rollback thì User A mang rác về báo cáo CEO.
   D. SQL Query Optimizer bị nghẽn mạng quá thời gian.

9. **Mệnh lệnh tạo 1 Điểm Phục hồi nằm giữa chuỗi Transaction bự (Giống tựa game chọt Save game đi tiếp), để khi có lỗi thì Back lại đúng cái Ngã 3 này gọi là gì?**
   A. `CHECKPOINT`
   B. `SAVEPOINT`
   C. `RESTORE_TO`
   D. `RETURN_HERE`

10. **Ngôn ngữ Khởi động Lập quyền (Data Control Language - DCL) được thao tác trực diện bởi chức danh nào trong quy trình kỹ thuật Database nhất?**
    A. Frontend Designer
    B. Junior Data Entry (Người gõ liệu)
    C. DBA (Database Administrator)
    D. HR Manager

11. **Câu lệnh GRANT DCL có khả năng cấm cản quyền hành gì?**
    A. `GRANT` không cấm, ngược lại nó là Dấu mộc CẤP PHÁT đặc ân quyền xài DB cho User.
    B. `GRANT` xóa thẳng dữ liệu hệ thống vào chế độ an toàn.
    C. `GRANT` thu hẹp băng thông truy vấn CPU của Postgres.
    D. Cấm chui lủi đăng nhập.

12. **Mệnh lệnh DCL Cướp lại quyền (Tịch thu bùa phép) được gọi là?**
    A. `TAKE_BACK`
    B. `CANCELED`
    C. `REVOKE`
    D. `DROP_ROLE`

13. **Lệnh sau đây mang ý nghĩa ra sao? `GRANT SELECT, INSERT ON patients TO doctor_role;`**
    A. Xóa hết quyền sờ lên bảng patients của team Bác Sỹ.
    B. Cho phép nhóm `doctor_role` được đọc (view data) và thêm bệnh án mới (insert) vào Bảng `patients`.
    C. Bắt buộc doctor_role phải Select để rà xuất patients xong thì xóa rỗng tụi nó.
    D. Lỗi do không xài từ DCL hợp lệ.

14. **Giao dịch (Transaction) của bạn lướt qua mọi bức tường lửa Validation của các Constraints như Foreign Key, Check Rule mà không tì vết. Nó giữ vững sự trong sạch đó cho DB. Nó tuân thủ chữ gì trong ACID?**
    A. I (Isolation)
    B. C (Consistency)
    C. A (Atomicity)
    D. D (Durability)

15. **User Admin gõ `REVOKE ALL PRIVILEGES ON account FROM normal_user;` Hậu quả của anh bạn ráng mở bảng account là gì?**
    A. Bị báo Error `Permission Denied` đuổi khéo ngay lập tức.
    B. Được quyền Insert nhưng cấm cãi Delete.
    C. Tự động đúp bảng account ra cho anh xài tạm.
    D. Hủy luôn cả User ra khỏi Database log.

16. **Viết tắt TCL là gì?**
    A. Transparent Control Level
    B. Transaction Control Language
    C. Type Character Length
    D. Table Column Logic

17. **Cảnh giới Phân lập (Isolation Level) nào ở Postgres là Cảnh giới cao nhất và chặt chẽ khắt khe nhất dẫn tới Block mọi giao diện song song?**
    A. Read Uncommitted
    B. Read Committed
    C. Repeatable Read
    D. Serializable

18. **Mọi SQL Statement bạn gõ `INSERT` hay `UPDATE` ngày thường đều lén lút có 1 lớp cất nhắc Transaction âm thầm chạy bọc xung quanh nó (Tự bọc mộc chạy `BEGIN` rồi lập tức phán quyết `COMMIT`). Cơ chế đó gọi là gì?**
    A. Self-Commiting
    B. Auto-Commit
    C. Meta-Transaction
    D. Background Check

19. **Có khả năng `COMMIT` nhầm xong vẫn dùng `ROLLBACK` lộn ngược vòng chu trình giao dịch lại cứu rỗi Database được không?**
    A. Không bao giờ. Đã `COMMIT` là khắc lên đá rồi. Chỉ có tự gõ ngược dữ liệu SQL thủ công bằng `UPDATE` chạy bộ lại.
    B. Vẫn cứu được nếu là Admin DBA.
    C. Vẫn cứu bằng `ROLLBACK TO ROOT`.
    D. Không được vì `ROLLBACK` sẽ format lại máy hệ điều hành của bạn.

20. **Lệnh `GRANT SELECT(name, email) ON users TO dev_team;` phản ánh quyền hạn sâu cắm đến mức độ gì?**
    A. Phân quyền ở cấp Table-Level.
    B. Phân quyền đâm sâu ở cấp Cột (Column-Level Privilege) - Dev team chỉ xem rải rác đúng 2 cột mà k thể ngó vô cột password.
    C. Lệnh sai cú pháp.
    D. Phân quyền nguyên Database to lớn.

---
**ĐÁP ÁN THAM KHẢO**
1. C | 2. B | 3. C | 4. D | 5. B | 6. C | 7. D | 8. C | 9. B | 10. C | 11. A | 12. C | 13. B | 14. B | 15. A | 16. B | 17. D | 18. B | 19. A | 20. B


---

<!-- Gộp nội dung từ: final-exam-theory.md -->
# Final Exam: Theory 

**Thời lượng:** 60 phút
**Hình thức:** Đề thi Tổng hợp kiến thức (Trắc nghiệm + Giải đáp Logic ngắn) bao trùm cả Lịch sử, Nguyên lý (ACID, Lập mô hình Thiết kế), và Thao tác RDBMS chuyên sâu.

---

## Phần 1: Tự luận Ngắn gọn (Short Essay Tasks)

**Đề 1 (20 điểm): So sánh SQL và NoSQL**
Trưởng phòng kĩ thuật giao cho bạn phân tích nền tảng Database chuẩn bị Build cho Dịch vụ Video Streaming (như Netflix 2.0). 
Trong đó: Log tương tác App (Mỗi giây xả về 50.000 logs), và Bảng Profile Thuận lợi Đăng ký Phân quyền VIP Thanh toán Thẻ Tín Dụng User (Xử lý chi trả tài chính). 
- *Câu hỏi:* Bạn chọn ứng dụng nền tảng Database RDBMS (như PostgreSQL) và Không RDBMS (NoSQL như MongoDB) đặt gác vị trí nào? Tại vì sao dựa trên đặc tính của kiến trúc phân tán?

**Đề 2 (20 điểm): Review Data Schema Anomaly (Rủi ro dị thường)**
DB Designer gửi bạn Mảng Thiết kế Bảng Giỏ Đương (Basket) cực rộng:
`[CartID, User_Name, User_Phone, Product1_SKU, Product1_Name, Product2_SKU, Product2_Name, Price_Total, Date]`
- *Câu hỏi:* Sự phá vỡ Quy tắc chuẩn hóa lớn cỡ nào đang chìm sâu dưới Table này? Liệt kê ít nhất 2 bất cập nếu Backend chạy code Push Data vào khi User nhặt 10 sản phẩm cùng lúc. Hãy tư vấn hóa giải Table trên về Chuẩn 3NF (Bút phá nó ra bao nhiêu Table Con nhỏ).

---

## Phần 2: Trắc nghiệm Tổng hợp (MCQs - 60 điểm)

*(Đánh dấu X vào đáp án đúng)*

**1. Hành động Xóa nguyên 1 bảng không để lại dấu tích Khung móng rác rưởi là?**
[ ] A. DELETE * FROM table;
[ ] B. ERASE TABLE table;
[ ] C. DROP TABLE table; 
[ ] D. TRUNCATE TABLE table;

**2. Đột nhiên Client cần Cột Lương phải Ràng buột bắt buộc nằm trong khoảng lớn hơn 0 và nhỏ hơn 1 Triệu Đô.**
[ ] A. Áp `DEFAULT >= 0` 
[ ] B. Set `UNIQUE(0, 1000000)`
[ ] C. Dùng `PRIMARY LIMIT 1000M`
[ ] D. Dùng Lưới Rào `CHECK (salary > 0 AND salary < 1000000)`

**3. Khác biệt máu chốt lớn nhất tạc lên tên tuổi GROUP BY và ORDER BY?**
[ ] A. Cả hai đều gộp bảng. Khác biệt chỉ ở Cách sắp xếp thời gian.
[ ] B. ORDER BY rải lại thứ tự vị trí dòng dữ liệu theo Alphabet hoặc Lớn nhỏ. Tính toán dòng nào y y dòng đó. GROUP BY vò, nhào, gom một tỷ dòng dính chặt lại thành Khối dựa trên thuộc tính giống nhau để Lột Báo Cáo.
[ ] C. ORDER dùng trong Select. Group dùng trong Update.
[ ] D. Group By chạy lề trái. Order phân trang lề phải.

**4. Dữ liệu thời thiết được đóng trong tệp `.json` truyền vào có cặp chìa khóa `{ temp: 15, location: 'HN' }`. Đây được vinh danh là luồng Dữ liệu kiểu dáng gì?**
[ ] A. Structured Data
[ ] B. Un-structured Data
[ ] C. Semi-structured (Bán Cấu Trúc)
[ ] D. Hardened Data

**5. Lệnh sau: `REVOKE DELETE ON accounts FROM app_user_role;` phát hiệu tín hiệu rủi ra gì?**
[ ] A. Hạ sát xóa account nào có chữ `app_user_role`.
[ ] B. Cúp quyền "chặt chém" data (Xóa) ở bảng Khách hàng ra khỏi tay ứng dụng Role API kia tránh phá hoại. Role đó bị khóa mất dao Xóa.
[ ] C. Đang cấp phép gán quyền cho phép Delete nhầm Bảng.
[ ] D. Đóng kết nối hệ thống.

**6. Cục Toán Logic sau dội lại Bảng Dữ liệu như nào: Trái Tròn 10 dòng... Phải Tròn 20 dòng... SQL gõ `OUTER FULL JOIN` mà Cả hai bảng hoàn thoàn lạc lỏng chả Giao Cắt được lấy 1 Hàng qua Constraint?**
[ ] A. Bắn Error chết ngắt đỏ mặt báo rỗng mạng hỏng.
[ ] B. Trả về đúng 0 dòng.
[ ] C. Ghép Lệch trả ra Rắn nối dài 30 dòng. Đầu Trái dính thì Đuôi mảng kia ôm chữ `NULL` và ngược lại. Gom hết rác rưởi trọn ổ lên báo cáo. 
[ ] D. Trả ra 15 dòng chia trung bình.

**7. Nguyên lý Nới Rộng (BASE) thay vì Rắn chắt (ACID) ưu tiên giữ điều gì xuyên Không trong môi trường NoSQL Network Đứt gãy Mất Node (Partition Tolarance)?**
[ ] A. Consistency (Chống trễ báo cáo sai số dù phải ngừng cung cấp Màn Hình Phục Vụ).
[ ] B. Security (Khóa chốt Tường Lửa cực đoạn).
[ ] C. Availability (Mạng sống Máy chủ, Luôn gật đầu nhả Response kể cả Data báo lộn xộn độ Cũ kĩ delay Eventually Consistent).
[ ] D. Durability (Lưu dữ liệu vào ổ băng đĩa thời xa xưa siêu bền vững trăm năm).

**8. Bạn đang muốn xem "Tổng thu nhập lớn nhất Của Cùng 1 Vị Trí Công việc Nhất Đinh" ở Công ti (Bộ Đếm Gộp Nhóm Đại Cực Giá). Dãy Toán học Aggregation là chuẩn vị nhất?**
[ ] A. `SELECT SUM(salary) FROM employees ORDER BY 1 LIMIT 1`
[ ] B. `SELECT job_id, MAX(salary) FROM employees GROUP BY job_id`
[ ] C. `SELECT GROUP(job_id) FROM MIN(salary)`
[ ] D. `SELECT AVG(salary), job_id WHERE MAX(salary)`

*(Hết đề - Hãy kiểm tra lại bài trước khi nộp)*


---

<!-- Gộp nội dung từ: final-exam-practical.md -->
# Final Exam: Practical Implementation

**Thời lượng:** 180 phút
**Công cụ:** PostgreSQL / MySQL, DBeaver hoặc pgAdmin
**Định dạng nộp:** 1 File `.sql` duy nhất chứa toàn bộ đoạn script từ Bài 1 đến Bài 4.

Đây là bài kiểm tra thực hành toàn diện. Đòi hỏi bạn áp dụng tổng lực tất cả kỹ năng Database Fundamentals đã học: Thiết kế chuẩn hóa, Khởi tạo bảng, Gán khóa bảo mật, Truy vấn ma trận và Kiểm soát giao dịch.

---

## 1. Mệnh lệnh Kiến thiết DDL (30 Bảng)

Bạn được cấp một tờ Requirement của hệ thống Bán Hàng Trực Tuyến (E-Commerce):
- Cửa hàng bán các Sản Phẩm (Products - Mã SP, Tên, Giá, Số lượng Tồn kho). Sản phẩm thuộc về 1 Danh Mục (Category - Tên Danh mục).
- Dữ liệu Khách Hàng (Customers) cần lưu Tên, Email, SĐT, Địa chỉ giao hàng.
- Khi Khách đặt mua, sinh ra 1 Đơn Hàng (Orders - Mã Order, Ngày đặt, Trạng thái Giao, Mã Khách).
- Một Đơn hàng chứa nhiều Sản phẩm. 

**Yêu cầu:** 
Viết lệnh `CREATE TABLE` xây dựng 5 bảng (Kể cả Bảng Trung gian để phá vỡ quan hệ Nhiều-Nhiều). 
Quy chuẩn BẮT BUỘC: 
1. `Email` của khách không được lặp lại.
2. Giá SP phải thuộc loại số Thập phân `DECIMAL`, và `Tồn kho` ép vào rào cản `>= 0`.
3. Bất kì `Order` nào sinh ra cũng phải tự động nhận `CURRENT_DATE`.
4. Nếu Sản phẩm bị Ngừng Kinh Doanh (Xóa thẳng khỏi bảng Products), Không được cho lệnh xóa đó chạy nếu đơn hàng của khách ngày xưa có dính chùm tới sản phẩm đó. Báo cáo Ràng buộc khắt khe qua FOREIGN KEY.

## 2. Kích hoạt Rắc mầm Dữ liệu DML (20 Bảng)

Viết chuỗi `INSERT INTO` (Sử dụng lệnh Bulk Insert nhiều dòng cùng lúc để tối ưu CPU).
1. Thả vào 2 Danh Mục Hàng. 
2. Nạp thêm 4 Khách. (Tự chém nội dung).
3. Cho ra 5 Sản Phẩm.
4. Điều khiển 2 vị Khách (C1, C2) đăng ký đặt 3 Đơn Hàng (O1, O2, O3). Nạp Mảng Sản Phẩm Chi tiết (Ví dụ O1 mua 2 cái Laptop, 1 cái Chuột) vào đúng Bảng Order_Details trung gian.

## 3. Chinh phạt Truy xuất Aggregating/Joins (40 Bảng)

Hãy gõ Truy vấn `SELECT` báo cáo cho Giám Đốc các câu hỏi sau:

**Report Kho Hàng:** Lọc tất cả những Mặt hàng (Sản phẩm) trên tổng 40 Chiếc đang nằm Tồn kho, Nối bảng để in Rõ Tên Sản Phẩm đó và Tên Danh Mục chứa nó.

**Report Chi Têu Hoàng Gia:** Khách Hàng nào là Đại Gia đã ném nhiều tiền nhất vào App của mình trong tháng Này? (Gợi ý câu này có bẫy: Cần dùng `SUM(Giá x Số Lượng)` để cộng dồn chùm hóa đơn cho TỔNG đơn, kẹp nhét `ORDER BY` ném lên Top đầu).

**Report Bỏ Quên Dĩ Vãng (LEFT JOIN Cảnh sát):** Có Sản phẩm nào Ế ẩm mốc meo từ ngay Khai trương mà chưa thấy con bóng Ma Khách hàng nào dám đặt vô Đơn hàng đâu k? (Dùng Join bắt Null IS NULL).

## 4. Bảo Vệ & Giao Xử Lý An Toàn (10 Bảng)
Bạn nhận nhiệm vụ Viết 1 Block Script Mua Hàng cho User 1 (Nó muốn mua Mặt hàng A giá 100$). Trình tự: Trừ 1 Số lượng tồn Mặt Hàng A -> Chèn Đơn Hàng -> Cập nhật Doanh thu Tự Cấp Kì Lạ...  Do lo sợ sập điện nửa chừng: 
=> Yêu cầu: Viết Bọc Bằng Khối Transaction `BEGIN` - `COMMIT`. (Chèn thử câu lệnh lỗi nhảm vào giữa rồi ấn `ROLLBACK` chạy thử).

Cuối ngày nghỉ việc, bàn giao User Admin. Tạo 1 User tên `Sales_Staff` chỉ được ban cái Quyền là Đi Nhòm ngó dữ liệu bảng Orders, không được quyền Đắp Dữ liệu Mới. Lệnh DCL đó là lệnh gì? 

---
*(Chúc mùng Bạn Tốt nghiệp Khóa Học! Output trọn hình thức này sẽ là Bệ phòng để bạn tiến đến cõi Backend Developer hoặc Xử Lý Trữ Lượng Big Data Engineering).*


---

