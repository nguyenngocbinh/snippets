---
title: Cài đặt môi trường Python
---

# 🐍 Hướng dẫn cài đặt môi trường Python

## 📋 Mục lục nhanh

- [🏢 Môi trường công ty](#-môi-trường-công-ty-corporate-environment)
- [💻 Máy tính cá nhân](#-máy-tính-cá-nhân-personal-setup)  
- [📊 Data Science Workflow](#-data-science-workflow)
- [🌐 Cross-platform Deployment](#-cross-platform-deployment)
- [🆘 Troubleshooting](#-troubleshooting--common-issues)

---

## 🏢 Môi trường công ty (Corporate Environment)

> *Dành cho môi trường có proxy, hạn chế mạng, cài đặt offline*

### 🌐 Thiết lập Behind Proxy

#### Cấu hình Proxy cho Conda
```cmd
conda config --set proxy_servers.http http://proxy.company.com:8080
conda config --set proxy_servers.https https://proxy.company.com:8080
```

#### Cấu hình Proxy cho Pip
```cmd
pip config set global.proxy http://proxy.company.com:8080
```

#### Thiết lập biến môi trường (PowerShell)
```powershell
$env:HTTP_PROXY = "http://proxy.company.com:8080"
$env:HTTPS_PROXY = "https://proxy.company.com:8080"
```

### 💾 Cài đặt Offline Package

#### Bước 1: Tạo danh sách packages cần thiết
```cmd
# Tạo requirements.txt cho dự án
pip freeze > requirements.txt
```

#### Bước 2: Tải packages về máy có mạng
```cmd
# Tạo thư mục chứa packages
mkdir D:\offline_packages

# Tải tất cả packages và dependencies
pip download -r requirements.txt -d D:\offline_packages
```

#### Bước 3: Cài đặt từ thư mục offline
```cmd
# Cài đặt từ thư mục local
pip install -r requirements.txt --find-links=D:\offline_packages --no-index
```

### 🔒 Bảo mật và Compliance

#### Tạo environment cô lập
```cmd
conda create -n secure_env python=3.10 pip
conda activate secure_env
```

#### Kiểm tra packages có lỗ hổng bảo mật
```cmd
pip install safety
safety check
```

---

## 💻 Máy tính cá nhân (Personal Setup)

> *Setup nhanh, tùy chỉnh theo sở thích cá nhân*

### ⚡ Quick Setup (5 phút)

#### 1. Thêm Conda vào PATH
**Command Prompt:**
```cmd
set PATH=D:\anaconda3\condabin;%PATH%
```

**PowerShell:**
```powershell
$env:PATH = "D:\anaconda3\condabin;" + $env:PATH
```

#### 2. Tạo environment đa năng
```cmd
conda create -n myenv python=3.10 pandas numpy matplotlib jupyter ipykernel
conda activate myenv
```

#### 3. Cài đặt VSCode integration
Thêm vào `settings.json` của VSCode:
```json
{
    "terminal.integrated.env.windows": {
        "PATH": "D:\\anaconda3\\condabin;${env:PATH}"
    },
    "python.defaultInterpreterPath": "D:\\anaconda3\\envs\\myenv\\python.exe"
}
```

### 🎨 Tùy chỉnh giao diện

#### Jupyter Notebook Themes
```cmd
# Cài đặt themes
pip install jupyterthemes

# Áp dụng theme đẹp
jt -t onedork -fs 13 -altp -tfs 14 -nfs 14 -cellw 88% -T
```

#### Jupyter Extensions
```cmd
pip install jupyter_contrib_nbextensions jupyter_nbextensions_configurator
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user
```

### 🔧 Quản lý Environment cá nhân

#### Tạo environment cho từng dự án
```cmd
# Web scraping
conda create -n webscraping python=3.10 requests beautifulsoup4 selenium

# Machine Learning  
conda create -n ml python=3.10 scikit-learn tensorflow pandas

# Data Analysis
conda create -n analysis python=3.10 pandas numpy matplotlib seaborn jupyter
```

#### Lệnh thường dùng
```cmd
# Liệt kê environments
conda env list

# Kích hoạt environment
conda activate myenv

# Xóa environment
conda env remove -n old_env

# Dọn dẹp cache
conda clean --all
```

---

## 📊 Data Science Workflow

> *Tối ưu cho phân tích dữ liệu và machine learning*

### 📓 Jupyter Lab Setup

#### Cài đặt JupyterLab với extensions
```cmd
conda create -n datascience python=3.10
conda activate datascience

# Core packages
conda install pandas numpy matplotlib seaborn plotly

# Jupyter ecosystem
conda install jupyterlab jupyter-collaboration
pip install jupyterlab-git jupyterlab-lsp
```

#### Tạo kernel cho Jupyter
```cmd
conda activate datascience
ipython kernel install --user --name=datascience --display-name="Data Science"
```

### 🤖 Machine Learning Environment

#### Standard ML Stack
```cmd
conda create -n ml python=3.10
conda activate ml

# Core ML libraries
conda install scikit-learn pandas numpy matplotlib seaborn
pip install optuna xgboost lightgbm

# Deep Learning (chọn 1)
# TensorFlow
pip install tensorflow

# PyTorch  
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
```

#### Specialized environments
```yaml
# environment_nlp.yaml
name: nlp
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.10
  - pandas
  - numpy
  - jupyter
  - pip
  - pip:
    - transformers
    - datasets
    - tokenizers
    - spacy
```

```cmd
conda env create -f environment_nlp.yaml
```

### 📈 Visualization & Reporting

#### Advanced plotting environment
```cmd
conda create -n viz python=3.10
conda activate viz

conda install pandas matplotlib seaborn plotly bokeh
pip install altair streamlit dash
```

#### Report generation
```cmd
# Thêm vào environment
pip install nbconvert pandoc-python-filter
conda install -c conda-forge pandoc
```

---

## 🌐 Cross-platform Deployment

> *Triển khai trên nhiều hệ điều hành*

### 🪟 Windows Specific

#### PowerShell Profile setup
```powershell
# Thêm vào $PROFILE
function conda-init {
    D:\anaconda3\condabin\conda.bat init powershell
}

function ca { conda activate $args }
function cda { conda deactivate }
```

#### Windows Terminal integration
```json
{
    "name": "Conda Python",
    "commandline": "powershell.exe -NoExit -Command \"& 'D:\\anaconda3\\condabin\\conda.bat' activate base\"",
    "icon": "🐍"
}
```

### 🐧 Linux Deployment

#### Environment export cho Linux
```cmd
# Trên Windows, tạo environment.yml cross-platform
conda env export --no-builds > environment_linux.yml
```

#### Platform-specific package download
```cmd
# Tải packages cho Linux từ Windows
pip download --platform linux_x86_64 --only-binary=:all: pandas numpy -d linux_packages/
```

### 🍎 macOS Considerations

#### M1/M2 Mac compatibility
```yaml
# environment_mac.yaml
name: mac_env
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.10
  - pandas
  - numpy
  - matplotlib
  - pip
  - pip:
    - tensorflow-macos  # For M1/M2
    - tensorflow-metal  # GPU acceleration
```

### 🐳 Docker Integration

#### Dockerfile với Conda
```dockerfile
FROM continuumio/miniconda3

COPY environment.yml .
RUN conda env create -f environment.yml

SHELL ["conda", "run", "-n", "myenv", "/bin/bash", "-c"]
ENTRYPOINT ["conda", "run", "--no-capture-output", "-n", "myenv"]
```

---

## 🆘 Troubleshooting & Common Issues

### ❌ Lỗi thường gặp

#### Conda không được nhận diện
```cmd
# Reset conda
conda init
# Hoặc
conda init --reverse
conda init
```

#### Environment activation không hoạt động
```cmd
# Kiểm tra conda config
conda info

# Reset environment variables
conda info --envs
conda activate base
```

#### Package conflicts
```cmd
# Kiểm tra conflicts
python -m pip check

# Resolve conflicts
conda update --all
pip install --upgrade package_name
```

### 🔍 Debug Commands

```cmd
# Kiểm tra conda installation
conda --version
conda info

# Kiểm tra environments
conda env list

# Kiểm tra packages trong environment
conda list
pip list

# Kiểm tra Python path
python -c "import sys; print(sys.executable)"
```

### 💡 Best Practices

1. **Luôn sử dụng environments riêng cho từng dự án**
2. **Export environment.yml để chia sẻ**
3. **Dọn dẹp cache định kỳ: `conda clean --all`**
4. **Sử dụng conda cho packages chính, pip cho packages đặc biệt**
5. **Backup danh sách packages quan trọng**

### 📞 Hỗ trợ thêm

- **Conda documentation**: https://docs.conda.io/
- **Anaconda community**: https://community.anaconda.cloud/
- **Stack Overflow**: Tag `conda`, `anaconda`