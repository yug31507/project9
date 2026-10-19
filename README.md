# Sales Data Analysis Program Overview

## 1. Overview
This Python script defines a `SalesData` class designed for interactive data analysis, cleaning, manipulation, and visualization of tabular data (such as video game sales datasets) using the Pandas, NumPy, Matplotlib, and Seaborn libraries.

The code features menu-driven routines that validate user inputs, handle missing data, perform mathematical and statistical operations, transform DataFrames, and prepare visualizations.

---

## 2. Key Dependencies
* **`pandas`**: DataFrame management, data reading, merging, grouping, and cleaning.
* **`numpy`**: Numeric operations and data type identification.
* **`matplotlib.pyplot`**: Plot creation and rendering.
* **`seaborn`**: Enhanced statistical data visualization.

---

## 3. Class Structure & Functionalities

### Class: `SalesData`

#### Attributes
* `self.data`: Stores the primary loaded Pandas DataFrame (initialized to `None`).
* `self.fig`: Placeholder for figure objects during plot generation.

---

### Helper Methods

* `check_data()`: Verifies whether a dataset is currently loaded into `self.data`. Returns `True` if loaded, or prints an error message and returns `False` if `None`.
* `get_int(prompt)`: A static utility method to prompt the user for integer inputs safely using `try-except` blocks to catch `ValueError` exceptions.

---

### Core Operational Methods

#### 1. `load_data(file_path)`
* Reads a target CSV file path into `self.data`.
* Includes exception handling for `FileNotFoundError`, `EmptyDataError`, `ParserError`, and general exceptions.
* Displays total row and column counts upon successful loading.

#### 2. `explore_data()`
* Interactively displays properties of the loaded dataset.
* **Options:**
  1. Display first 5 rows (`.head()`)
  2. Display last 5 rows (`.tail()`)
  3. List column names (`.columns`)
  4. Show column dtypes (`.dtypes`)
  5. Print concise summary (`.info()`)

#### 3. `clean_data()`
* Provides methods for inspecting and addressing missing values (`NaN`s).
* **Options:**
  1. Display rows containing missing values.
  2. Impute numeric missing values with their column means.
  3. Drop rows containing missing values (`.dropna()`).
  4. Replace all missing values with a user-specified static value.

#### 4. `mathematical_operations()`
* Performs element-wise arithmetic operations on a selected numeric column.
* **Supported Operations:** Addition, Subtraction, Multiplication, Division (with zero-division checks), Modulus, Exponentiation/Power, Square, Square Root (with negative-value checks), and Absolute Value.

#### 5. `combine_data()`
* Combines the current dataset with a second external CSV file.
* **Support Modes:**
  1. **Concatenation:** Stacks rows from both datasets vertically.
  2. **Merging:** Performs an inner join using a shared key column.
* Option to overwrite `self.data` with the resulting merged DataFrame.

#### 6. `split_data()`
* Splits the DataFrame into two separate DataFrames based on matching or non-matching criteria for a target column value.
* Provides an option to export both subsets to CSV files: `vgsales_group_1.csv` and `vgsales_group_2.csv`.

#### 7. `search_sort_filter()`
* Provides tools for querying and sorting the dataset:
  1. **Search:** Match exact values in a target column.
  2. **Sort:** Order rows ascending or descending based on a chosen column.
  3. **Numeric Filtering:** Filter rows where values in a numeric column exceed a threshold.
  4. **Categorical Filtering:** Filter rows by categorical values.

#### 8. `advanced_operations()`
* Performs structural DataFrame transformations:
  1. **Pivot Table:** Aggregates numeric values by index groups (`sum`, `mean`, `count`).
  2. **Reset Index:** Re-indexes the current DataFrame.
  3. **Group-based Transformation:** Appends a `Group_Average` column using `.groupby().transform("mean")`.
  4. **Column Renaming:** Safely renames columns with validation against empty names or collisions.

#### 9. `statistical_analysis()`
* Generates quick statistical summaries over numeric columns:
  * **Measures of Central Tendency:** Sum, Mean, Median.
  * **Measures of Dispersion:** Standard Deviation, Variance, Min/Max, Percentiles.
  * **Relational & Group Statistics:** Correlation matrices, full descriptive summaries (`.describe()`), and grouped aggregate metrics (`.agg()`).

#### 10. `visualize_data()`
* Interactively prompts the user to select plot options (Bar, Line, Scatter, Pie, Histogram, Stack Plot) for numeric analysis.

---

## 4. Error Handling & Robustness
* **Safety Checks:** Verifies `self.data` existence prior to executing actions.
* **Type Filtering:** Restricts numerical operations and statistical options to valid numeric columns using `select_dtypes(include=np.number)`.
* **Input Guardrails:** Validates choice ranges, column presence, division by zero, and real-number constraints for square roots.
