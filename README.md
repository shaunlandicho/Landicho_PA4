# PROGRAMMING ASSIGNMENT 4

**Made by: Shaun Jakob C. Landicho | 2ECE-A**

This repository contains Programming Assignment 4 for "Advanced Computer Programming". The project covers data manipulation, conditional filtering, summary analytics, and visualization of student board exam performance using `pandas` and `matplotlib`.

---

# **1. Dataset Setup & Overview**

Loaded the `board2.csv` dataset into a DataFrame and computed the overall average score for each student across `Math`, `Electronics`, `GEAS`, and `Communication`.

### **Functions and Methods Used:**
* `pd.read_csv()` – Loads the CSV dataset into a Pandas DataFrame.
* `.mean(axis=1)` – Calculates the row-wise mean across specified subject columns to populate the `Average` column.
* `.describe()` – Generates summary statistics for all numerical columns in the DataFrame.

```python
import pandas as pd
import matplotlib.pyplot as plt

# Read CSV and calculate average grade per student
df = pd.read_csv('board2.csv')
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

# Summary statistics
df.describe()

```

---

# **2. Visayas Communication Dataframe**

Extracted a subset containing students whose hometown is **Visayas** and whose track is **Communication**, displaying only their `Name`, `Gender`, `Math`, `Electronics`, and overall `Average` score.

### **Functions and Methods Used:**

* Boolean Indexing (`&`) – Filters rows matching multiple condition criteria (`Hometown == 'Visayas'` and `Track == 'Communication'`).


* `len()` – Counts the total number of resulting records.



```python
VisComm = df[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication')][
    ['Name', 'Gender', 'Math', 'Electronics', 'Average']
]
print(f"Number of Rows: ", (len(VisComm)))
VisComm

```

---

# **3. Visayas Female Dataframe**

Created a filtered view of **Female** students from **Visayas**, selecting their `Name`, `Track`, `GEAS`, `Electronics`, and `Average` scores. A secondary filter was applied to display only those with an average score of at least 60.

### **Functions and Methods Used:**

* `display()` – Renders DataFrames cleanly within Jupyter Notebook outputs.


* Comparative Filtering (`>= 60`) – Filters rows based on a minimum threshold score.



```python
VisFemale = df[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female')][
    ['Name', 'Track', 'GEAS', 'Electronics', 'Average']
]
display(VisFemale)

# Filter for average score >= 60
print("\nVisayas Female Students with Average of at least 60:")
display(VisFemale[VisFemale['Average'] >= 60])

```

---

# **4. Category-Average Visualization**

Calculated the mean average scores grouped by `Track`, `Gender`, and `Hometown`, then generated comparative bar charts to visualize performance trends.

### **Functions and Methods Used:**

* `.groupby()` – Groups data by specified categorical columns.


* `.reset_index()` – Converts grouped index objects back into DataFrame columns.


* `plt.subplots()` – Creates a multi-panel figure layout for visual comparison.



```python
track_avg = df.groupby('Track')['Average'].mean().reset_index()
gender_avg = df.groupby('Gender')['Average'].mean().reset_index()
hometown_avg = df.groupby('Hometown')['Average'].mean().reset_index()

display("Track Summary:", track_avg)
display("Gender Summary:", gender_avg)
display("Hometown Summary:", hometown_avg)

# Visualization
fig, axes = plt.subplots(1, 3, figsize=(15, 5), sharey=True)

axes[0].bar(track_avg['Track'], track_avg['Average'], color='skyblue')
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Average')

```

---

Thank you for reading!

To run the main notebook file, clone this repository, open `PA #4.ipynb` on Jupyter Notebook or Google Colab, and run all cells.
