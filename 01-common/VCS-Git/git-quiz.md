# Git Quiz

---

## Q1. Kiến trúc 3 tầng

Flow chuẩn xác nhất của kiến trúc 3 tầng trong Git khi bạn muốn lưu code là gì?

- [ ] A. Working Directory → Repository → Staging Area
- [ ] B. Staging Area → Working Directory → Repository
- [x] C. Working Directory → Staging Area → Repository
- [ ] D. Repository → Staging Area → Working Directory

<details>
<summary>Đáp án</summary>

**C** - Đúng chuẩn: bạn gõ code ở Working Dir, đưa vào phòng chờ Staging Area bằng lệnh `add`, rồi chốt vào Repository bằng lệnh `commit`.

</details>

---

## Q2. Xóa file khỏi Git nhưng giữ trên máy

Bạn lỡ commit file `config.json` chứa mật khẩu lên Git. Lệnh nào giúp gỡ file này khỏi Git nhưng vẫn giữ nguyên trên máy tính?

- [ ] A. `git rm config.json`
- [ ] B. `git clean -f`
- [x] C. `git rm --cached config.json`
- [ ] D. `git restore config.json`

<details>
<summary>Đáp án</summary>

**C** - Cờ `--cached` chỉ xóa file khỏi danh sách theo dõi (index/staging) của Git mà không chạm đến file thật trên ổ cứng.

</details>

---

## Q3. Merge vs Rebase

Sự khác biệt cốt lõi khiến Rebase nguy hiểm hơn Merge khi làm việc nhóm là gì?

- [ ] A. Rebase chỉ áp dụng được cho nhánh main
- [ ] B. Rebase không cho phép giải quyết conflict
- [ ] C. Rebase tự động xóa các nhánh đã gộp
- [x] D. Rebase tạo ra các ID commit mới và viết lại lịch sử hoàn toàn

<details>
<summary>Đáp án</summary>

**D** - Rebase thay đổi mã hash của các commit, làm xáo trộn lịch sử nếu các commit này đã được chia sẻ với đồng đội trên remote.

</details>

---

## Q4. Git Stash

Bạn đang code dở tính năng mới nhưng cần sang nhánh khác fix bug khẩn cấp. Lệnh nào để cất tạm code, sau đó lấy ra dùng tiếp và xóa luôn bản nháp đó?

- [x] A. `git stash pop`
- [ ] B. `git stash apply`
- [ ] C. `git reset --soft`
- [ ] D. `git restore`

<details>
<summary>Đáp án</summary>

**A** - Lệnh `pop` vừa áp dụng (apply) thay đổi vừa xóa (drop) bản nháp khỏi danh sách stash.

**Lưu ý:** `git stash apply` chỉ lấy code ra nhưng vẫn giữ bản nháp trong list.

</details>

---

## Q5. Sửa commit cuối

Lệnh nào giúp sửa nhanh message của commit cuối cùng mà không cần tạo commit mới?

- [x] A. `git commit --amend -m "new message"`
- [ ] B. `git reset --soft HEAD~1`
- [ ] C. `git rebase -i HEAD~1`
- [ ] D. `git commit -am "new message"`

<details>
<summary>Đáp án</summary>

**A** - Cờ `--amend` cho phép đắp thêm code hoặc sửa lại lời nhắn của commit ngay trước đó.

</details>

---

## Q6. Config levels

Cờ (flag) nào trong cấu hình Git quyết định phạm vi cài đặt ảnh hưởng đến mọi repository của user hiện tại trên máy?

- [ ] A. `--system`
- [ ] B. `--local`
- [x] C. `--global`
- [ ] D. `--all`

<details>
<summary>Đáp án</summary>

**C** - Mức `--global` áp dụng cho toàn bộ các dự án Git của user đang đăng nhập.

**Lưu ý:** `--system` áp dụng cho mọi user trên máy, `--local` chỉ cho repo hiện tại.

</details>

---

## Q7. Recovery

Bạn vừa gõ nhầm lệnh reset nguy hiểm khiến code mất dấu. Lệnh nào giúp xem lại mọi thao tác để tìm đường quay về?

- [x] A. `git reflog`
- [ ] B. `git log --oneline`
- [ ] C. `git status`
- [ ] D. `git diff`

<details>
<summary>Đáp án</summary>

