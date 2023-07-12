# 1. Setup environment

## 1.1. Using **conda**

### 1.1.1. Create conda environment

- Create env by common command line

```python
conda create -n python38 python=3.8.5 pip=20.2.4 ipykernel notebook
conda activate python38
```

- Create env use `environment.yaml` file

```
name: env_ascore
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.8
  - pandas==1.4.4  
  - joblib==1.1.0
  - statsmodels==0.13.2
  - ipykernel
  - zipp  
  - pip
  - pip: 
    - optbinning==0.17.3
    - ortools==9.4.1874
# conda env create -f environment.yaml  
# conda env remove -n env_ascore
# set https_proxy=10.1.33.23:8080
# set http_proxy=10.1.33.23:8080
# conda install -n env_ascore ipykernel --update-deps --force-reinstall
```

- Create env use `requirements.txt` file

```
conda list --export > requirements.txt
conda install --file requirements.txt
```

### 1.1.2. Conda common commands

-  Conda environment list

```python
conda info --env
```

- Remove conda environment

```python
conda deactivate
conda env remove -n python38
```

- Activate conda environment

```python
conda activate python38
```
- Clean unused library

```
conda clean --all
pip cache remove *
```

## 1.2. Create environment for jupyter notebook

### 1.2.1. create

```python
conda activate python38
ipython kernel install --user --name=python38
```
 

### 1.2.2. Remove jupyter notebook environment (require run as administrator)

```python
jupyter kernelspec list
jupyter kernelspec uninstall python38 
```

# 2. Install packages

## 2.1. Install OFFLINE packages using requirements.txt 

- Step 1: Input to `requirements.txt` file in current directory.  Eg. content `"jupyter-contrib-nbextensions==0.5.1"`

- Step 2: Create folder `wheel` (Eg. D:\wheel)

- Step 3: Run following command to download dependencies packages to folder `wheel`

```python
pip download -r requirements.txt -d wheel
```

- Step 4: Run following command to install


```
pip install -r requirements.txt --find-links=D:\wheel --no-index
```

## 2.2. Install OFFLINE Linux package

Activate same version python (i.e 3.7.0) and type command following

```
pip download --platform manylinux1_x86_64 --only-binary=:all: --no-binary=:none: pandas
```

## 2.3. Export requirements

```
pip list --format=freeze > requirements.txt
```

# 3. Install Extension for jupyter notebook

- nbextension

```
pip install jupyter_contrib_nbextensions
pip install jupyter_nbextensions_configurator
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user
```

# 4. Other ultilities command

#### check dependencies

```
python -m pip check 
pip freeze > requirements.txt
```

#### install pycaret

```
pip install pycaret --use-feature=2020-resolver
```

#### Themes

- jupyter notebook

```
jt -t onedork -fs 13 -altp -tfs 14 -nfs 14 -cellw 88% -T
```


# 5. Pandas

- case when

```python
df['new_column'] = np.where(df['col2']<9, 'value1',
                   np.where(df['col2']<12, 'value2',
                   np.where(df['col2']<15, 'value3', 'value4')))
```

- clean names

```python
X.columns = X.columns.str.translate("".maketrans({"[":"{", "]":"}","<":"^"}))
```

- rename

```python
df.columns = df.columns.str.lower()
```

- binning

```python
df['Cat Age'] = pd.cut(x=df['Age'], bins=[0, 25, 30, 35, 40, 45, 50, 75])
```

- groupby stratify

```python
df.groupby('target', group_keys=False).apply(lambda x: x.sample(frac=0.8))  
```
- groupby partition (transform)
```python
df['new'] = df.groupby('group_var')['value_var'].transform('mean')
df['new'] = df.groupby('group_var')['value_var'].transform(lambda x: some function)
```
- read data

```python
appended_data = []
for infile in glob.glob("*.xlsx"):
    data = pandas.read_excel(infile)
    # store DataFrame in list
    appended_data.append(data)

# Use pd.concat to merge a list of DataFrame into a single big DataFrame.
appended_data = pd.concat(appended_data)
appended_data = [df.set_index('ID') for df in appended_data]
appended_data = pd.concat(appended_data)
```

- filter

```python
df[~df['name'].isin(list1)]
df[df['name'].isna()]
df[df['name'].notna()]

#filter for rows where team name is not in one of several columns
df[~df[['star_team', 'backup_team']].isin(values_list).any(axis=1)] 

```

- convert

```python
# pd.to_numeric
# pd.factorize
# df['STRING'].astype(str)
# pd.to_datetime(df['DATE'], format='%d%m%Y')
```

- Excel date

```python
import functools as ft
fn_convert_date = ft.partial(xlrd.xldate_as_datetime, datemode=0)
df['DATE'].apply(fn_convert_date).dt.year
```
- aggregate

```python
df = df.groupby('ID').agg('first')
```

