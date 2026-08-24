# Cài OmniRoute bằng npm rồi tích hợp vào Hermes Agent

### 1. Cài OmniRoute

```powershell
npm install -g omniroute
```

Kiểm tra:

```powershell
omniroute --version
```

### 2. Chạy OmniRoute

```powershell
omniroute
```

Mở:

```text
http://localhost:20128
```

### 3. Cấu hình Provider

Trong OmniRoute:

```text
Providers → thêm provider/model
```

Sau đó tạo API key cho OmniRoute.

### 4. Set API key trên Windows

```powershell
$env:OMNIROUTE_API_KEY="YOUR_API_KEY"
```

Nếu muốn lưu vĩnh viễn:

```powershell
[Environment]::SetEnvironmentVariable(
  "OMNIROUTE_API_KEY",
  "YOUR_API_KEY",
  "User"
)
```

Mở terminal mới sau đó.

### 5. Test OmniRoute

```powershell
curl http://localhost:20128/v1/models `
  -H "Authorization: Bearer $env:OMNIROUTE_API_KEY"
```

Nếu trả về danh sách model → **OmniRoute OK**.

### 6. Cấu hình Hermes

Trong:

```text
%USERPROFILE%\.hermes\config.yaml
```

trỏ Hermes vào:

```text
http://localhost:20128/v1
```

và chọn model của OmniRoute.


