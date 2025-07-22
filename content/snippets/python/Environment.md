---
title: Environment
---

# Environment setup

## 1. Using **conda**

### 1. Add Anaconda Portable to `PATH`

#### For **Command Prompt (cmd.exe)**

```cmd
set PATH=D:\anaconda3\condabin;%PATH%
```

#### For **PowerShell**

```powershell
$env:PATH = "D:\anaconda3\condabin;" + $env:PATH
```

### 2. Set Default `PATH` in Visual Studio Code

#### Step 1: Open VSCode Settings
1. **Open VSCode**.
2. Press `Ctrl + ,` to open the **Settings**.

#### Step 2: Edit `settings.json`
1. In the **Settings** search bar, type: **terminal.integrated.env.windows**.
2. Click on **Edit in settings.json** (you can also directly open `settings.json` by pressing `Ctrl + Shift + P` and typing "Preferences: Open Settings (JSON)").

#### Step 3: Add Anaconda Path to `settings.json`
In the `settings.json` file, add the following lines to include Anaconda's `condabin` in your `PATH`:

```json
{
    "terminal.integrated.env.windows": {
        "PATH": "D:\\anaconda3\\condabin;${env:PATH}"
    }
}
```

### 3. Create conda environment

#### 1. Quick create env using `conda create`
       
```cmd
conda create -n env_rdm python=3.10 pip ipykernel notebook
conda activate env_rdm
```

#### 2. Create env use `environment.yaml` file

- First, create `environment.yaml ` file with example content following
- Second, run command `conda env create -f environment.yaml`
- Optional, remove environment if needed `conda env remove -n env_ascore`
             
```yml
name: env_ascore
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.10
  - pandas
  - joblib
  - statsmodels
  - ipykernel
  - zipp  
  - pip
  - pip: 
    - optbinning==0.17.3
    - ortools==9.4.1874
# set https_proxy=10.1.33.23:8080
# set http_proxy=10.1.33.23:8080   
```

#### 3. Create env use `requirements.txt` file

```cmd
conda list --export > requirements.txt
conda install --file requirements.txt
```


### 4. Conda Common Commands

#### List All Conda Environments
This command displays a list of all available Conda environments on your system:

```sh
conda info --env
```
Alternatively, you can use:

```sh
conda env list
```

#### Remove a Conda Environment
To remove a specific Conda environment (e.g., `python38`):

```sh
conda deactivate  # Deactivate any active environment first
conda env remove -n python38
```

#### Activate a Conda Environment
To activate a specific Conda environment (e.g., `python38`):

```sh
conda activate python38
```

#### Clean Unused Libraries and Cache
To clean up unused libraries and cache, use:

```sh
conda clean --all  # Cleans all Conda caches
pip cache remove *  # Removes all pip caches
```

## 2. Create Environment for Jupyter Notebook

### 1. Use Conda to Create a New Environment
You can create a new environment in Conda for use with Jupyter Notebook. Replace `python38` with the desired environment name and `3.x` with the desired Python version.

```sh
conda create -n python38 python=3.x
```

### 2. Use `ipython` to Add the Environment to Jupyter

After activating the environment, use the `ipython` command to install the environment's kernel for Jupyter Notebook:

```sh
conda activate python38
ipython kernel install --user --name=python38
```

This will make the environment available in Jupyter Notebook as an option when selecting kernels.

### 3. Remove Jupyter Notebook Environment (Run as Administrator)
To remove the environment's kernel from Jupyter, list all the installed kernels and then uninstall the specific one. You may need administrator privileges for this step.

1. **List the installed kernels:**

```sh
jupyter kernelspec list
```

2. **Uninstall the kernel:**

```sh
jupyter kernelspec uninstall python38
```

## 3. Install Packages in **OFFLINE** Mode with `pip`

### 1. Install Offline Packages Using `requirements.txt`

#### Step 1: Export Installed Packages to `requirements.txt`
If you want to create a `requirements.txt` file containing the list of installed packages, you can use this command:

```cmd
pip list --format=freeze > requirements.txt
```

This will export the list of currently installed packages and their versions into a `requirements.txt` file.

#### Step 2: Create a `wheel` Folder
Create a folder where the downloaded `.whl` (wheel) files will be stored. For example, you can create a folder named `wheel`:

```cmd
mkdir D:\wheel
```

#### Step 3: Download Dependencies into the `wheel` Folder
Run the following command to download the dependencies listed in `requirements.txt` into the `wheel` folder:

```cmd
pip download -r requirements.txt -d D:\wheel
```

This command will download all the required packages and their dependencies into the `wheel` directory for offline installation.

#### Step 4: Install Packages from the `wheel` Folder
Once you have downloaded all necessary packages, you can install them offline by running:

```cmd
pip install -r requirements.txt --find-links=D:\wheel --no-index
```

- `--find-links=D:\wheel`: Instructs `pip` to look for package files in the `wheel` folder.
- `--no-index`: Disables checking online package indexes (e.g., PyPI) to ensure installation from offline files.

---

### 2. Install Offline Linux Packages

When downloading Python packages for Linux (or another platform) while being on a different platform (e.g., Windows), you can specify the platform and Python version.

#### Case 1: Activate the Same Python Version
If you are working with the same Python version as required (e.g., Python 3.7), activate the appropriate environment and run the following command to download the necessary package for Linux:

```cmd
pip download --platform manylinux1_x86_64 --only-binary=:all: --no-binary=:none: pandas
```

- `--platform manylinux1_x86_64`: Specifies the platform for the Linux package.
- `--only-binary=:all:`: Ensures only binary files (like wheels) are downloaded.
- `--no-binary=:none:`: Prevents downloading source distributions, ensuring only precompiled binaries are fetched.

#### Case 2: Specify a Python Version
If you are using a different Python version, specify the required version using the `--python-version` flag:

```cmd
pip download --platform manylinux1_x86_64 --only-binary=:all: --python-version=38 --no-binary=:none: pandas
```

- `--python-version=38`: Specifies the Python version (e.g., 3.8) for which you need to download packages.

## 4. Other Utility Commands

### 1. Check for Dependency Issues
To check for problems with package dependencies:

```cmd
python -m pip check
```

To save a list of all installed packages to `requirements.txt`:

```cmd
pip freeze > requirements.txt
```

### 2. Change Jupyter Notebook Theme
To change the theme of Jupyter Notebook (for example, applying the `onedork` theme with custom font sizes and cell width):

```cmd
jt -t onedork -fs 13 -altp -tfs 14 -nfs 14 -cellw 88% -T
```

- `-fs`: Font size.
- `-tfs`: Title font size.
- `-nfs`: Notebook name font size.
- `-cellw`: Cell width.
- `-T`: Show or hide the toolbar.

To install Jupyter themes:

```cmd
pip install jupyterthemes
```

### 3. Install Jupyter Notebook Extensions
To add useful features like a table of contents, code folding, and more, install the extensions:

```cmd
pip install jupyter_contrib_nbextensions
pip install jupyter_nbextensions_configurator
```

Then, set them up and enable them:

```cmd
jupyter contrib nbextension install --user
jupyter nbextensions_configurator enable --user
```