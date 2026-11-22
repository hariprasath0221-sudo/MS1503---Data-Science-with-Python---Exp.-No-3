# Experiment 3: Retail Sales and Profit Analysis Using Pandas

## Aim

To create a sample retail dataset, identify and handle missing values (`NaN`/`None`) and duplicate records, and compute summary statistics using Pandas in Python.

## Algorithm

1. **Start** the program.
2. **Import Library**: Import the `pandas` library as `pd` for tabular data cleaning and analysis.
3. **Initialize Raw Retail Dataset**: Create a Python dictionary `data` containing retail records (`Order_ID`, `Product`, `Region`, `Sales`, `Discount`, `Profit`) with deliberate missing (`None`) entries and duplicate rows.
4. **Construct DataFrame & Inspect**:
   * Convert `data` into a Pandas DataFrame `df` using `pd.DataFrame(data)`.
   * Print the original dataset and its initial dimensions (`df.shape`).
5. **Detect Missing Values**:
   * Count missing entries per column using `df.isnull().sum()`.
6. **Impute Missing Values**:
   * Replace missing numerical values in `Sales`, `Discount`, and `Profit` with their respective column means using `.fillna(df[col].mean())`.
   * Replace missing categorical values in `Region` with the column mode (most frequent category) using `.fillna(df["Region"].mode()[0])`.
7. **Remove Duplicate Records**:
   * Drop exact duplicate rows from `df` using `df.drop_duplicates()`.
8. **Display Cleaned Dataset & Summary Statistics**:
   * Print the cleaned DataFrame, updated dimensions (`df.shape`), and descriptive statistical metrics (`df.describe()`).
9. **Stop** the program.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation & Inspection** | `pd.DataFrame()` | Converts a Python dictionary into a labeled 2D tabular DataFrame |
| | `df.shape` | Returns the `(rows, columns)` dimensions before and after cleaning |
| | `df.isnull().sum()` | Counts the number of missing (`NaN`/`None`) values in each column |
| **Missing Value Imputation** | `df[col].fillna()` | Replaces missing values with a specified replacement value |
| | `df[col].mean()` | Calculates the arithmetic mean for numerical column imputation |
| | `df[col].mode()[0]` | Retrieves the most frequent category for categorical column imputation |
| **Deduplication & Summary** | `df.drop_duplicates()` | Identifies and removes duplicate rows from the DataFrame |
| | `df.describe()` | Generates count, mean, standard deviation, min, quartiles, and max for numerical features |

## Program

```python
# Cleaning and Preparing Retail Data using Pandas
import pandas as pd

# Show all columns when printing DataFrames
pd.set_option("display.max_columns", None)
pd.set_option("display.width", 200)

# Step 1: Create a sample retail dataset (with missing values and duplicates)
data = {
    "Order_ID": [1001, 1002, 1003, 1004, 1005, 1006, 1007, 1008, 1009, 1003, 1010, 1006],
    "Product":  ["Laptop", "Mouse", "Keyboard", "Monitor", "Printer", "Tablet",
                 "Phone", "Headset", "Webcam", "Keyboard", "Router", "Tablet"],
    "Region":   ["South", "North", None, "West", "South", "North",
                 "South", None, "East", None, "West", "North"],
    "Sales":    [55000, 800, 1500, 12000, None, 28000,
                 32000, 2500, 3000, 1500, None, 28000],
    "Discount": [0.10, 0.05, None, 0.08, 0.12, 0.15,
                 0.10, 0.05, None, None, 0.07, 0.15],
    "Profit":   [8000, 150, 300, None, 900, 4200,
                 5100, None, 450, 300, 700, 4200]
}

df = pd.DataFrame(data)
print("Original Dataset:")
print(df)
print("\nOriginal Shape:", df.shape)

# Step 2: Check for missing values
print("\nMissing Values per Column:")
print(df.isnull().sum())

# Step 3: Fill missing numeric values with column mean
for col in ["Sales", "Discount", "Profit"]:
    df[col] = df[col].fillna(df[col].mean())

# Step 4: Fill missing Region with mode (most frequent value)
df["Region"] = df["Region"].fillna(df["Region"].mode()[0])

print("\nDataset after Handling Missing Values:")
print(df)
print("\nMissing Values after Imputation:")
print(df.isnull().sum())

# Step 5: Remove duplicate records
print("\nNumber of duplicate rows:", df.duplicated().sum())
df = df.drop_duplicates()
print("\nCleaned Dataset (duplicates removed):")
print(df)
print("\nCleaned Shape:", df.shape)

# Step 6: Display summary statistics
print("\nSummary Statistics:")
print(df.describe())
```

