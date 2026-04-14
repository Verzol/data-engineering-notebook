<!-- Gộp nội dung cho phần giới thiệu Pandas căn bản -->
# Học phần: Pandas Fundamentals & Data Manipulation

## 1. Tổng quan về Pandas (Pandas Overview)

### Sự ra đời và Tầm quan trọng
**Pandas** (Panel Data) là một thư viện mã nguồn mở lõi trong hệ sinh thái Data Science của Python, được phát triển lần đầu bởi Wes McKinney vào năm 2008. Công cụ này cung cấp cấu trúc dữ liệu cực kỳ linh hoạt và nhanh chóng, giải quyết hiệu quả các tác vụ làm sạch, thao tác và phân tích dữ liệu dạng bảng (Tabular Data).

**Tại sao Pandas lại thống trị mảng phân tích dữ liệu?**
- **Trực quan như bảng Excel/SQL**: Đại diện dữ liệu thông qua cấu trúc hàng và cột được dán nhãn mốc (labeled axes).
- **Tự động căn chỉnh (Data Alignment)**: Xử lý mượt mà và tự động vị trí dữ liệu không đồng nhất hoặc bị thiếu (Missing/NaN data).
- **Tối ưu hóa mạnh mẽ**: Được xây dựng kết nối chặt chẽ với C và thư viện NumPy, hỗ trợ tính toán Vector hóa với những Dataframe lớn.
- **Tích hợp mạnh mẽ**: Hỗ trợ đọc/ghi trơn tru vào SQL, CSV, JSOn, Excel.

### Khai báo thư viện chuẩn
Tại mọi hệ thống và các cuốn sách chuyên ngành, bạn luôn định danh (`alias`) pandas thành `pd`.
```python
import pandas as pd
import numpy as np # Thông thường numpy luôn được đi kèm
```

---

## 2. Cấu trúc dữ liệu Từng Thành Phần (Creating Series & DataFrame)

Pandas xây dựng nền tảng của mình dựa trên 2 kiến trúc: **Series** (1 chiều) và **DataFrame** (2 chiều).

### 2.1 Đối tượng Pandas Series
Series được định nghĩa là hệ thống mảng một chiều (1D), chứa chuỗi các dữ liệu cùng kiểu, đi kèm một mảng nhãn định danh gọi là **Index**. 

**Khởi tạo cơ bản:**
```python
# Tạo từ một List, thêm tùy chỉnh danh sách Index
sr_scores = pd.Series(
    [90, 85, 78, 92], 
    index=['Alice', 'Bob', 'Charlie', 'David']
)
print(sr_scores)
# Alice      90
# Bob        85
# Charlie    78
# David      92
# dtype: int64

# Tạo cấp tốc từ Dictionary
sdata = {'Ohio': 35000, 'Texas': 71000, 'Oregon': 16000}
sr_state = pd.Series(sdata)
```
*Các hàm thường dùng của Series:*
- `sr_scores.values`: Trả về mảng các giá trị nội tại (NumPy array thô).
- `sr_scores.index`: Xem danh sách Index cấp phát.
- `sr_scores.value_counts()`: Báo cáo tần suất xuất hiện của từng giá trị (Group and Count).
- `sr_scores.nunique()`: Số lượng phân lớp giá trị không trùng lặp (Unique count).

### 2.2 Đối tượng Pandas DataFrame
DataFrame là xương sống của mọi bài toán Data Pipeline. Nó tạo ra cấu trúc 2 chiều (Row/Column), bao hàm trong nó **nhiều đối tượng Series ghép lại**, dùng chung một bộ quy chiếu Index bên tay trái.

**Khởi tạo từ một Dictionary chứa các Array:**
```python
data = {
    "employee_id": ['101', '102', '103', '104', '105'],
    "name": ["Alice", "Bob", "Charlie", "David", "Eva"],
    "department": ["HR", "IT", "IT", "Finance", "HR"],
    "salary": [50000, 70000, 65000, 90000, 62000],
    "is_active": [True, True, False, True, True]
}
df_employees = pd.DataFrame(data)
```

**Các phương thức quan sát Dataframe Cốt lõi:**
| Method / Attribute | Chức năng (Description) |
| --- | --- |
| `.head(n)` / `.tail(n)` | Trích xuất `n` dòng quan sát ở đỉnh (Head) hoặc ở đáy (Tail) của DataFrame (Mặc định n=5) |
| `.sample(n)` | Trích xuất ngẫu nhiên ra lượng `n` mẫu dòng phân bố đều để đánh giá dữ liệu |
| `.shape` | Trả về tuple mốc kích thước ma trận `(số_hàng, số_cột)` |
| `.info()` | Hiển thị thông tin hệ thống của Dataframe: Data Type từng cột, lượng null/rỗng, và bộ nhớ chiếm dụng RAM |
| `.describe()` | Đưa ra bảng báo cáo thống kê tóm tắt 5 chỉ số (Mean, Std, Min, Max, Quantile 25-50-75) phục vụ các cột dạng số Numeric |

