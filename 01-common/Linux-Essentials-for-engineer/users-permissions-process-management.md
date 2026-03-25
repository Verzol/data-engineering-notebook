# Users, Permissions & Processes

## Lý thuyết

Trong Linux, bảo mật và kiểm soát hệ thống xoay quanh 3 ý chính:

User (Người dùng): mỗi người đăng nhập vào hệ thống sẽ có tài khoản riêng.
Group (Nhóm): tập hợp nhiều user để cấp quyền dễ hơn.
Permission (Quyền): xác định ai được đọc, ghi, thực thi file/thư mục.
Process (Tiến trình): một chương trình đang chạy trên hệ thống.

## Users & Groups Management

Linux không chỉ quản lý từng user riêng lẻ mà còn quản lý theo group để phân quyền hiệu quả hơn.

1. `whoami`: xem user hiện tại đang đăng nhập.

```bash
$ whoami
dem
```

2. `id`: xem thông tin chi tiết về user và các group mà user đang thuộc về.

```bash
$ id
uid=1000(dem) gid=1000(dem) groups=1000(dem),27(sudo)
```

3. `sudo adduser`: tạo user mới.

```bash
$ sudo adduser analyst
```

4. `sudo groupadd`: tạo group mới.

```bash
$ sudo groupadd data-team
```

5. `sudo usermod -aG`: thêm user vào group.

```bash
$ sudo usermod -aG data-team analyst
```

6. `groups`: xem user đang thuộc những group nào.

```bash
$ groups analyst
analyst : analyst data-team
```
## File Permissions (chmod, chown)

Mỗi file/thư mục có 3 nhóm quyền:
- `u` (user/owner): chủ sở hữu
- `g` (group): nhóm sở hữu
- `o` (others): những người còn lại

Mỗi nhóm có 3 loại quyền:
- `r` (read): đọc
- `w` (write): ghi
- `x` (execute): thực thi

Ví dụ một dòng quyền:

```bash
-rwxr-xr--
```

Giải thích nhanh:
- Chủ file: `rwx` -> đọc, ghi, thực thi
- Group: `r-x` -> đọc, thực thi
- Others: `r--` -> chỉ đọc

1. `ls -l`: xem quyền của file.

```bash
$ ls -l script.sh
-rwxr-xr-- 1 dem data-team 120 Oct 9 10:00 script.sh
```

2. `chmod`: thay đổi quyền.

```bash
$ chmod 755 script.sh      # Chủ file toàn quyền, group và others được đọc + thực thi
$ chmod 644 note.txt       # Chủ file đọc/ghi, người khác chỉ đọc
$ chmod +x run.sh          # Thêm quyền thực thi
```

3. `chown`: đổi owner hoặc group sở hữu file.

```bash
$ sudo chown analyst script.sh
$ sudo chown analyst:data-team script.sh
```

4. `chgrp`: đổi group sở hữu file.

```bash
$ sudo chgrp data-team report.csv
```

## Process Monitoring (ps, top, kill)

Process là chương trình đang chạy. Quản lý process giúp bạn biết chương trình nào đang hoạt động, chiếm tài nguyên, hoặc bị treo.

1. `ps`: xem snapshot các process đang chạy.

```bash
$ ps aux
```

Một vài cột quan trọng:
- `USER`: ai chạy process này
- `PID`: mã số process
- `%CPU`: phần trăm CPU đang dùng
- `%MEM`: phần trăm RAM đang dùng
- `COMMAND`: lệnh đã chạy

2. `top`: theo dõi realtime CPU, RAM, process nặng.

```bash
$ top
```

3. `kill`: gửi tín hiệu đến process theo PID.

```bash
$ kill 12345      # Dừng mềm
$ kill -9 12345   # Dừng cưỡng bức
```

4. `pkill`: kill theo tên process.

```bash
$ pkill python
```

5. `jobs`: xem các background jobs trong shell hiện tại.

```bash
$ jobs
```