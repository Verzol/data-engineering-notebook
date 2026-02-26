# Version Control System & Git

## 1. Tổng Quan

**VCS (Version Control System)** là hệ thống theo dõi mọi thay đổi của code theo thời gian, cho phép quay lại các trạng thái trước đó khi cần.

| Loại            | Đặc điểm                                                       | Ví dụ |
| --------------- | -------------------------------------------------------------- | ----- |
| **Centralized** | Một server trung tâm. Server gặp sự cố thì không làm việc được | SVN   |
| **Distributed** | Mỗi máy có bản sao hoàn chỉnh. Có thể làm việc offline         | Git   |

**Ưu điểm của Git:** Nhanh, bảo mật (SHA-1), branching nhẹ, mã nguồn mở.

---

## 2. Cấu Hình Ban Đầu

Mức độ ưu tiên: `--local` (repo hiện tại) > `--global` (user) > `--system`

```bash
# Thông tin cá nhân
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

# Editor mặc định
git config --global core.editor "code --wait"

# Branch mặc định
git config --global init.defaultBranch main

# Line ending: Windows = true, macOS/Linux = input
git config --global core.autocrlf true

# Xem cấu hình
git config --list
git config --global -e
```

---

## 3. Kiến Trúc 3 Tầng

| Tầng                  | Mô tả                       | Lệnh         |
| --------------------- | --------------------------- | ------------ |
| **Working Directory** | Thư mục làm việc            | —            |
| **Staging Area**      | Khu vực chuẩn bị cho commit | `git add`    |
| **Repository**        | Lưu trữ lịch sử commit      | `git commit` |

**Workflow:** `Edit` → `git add` → `git commit` → `git push`

---

## 4. Các Lệnh Cơ Bản

### Khởi Tạo

```bash
git init                    # Tạo repo mới
git clone <url>             # Clone repo
```

### Staging & Commit

```bash
git status                  # Xem trạng thái
git status -s               # Trạng thái rút gọn

git add <file>              # Stage một file
git add .                   # Stage tất cả

git commit -m "message"     # Commit
git commit -am "message"    # Add + Commit (chỉ tracked files)
```

**Commit message convention:**

- `feat:` Tính năng mới
- `fix:` Sửa lỗi
- `docs:` Tài liệu
- `refactor:` Tái cấu trúc
- `chore:` Bảo trì

### Xem Thay Đổi

```bash
git diff                    # Working Dir vs Staging
git diff --staged           # Staging vs Last Commit

git log --oneline           # Lịch sử ngắn gọn
git log --oneline --graph   # Hiển thị graph
git log -p                  # Chi tiết thay đổi
```

---

## 5. Hoàn Tác

### Unstage & Discard

```bash
git restore --staged <file> # Rút khỏi Staging (giữ thay đổi)
git restore <file>          # Hủy thay đổi (mất vĩnh viễn!)
```

### Sửa Commit

```bash
git commit --amend -m "msg" # Sửa commit cuối

git reset --soft HEAD~1     # Xóa commit, giữ code ở Staging
git reset --hard HEAD~1     # Xóa commit và code (nguy hiểm!)
```

### Dọn Dẹp

```bash
git clean -n                # Xem trước
git clean -f                # Xóa untracked files
git clean -fd               # Xóa cả thư mục
```

---

## 6. File Operations

```bash
git rm <file>               # Xóa + stage
git rm --cached <file>      # Bỏ track, giữ file local
git mv <old> <new>          # Đổi tên
```

### .gitignore

```gitignore
*.log
node_modules/
.env
**/temp/
!important.log              # Ngoại lệ
```

---

## 7. Branching

```bash
git branch                  # Liệt kê
git branch <name>           # Tạo mới
git switch <name>           # Chuyển branch
git switch -c <name>        # Tạo + chuyển

git branch -d <name>        # Xóa (đã merge)
git branch -D <name>        # Force xóa
git branch -m <new-name>    # Đổi tên
```

### Merge

```bash
git switch main
git merge <branch>
```

---

## 8. Remote

```bash
git remote -v               # Xem remotes
git remote add origin <url>

git push origin <branch>
git push -u origin <branch> # Set upstream

git pull origin <branch>    # Fetch + Merge
git fetch origin            # Chỉ fetch
```

---

## 9. Stash

Lưu tạm thay đổi khi cần chuyển context:

```bash
git stash                   # Lưu
git stash push -m "message" # Lưu với mô tả
git stash -u                # Bao gồm untracked

git stash list              # Danh sách
git stash show -p           # Xem nội dung

git stash pop               # Áp dụng + xóa
git stash apply             # Áp dụng + giữ
git stash drop              # Xóa
git stash clear             # Xóa tất cả
```

---

## 10. Merge vs Rebase

### Merge

Tạo merge commit, giữ nguyên lịch sử:

```
      A---B---C  (feature)
     /         \
D---E---F---G---M  (main)
```

### Rebase

Viết lại lịch sử thành đường thẳng:

```
              A'--B'--C'  (feature)
             /
D---E---F---G  (main)
```

```bash
git rebase main             # Rebase lên main
git rebase -i HEAD~3        # Interactive (sửa/gộp commits)
```

|          | Merge        | Rebase        |
| -------- | ------------ | ------------- |
| Lịch sử  | Giữ nguyên   | Linear        |
| Dùng cho | Nhánh public | Nhánh cá nhân |

**Nguyên tắc:** Không rebase commits đã push lên public repo.

```bash
git pull --rebase origin main
```

---

## 11. Xử Lý Conflict

Conflict xảy ra khi cùng một dòng bị sửa ở nhiều nhánh.

**Markers:**

```
<<<<<<< HEAD
Code của bạn
=======
Code từ nhánh khác
>>>>>>> branch
```

**Xử lý:**

1. Mở file, xóa markers
2. Chỉnh sửa code
3. `git add` + `git commit`

```bash
git checkout --ours <file>   # Giữ của mình
git checkout --theirs <file> # Giữ của họ

git merge --abort            # Hủy merge
git rebase --abort           # Hủy rebase
```

---

## 12. Recovery

```bash
git reflog                  # Xem lịch sử mọi thao tác
git reset --hard HEAD@{n}   # Quay về trạng thái n
```

---

## Quick Reference

| Lệnh                  | Mô tả         |
| --------------------- | ------------- |
| `git status`          | Trạng thái    |
| `git add .`           | Stage all     |
| `git commit -m "msg"` | Commit        |
| `git push`            | Push          |
| `git pull`            | Pull          |
| `git log --oneline`   | Lịch sử       |
| `git branch`          | Branches      |
| `git switch <b>`      | Chuyển branch |
| `git merge <b>`       | Merge         |
| `git stash`           | Lưu tạm       |
| `git stash pop`       | Khôi phục     |
| `git diff`            | Xem thay đổi  |
| `git restore <f>`     | Hủy thay đổi  |