**A** - Reflog (Reference logs) ghi lại lịch sử mọi sự di chuyển của con trỏ HEAD, giúp khôi phục cả những commit tưởng chừng đã mất.

</details>

---

## Q8. Conflict markers

Trong lúc xử lý Conflict, dấu hiệu nhận biết phần code của nhánh bạn đang đứng (ours) là gì?

- [ ] A. `>>>>>>> branch_name`
- [ ] B. `=======`
- [ ] C. `||||||| merged`
- [x] D. `<<<<<<< HEAD`

<details>
<summary>Đáp án</summary>

**D** - Git sử dụng marker `<<<<<<< HEAD` để đánh dấu điểm bắt đầu đoạn code thuộc về nhánh hiện tại.

</details>

---

## Q9. Push với upstream

Lệnh `git push -u origin feature-branch` có tác dụng gì đặc biệt ở lần push đầu tiên?

- [ ] A. Ép buộc (force) đẩy code lên đè mất code cũ trên remote
- [ ] B. Upload toàn bộ các nhánh local lên server cùng lúc
- [x] C. Thiết lập liên kết (upstream) giữa nhánh local và nhánh trên remote
- [ ] D. Tự động merge code ngay sau khi đẩy lên GitHub

<details>
<summary>Đáp án</summary>

**C** - Cờ `-u` (`--set-upstream`) giúp Git ghi nhớ mối liên kết, để lần sau chỉ cần `git push` hoặc `git pull` là xong.

</details>

---

## Q10. Commit shortcut

Để gộp nhanh việc stage file đã tracked và commit trong một lệnh, bạn dùng cú pháp nào?

- [ ] A. `git commit -m "message"`
- [x] B. `git commit -am "message"`
- [ ] C. `git add commit -m "message"`
- [ ] D. `git commit -a`

<details>
<summary>Đáp án</summary>

**B** - Cờ `-a` (all) add các file đã tracked bị chỉnh sửa, `-m` để viết message.

**Lưu ý:** Lệnh này không áp dụng cho file untracked (file mới chưa từng được add).

</details>

---

## Q11. Distributed VCS vs Centralized VCS

Đặc điểm cốt lõi nào làm nên sự khác biệt của hệ thống quản lý phiên bản phân tán (Distributed VCS) như Git so với hệ thống tập trung (Centralized VCS)?

- [ ] A. Chỉ có một máy chủ duy nhất được phép lưu trữ lịch sử commit
- [ ] B. Cần phải có kết nối mạng liên tục để có thể lưu lại các thay đổi của code
- [ ] C. Không cho phép tạo ra các nhánh (branch) riêng lẻ để phát triển tính năng
- [x] D. Mỗi máy tính của lập trình viên đều chứa một bản sao hoàn chỉnh của kho lưu trữ

<details>
<summary>Đáp án</summary>

**D** - Khác với hệ thống tập trung phụ thuộc hoàn toàn vào một server, Git cho phép lưu trữ toàn bộ lịch sử trên máy cá nhân, giúp việc code offline trở nên dễ dàng.

</details>

---

## Q12. Xem cấu hình Git

Lệnh nào giúp bạn kiểm tra danh sách toàn bộ các thiết lập cấu hình Git hiện tại trên máy?

- [x] A. `git config --list`
- [ ] B. `git config --show`
- [ ] C. `git log --config`
- [ ] D. `git status`

<details>
<summary>Đáp án</summary>

**A** - Lệnh này in ra toàn bộ cấu hình từ các mức system, global đến local để bạn dễ dàng rà soát.

**Lưu ý:** Git không sử dụng cờ `--show` cho mục đích liệt kê cấu hình.

</details>

---

## Q13. Cấu hình autocrlf

Đối với người dùng hệ điều hành macOS hoặc Linux, cấu hình `core.autocrlf` nào nên được sử dụng để xử lý lỗi ký tự xuống dòng?

- [ ] A. `true`
- [x] B. `input`
- [ ] C. `false`
- [ ] D. `auto`

<details>
<summary>Đáp án</summary>

**B** - Các hệ điều hành dựa trên Unix sử dụng chuẩn LF, nên thiết lập `input` sẽ giúp Git tự động chuyển đổi CRLF sang LF khi commit.

**Lưu ý:** Giá trị `true` thường được khuyến nghị cho người dùng hệ điều hành Windows.

</details>

---

## Q14. Khởi tạo Repository

