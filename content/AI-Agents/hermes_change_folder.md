# Chuyển Hermes từ C sang D bằng Junction

## Quy trình đã thực hiện

### Bước 1 — Xác định thư mục Hermes

Thư mục ban đầu:

```text
C:\Users\binhnn2\AppData\Local\hermes
```

Hermes hiện có:

```text
C:\Users\binhnn2\AppData\Local\hermes\hermes-agent
```

---

### Bước 2 — Copy Hermes sang ổ D

Tạo thư mục đích:

```cmd
mkdir "D:\AI agent\Hermes"
```

Copy toàn bộ Hermes từ C sang D.

Kết quả mong muốn:

```text
D:\AI agent\Hermes
└── hermes-agent
    └── venv
        └── Scripts
            └── hermes.exe
```

Kiểm tra:

```cmd
"D:\AI agent\Hermes\hermes-agent\venv\Scripts\hermes.exe" --version
```

Nếu trả về:

```text
Hermes Agent v0.20.1
```

thì bản copy trên D hoạt động.

---

### Bước 3 — Đóng Hermes

Kiểm tra:

```cmd
tasklist | findstr /I "hermes"
```

và:

```cmd
tasklist | findstr /I "python"
```

Không còn process liên quan thì tiếp tục.

---

### Bước 4 — Đổi tên thư mục Hermes cũ

Ban đầu:

```text
C:\Users\binhnn2\AppData\Local\hermes
```

Đổi thành:

```cmd
ren "C:\Users\binhnn2\AppData\Local\hermes" hermes_backup
```

Trong trường hợp của bạn ban đầu bị:

```text
Access is denied
```

Sau khi restart Windows, lệnh đã thực hiện được.

Kết quả:

```text
C:\Users\binhnn2\AppData\Local\
└── hermes_backup
```

---

### Bước 5 — Tạo Junction

Tạo Junction tại **đường dẫn cũ**:

```cmd
mklink /J "C:\Users\binhnn2\AppData\Local\hermes" "D:\AI agent\Hermes"
```

Kết quả của bạn hiện tại:

```text
08/24/2026  10:28 AM    <JUNCTION>     hermes [D:\AI agent\Hermes]
08/24/2026  10:26 AM    <DIR>          hermes_backup
```

Đây là trạng thái **đúng**.

---

## Sau khi chuyển

Cấu trúc hiện tại:

```text
C:\Users\binhnn2\AppData\Local\
│
├── hermes
│   └── <JUNCTION> ──────────────► D:\AI agent\Hermes
│
└── hermes_backup
    └── bản dữ liệu cũ
```

Khi Hermes truy cập:

```text
C:\Users\binhnn2\AppData\Local\hermes\...
```

Windows tự chuyển sang:

```text
D:\AI agent\Hermes\...
```

Do đó **dữ liệu Hermes mới sẽ được ghi trên ổ D**.

---

## Bước 6 — Kiểm tra Junction

Chạy:

```cmd
dir "C:\Users\binhnn2\AppData\Local"
```

Phải thấy:

```text
<JUNCTION> hermes [D:\AI agent\Hermes]
```

Kiểm tra tiếp:

```cmd
dir "C:\Users\binhnn2\AppData\Local\hermes"
```

và:

```cmd
dir "D:\AI agent\Hermes"
```

Hai đường dẫn phải truy cập được cùng dữ liệu.

---

## Bước 7 — Test ghi dữ liệu

Đây là test rất hữu ích:

```cmd
echo junction_test > "C:\Users\binhnn2\AppData\Local\hermes\junction_test.txt"
```

Sau đó:

```cmd
dir "D:\AI agent\Hermes\junction_test.txt"
```

Nếu thấy file `junction_test.txt` → Junction hoạt động chính xác.

Xóa file test:

```cmd
del "C:\Users\binhnn2\AppData\Local\hermes\junction_test.txt"
```

---

## Bước 8 — Chạy Hermes

Chạy:

```cmd
hermes --version
```

hoặc:

```cmd
"C:\Users\binhnn2\AppData\Local\hermes\hermes-agent\venv\Scripts\hermes.exe" --version
```

Nếu:

```text
Hermes Agent v0.20.1
```

thì đường dẫn cũ vẫn hoạt động bình thường.

---

## Bước 9 — Chưa xóa backup ngay

Hiện tại:

```text
C:\Users\binhnn2\AppData\Local\hermes_backup
```

vẫn là **bản dự phòng**.

Tôi khuyên bạn giữ nó vài ngày để đảm bảo:

* Hermes chạy bình thường
* Config vẫn còn
* History/session vẫn còn
* Các agent/tool vẫn hoạt động
* Không có lỗi bất thường

Sau khi chắc chắn, mới xóa backup:

```cmd
rmdir /S /Q "C:\Users\binhnn2\AppData\Local\hermes_backup"
```

### Lưu ý quan trọng

Lệnh trên **chỉ xóa `hermes_backup`**, không xóa:

```text
D:\AI agent\Hermes
```

và cũng không xóa Junction:

```text
C:\Users\binhnn2\AppData\Local\hermes
```

---

## Sơ đồ cuối cùng

```text
                    Windows
                       │
                       ▼
C:\Users\binhnn2\AppData\Local\hermes
                       │
                       │ Junction
                       ▼
              D:\AI agent\Hermes
                       │
          ┌────────────┴────────────┐
          ▼                         ▼
    hermes-agent                  config
          │
          ▼
         venv
          │
          ▼
      hermes.exe
```

**Mục tiêu cuối cùng:** Hermes vẫn sử dụng đường dẫn quen thuộc trên C, nhưng **dữ liệu thực tế nằm trên D**, giúp giảm việc ổ C bị đầy do Hermes.
