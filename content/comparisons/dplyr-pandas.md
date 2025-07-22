---
title: So sánh dplyr (R) và pandas (Python) - Hướng dẫn thao tác dữ liệu
---

Bảng so sánh chi tiết các thao tác xử lý dữ liệu giữa **<span style="color: #007ACC;">dplyr (R)</span>** và **<span style="color: #FF6B35;">pandas (Python)</span>**:

## 🔧 **Các phương thức xử lý Data Frame**

### 1. 📋 **Thao tác với Hàng (Rows)**

| **Chức năng**           | **<span style="color: #007ACC;">dplyr (R)</span>**               | **<span style="color: #FF6B35;">pandas (Python)</span>**        |
|-------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| **<span style="color: #28A745;">Arrange</span>** *(Sắp xếp)*     | `arrange(df, col)`                                               | `df.sort_values(by='col', ascending=True)`                      |
| **<span style="color: #28A745;">Distinct</span>** *(Loại bỏ trùng)*| `distinct(df, col)`                                              | `df.drop_duplicates(subset='col')`                              |
| **<span style="color: #28A745;">Filter</span>** *(Lọc dữ liệu)*  | `filter(df, condition)`                                          | `df[df['condition']]`                                           |
| **<span style="color: #28A745;">Slice</span>** *(Cắt dữ liệu)*   | `slice(df, rows)`                                                | `df.iloc[rows]`                                                 |

### 2. 📊 **Thao tác với Cột (Columns)**

| **Chức năng**           | **<span style="color: #007ACC;">dplyr (R)</span>**               | **<span style="color: #FF6B35;">pandas (Python)</span>**        |
|-------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| **<span style="color: #28A745;">Glimpse</span>** *(Xem tổng quan)*| `glimpse(df)`                                                   | `df.info()`                                                     |
| **<span style="color: #28A745;">Mutate</span>** *(Tạo cột mới)*  | `mutate(df, new_col = func(old_col))`                           | `df['new_col'] = df['old_col'].apply(func)`                    |
| **<span style="color: #28A745;">Pull</span>** *(Trích xuất cột)* | `pull(df, col)`                                                 | `df['col']`                                                     |
| **<span style="color: #28A745;">Rename</span>** *(Đổi tên cột)*  | `rename(df, new_col_name = old_col_name)`                       | `df.rename(columns={'old_col_name': 'new_col_name'}, inplace=True)` |
| **<span style="color: #28A745;">Select</span>** *(Chọn cột)*     | `select(df, col1, col2, ...)`                                   | `df[['col1', 'col2', ...]]`                                    |

### 3. 👥 **Thao tác với Nhóm (Groups)**

| **Chức năng**           | **<span style="color: #007ACC;">dplyr (R)</span>**               | **<span style="color: #FF6B35;">pandas (Python)</span>**        |
|-------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| **<span style="color: #28A745;">Group By</span>** *(Nhóm theo)*  | `group_by(df, col)`                                             | `df.groupby('col')`                                             |
| **<span style="color: #28A745;">Summarise</span>** *(Tổng hợp)*  | `summarise(df, new_col = func(col))`                            | `df.agg({'col': func})`                                         |

### 4. 🔗 **Thao tác với Data Frames**

