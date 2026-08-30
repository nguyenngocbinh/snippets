# AI Coding CLI — Claude Code, Codex, OmniRoute & Hermes Agent

Tài liệu này hướng dẫn cài đặt nhanh 4 công cụ AI/agent CLI bằng `npm`:

- **Claude Code** — CLI coding agent của Anthropic.
- **OpenAI Codex** — CLI coding agent của OpenAI.
- **OmniRoute** — CLI/tooling để định tuyến và sử dụng nhiều AI model/provider.
- **Hermes Agent** — AI agent CLI cho workflow tự động hóa và coding.

## 1. Yêu cầu môi trường

Khuyến nghị:

- Windows 10/11, macOS hoặc Linux
- Node.js phiên bản LTS
- npm
- Git

Kiểm tra:

```bash
node --version
npm --version
git --version
```

Nếu `node` hoặc `npm` chưa được nhận diện, cần cài Node.js và kiểm tra lại biến môi trường `PATH`.

> **Windows:** Sau khi cài Node.js, nếu PowerShell vẫn không nhận `node`/`npm`, hãy đóng và mở lại terminal/IDE để nạp lại `PATH`.

## 2. Cài đặt Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

Kiểm tra:

```bash
claude --version
```

Khởi chạy:

```bash
claude
```

## 3. Cài đặt OpenAI Codex

```bash
npm install -g @openai/codex
```

Kiểm tra:

```bash
codex --version
```

Khởi chạy:

```bash
codex
```

## 4. Cài đặt OmniRoute

```bash
npm install -g omniroute
```

Kiểm tra:

```bash
omniroute --version
```

Xem danh sách lệnh:

```bash
omniroute --help
```

## 5. Cài đặt Hermes Agent

```bash
npm install -g hermes-agent
```

Kiểm tra:

```bash
hermes-agent --version
```

Nếu package cung cấp executable với tên `hermes`, kiểm tra thêm:

```bash
hermes --version
```

Xem help:

```bash
hermes-agent --help
```

hoặc:

```bash
hermes --help
```

> Tên executable có thể phụ thuộc vào phiên bản/package configuration.

## 6. Cài đặt tất cả cùng lúc

Có thể cài 4 package bằng một command:

```bash
npm install -g @anthropic-ai/claude-code @openai/codex omniroute hermes-agent
```

Sau đó:

```bash
claude --version
codex --version
omniroute --version
hermes-agent --version
```

## 7. Kiểm tra package đã cài

Liệt kê các package global:

```bash
npm list -g --depth=0
```

Hoặc kiểm tra riêng:

```bash
npm list -g @anthropic-ai/claude-code
npm list -g @openai/codex
npm list -g omniroute
npm list -g hermes-agent
```

## 8. Kiểm tra PATH trên Windows

Nếu cài thành công nhưng command không chạy, vấn đề thường nằm ở `PATH`.

Kiểm tra npm global prefix:

```powershell
npm config get prefix
```

Kiểm tra npm global root:

```powershell
npm root -g
```

Kiểm tra command:

```powershell
where.exe claude
where.exe codex
where.exe omniroute
where.exe hermes-agent
```

Kiểm tra PATH:

```powershell
$env:Path -split ';'
```

Thông thường npm global executable trên Windows nằm ở dạng:

```text
C:\Users\<USERNAME>\AppData\Roaming\npm
```

Nếu vừa thay đổi PATH:

1. Đóng PowerShell.
2. Đóng IDE/terminal hiện tại.
3. Mở lại.
4. Chạy lại:

```powershell
claude --version
codex --version
```

## 9. Global installation

Các package trên được cài bằng:

```bash
npm install -g ...
```

`-g` nghĩa là **global installation**.

Điều này phù hợp với CLI vì có thể gọi command từ bất kỳ repository nào:

```bash
cd my-project
claude
```

hoặc:

```bash
cd my-project
codex
```

Không cần cài lại package cho từng project.

## 10. Gợi ý workflow

```text
                    Git Repository
                         │
                         ▼
                 ┌───────────────┐
                 │   Terminal    │
                 │ / IDE / Orca  │
                 └───────┬───────┘
                         │
             ┌───────────┼───────────┐
             │           │           │
             ▼           ▼           ▼
          Claude        Codex    Hermes Agent
          Code                    │
             │                    ▼
             │                 OmniRoute
             │                    │
             └────────────┬───────┘
                          ▼
                    AI Model Layer
```

| Tool | Vai trò chính |
|---|---|
| Claude Code | Coding agent / repository agent |
| Codex | Coding agent / implementation & debugging |
| OmniRoute | Routing / kết nối nhiều model/provider |
| Hermes Agent | Agent workflow / automation |

## 11. Kiểm tra toàn bộ môi trường

```powershell
node --version
npm --version
git --version

claude --version
codex --version
omniroute --version
hermes-agent --version
```

Nếu tất cả command trả về version, môi trường CLI cơ bản đã sẵn sàng.

## 12. Troubleshooting

### `npm` không được nhận diện

Lỗi:

```text
npm : The term 'npm' is not recognized...
```

Kiểm tra:

```powershell
where.exe node
where.exe npm
```

Nếu không có kết quả, kiểm tra Node.js installation và `PATH`.

### Package cài được nhưng command không được nhận diện

Ví dụ:

```bash
npm install -g hermes-agent
```

thành công nhưng:

```text
hermes-agent
```

không chạy.

Kiểm tra:

```powershell
npm config get prefix
npm root -g
where.exe hermes-agent
```

Sau đó kiểm tra thư mục npm global executable có nằm trong `PATH` hay không.

### Kiểm tra package global

```powershell
npm list -g --depth=0
```

Ví dụ:

```text
+-- @anthropic-ai/claude-code@...
+-- @openai/codex@...
+-- hermes-agent@...
`-- omniroute@...
```

## 13. Update

```bash
npm update -g @anthropic-ai/claude-code
npm update -g @openai/codex
npm update -g omniroute
npm update -g hermes-agent
```

Hoặc cài phiên bản mới nhất:

```bash
npm install -g @anthropic-ai/claude-code@latest
npm install -g @openai/codex@latest
npm install -g omniroute@latest
npm install -g hermes-agent@latest
```

## 14. Uninstall

```bash
npm uninstall -g @anthropic-ai/claude-code
npm uninstall -g @openai/codex
npm uninstall -g omniroute
npm uninstall -g hermes-agent
```

## Quick Start

Nếu Node.js/npm đã sẵn sàng:

```bash
npm install -g @anthropic-ai/claude-code @openai/codex omniroute hermes-agent
```

Sau đó:

```bash
claude --version
codex --version
omniroute --version
hermes-agent --version
```

Mở repository:

```bash
cd <your-project>
```

và khởi chạy agent phù hợp.

## Lưu ý

Tên command, cách authentication, model/provider hỗ trợ và các subcommand có thể thay đổi theo phiên bản của từng package.

Khi gặp khác biệt, ưu tiên kiểm tra:

```bash
<command> --help
```

và tài liệu chính thức của package đang sử dụng.