---

## 3. Lựa chọn và Trích xuất Dữ liệu (Indexing & Selection)

Lọc đúng điểm ảnh hưởng và khoanh vùng Cột mục tiêu là tác vụ đầu tiên khi nhận được bộ dữ liệu khổng lồ.

### 3.1 Truy xuất theo trục dọc (Column Selection)
```python
# Chọn 1 cột (Return Series)
s_salary = df_employees['salary']

# Chọn nhiều cột đồng thời (Chú ý sử dụng ngoặc vuông KÉP [[ ]])
# Return Sub-DataFrame
df_subset = df_employees[['name', 'department', 'salary']]
```

### 3.2 Bộ định vị nhãn Index `.loc[]` (Label-based Locator)
Hàm `.loc[rows_label, cols_label]` xác định điểm nhắm dựa vào giá trị/tên/nhãn rõ ràng của Index.
> [!IMPORTANT]
> Trong logic slicing của `.loc`, giá trị chốt kết thúc **HOÀN TOÀN ĐƯỢC BAO GỒM TÍNH TOÁN (Inclusive Edge)**.

```python
# Lấy nội dung tại index (dòng) có nhãn là 0 và 2, bóc tách ra cột Name, Salary.
df_employees.loc[[0, 2], ['name', 'salary']]

# Lấy vùng dải băng từ index 1 ĐẾN index 3 (lấy trọn cả vị trí số 3), chạy từ cột 'employee_id' ngang qua 'department'
df_employees.loc[1:3, 'employee_id':'department']
```

### 3.3 Bộ định vị mốc toán học `.iloc[]` (Position-based Locator)
Trái ngược `.loc`, hàm `.iloc[rows_idx, cols_idx]` chỉ chạy bằng các toạ độ vị trí chuẩn tương tự như array truyền thống trong Python (luôn luôn tính từ 0 tới N-1).
> [!NOTE]
> Khác với `.loc`, đối với hệ slicing của `.iloc`, điểm kết thúc mốc sẽ **BỊ LOẠI TRỪ KHỎI KẾT QUẢ (Exclusive Edge)**.

```python
# Chọn list hàng ở vị trí 0-2-4, thuộc 2 cột đầu tiên dạng Array
df_employees.iloc[[0, 2, 4], [0, 1]]

# Mốc cắt từ hàng 0 -> 2 (cắt kết quả bỏ hụt hàng số 2), từ cột 1 -> 3
df_employees.iloc[0:2, 1:3]
```

---

## 4. Lọc và Truy vấn dữ liệu (Filtering & Querying)

Kỹ năng loại trừ noise (dữ liệu rác) hoặc tìm kiếm dữ liệu thỏa mãn Insight.

### 4.1 Lọc điều kiện đơn tuyến Boolean (Boolean Masking)
Khi kết hợp cột dữ liệu trong dataframe với một biểu thức toán học (`==`, `>`, `<=`), Pandas sẽ gióng và tạo ra một vector `True/False` tạm thời. Nó hoạt động như một mặt nạ sàng lọc.

```python
# Ví dụ: Lọc tìm người có thu nhập cao
high_income_mask = df_employees['salary'] >= 65000

# Áp cái mặt nạ đó đè lại lên df
df_high = df_employees[high_income_mask]

# Viết vắn tắt
df_employees[df_employees['salary'] >= 65000]
```

### 4.2 Cú pháp Móc nối mệnh đề Toán tử (Multiple Conditions Line)
Ta dùng các ký tự bitwise thay mặt cho Operator chuẩn: `&` mang ý nghĩa là (AND), `|` được coi là (OR) và `~` đứng trước mệnh đề (NOT đảo ngược logic).
> [!WARNING]
> Phải bọc mọi khối lệnh lẻ bằng Cặp dấu ngoặc đơn `(  )` khi viết dồn. Nếu không Pandas sẽ báo Exception Type Error ngầm định do không hiểu thứ tự thực thi ưu tiên của các chuỗi logic.

```python
# Nhân viên phòng IT LÀM song song Mức lương chạm ngưỡng 70 ngàn
df_employees[(df_employees['department'] == 'IT') & (df_employees['salary'] >= 70000)]

# Dùng hàm phủ định '~' Nghịch đảo logic is_active
df_employees[~df_employees['is_active']] 
```

### 4.3 Khai thả tối ưu với `.isin()` / `.between()` / `.query()`
Pandas cung cấp phương pháp nâng cao để viết biểu thức gọn gàng.

