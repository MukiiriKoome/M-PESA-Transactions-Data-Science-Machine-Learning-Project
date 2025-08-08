# M-PESA-Transactions-Data-Science-Machine-Learning-Project

## 📌 Overview

This project is a personal learning journey into **Data Science** and **Machine Learning**, using my own M-PESA transactions as the dataset.
Don’t worry—I'm just a student, so there are no *crazy millions* in here! 😉
The goal is to explore real-world data, practice cleaning and analysis, and experiment with machine learning techniques on something relatable.

---

## 🎯 Objectives

* Learn how to **extract, clean, and structure** transaction data
* Perform **Exploratory Data Analysis (EDA)** to uncover spending and income patterns
* Apply **data visualization** to make insights easier to understand
* Experiment with **machine learning** models for:

  * Expense prediction
  * Transaction categorization (e.g., Sent, Received, Buy Goods, etc.)
* Practice working with **pandas, matplotlib, seaborn, scikit-learn**, and other data tools

---

## 📂 Project Structure

```
.
├── data/               # Contains cleaned and raw transaction datasets
├── notebooks/          # Jupyter/Colab notebooks for analysis and modeling
├── README.md           # You’re reading this now :)
└── requirements.txt    # Python dependencies
```

---

## 🛠️ Tools & Libraries

* **Python** 🐍
* **Pandas** for data manipulation
* **Matplotlib & Seaborn** for visualization
* **Scikit-learn** for machine learning
* **Regex** for parsing M-PESA SMS messages
* **ElementTree** for XML parsing (when extracting messages from backups)

---

## 📊 Data

The dataset contains:

* **Type** (Sent, Received, Buy Goods, etc.)
* **Amount**
* **Date & Time**
* **Recipient/Sender**
* **Balance** (where available)

⚠️ **Note:** All sensitive personal information has been removed or anonymized before analysis.

---

## 📥 How I Got the Data

Since M-PESA doesn’t directly give you a CSV download of your transactions, I used the following method:

1. **Back up SMS messages**

   * On Android: Use **Google Drive Backup** or apps like [SMS Backup & Restore](https://play.google.com/store/apps/details?id=com.riteshsahu.SMSBackupRestore)
   * This will create an **XML file** containing all messages, including M-PESA transaction notifications.

2. **Download the XML file**

   * If using Google Drive backup, export/download it to your computer.
   * If using SMS Backup & Restore, save the file locally or in Google Drive.

3. **Load XML into Google Colab**

   ```python
   from xml.etree import ElementTree as ET

   # Parse XML file from Google Drive
   tree = ET.parse('/content/drive/MyDrive/mpesa_backup.xml')
   root = tree.getroot()
   ```

4. **Extract M-PESA messages using regex**

   * Look for messages where the `address` field is `"M-PESA"`
   * Use regular expressions to capture:

     * Amount
     * Transaction type (Sent, Received, Buy Goods)
     * Date & time
     * Recipient/Sender
     * Balance (optional)

   Example snippet:

   ```python
   import re

   for sms in root.findall('sms'):
       if sms.get('address') == 'M-PESA':
           msg = sms.get('body')
           match = re.search(r'Ksh([\d,]+\.\d{2})\s(sent|received)', msg.lower())
           if match:
               amount = float(match.group(1).replace(',', ''))
               transaction_type = match.group(2).capitalize()
   ```

5. **Convert to DataFrame**

   ```python
   import pandas as pd

   df = pd.DataFrame(transactions)  # transactions = list of dicts
   df.to_csv('mpesa_transactions.csv', index=False)
   ```

---

## 🚀 Learning Outcomes

By the end of this project, I’ll have:

* A deeper understanding of **data wrangling** techniques
* Experience in **EDA and visualization**
* Applied **ML models** on real-life data
* Insights into my own spending habits (which might be scary 😅)

---

## 📬 Contact

If you have suggestions or want to collaborate on data science learning projects:

* **Email:** [koomemukiiri@gmail.com](mailto:koomemukiiri@gmail.com)
* **GitHub:** [MukiiriKoome](https://github.com/MukiiriKoome)

---

💡 *This is a personal, educational project—no financial advice, no huge bank transactions, just learning with what I have!* 📚

---