Để bắt đầu theo dõi một thư mục dự án hoàn toàn mới bằng Git trên máy tính của bạn (chưa có trên GitHub), bạn dùng lệnh nào?

- [ ] A. `git create`
- [x] B. `git init`
- [ ] C. `git start`
- [ ] D. `git clone`

<details>
<summary>Đáp án</summary>

**B** - Lệnh này sẽ tạo ra một thư mục ẩn `.git` bên trong dự án, chính thức biến nó thành một kho lưu trữ (repository).

</details>

---

## Q15. Xem thay đổi chưa staged

Bạn vừa gõ thêm vài dòng code nhưng chưa dùng lệnh `git add`. Lệnh nào giúp bạn xem chi tiết những thay đổi ĐÃ gõ nhưng CHƯA được đưa vào phòng chờ?

- [x] A. `git diff`
- [ ] B. `git show`
- [ ] C. `git diff --staged`
- [ ] D. `git log -p`

<details>
<summary>Đáp án</summary>

**A** - Khi chạy không có tham số, lệnh này so sánh trực tiếp nội dung giữa thư mục làm việc (Working Directory) và khu vực chuẩn bị (Staging Area).

**Lưu ý:** `git log -p` dùng để xem chi tiết code thay đổi của các commit TRONG QUÁ KHỨ.

</details>

---

## Q16. Xem thay đổi đã staged

Sau khi đã đưa file vào phòng chờ bằng lệnh add, làm sao để xem chi tiết những thay đổi đó trước khi chính thức gõ lệnh commit?

- [ ] A. `git diff HEAD`
- [ ] B. `git status -s`
- [ ] C. `git diff`
- [x] D. `git diff --staged`

<details>
<summary>Đáp án</summary>

**D** - Cờ `--staged` (hoặc `--cached`) chỉ thị cho Git so sánh nội dung của Staging Area với commit cuối cùng.

**Lưu ý:** `git status -s` chỉ báo cho bạn biết file nào bị đổi màu (thay đổi trạng thái), chứ không cho xem chi tiết dòng code nào bị sửa.

</details>

---

## Q17. Log dạng graph

Cú pháp nào giúp in ra lịch sử commit dưới dạng một sơ đồ cây (graph) thu gọn trên một dòng, dễ nhìn nhất?

- [x] A. `git log --oneline --graph`
- [ ] B. `git log --tree`
- [ ] C. `git status --graph`
- [ ] D. `git log -p`

<details>
<summary>Đáp án</summary>

**A** - Sự kết hợp này hiển thị mã hash rút gọn, lời nhắn trên một dòng, kèm theo các đường kẻ mô phỏng sự phân nhánh và gộp nhánh.

**Lưu ý:** Lệnh `status` không nhận cờ `--graph`.

</details>

---

## Q18. Restore file nguy hiểm

Lệnh nào sau đây là thao tác NGUY HIỂM, sẽ vứt bỏ sạch mọi thay đổi của một file trong Working Directory, đưa nó trở về trạng thái y hệt commit cuối cùng?

- [ ] A. `git clean -f`
- [x] B. `git restore <file>`
- [ ] C. `git rm <file>`
- [ ] D. `git restore --staged <file>`

<details>
<summary>Đáp án</summary>

**B** - Không có cờ bảo vệ nào đi kèm, lệnh này ghi đè trực tiếp lên file trên ổ cứng, làm mất vĩnh viễn các thay đổi chưa được lưu.

</details>

---

## Q19. Reset soft

Bạn vừa commit xong nhưng nhớ ra quên chưa đưa một file quan trọng vào. Lệnh nào xóa bỏ commit đó đi nhưng VẪN GIỮ LẠI toàn bộ code ở Staging Area để bạn add thêm file?

- [ ] A. `git reset --hard HEAD~1`
- [ ] B. `git revert HEAD`
- [ ] C. `git commit --undo`
- [x] D. `git reset --soft HEAD~1`

<details>
<summary>Đáp án</summary>

**D** - Cờ `--soft` lùi lịch sử lại một bước nhưng nương tay giữ lại toàn bộ code đã chuẩn bị, rất thích hợp để gộp thêm file rồi commit lại.

**Lưu ý:** `git revert HEAD` tạo ra một commit mới đảo ngược lại commit cũ, thay vì xóa nó đi.

</details>

---

## Q20. Git Clean

Trong quá trình dọn dẹp dự án, lệnh `git clean -fd` đảm nhận nhiệm vụ gì?