```python
# .isin() : Thay thế cho chuỗi nhiều logic OR nối đuôi nhau.
target_depts = ['HR', 'Finance']
df_employees[df_employees['department'].isin(target_depts)]

# .between() : Thay thế logic khoảng chặn >= x & <= y (Hai đầu chốt đều Inclusive tính gộp).
df_employees[df_employees['salary'].between(50000, 70000)]

# .query() : Triển khai lọc truy vấn dưới định dạng Text/SQL, 
# Tựa như khối lệnh lệnh WHERE - Truyền biến động thông qua kí tự '@'.
min_sal = 60000
df_employees.query("department == 'IT' and salary > @min_sal")
```

---

## 5. Cấu trúc Sắp xếp Dữ liệu (Data Sorting)

Tái sinh kết cấu trật tự theo ý đồ phân tích (như View bảng xếp hạng TOP, Bottom). Chìa khóa thành công là sử dụng `.sort_values()`.

### 5.1 Sort toàn bộ khối (Global Sort)
Kích hoạt sắp xếp theo trục cột giá trị trị số: Tham chiếu bằng Option `by` với mốc thiết lập `ascending` chi phối chiều quay (True = tăng dần lên, False = tụt giảm đi).

```python
# Xếp Lương Nhân Tự động trượt Dốc
df_employees.sort_values(by='salary', ascending=False)

# Sorting đa tầng mảng Tùy biến : Kích hoạt Cấp Ưu Tiên sắp xếp.
# (Vd: Phòng Ban chốt xếp theo chuẩn A-Z chữ cái. Nhưng nhóm người trong Phòng đó lại xếp theo Lương Cao-Low)
df_employees.sort_values(
    by=['department', 'salary'], 
    ascending=[True, False]
)
```

### 5.2 Lấy gọn Top Đầu/Cuối hiệu suất Cao (nlargest / nsmallest)
Để truy lùng Top giá trị, ta có thể kết hợp `sort_values` + `.head()`. Nhưng trên kho dữ liệu Big Data triệu dòng thì chi phí chạy Thuật Toán sort all array sẽ bị tổn hao kinh khủng. Thay vào đó hãy dùng:
- `df_employees.nlargest(3, 'salary')` : Chọn 3 cá thể sở hữu Lương bổng quyền lực nhất.
- `df_employees.nsmallest(2, 'age')` : Trích lọc ra 2 em Út trẻ nhất tổ đội.

---

## 6. Logic Nhóm và Ráp Tổ hợp Thống kê (Grouping & Aggregation)

Tính năng huyền thoại của cơ sở nền Analysis Data: **Bọc vỏ - Gom nhóm - Nén gộp lại**.
Thủ tục `.groupby()` áp dụng mô hình triết lí xoay vòng 3 Phase: **Split -> Apply -> Combine**.

![alt text](https://pandas.pydata.org/docs/_images/06_groupby.svg)

### 6.1 Gộp và chạy logic cơ sở (Simple Aggregation)

```python
# Nhiệm vụ: Xây Báo Cáo Tính Trung bình lương Nhân viên Từng Ban Mảng
# 1. Tách mảng (Split) the df qua 'department'
# 2. Hướng đích (Select Column) vô mục tiêu 'salary' 
# 3. Phủ nén phép toán Hàm Thống (Apply): mean()

df_employees.groupby('department')['salary'].mean()
```

### 6.2 Dàn trải đa tổ hợp cùng Multi-Aggregation (`.agg`)
Sử dụng hàm `.agg()` giúp chúng ta làm thủ tục tính toán phân lô nhiều lớp hàm Toán trong 1 Scope mãnh lệnh gọn gàng.

```python
# Cho xuất mọi mảng khối ra 3 bảng đo: Min / Max / Lăng Kính Số Lượng Nhân Tố (Count)
df_employees.groupby('department')['salary'].agg(['min', 'max', 'count'])
```

Áp đặt riêng biệt chuẩn loại Hàm Toán Học cho từng Khu Vực Cột thông qua cú pháp Dictionary Mapping:
```python
report_df = df_employees.groupby('department').agg({
    'employee_id': 'nunique', # Check lượt Mã duy nhất
    'age': 'mean',            # Tính Tuổi Bình Quân
    'salary': ['sum', 'mean'] # Kép 2 loại cho khối lương
})
```

> [!TIP]
> **Đưa Index Trở Về làm Cột Thường (Flatten Structure):**
> Sau bất cứ màn Groupby nào, Pandas cũng sẽ gán biến trục gom cột vào Khối Móng Index gây khó khăn về thẩm mĩ trích xuất dòng phụ. Để hạ bệ tầng lớp Index đó cho bằng ngang lại thành Table phăng ngang phẳng, ta gọi Method kết liễu chặn đuôi lệnh là `.reset_index()` hoặc set flag `as_index=False`.

```python
# Thẩm mĩ trả Result chuẩn Dataframe SQL
df_employees.groupby('department', as_index=False)['salary'].mean()
```

---
<!-- End of Document -->
