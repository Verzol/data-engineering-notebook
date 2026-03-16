# Linux Architecture (Kiến trúc Linux)

## Lý thuyết

Kiến trúc của một hệ điều hành Linux gồm nhiều lớp bọc lấy nhau. Hai thành phần cốt lõi là **Kernel** và **Shell**.

Hardware (Phần cứng): CPU, RAM, ổ cứng.
Kernel (Hạt nhân): Là "trái tim" và "bộ não" của hệ điều hành. Nó nằm toàn quyền kiểm soát hệ thống và giao tiếp trực tiếp với phần cứng để cấp phát tài nguyên.
Shell (Lớp vỏ): Là giao diện giao tiếp giữa người dùng và Kernel. Nó nhận các lệnh bạn gõ vào, dịch chúng sang ngôn ngữ mà Kernel hiểu được, và trả về kết quả. Các loại Shell phổ biến là Bash hoặc Zsh.

## CLI Navigation & File Management

CLI (Command Line Interface) là giao diện dòng lệnh. Thay vì dùng chuột để click vào các thư mục (GUI - Graphical User Interface), ta dùng các dòng lệnh để điều khiển.

**Các lệnh điều hướng cơ bản:**

1. `pwd` (print working directory): in ra đường dẫn của thư mục hiện tại, xem mình đang ở đâu trong máy tính.

```bash
$ pwd
/home/dem/documents
```

2. `ls` (list): liệt kê các file và thư mục con nằm trong thư mục hiện tại.
   Dùng thêm `-l` để xem chi tiết, `-a` để xem file ẩn.

```bash
$ ls -la
drwxr-xr-x 2 dem dem 4096 Oct  9 10:00 .
drwxr-xr-x 4 dem dem 4096 Oct  9 09:30 ..
-rw-r--r-- 1 dem dem   14 Oct  9 10:00 note.txt
```

3. `cd` (change directory): di chuyển từ thư mục này sang thư mục khác.

```bash
$ cd /var/log    # Di chuyển đến thư mục /var/log
$ cd ..          # Lùi lại một thư mục (đi ra ngoài cửa)
$ cd ~           # Đi thẳng về nhà (thư mục Home của user)
```

## File Operations (Thao tác với tập tin)

1. `touch`: tạo một file trống mới tinh hoặc cập nhật thời gian sửa đổi của file đã có.

```bash
$ touch bai_tap.txt    # Tạo ngay một file tên là bai_tap.txt
```

2. `cp` (copy): nhân bản file hoặc thư mục. Cần chỉ định bản gốc và đích đến.

```bash
$ cp bai_tap.txt bai_tap_copy.txt    # Copy ra một bản backup
$ cp -r thu_muc_A/ thu_muc_B/        # Thêm -r (recursive) để copy cả một thư mục
```

3. `mv` (move): lệnh này có 2 tác dụng là "Cut & Paste" (di chuyển file đến nơi khác) hoặc Đổi tên file.

```bash
$ mv bai_tap.txt /home/dem/        # Di chuyển file vào thư mục /home/dem/
$ mv file_cu.txt file_moi.txt      # Đổi tên file_cu thành file_moi
```

4. `rm` (remove): xóa file hoặc thư mục. Xóa ở CLI là mất luôn, không ở trong thùng rác.

```bash
$ rm rác.txt               # Xóa file rác.txt
$ rm -r thu_muc_rac/       # Xóa thư mục (phải có -r)
# CẢNH BÁO: Tuyệt đối không bao giờ gõ 'rm -rf /' nếu không muốn phá hủy toàn bộ hệ thống.
```

## File Permissions & Ownership (Quyền truy cập và sở hữu)

Mỗi file/thư mục trên Linux đều có quyền hạn và chủ sở hữu để kiểm soát ai được đọc, ghi, thực thi.

1. `chmod` (change mode): thay đổi quyền truy cập của file/thư mục.

```bash
$ chmod 644 note.txt         # Chủ file: đọc/ghi, người khác: chỉ đọc
$ chmod +x script.sh         # Thêm quyền thực thi cho script
```