- [ ] A. Dọn dẹp bộ nhớ đệm (cache) lưu trữ nội bộ của Git
- [x] B. Xóa bỏ toàn bộ các file và thư mục chưa được Git theo dõi (untracked files & directories)
- [ ] C. Buộc xóa (force delete) một nhánh cứng đầu
- [ ] D. Xóa bỏ tất cả các file đã được theo dõi nhưng bị thay đổi

<details>
<summary>Đáp án</summary>

**B** - Chữ `f` (force) ép buộc xóa file, và `d` (directory) mở rộng phạm vi xóa cho cả các thư mục rác không nằm trong tầm kiểm soát của Git.

</details>

---

## Q21. Gitignore

Làm sao để cấu hình cho Git tự động ngó lơ, không theo dõi tất cả các file có đuôi `.temp` sinh ra trong dự án?

- [ ] A. Thêm dòng `ignore: *.temp` vào file `.gitconfig` toàn cục
- [x] B. Thêm dòng `*.temp` vào file `.gitignore`
- [ ] C. Dùng lệnh `git rm --cached *.temp` sau mỗi lần tạo file
- [ ] D. Gõ trực tiếp lệnh `git ignore *.temp` vào terminal

<details>
<summary>Đáp án</summary>

**B** - Dấu hoa thị `*` đóng vai trò là ký tự đại diện (wildcard), giúp Git hiểu là bỏ qua bất kỳ file nào kết thúc bằng chuỗi `.temp`.

</details>

---

## Q22. Đổi tên file với Git

Lệnh Git chuẩn xác nhất để đổi tên file `old.js` thành `new.js` và tự động cập nhật sự thay đổi này vào phòng chờ (Staging Area) là gì?

- [ ] A. `git rename old.js new.js`
- [ ] B. `git cp old.js new.js`
- [ ] C. `mv old.js new.js`
- [x] D. `git mv old.js new.js`

<details>
<summary>Đáp án</summary>

**D** - Lệnh này thực hiện cả 2 việc cùng lúc: đổi tên file vật lý trên máy và ghi nhận hành động đổi tên đó vào trạng thái sẵn sàng commit.

</details>

---

## Q23. Tạo và chuyển nhánh

Để tạo ra một nhánh mới mang tên `bug-fix` và ngay lập tức nhảy sang nhánh đó làm việc chỉ bằng 1 câu lệnh, bạn sử dụng cú pháp nào?

- [ ] A. `git switch bug-fix`
- [x] B. `git switch -c bug-fix`
- [ ] C. `git branch bug-fix`
- [ ] D. `git checkout -b bug-fix`

<details>
<summary>Đáp án</summary>

**B** - Cờ `-c` (create) kết hợp với `switch` tạo ra chuỗi thao tác tiện lợi nhất để khởi tạo và chuyển đổi môi trường làm việc.

</details>

---

## Q24. Force delete nhánh

Bạn vừa tạo một nhánh làm tính năng, nhưng code bị hỏng nên bạn muốn xóa bay nhánh đó đi dù CHƯA merge vào main. Git sẽ ngăn cản hành động xóa thông thường. Lệnh nào ép buộc (force) xóa nhánh này?

- [ ] A. `git branch --remove <tên_nhánh>`
- [ ] B. `git branch -d <tên_nhánh>`
- [ ] C. `git rm branch <tên_nhánh>`
- [x] D. `git branch -D <tên_nhánh>`

<details>
<summary>Đáp án</summary>

**D** - Cờ `-D` in hoa tương đương với `--delete --force`, bỏ qua mọi cảnh báo mất mát dữ liệu chưa được hợp nhất.

**Lưu ý:** Cú pháp `--remove` không được sử dụng để xóa nhánh.

</details>

---

## Q25. Fetch vs Pull

Điểm khác biệt cốt lõi nhất giữa `git fetch` và `git pull` khi tương tác với kho lưu trữ trên mạng (Remote Repository) là gì?

- [x] A. Fetch chỉ tải thông tin về máy để xem trước, còn Pull sẽ vừa tải thông tin vừa tự động gộp (merge) code mới vào nhánh hiện tại
- [ ] B. Không có sự khác biệt, hai lệnh này có thể dùng thay thế cho nhau trong mọi trường hợp
- [ ] C. Fetch tự động xử lý xung đột code (conflict), còn Pull yêu cầu xử lý thủ công
- [ ] D. Pull dùng cho nhánh public như main, còn Fetch chỉ dùng cho nhánh cá nhân

