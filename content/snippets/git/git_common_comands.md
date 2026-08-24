Các lệnh Git thường dùng cho quản lý branch, reset, remote, merge, push/pull và xử lý lỗi proxy.

## 1. Cấu hình Git

Thiết lập tên và email cho Git:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Kiểm tra cấu hình:

```bash
git config --list
```

---

## 2. Tạo và chuyển sang branch mới

Tạo branch mới và chuyển sang branch đó:

```bash
git checkout -b dev
```

Ví dụ:

```bash
git checkout -b jump_dev
```

Với Git phiên bản mới, có thể dùng:

```bash
git switch -c dev
```

---

## 3. Reset local theo remote

### Reset branch hiện tại theo `origin/main`

```bash
git fetch origin
git reset --hard origin/main
```

### Reset branch hiện tại theo `origin/dev`

```bash
git fetch origin
git reset --hard origin/dev
```

> ⚠️ `git reset --hard` sẽ xóa các thay đổi chưa commit trong working tree.

---

## 4. Reset toàn bộ thay đổi local

Khôi phục các file đã được Git tracking về trạng thái của commit hiện tại:

```bash
git reset --hard HEAD
```

Xóa thêm các file/thư mục **untracked**:

```bash
git clean -fd
```

> ⚠️ `git clean -fd` sẽ xóa vĩnh viễn các file và thư mục chưa được Git tracking.

Nếu muốn kiểm tra trước những gì sẽ bị xóa:

```bash
git clean -fdn
```

---

## 5. Git Add

Thêm toàn bộ thay đổi vào staging:

```bash
git add .
```

Kiểm tra trạng thái:

```bash
git status
```

---

## 6. Bỏ file khỏi Git nhưng giữ file local

Nếu file đã được `git add` nhưng muốn bỏ khỏi staging:

```bash
git restore --staged test.html
```

Nếu file đã được tracking và muốn Git ngừng tracking nhưng **không xóa file local**:

```bash
git rm --cached test.html
```

---

## 7. Commit

Tạo commit:

```bash
git commit -m "initial"
```

Ví dụ:

```bash
git commit -m "update git snippets"
```

---

## 8. Kiểm tra và thay đổi remote

Xem remote hiện tại:

```bash
git remote -v
```

Thay đổi URL của `origin`:

```bash
git remote set-url origin <REMOTE_URL>
```

Ví dụ:

```bash
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git
```

> Không nên ghi username, password, token hoặc URL chứa credential trực tiếp vào file snippet.

---

## 9. Xóa các branch remote đã bị xóa

Cập nhật thông tin remote và xóa các remote-tracking branch không còn tồn tại:

```bash
git fetch --prune
```

Có thể viết ngắn:

```bash
git fetch -p
```

Kiểm tra branch:

```bash
git branch -a
```

---

## 10. Merge branch hiện tại với `origin/main`

Cập nhật thông tin từ remote trước:

```bash
git fetch origin
```

Sau đó merge:

```bash
git merge origin/main
```

---

## 11. Tạo branch mới từ `origin/main`

Tạo branch `refactor` dựa trên `origin/main` và chuyển sang branch đó:

```bash
git checkout -b refactor origin/main
```

Với Git mới:

```bash
git switch -c refactor origin/main
```

---

## 12. Push branch lên remote

Push branch `refactor` lên `origin`:

```bash
git push origin refactor
```

Để thiết lập upstream:

```bash
git push -u origin refactor
```

Sau khi đã thiết lập upstream, có thể dùng:

```bash
git push
```

---

## 13. Kiểm tra lỗi HTTP 407 Proxy Authentication Required

Nếu `git push` hoặc `git pull` gặp lỗi:

```text
HTTP 407 Proxy Authentication Required
```

Kiểm tra các cấu hình liên quan đến proxy, HTTP, remote và credential:

```powershell
git config --list | Select-String -Pattern "proxy|http|remote|credential"
```

Kiểm tra riêng proxy của Git:

```bash
git config --global --get http.proxy
git config --global --get https.proxy
```

---

## 14. Tạm thời bỏ proxy khi push/pull

Nếu remote nằm trong mạng nội bộ và không cần proxy, có thể tạm thời vô hiệu hóa proxy trong PowerShell:

```powershell
$env:NO_PROXY = "<INTERNAL_HOST>"
$env:no_proxy = "<INTERNAL_HOST>"
$env:HTTP_PROXY = ""
$env:HTTPS_PROXY = ""

git push origin
```

Hoặc:

```powershell
$env:NO_PROXY = "<INTERNAL_HOST>"
$env:no_proxy = "<INTERNAL_HOST>"
$env:HTTP_PROXY = ""
$env:HTTPS_PROXY = ""

git pull origin
```

> Cách này chỉ thay đổi biến môi trường của **PowerShell hiện tại**, không xóa cấu hình proxy toàn hệ thống.

---

## 15. Một workflow Git cơ bản

Quy trình thường dùng:

```bash
git status
git pull
git checkout -b feature/my-feature

# chỉnh sửa code

git add .
git commit -m "Add my feature"
git push -u origin feature/my-feature
```

---

## 16. Một số lệnh kiểm tra nhanh

### Xem branch hiện tại

```bash
git branch --show-current
```

### Xem tất cả branch

```bash
git branch -a
```

### Xem lịch sử commit

```bash
git log --oneline --graph --all
```

### Xem remote

```bash
git remote -v
```

### Xem trạng thái working tree

```bash
git status
```

### Xem thay đổi chưa commit

```bash
git diff
```

### Xem các commit chưa push

```bash
git log origin/main..HEAD --oneline
```

---

## ⚠️ Các lệnh cần đặc biệt cẩn thận

| Lệnh                | Tác dụng                             |
| ------------------- | ------------------------------------ |
| `git reset --hard`  | Xóa thay đổi local chưa commit       |
| `git clean -fd`     | Xóa file/thư mục untracked           |
| `git push --force`  | Có thể ghi đè lịch sử remote         |
| `git rm --cached`   | Bỏ tracking nhưng giữ file local     |
| `git fetch --prune` | Dọn remote-tracking branch đã bị xóa |

Trước khi sử dụng các lệnh có khả năng mất dữ liệu, nên chạy:

```bash
git status
```

và kiểm tra kỹ thay đổi hiện tại.