```python
def fn_describe(df):
    tbl = df.describe(include='all')
    tbl.loc['dtype'] = df.dtypes
    tbl.loc['total'] = len(df)
    tbl.loc['%null'] = df.isnull().mean() * 100
    tbl.loc['nbr.zero'] = (df == 0).sum(axis=1)
    tbl.loc['%zero'] = (df == 0).sum(axis=1)/len(dat)    
    tbl = tbl.T
    tbl['nbr.null'] = tbl['total'] - tbl['count']
    tbl['nbr.top'] = tbl['freq'] 
    tbl['%top'] = tbl['freq']/tbl['total']*100
    tbl = tbl[['dtype', 'total', 'nbr.null', '%null', 'nbr.zero', '%zero', 'mean', 'std', 'min', 'max', 'unique', 'top', 'nbr.top', '%top']]
    return tbl
```

- date

```python
# difference of month
df['nb_months'] = ((df.dates1 - df.dates2)/np.timedelta64(1, 'M'))
df['nb_months'] = df['nb_months'].astype(int)
# difference of day
df['Number_of_days'] = ((df.dates1 - df.dates2)/np.timedelta64(1, 'D'))
df['Number_of_days'] = df['Number_of_days'].astype(int)
```

- mapping 

```python
mapping = dict(zip(df[col],df['temp2']))
temp_df[col] = temp_df[col].map(mapping)
```

- Apply to all values except missing

```python
s.apply(lambda a: a+2 if pd.notnull(a) else a)
```

- fillna

```python
dat['MOBILE'] = dat['MOBILE'].fillna(dat['MOBILE2'])
```

- to_excel

```python
pred_train.reset_index(inplace=True, drop=True)
pred_test.reset_index(inplace=True, drop=True)
with pd.ExcelWriter(product['t_pred']) as writer:
    pred_train.to_excel(writer, sheet_name='pred_train')
    pred_test.to_excel(writer, sheet_name='pred_test')    
```

# 6. Join

#### reduce merge

- `pandas.concat`

```python
dfs = [df0, df1, df2, ..., dfN]
# require set_index, not using key
dfs = [df.set_index('name') for df in dfs]
# can't not run if index not unique 
dfs = pd.concat(dfs, join='outer', axis = 1) 
```


- `functools.reduce`

```python
# still run with index not unique 
import functools as ft
dfs = ft.reduce(lambda left, right: pd.merge(left, right, on='name', how = 'outer'), dfs)
```
- `join`

```python
# cant not run if index not unique 
dfs = [df.set_index('name') for df in dfs]
dfs[0].join(dfs[1:], how = 'outer')
```
# 7. Files and folder

```python
list_files = glob.glob(".data/*.xlsx")
```

# 8. List

# Delete multiple elements from list python
```python
unwanted = [1, 3]
for ele in sorted(unwanted, reverse = True):
    del list1[ele]
```

# 9. Regex

```python
import re

# Validate number
number_pattern = "^\\d+$"
re.match(number_pattern, '42') # Returns Match object
re.match(number_pattern, 'notanumber') # Returns None

# Extract number from a string
number_extract_pattern = "\\d+"
re.findall(number_extract_pattern, 'Your message was viewed 203 times.') # returns ['203']
```

# 10. Database

## Connect to database
```python
import pandas as pd
import pyodbc
import sqlalchemy as sa
import urllib
from sqlalchemy import create_engine, event
from sqlalchemy.engine.url import URL

server = 'VM-DC-JUMPSRV77\\IFRS9' 
database = 'DATA' 
username = 'username' 
password = '@@@@@@' 
    
params = urllib.parse.quote_plus("DRIVER={SQL Server};"
                                     "SERVER="+server+";"
                                     "DATABASE="+database+";"
                                     "UID="+username+";"
                                     "PWD="+password+";")
    
engine = sa.create_engine("mssql+pyodbc:///?odbc_connect={}".format(params))
```

## Read/push table to database

```python
# read data
df_test = pd.read_sql('SELECT top 5 * FROM b_tmp_cl020', engine)
# push data
df_test.to_sql('binh_test', engine, if_exists = 'append')
```

## sqlite3

```python
con = sqlite3.connect("data/mydata.sqlite")

cur = con.cursor()

# The result of a "cursor.execute" can be iterated over by row
for row in cur.execute('SELECT * FROM tbl;'):
    print(row)

# Be sure to close the connection
con.close()
```

# 11. Writing shorthand statements

- lambda

```python
# lambda statement
foo = lambda a: a+3
foo(10)

# Self called Lambda
(lambda a: a+3)(8)
```

- List Comprehension

```python
[i for i in range(10) if i%2==0]
```

- Dict Comprehension

```python
mylist = ['MANGO', 'APPLE', 'ORANGE']
d ={i.lower(): 2 for i in mylist}
```

- String Concatenation  with delimiter

```python
"_".join(["how", "are", "you"])
```

# 12. API

### JSON file

```python
# Open JSON file    
try:    
    with open ('data/sample.json', "r") as f:   
        data = json.load(f)
except IOError:
    print('cannot open file')  
    
# save
with open('data/sample.json', 'w') as f:
    json.dump(data, f)
```

# 99. Equivalent R

- `functools` ~ `purrr`
