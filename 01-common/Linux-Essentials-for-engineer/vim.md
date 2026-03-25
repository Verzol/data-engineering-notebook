# Vim

Mỗi phím gõ không phải là viết ra chữ mà là ra lệnh cho Vim.

Cấu trúc lệnh chuẩn Vim thường là:

```bash
[Số lượng] + [Động từ] + [Đối tượng/ Chuyển động]
```

**Số lượng:** Lặp lại hành động bao nhiêu lần (1, 2, 3...)
**Động từ:** Muốn làm gì? (Xóa, Copy, Thay đổi...)
**Đối tượng:** Muốn làm gì lên chỗ đó (Một từ, một câu, di chuyển sang trái phải...)

## Các thành phần để ghép câu

### 1. Các phím di chuyển

Sử dụng 4 phím ở ngón phải khi đặt tay trên bàn phím để di chuyển con trỏ.

- `h`: sang trái
- `l`: sang phải
- `j`: xuống dưới
- `k`: lên trên
- `w`: nhảy tiến lên 1 từ
- `b`: nhảy lùi lại 1 từ

### 2. Các động từ thông dụng

Những hành động chính sẽ làm với văn bản:

- `d`: xóa (thực chất là Cut)
- `y`: copy (yank)
- `c`: xóa và lập tức chuyển sang insert mode để gõ chữ mới thay thế
- `p`: dán nội dung vừa Cắt hoặc Copy ra phía sau con trỏ

### 3. Các mode quan trọng trong Vim

Vim không chỉ có một trạng thái gõ chữ. Bạn phải biết mình đang ở mode nào.

- `Normal mode`: mode mặc định để di chuyển và ra lệnh.
- `Insert mode`: mode để gõ văn bản bình thường.
- `Visual mode`: mode để bôi chọn văn bản.

Phím chuyển mode cơ bản:

- `i`: vào Insert mode tại vị trí con trỏ
- `a`: vào Insert mode sau con trỏ
- `o`: mở dòng mới bên dưới và vào Insert mode
- `Esc`: thoát về Normal mode

## Những lệnh sống còn

### 1. Lưu và thoát file

Các lệnh bạn dùng hằng ngày khi làm việc với Vim:

- `:w`: lưu file
- `:q`: thoát (nếu chưa sửa gì)
- `:wq` hoặc `ZZ`: lưu và thoát
- `:q!`: thoát không lưu

### 2. Undo/Redo

Sửa nhầm trong Vim là chuyện bình thường, quan trọng là biết quay lại.

- `u`: undo (hoàn tác)
- `Ctrl + r`: redo (làm lại)

### 3. Xóa nhanh theo đối tượng

Ghép động từ + đối tượng để thao tác cực nhanh:

- `dw`: xóa từ vị trí con trỏ đến hết từ
- `dd`: xóa nguyên một dòng
- `d$`: xóa từ vị trí con trỏ đến cuối dòng
- `diw`: xóa bên trong một từ (delete inner word)
- `ciw`: thay đổi nội dung của một từ ngay tại chỗ

## Copy/Paste chuẩn Vim

### 1. Yank và Paste

- `yy`: copy nguyên dòng hiện tại
- `3yy`: copy 3 dòng liên tiếp
- `p`: dán phía sau
- `P`: dán phía trước

### 2. Delete cũng là cắt

Trong Vim, lệnh `d` vừa xóa vừa đưa vào bộ nhớ tạm để có thể dán lại bằng `p`.

## Tìm kiếm và thay thế

### 1. Tìm từ trong file

- `/keyword`: tìm xuôi xuống dưới
- `?keyword`: tìm ngược lên trên
- `n`: nhảy đến kết quả tiếp theo
- `N`: nhảy đến kết quả trước đó

### 2. Thay thế (replace)

```bash
:%s/old/new/g
```

Giải thích nhanh:

- `%`: áp dụng cho toàn bộ file
- `s`: substitute
- `g`: thay tất cả kết quả trên mỗi dòng

Thay có xác nhận từng chỗ:

```bash
:%s/old/new/gc
```

## Visual mode để chọn nhanh

### 1. Chọn ký tự, dòng, khối

- `v`: vào Visual mode theo ký tự
- `V`: chọn theo dòng
- `Ctrl + v`: chọn theo cột (block)

Sau khi chọn có thể bấm:

- `d`: xóa vùng chọn
- `y`: copy vùng chọn
- `c`: thay thế vùng chọn

## Mẹo di chuyển nhanh hơn

Ngoài `w` và `b`, nên nhớ thêm:

- `0`: về đầu dòng
- `$`: về cuối dòng
- `gg`: về đầu file
- `G`: về cuối file
- `5G`: nhảy tới dòng số 5

## Cheatsheet

Một vài ví dụ để nhớ công thức `[Số lượng] + [Động từ] + [Đối tượng]`:

- `3dw`: xóa 3 từ
- `2yy`: copy 2 dòng
- `ci("`: thay nội dung bên trong cặp dấu ngoặc kép
- `da("`: xóa cả cụm bao gồm dấu ngoặc kép