2. `chown` (change owner): đổi chủ sở hữu file/thư mục.

```bash
$ sudo chown dem:dem note.txt    # Đổi owner và group của note.txt thành dem
```

3. `whoami`: xem user hiện tại bạn đang đăng nhập.

```bash
$ whoami
dem
```

## Viewing & Editing File Content (Xem và chỉnh sửa nội dung file)

Khi làm việc với file log hoặc file cấu hình, bạn thường cần xem nhanh hoặc chỉnh nội dung.

1. `cat` (concatenate): in toàn bộ nội dung file ra màn hình.

```bash
$ cat note.txt
Hom nay hoc Linux co ban.
```

2. `less`: xem file dài theo từng trang, dễ đọc log lớn.

```bash
$ less /var/log/syslog
```

3. `head` / `tail`: xem vài dòng đầu hoặc cuối file.

```bash
$ head -n 5 app.log      # Xem 5 dòng đầu
$ tail -n 20 app.log     # Xem 20 dòng cuối
$ tail -f app.log        # Theo dõi log realtime
```

## Search & Filter (Tìm kiếm và lọc dữ liệu)

Linux rất mạnh ở khả năng tìm file và lọc text bằng command line.

1. `find`: tìm file/thư mục theo tên, loại, vị trí.

```bash
$ find . -name "*.md"                 # Tìm mọi file .md trong thư mục hiện tại
$ find /var/log -type f -name "*.log" # Tìm file log trong /var/log
```

2. `grep`: tìm dòng có chứa từ khóa trong file.

```bash
$ grep "ERROR" app.log
$ grep -R "database" .      # Tìm đệ quy trong thư mục hiện tại
```

## Redirection & Pipe (Chuyển hướng và ống lệnh)

Đây là "vũ khí" giúp ghép nhiều lệnh nhỏ thành luồng xử lý mạnh mẽ.

1. `>` và `>>`: chuyển hướng output ra file.

```bash
$ echo "hello" > note.txt      # Ghi đè file
$ echo "new line" >> note.txt  # Ghi nối thêm vào file
```

2. `|` (pipe): lấy output lệnh trước làm input cho lệnh sau.

```bash
$ ls -la | grep ".md"         # Liệt kê rồi lọc các file .md
$ cat app.log | grep "ERROR"   # Lọc log lỗi
```

## Process Management (Quản lý tiến trình)

Tiến trình (process) là chương trình đang chạy. Biết cách xem và dừng process là kỹ năng bắt buộc.

1. `ps`: xem danh sách tiến trình đang chạy.

```bash
$ ps aux
```

2. `top`: xem realtime CPU/RAM và process nào đang tốn tài nguyên.

```bash
$ top
```

3. `kill`: dừng một process theo PID.

```bash
$ kill 12345          # Gửi tín hiệu dừng mềm
$ kill -9 12345       # Dừng cưỡng bức khi process bị treo
```

## Package & Service Basics (Gói phần mềm và dịch vụ)

Linux distro thường có trình quản lý gói để cài software, và service manager để quản lý dịch vụ nền.

1. `apt` (Ubuntu/Debian): cài và cập nhật phần mềm.

```bash
$ sudo apt update
$ sudo apt install curl
```

2. `systemctl`: quản lý service (start/stop/restart/status).

```bash
$ sudo systemctl status nginx
$ sudo systemctl restart nginx
$ sudo systemctl enable nginx
```

## Useful Shortcuts & History (Phím tắt và lịch sử lệnh)

Dùng phím tắt giúp thao tác terminal nhanh và chuyên nghiệp hơn.

1. `history`: xem lại các lệnh đã chạy trước đó.

```bash
$ history
```

2. Phím tắt hay dùng trong terminal:

```bash
Ctrl + C   # Dừng lệnh đang chạy
Ctrl + L   # Xóa màn hình terminal
Ctrl + R   # Tìm kiếm ngược trong history
```