## Output

```
Original Dataset:
    Order_ID   Product Region    Sales  Discount  Profit
0       1001    Laptop  South  55000.0      0.10  8000.0
1       1002     Mouse  North    800.0      0.05   150.0
2       1003  Keyboard    NaN   1500.0       NaN   300.0
3       1004   Monitor   West  12000.0      0.08     NaN
4       1005   Printer  South      NaN      0.12   900.0
5       1006    Tablet  North  28000.0      0.15  4200.0
6       1007     Phone  South  32000.0      0.10  5100.0
7       1008   Headset    NaN   2500.0      0.05     NaN
8       1009    Webcam   East   3000.0       NaN   450.0
9       1003  Keyboard    NaN   1500.0       NaN   300.0
10      1010    Router   West      NaN      0.07   700.0
11      1006    Tablet  North  28000.0      0.15  4200.0

Original Shape: (12, 6)

Missing Values per Column:
Order_ID    0
Product     0
Region      3
Sales       2
Discount    3
Profit      2
dtype: int64

Dataset after Handling Missing Values:
    Order_ID   Product Region    Sales  Discount  Profit
0       1001    Laptop  South  55000.0  0.100000  8000.0
1       1002     Mouse  North    800.0  0.050000   150.0
2       1003  Keyboard  North   1500.0  0.096667   300.0
3       1004   Monitor   West  12000.0  0.080000  2430.0
4       1005   Printer  South  16430.0  0.120000   900.0
5       1006    Tablet  North  28000.0  0.150000  4200.0
6       1007     Phone  South  32000.0  0.100000  5100.0
7       1008   Headset  North   2500.0  0.050000  2430.0
8       1009    Webcam   East   3000.0  0.096667   450.0
9       1003  Keyboard  North   1500.0  0.096667   300.0
10      1010    Router   West  16430.0  0.070000   700.0
11      1006    Tablet  North  28000.0  0.150000  4200.0

Missing Values after Imputation:
Order_ID    0
Product     0
Region      0
Sales       0
Discount    0
Profit      0
dtype: int64

Number of duplicate rows: 2

Cleaned Dataset (duplicates removed):
    Order_ID   Product Region    Sales  Discount  Profit
0       1001    Laptop  South  55000.0  0.100000  8000.0
1       1002     Mouse  North    800.0  0.050000   150.0
2       1003  Keyboard  North   1500.0  0.096667   300.0
3       1004   Monitor   West  12000.0  0.080000  2430.0
4       1005   Printer  South  16430.0  0.120000   900.0
5       1006    Tablet  North  28000.0  0.150000  4200.0
6       1007     Phone  South  32000.0  0.100000  5100.0
7       1008   Headset  North   2500.0  0.050000  2430.0
8       1009    Webcam   East   3000.0  0.096667   450.0
10      1010    Router   West  16430.0  0.070000   700.0

Cleaned Shape: (10, 6)

Summary Statistics:
         Order_ID         Sales   Discount  Profit
count    10.00000     10.000000  10.000000  10.000000
mean   1005.50000  16766.000000   0.091333  2466.000000
std       3.02765  17397.452687   0.030680  2587.646722
min      1001.00000    800.000000   0.050000   150.000000
25%      2625.000000   0.072500   512.500000
50%      1005.50000  14215.000000   0.096667  1665.000000
75%      1007.75000  25107.500000   0.100000  3757.500000
max      1010.00000  55000.000000   0.150000  8000.000000
```

## Result

The program successfully creates a retail dataset, identifies missing entries and duplicate rows, imputes missing values using mean and mode strategies, removes duplicates, and outputs a clean dataset ready for downstream analysis.
