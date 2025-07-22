---
title: "Python Snippets - Hướng dẫn thực hành"
---

<div align="center">

![Python Logo](https://www.python.org/static/img/psf-logo.png)

# 🐍 **Python Snippets Collection**
*Tập hợp các đoạn code Python hữu ích cho công việc hàng ngày*

</div>

---

## 🚀 **1. Thiết lập môi trường**

### 📦 **1.1. Sử dụng Conda**

#### **Tạo môi trường mới**
```bash
# Tạo môi trường cơ bản
conda create -n myenv python=3.8 pip ipykernel notebook
conda activate myenv

# Sử dụng file environment.yml
conda env create -f environment.yml
```

<details>
<summary><strong>📄 Template environment.yml</strong></summary>

```yml
name: myproject
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.8
  - pandas>=1.4.0
  - numpy>=1.21.0
  - jupyter
  - ipykernel
  - pip
  - pip:
    - requests>=2.28.0
    - plotly>=5.0.0
```
</details>

#### **Quản lý môi trường**
```bash
# Liệt kê môi trường
conda info --envs

# Xóa môi trường
conda env remove -n myenv

# Dọn dẹp cache
conda clean --all
```

### 🔧 **1.2. Jupyter Kernel**

```bash
# Thêm kernel
conda activate myenv
python -m ipykernel install --user --name=myenv

# Xóa kernel (chạy với quyền admin)
jupyter kernelspec uninstall myenv
```

---

## 📦 **2. Cài đặt packages**

### 💾 **Cài đặt OFFLINE**
```bash
# Bước 1: Tải packages
pip download -r requirements.txt -d wheels/

# Bước 2: Cài đặt offline
pip install -r requirements.txt --find-links=wheels/ --no-index
```

### 📋 **Export requirements**
```bash
pip freeze > requirements.txt
# hoặc
conda list --export > environment.yml
```

---

## 🔍 **3. Pandas - Xử lý dữ liệu**

### **<span style="color: #007ACC;">📊 Thao tác cơ bản</span>**

```python
# Case when - Điều kiện
df['new_col'] = np.where(df['col'] < 10, 'low',
                np.where(df['col'] < 20, 'medium', 'high'))

# Clean column names
df.columns = df.columns.str.lower().str.replace(' ', '_')

# Binning - Phân nhóm
df['age_group'] = pd.cut(df['age'], bins=[0, 25, 50, 75, 100], 
                        labels=['young', 'adult', 'senior', 'elderly'])
```

### **<span style="color: #28A745;">🔍 Lọc và tìm kiếm</span>**

```python
# Lọc dữ liệu
df[~df['name'].isin(exclude_list)]  # Loại trừ
df[df['value'].between(10, 50)]     # Trong khoảng
df[df['date'] > '2023-01-01']       # Theo ngày

# Xử lý missing values
df[df['col'].notna()]               # Không null
df['col'].fillna(method='ffill')    # Forward fill
```

### **<span style="color: #FF6B35;">📈 Aggregation & Grouping</span>**

```python
# Group by với transform
df['avg_by_group'] = df.groupby('category')['value'].transform('mean')

# Multiple aggregations
df.groupby('category').agg({
    'sales': ['sum', 'mean'],
    'profit': 'sum',
    'date': 'max'
}).round(2)

# Stratified sampling
df.groupby('target').apply(lambda x: x.sample(frac=0.8))
```

---

## 🔗 **4. Joins & Merging**

### **<span style="color: #6F42C1;">Merge nhiều DataFrames</span>**

```python
# Sử dụng functools.reduce
import functools as ft
dfs = [df1, df2, df3, df4]
result = ft.reduce(lambda left, right: pd.merge(left, right, on='id', how='outer'), dfs)

# Concat với index
dfs = [df.set_index('id') for df in dfs]
result = pd.concat(dfs, axis=1, join='outer')
```

---

## 📁 **5. Files & I/O**

### **<span style="color: #DC3545;">📄 Excel Operations</span>**

```python
# Đọc nhiều files
import glob
files = glob.glob("data/*.xlsx")
dfs = [pd.read_excel(f) for f in files]
combined = pd.concat(dfs, ignore_index=True)

# Ghi nhiều sheets
with pd.ExcelWriter('output.xlsx') as writer:
    df_train.to_excel(writer, sheet_name='train', index=False)
    df_test.to_excel(writer, sheet_name='test', index=False)
```

### **<span style="color: #17A2B8;">🗄️ Database</span>**

```python
import sqlalchemy as sa
import urllib.parse

# Kết nối SQL Server
params = urllib.parse.quote_plus(
    "DRIVER={SQL Server};SERVER=server;DATABASE=db;UID=user;PWD=pass"
)
engine = sa.create_engine(f"mssql+pyodbc:///?odbc_connect={params}")

# Thao tác
df = pd.read_sql("SELECT * FROM table", engine)
df.to_sql('new_table', engine, if_exists='replace', index=False)
```

---

## ⚡ **6. Python Shortcuts**

### **<span style="color: #20C997;">🎯 Lambda & Comprehensions</span>**

```python
# List comprehension
evens = [x for x in range(20) if x % 2 == 0]

# Dict comprehension
word_lengths = {word: len(word) for word in ['hello', 'world', 'python']}

# Lambda với error handling
safe_divide = lambda x, y: x/y if y != 0 else 0
```

### **<span style="color: #FD7E14;">🔤 String Operations</span>**

```python
# Join với delimiter
result = "_".join(["python", "is", "awesome"])

# Regex patterns
import re
numbers = re.findall(r'\d+', 'Extract 123 and 456 from text')
cleaned = re.sub(r'[^\w\s]', '', 'Clean! this@ string#')
```

---

## 📊 **7. Data Analysis Utilities**

### **<span style="color: #E83E8C;">📋 Data Profiling</span>**

```python
def profile_dataframe(df):
    """Tạo báo cáo tổng quan về DataFrame"""
    profile = df.describe(include='all').T
    profile['dtype'] = df.dtypes
    profile['null_count'] = df.isnull().sum()
    profile['null_pct'] = (df.isnull().sum() / len(df) * 100).round(2)
    profile['unique_count'] = df.nunique()
    
    return profile[['dtype', 'count', 'null_count', 'null_pct', 
                   'unique_count', 'mean', 'std', 'min', 'max']]
```

### **<span style="color: #6C757D;">📅 Date Operations</span>**

```python
# Tính khoảng cách thời gian
df['months_diff'] = ((df['end_date'] - df['start_date']) / 
                    pd.Timedelta(days=30.44)).round().astype(int)

df['days_diff'] = (df['end_date'] - df['start_date']).dt.days
```

---

## 🔧 **8. JSON & API**

```python
import json

# Đọc/ghi JSON an toàn
def safe_json_load(filepath):
    try:
        with open(filepath, 'r', encoding='utf-8') as f:
            return json.load(f)
    except (FileNotFoundError, json.JSONDecodeError) as e:
        print(f"Error loading {filepath}: {e}")
        return {}

def save_json(data, filepath):
    with open(filepath, 'w', encoding='utf-8') as f:
        json.dump(data, f, indent=2, ensure_ascii=False)
```

---

## 🎨 **9. Jupyter Extensions**

```bash
# Cài đặt extensions hữu ích
pip install jupyter_contrib_nbextensions jupyter_nbextensions_configurator
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user

# Theme đẹp cho notebook
pip install jupyterthemes
jt -t onedork -fs 13 -cellw 88% -T
```

---

<div align="center">

### 💡 **Tips & Best Practices**

- ✅ Luôn sử dụng virtual environment
- ✅ Đặt tên biến và function rõ ràng
- ✅ Comment code phức tạp
- ✅ Sử dụng type hints khi có thể
- ✅ Test code trước khi deploy

</div>
