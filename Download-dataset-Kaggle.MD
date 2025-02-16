# 📥 Download Kaggle Dataset Directly to Google Colab

This guide explains how to download datasets directly from Kaggle into Google Colab without manually uploading files.

---

## 🚀 Step 1: Install & Set Up Kaggle API

First, install the `kaggle` library:

```bash
!pip install kaggle
```

Now, upload your `kaggle.json` API key:

```python
from google.colab import files
files.upload()  # Select the kaggle.json file when prompted
```

Move it to the correct directory:

```bash
!mkdir -p ~/.kaggle
!mv kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json
```

---

## 🔽 Step 2: Download the Dataset

Use the following command to download the dataset:

```bash
!kaggle datasets download -d mathchi/diabetes-data-set
```

Make sure to replace `mathchi/diabetes-data-set` with the correct Kaggle dataset path.

---

## 📂 Step 3: Unzip the Dataset

Extract the downloaded dataset:

```bash
!unzip diabetes-data-set.zip -d /content/
```

This will extract the files to `/content/` in Colab.

---

## 📊 Step 4: Load the Dataset in Pandas

If the dataset is a CSV file, load it into a Pandas DataFrame:

```python
import pandas as pd

df = pd.read_csv("/content/diabetes.csv")  # Update filename if needed
print(df.head())  # Show first 5 rows
```

---

## ✅ Summary
1. 📥 Install `kaggle` and upload `kaggle.json`
2. 🔑 Move `kaggle.json` to the correct directory
3. ⬇️ Download dataset using `kaggle datasets download`
4. 📂 Unzip and load it in Pandas

Now, you have successfully downloaded a Kaggle dataset **directly into Google Colab**! 🚀🔥

---

### 📝 Notes:
- If the dataset is in another format (e.g., `.json`, `.xlsx`), use the appropriate Pandas function to read it.
- Ensure your dataset name and file path are correct before running commands.
