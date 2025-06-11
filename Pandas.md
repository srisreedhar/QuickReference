


# Pandas Data Manipulation Functions

Below is a table of common Pandas functions for data manipulation, including descriptions, example commands, and their outputs. The examples use a sample DataFrame with toy car data:

```python
import pandas as pd
data = {
    'Color': ['Red', 'Blue', 'Red', 'Blue', 'Green'],
    'Size': ['Small', 'Big', 'Medium', 'Small', 'Big'],
    'Price': [10, 20, 15, 12, 25]
}
df = pd.DataFrame(data)
```

| Tasks | Functions | Description | Example Command | Example Output |
|-------|-----------|-------------|-----------------|----------------|
| Extract Column Names | `df.columns` | Returns the column labels of the DataFrame. | `df.columns` | `Index(['Color', 'Size', 'Price'], dtype='object')` |
| Select first 2 rows | `df.iloc[:2]` | Selects the first two rows using integer-based indexing. | `df.iloc[:2]` | `   Color  Size  Price\n0   Red  Small     10\n1  Blue    Big     20` |
| Select first 2 columns | `df.iloc[:,:2]` | Selects the first two columns using integer-based indexing. | `df.iloc[:,:2]` | `   Color  Size\n0   Red  Small\n1  Blue    Big\n2   Red  Medium\n3  Blue  Small\n4 Green    Big` |
| Select columns by name | `df.loc[:,["col1","col2"]]` | Selects specific columns by their names using label-based indexing. | `df.loc[:,["Color","Price"]]` | `   Color  Price\n0   Red     10\n1  Blue     20\n2   Red     15\n3  Blue     12\n4 Green     25` |
| Select random no. of rows | `df.sample(n=10)` | Randomly selects a specified number of rows (e.g., 10). | `df.sample(n=2)` | `(Random, e.g.)\n   Color  Size  Price\n3  Blue  Small     12\n0   Red  Small     10` |
| Select fraction of random rows | `df.sample(frac=0.2)` | Randomly selects a fraction of rows (e.g., 20% of the DataFrame). | `df.sample(frac=0.2)` | `(Random, e.g.)\n   Color Size  Price\n4 Green  Big     25` |
| Rename the variables | `df.rename()` | Renames columns or index labels using a dictionary or function. | `df.rename(columns={'Color': 'Car_Color'})` | `  Car_Color  Size  Price\n0      Red  Small     10\n1     Blue    Big     20\n2      Red  Medium     15\n3     Blue  Small     12\n4    Green    Big     25` |
| Selecting a column as index | `df.set_index()` | Sets a column (or columns) as the DataFrame index. | `df.set_index('Color')` | `       Size  Price\nColor\nRed    Small     10\nBlue     Big     20\nRed   Medium     15\nBlue   Small     12\nGreen    Big     25` |
| Removing rows or columns | `df.drop()` | Removes specified rows or columns by labels. | `df.drop(columns='Size')` | `   Color  Price\n0   Red     10\n1  Blue     20\n2   Red     15\n3  Blue     12\n4 Green     25` |
| Sorting values | `df.sort_values()` | Sorts the DataFrame by specified column(s) in ascending or descending order. | `df.sort_values('Price')` | `   Color  Size  Price\n0   Red  Small     10\n3  Blue  Small     12\n2   Red  Medium     15\n1  Blue    Big     20\n4 Green    Big     25` |
| Grouping variables | `df.groupby()` | Groups data by specified columns for aggregation (e.g., sum, count, mean). | `df.groupby('Color')['Price'].sum()` | `Color\nBlue     32\nGreen    25\nRed      25\nName: Price, dtype: int64` |
| Filtering | `df.query()` | Filters rows using a query string (e.g., `"col1 > 5"`). | `df.query('Price > 15')` | `   Color Size  Price\n1  Blue  Big     20\n4 Green  Big     25` |
| Finding the missing values | `df.isnull()` | Returns a boolean DataFrame indicating missing (NaN) values. | `df.isnull()` | `   Color  Size  Price\n0  False False  False\n1  False False  False\n2  False False  False\n3  False False  False\n4  False False  False` |
| Dropping the missing values | `df.dropna()` | Removes rows or columns with missing values. | `df.dropna()` | `(No missing values, returns same df)\n   Color  Size  Price\n0   Red  Small     10\n1  Blue    Big     20\n2   Red  Medium     15\n3  Blue  Small     12\n4 Green    Big     25` |
| Removing the duplicates | `df.drop_duplicates()` | Removes duplicate rows based on specified columns. | `df.drop_duplicates(subset='Color')` | `   Color  Size  Price\n0   Red  Small     10\n1  Blue    Big     20\n4 Green    Big     25` |
| Creating dummies | `pd.get_dummies()` | Converts categorical variables into dummy/indicator variables (one-hot encoding). | `pd.get_dummies(df['Color'])` | `   Blue  Green  Red\n0     0      0    1\n1     1      0    0\n2     0      0    1\n3     1      0    0\n4     0      1    0` |
| Ranking | `df.rank()` | Assigns ranks to values in a column, handling ties as specified. | `df['Price'].rank()` | `0    1.0\n1    4.0\n2    3.0\n3    2.0\n4    5.0\nName: Price, dtype: float64` |
| Cumulative sum | `df.cumsum()` | Computes the cumulative sum of values in a column. | `df['Price'].cumsum()` | `0    10\n1    30\n2    45\n3    57\n4    82\nName: Price, dtype: int64` |
| Quantiles | `df.quantile()` | Calculates quantiles (e.g., median, 25th percentile) for columns. | `df['Price'].quantile(0.5)` | `15.0` |
| Selecting numeric variables | `df.select_dtypes()` | Selects columns based on data type (e.g., numeric, object). | `df.select_dtypes(include='int64')` | `   Price\n0     10\n1     20\n2     15\n3     12\n4     25` |
| Concatenating two DataFrames | `pd.concat()` | Concatenates DataFrames vertically or horizontally. | `pd.concat([df, df])` | `   Color  Size  Price\n0   Red  Small     10\n1  Blue    Big     20\n2   Red  Medium     15\n3  Blue  Small     12\n4 Green    Big     25\n0   Red  Small     10\n1  Blue    Big     20\n2   Red  Medium     15\n3  Blue  Small     12\n4 Green    Big     25` |
| Merging on basis of common variable | `pd.merge()` | Merges two DataFrames based on common columns or indices. | `df2 = pd.DataFrame({'Color': ['Red', 'Blue'], 'Type': ['Sport', 'Sedan']})\npd.merge(df, df2, on='Color')` | `  Color  Size  Price   Type\n0   Red  Small     10  Sport\n1   Red  Medium     15  Sport\n2  Blue    Big     20  Sedan\n3  Blue  Small     12  Sedan` |
| Filling missing values | `df.fillna()` | Replaces missing values with a specified value or method. | `df['Price'].fillna(0)` | `(No missing values, returns same)\n0    10\n1    20\n2    15\n3    12\n4    25\nName: Price, dtype: int64` |
| Replacing values | `df.replace()` | Replaces specific values in the DataFrame with new values. | `df['Color'].replace('Red', 'Yellow')` | `0  Yellow\n1    Blue\n2  Yellow\n3    Blue\n4   Green\nName: Color, dtype: object` |
| Applying a function | `df.apply()` | Applies a function along an axis (rows or columns) of the DataFrame. | `df['Price'].apply(lambda x: x * 2)` | `0    20\n1    40\n2    30\n3    24\n4    50\nName: Price, dtype: int64` |
| Mapping values | `df.map()` | Applies a function or dictionary mapping to a Series (single column). | `df['Size'].map({'Small': 1, 'Medium': 2, 'Big': 3})` | `0    1\n1    3\n2    2\n3    1\n4    3\nName: Size, dtype: int64` |
| Pivot table | `df.pivot_table()` | Creates a pivot table with aggregated values based on specified columns. | `df.pivot_table(values='Price', index='Color', aggfunc='mean')` | `       Price\nColor\nBlue    16.0\nGreen   25.0\nRed     12.5` |
| Melting DataFrame | `pd.melt()` | Transforms a wide DataFrame into a long format. | `pd.melt(df, id_vars=['Color'], value_vars=['Price'])` | `   Color variable  value\n0   Red   Price     10\n1  Blue   Price     20\n2   Red   Price     15\n3  Blue   Price     12\n4 Green   Price     25` |
| Transposing DataFrame | `df.transpose()` or `df.T` | Swaps rows and columns of the DataFrame. | `df.T` | `          0     1       2     3      4\nColor   Red  Blue     Red  Blue  Green\nSize  Small   Big  Medium Small    Big\nPrice    10    20      15    12     25` |
| Adding new column | `df.assign()` | Creates a new column with a specified value or computation. | `df.assign(Discounted_Price=df['Price'] * 0.9)` | `   Color  Size  Price  Discounted_Price\n0   Red  Small     10              9.0\n1  Blue    Big     20             18.0\n2   Red  Medium     15             13.5\n3  Blue  Small     12             10.8\n4 Green    Big     25             22.5` |
| String operations | `df.str.*` | Applies string methods (e.g., `lower()`, `strip()`) to a column of strings. | `df['Color'].str.lower()` | `0     red\n1    blue\n2     red\n3    blue\n4   green\nName: Color, dtype: object` |
| Converting data types | `df.astype()` | Converts the data type of a column (e.g., to integer, float). | `df['Price'].astype(float)` | `0    10.0\n1    20.0\n2    15.0\n3    12.0\n4    25.0\nName: Price, dtype: float64` |
| Clipping values | `df.clip()` | Trims values to a specified minimum and maximum range. | `df['Price'].clip(lower=12, upper=20)` | `0    12\n1    20\n2    15\n3    12\n4    20\nName: Price, dtype: int64` |
| Binning data | `pd.cut()` | Groups continuous data into discrete bins (e.g., age groups). | `pd.cut(df['Price'], bins=[0, 15, 30], labels=['Low', 'High'])` | `0     Low\n1    High\n2     Low\n3     Low\n4    High\nName: Price, dtype: category` |
| Crosstab | `pd.crosstab()` | Computes a cross-tabulation of two (or more) factors. | `pd.crosstab(df['Color'], df['Size'])` | `Size   Big  Medium  Small\nColor\nBlue     1       0      1\nGreen    1       0      0\nRed      0       1      1` |
| Shifting rows | `df.shift()` | Shifts rows or columns by a specified number of periods. | `df['Price'].shift(1)` | `0     NaN\n1    10.0\n2    20.0\n3    15.0\n4    12.0\nName: Price, dtype: float64` |
| Rolling calculations | `df.rolling()` | Performs rolling window calculations (e.g., moving average). | `df['Price'].rolling(window=2).mean()` | `0     NaN\n1    15.0\n2    17.5\n3    13.5\n4    18.5\nName: Price, dtype: float64` |
| Exploding lists | `df.explode()` | Expands lists within a column into separate rows. | `df2 = pd.DataFrame({'Color': ['Red', 'Blue'], 'Sizes': [['Small', 'Medium'], ['Big']]})\ndf2.explode('Sizes')` | `  Color  Sizes\n0   Red  Small\n0   Red Medium\n1  Blue    Big` |
| Counting unique values | `df.value_counts()` | Counts unique values in a column or combination of columns. | `df['Color'].value_counts()` | `Color\nRed      2\nBlue     2\nGreen    1\nName: count, dtype: int64` |



> More coming soon