| **Chức năng**           | **<span style="color: #007ACC;">dplyr (R)</span>**               | **<span style="color: #FF6B35;">pandas (Python)</span>**        |
|-------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| **<span style="color: #DC3545;">bind_cols</span>** *(Nối cột)*   | `bind_cols(df1, df2)`                                           | `pd.concat([df1, df2], axis=1)`                                 |
| **<span style="color: #DC3545;">bind_rows</span>** *(Nối hàng)*  | `bind_rows(df1, df2)`                                           | `pd.concat([df1, df2], axis=0)`                                 |
| **<span style="color: #17A2B8;">Inner Join</span>** *(Nối trong)*| `inner_join(df1, df2, by = "key_column")`                       | `pd.merge(df1, df2, on='key_column', how='inner')`             |
| **<span style="color: #17A2B8;">Left Join</span>** *(Nối trái)*  | `left_join(df1, df2, by = "key_column")`                        | `pd.merge(df1, df2, on='key_column', how='left')`              |
| **<span style="color: #17A2B8;">Right Join</span>** *(Nối phải)* | `right_join(df1, df2, by = "key_column")`                       | `pd.merge(df1, df2, on='key_column', how='right')`             |
| **<span style="color: #17A2B8;">Full Join</span>** *(Nối đầy đủ)*| `full_join(df1, df2, by = "key_column")`                        | `pd.merge(df1, df2, on='key_column', how='outer')`             |
| **<span style="color: #FFC107;">Semi Join</span>** *(Nối bán)*   | `semi_join(df1, df2, by = "key_column")`                        | <span style="color: #6C757D;">*Không có sẵn; có thể dùng `merge` và `isin` để đạt hiệu quả tương tự.*</span> |
| **<span style="color: #FFC107;">Anti Join</span>** *(Nối ngược)* | `anti_join(df1, df2, by = "key_column")`                        | <span style="color: #6C757D;">*Không có sẵn; có thể dùng `merge` và `isin` để đạt hiệu quả tương tự.*</span> |

### 5. ⚡ **Hàm xử lý Vector**

| **Chức năng**           | **<span style="color: #007ACC;">dplyr (R)</span>**               | **<span style="color: #FF6B35;">pandas (Python)</span>**        |
|-------------------------|-------------------------------------------------------------------|-------------------------------------------------------------------|
| **<span style="color: #6F42C1;">if_else</span>** *(Điều kiện)*   | `mutate(df, new_col = if_else(condition, true_val, false_val))` | `df['new_col'] = np.where(condition, true_val, false_val)`     |
| **<span style="color: #6F42C1;">na_if</span>** *(Thay NA)*       | `mutate(df, col = na_if(col, value))`                           | `df['col'].replace(value, np.nan)`                             |
| **<span style="color: #6F42C1;">n_distinct</span>** *(Đếm riêng)*| `n_distinct(df, col)`                                           | `df['col'].nunique()`                                           |
| **<span style="color: #6F42C1;">sample_n</span>** *(Mẫu số)*     | `sample_n(df, n)`                                               | `df.sample(n=n)`                                               |
| **<span style="color: #6F42C1;">sample_frac</span>** *(Mẫu %)*   | `sample_frac(df, fraction)`                                     | `df.sample(frac=fraction)`                                     |
| **<span style="color: #6F42C1;">case_when</span>** *(Nhiều điều kiện)*| `mutate(df, new_col = case_when(condition1 ~ value1, condition2 ~ value2, ...))` | `df['new_col'] = np.select([condition1, condition2, ...], [value1, value2, ...], default=default_value)` |
| **<span style="color: #6F42C1;">cummean</span>** *(Trung bình tích lũy)*| `mutate(df, new_col = cummean(col))`                            | `df['new_col'] = df['col'].expanding().mean()`                 |
| **<span style="color: #6F42C1;">row_number</span>** *(Số thứ tự)*| `mutate(df, row_num = row_number())`                            | `df['row_num'] = range(1, len(df)+1)`                          |
| **<span style="color: #6F42C1;">min_rank</span>** *(Xếp hạng min)*| `mutate(df, rank = min_rank(col))`                              | `df['rank'] = df['col'].rank(method='min')`                    |
| **<span style="color: #6F42C1;">dense_rank</span>** *(Xếp hạng dày)*| `mutate(df, rank = dense_rank(col))`                            | `df['rank'] = df['col'].rank(method='dense')`                  |

---

> **💡 Lưu ý:** Mặc dù nhiều chức năng có sẵn trực tiếp trong cả `dplyr` và `pandas`, một số có thể cần biến thể nhỏ hoặc hàm tùy chỉnh để đạt được kết quả tương tự.