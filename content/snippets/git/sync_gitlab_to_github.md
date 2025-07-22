# 🔄 Hướng dẫn đồng bộ repository từ GitLab sang GitHub
*Tự động đồng bộ hóa code giữa GitLab và GitHub using CI/CD*

Hướng dẫn này sẽ giúp bạn thiết lập quy trình tự động đồng bộ repository từ **GitLab** sang **GitHub** sử dụng GitLab CI/CD pipeline.

---

## 🔐 1. Thêm biến môi trường trên GitLab

Để đồng bộ, bạn cần tạo hai biến môi trường bảo mật trên GitLab:

### 📋 Các biến cần thiết:

- **`GITLAB_PERSONAL_ACCESS_TOKEN`** 🔑  
  *Token cá nhân dùng để truy cập GitLab repository*

- **`GITHUB_TOKEN`** 🔑  
  *Token cá nhân dùng để push code lên GitHub repository*

### 🛠️ Cách thêm biến môi trường trên GitLab

1. **Truy cập vào GitLab** → **Project Settings** → **CI/CD** → **Variables**
2. **Chọn "Add variable"** và thêm các biến sau:

#### Biến 1: GitLab Token
```
Key:   GITLAB_PERSONAL_ACCESS_TOKEN
Value: [Token cá nhân GitLab của bạn]
Type:  Variable
Mask:  ✅ (Nên bật để ẩn giá trị này trong logs)
```

#### Biến 2: GitHub Token
```
Key:   GITHUB_TOKEN
Value: [Token cá nhân GitHub của bạn]
Type:  Variable
Mask:  ✅ (Nên bật để bảo mật thông tin)
```

> **💡 Lưu ý**: Đảm bảo cấp quyền `read_repository` cho GitLab token và `repo` cho GitHub token.

---

## ⚙️ 2. Chỉnh sửa file `.gitlab-ci.yml`

Thêm đoạn script dưới đây vào file `.gitlab-ci.yml` để tự động đồng bộ từ GitLab sang GitHub:

```yaml
stages:
  - deploy

deploy_to_github:
  stage: deploy
  image: alpine:latest
  before_script:
    - apk add --no-cache git
  script:
    - git config --global user.email "nguyenngocbinhneu@gmail.com"
    - git config --global user.name "Nguyen Ngoc Binh"
    - echo "Cloning repository..."
    - git clone --mirror https://oauth2:$GITLAB_PERSONAL_ACCESS_TOKEN@gitlab.com/nguyenngocbinh/papers.git || (echo "Clone failed"; exit 1)
    - cd papers.git
    - echo "Adding GitHub remote..."
    - git remote add github https://$GITHUB_TOKEN@github.com/nguyenngocbinh/papers.git
    - echo "Pushing to GitHub..."
    - git push --mirror github || (echo "Push failed"; exit 1)
  only:
    - main
```

---

## 📖 3. Giải thích các bước quan trọng

### 🔍 Chi tiết từng bước:

| Lệnh | Mục đích | Giải thích |
|------|----------|------------|
| `git clone --mirror` | **Mirror Clone** | Clone repository từ GitLab ở chế độ mirror để giữ nguyên lịch sử commit |
| `git remote add github` | **Thêm Remote** | Thêm GitHub repository làm remote destination mới |
| `git push --mirror github` | **Mirror Push** | Đẩy toàn bộ repository (bao gồm tất cả branches và tags) lên GitHub |
| `only: - main` | **Trigger Condition** | Chỉ thực hiện job này khi có thay đổi trên nhánh `main` |

### 🏗️ Workflow hoạt động:

```mermaid
graph LR
    A[GitLab Commit] --> B[Pipeline Triggered]
    B --> C[Clone from GitLab]
    C --> D[Add GitHub Remote]
    D --> E[Push to GitHub]
    E --> F[Sync Complete]
```

---

## ⚠️ 4. Lưu ý quan trọng

### 🔒 Bảo mật:
- **Cấp quyền phù hợp** cho cả hai tokens để đảm bảo có thể đọc từ GitLab và ghi lên GitHub
- **Mask tokens** trong GitLab Variables để tránh lộ thông tin trong logs
- **Sử dụng HTTPS** thay vì SSH để đơn giản hóa authentication

### 📦 Repository:
- **Tạo repository trên GitHub** trước khi chạy pipeline
- **Đảm bảo tên repository** khớp với cấu hình trong script
- **Kiểm tra permissions** của cả GitLab và GitHub repositories

### 🚀 Performance:
- Nếu repository có **dung lượng lớn**, hãy xem xét:
  - Sử dụng **Git LFS** cho large files
  - **Shallow clone** nếu không cần full history
  - **Incremental sync** thay vì full mirror

---

## 🎯 5. Customization Options

### 📝 Thay đổi thông tin cá nhân:
```yaml
script:
  - git config --global user.email "your-email@example.com"
  - git config --global user.name "Your Name"
```

### 🌿 Sync multiple branches:
```yaml
only:
  - main
  - develop
  - release/*
```

### 📊 Thêm logging chi tiết:
```yaml
script:
  - echo "🚀 Starting GitLab to GitHub sync..."
  - echo "📦 Repository: $CI_PROJECT_NAME"
  - echo "🌿 Branch: $CI_COMMIT_REF_NAME"
  # ... existing script
  - echo "✅ Sync completed successfully!"
```

---

## 🔄 6. Kết quả

Sau khi thiết lập hoàn tất:

✅ **Mỗi khi có commit mới trên GitLab** → Pipeline tự động trigger  
✅ **Repository được đồng bộ hoàn toàn** → Giữ nguyên history và branches  
✅ **GitHub repository luôn up-to-date** → Real-time synchronization  
✅ **Zero manual intervention** → Hoàn toàn tự động  

> **🎉 Chúc mừng!** Bạn đã thiết lập thành công quy trình đồng bộ tự động từ GitLab sang GitHub!

---

## 🆘 Troubleshooting

### ❌ Các lỗi thường gặp:

| Lỗi | Nguyên nhân | Giải pháp |
|-----|-------------|-----------|
| `Clone failed` | Token GitLab không hợp lệ | Kiểm tra token và permissions |
| `Push failed` | Token GitHub không đủ quyền | Cấp quyền `repo` cho GitHub token |
| `Repository not found` | Tên repository sai | Kiểm tra URL trong script |
| `Permission denied` | Token hết hạn | Tạo token mới |

### 🔧 Debug tips:
- Kiểm tra **Pipeline logs** để xem chi tiết lỗi
- Sử dụng **`echo`** commands để debug variables
- Test tokens bằng cách **clone manually** trước

---

*Last updated: July 2025* | *GitLab CI/CD Integration Guide*