<details>
<summary>Đáp án</summary>

**A** - Fetch là phương án an toàn để kiểm tra xem đồng đội có cập nhật gì không, trong khi Pull là một tổ hợp lệnh mang tính thực thi ngay lập tức.

</details>

---

## Q26. Stash file untracked

Mặc định, lệnh `git stash` chỉ cất đi các file ĐÃ được theo dõi. Muốn cất đi cả những file MỚI TINH (untracked) vừa được tạo ra mà chưa từng dùng lệnh add, bạn dùng cờ nào?

- [ ] A. `git stash -a`
- [ ] B. `git stash --staged`
- [x] C. `git stash -u`
- [ ] D. `git stash save`

<details>
<summary>Đáp án</summary>

**C** - Cờ `-u` (viết tắt của `--include-untracked`) sẽ gom mọi file rác, file mới tạo vào chung một bản nháp sạch sẽ.

**Lưu ý:** Cờ `-a` (`--all`) sẽ lưu trữ cả file untracked LẪN các file rác đang bị bỏ qua trong `.gitignore`, thường không cần thiết.

</details>

---

## Q27. Merge commit

Về mặt logic lịch sử, hành động hợp nhất nào sẽ TẠO RA một commit nối hoàn toàn mới, giữ nguyên vẹn cấu trúc rẽ nhánh ban đầu?

- [x] A. `git merge`
- [ ] B. `git checkout`
- [ ] C. `git pull --rebase`
- [ ] D. `git rebase`

<details>
<summary>Đáp án</summary>

**A** - Thuật toán Merge sẽ sinh ra một "merge commit" gộp 2 điểm đầu mút lại với nhau, giữ nguyên tính đa tuyến tính của lịch sử.

**Lưu ý:** `git pull --rebase` tương tự như rebase cục bộ, lệnh này cũng kéo lịch sử thành đường thẳng.

</details>

---

## Q28. Interactive Rebase

Lệnh `git rebase -i HEAD~3` cung cấp cho lập trình viên sức mạnh gì?

- [ ] A. Tự động gộp 3 commit cuối cùng thành 1 commit duy nhất mà không cần hỏi thêm
- [ ] B. Hủy bỏ 3 commit cuối cùng một cách an toàn mà vẫn giữ lại mã nguồn
- [ ] C. Tải nội dung từ 3 commit mới nhất trên server đè lên máy cá nhân
- [x] D. Mở một giao diện tương tác (Interactive) cho phép chỉnh sửa, đổi tên, hoặc gộp 3 commit gần nhất lại với nhau

<details>
<summary>Đáp án</summary>

**D** - Đây là thủ thuật rất mạnh để "làm sạch" các commit rác (như fix typo, test nháp) trước khi đẩy code lên báo cáo công việc.

</details>

---

## Q29. Hủy merge khi conflict

Trong lúc merge hai nhánh lớn, Git báo Conflict quá phức tạp khiến bạn rối trí. Bạn muốn "quay xe", hủy bỏ toàn bộ quá trình merge này để đưa file về trạng thái an toàn lúc trước. Lệnh nào giúp bạn?

- [ ] A. `git reset --hard HEAD`
- [x] B. `git merge --abort`
- [ ] C. `git rebase --abort`
- [ ] D. `git merge --cancel`

<details>
<summary>Đáp án</summary>

**B** - Đây là chiếc "nút thoát hiểm" dọn sạch mọi dấu hiệu xung đột và trả lại cấu trúc thư mục y như lúc bạn chưa gõ lệnh merge.

</details>

---

## Q30. Giải quyết Conflict với theirs

Khi đối mặt với Conflict, nếu bạn quyết định nhượng bộ hoàn toàn, muốn lấy 100% code từ nhánh của đối tác đè lên file của mình trước khi commit, bạn dùng lệnh giải quyết nhanh nào?

- [ ] A. `git resolve --theirs <file>`
- [ ] B. `git accept incoming <file>`
- [ ] C. `git checkout --ours <file>`
- [x] D. `git checkout --theirs <file>`

<details>
<summary>Đáp án</summary>

**D** - Cờ `--theirs` báo hiệu bạn chấp nhận toàn bộ mã nguồn của luồng dữ liệu đang được đẩy vào (incoming branch).

</details>
