# Nano

Nano là trình soạn thảo terminal dễ dùng nhất cho người mới. Mở lên là gõ được ngay, không có nhiều mode như Vim.

## Lý thuyết

Tư duy dùng Nano rất đơn giản:

- Mở file -> sửa trực tiếp
- Lưu bằng tổ hợp phím
- Thoát bằng tổ hợp phím

Ký hiệu trong Nano:

- `^` nghĩa là `Ctrl`
- `M-` nghĩa là `Alt` (Meta)

## Mở file và tạo file

1. Mở file đã có hoặc tạo file mới nếu chưa tồn tại:

```bash
$ nano note.txt
```

2. Mở file với số dòng cụ thể:

```bash
$ nano +25 app.log     # Mở và nhảy tới dòng 25
```

## Các phím sống còn

1. Lưu file:

- `Ctrl + O` (`Write Out`) -> Enter để xác nhận tên file

2. Thoát Nano:

- `Ctrl + X`

3. Thoát khi có thay đổi chưa lưu:

- Bấm `Y` để lưu
- Bấm `N` để không lưu

## Chỉnh sửa văn bản cơ bản

1. Di chuyển:

- Dùng phím mũi tên để lên/xuống/trái/phải
- `Ctrl + A`: về đầu dòng
- `Ctrl + E`: về cuối dòng

2. Cắt/Xóa dòng:

- `Ctrl + K`: cắt dòng hiện tại

3. Dán:

- `Ctrl + U`: dán nội dung vừa cắt/copy

## Tìm kiếm và thay thế

1. Tìm kiếm:

- `Ctrl + W` -> gõ từ khóa -> Enter

2. Tìm tiếp kết quả sau:

- `Alt + W`

3. Thay thế:

- `Ctrl + \` -> nhập từ cũ -> nhập từ mới -> chọn `Y/N/A`

## Chọn và copy nhanh

1. Bắt đầu chọn văn bản (mark):

- `Alt + A`

2. Sau khi chọn:

- `Alt + 6`: copy vùng chọn
- `Ctrl + K`: cắt vùng chọn
- `Ctrl + U`: dán

## Cheatsheet

```bash
Ctrl + O   # Lưu
Ctrl + X   # Thoát
Ctrl + W   # Tìm
Ctrl + \   # Thay thế
Ctrl + K   # Cắt dòng/vùng chọn
Ctrl + U   # Dán
Ctrl + A   # Đầu dòng
Ctrl + E   # Cuối dòng
```
