# Exploring the World of Pandas DataFrame


## Introduction to the Pandas Library

The pandas library is Python's solution for tabular data operations, packing more punch for data analysis than NumPy, which is skewed towards numerical computations. Pandas houses two fundamental data structures: the Series (1D) and the DataFrame (2D). Often, the DataFrame is the go-to choice. Let's start by importing pandas:

```Python

import pandas as pd
```
Here, pd serves as a standard alias for pandas.

## Creating a DataFrame

Building a DataFrame in pandas is straightforward. It can be created from a dictionary, list, or NumPy array. Here's an example of creating a DataFrame from a dictionary:

```Python

student_data = {  
    'Name': ['Sara', 'Ray', 'John'],
    'Age': [15, 16, 17],
}

df = pd.DataFrame(student_data)

print(df)

'''Output:
   Name  Age
0  Sara   15
1   Ray   16
2  John   17
'''
```
In the student_data dictionary, each (key, value) pair becomes a DataFrame column. The DataFrame automatically assigns an index (0-2) to each row, but we can also specify our own if we choose to do so.

## Adding a Column to the DataFrame
Adding a new column to an existing DataFrame is straightforward: just like with dictionary, simply refer to a new key and assign an array to it. Let's add information about student's grades to our data:

```Python

df['Grade'] = [9, 10, 7]

print(df)

'''Output:
   Name  Age  Grade
0  Sara   15      9
1   Ray   16     10
2  John   17      7
'''
```
The 'Grade' column has been successfully added to the DataFrame.

## Classification of DataFrame Parts
A DataFrame consists of three components: data, index, and columns. Pandas neatly organize data into rows and columns — each row is a record, and each column is a feature (such as Name, Age, or Grade). The index, much like the index of a book, aids in data location. Columns serve as labels for the features in our data. Let's analyze these components with our student data:

```Python

print(df.index)  # Output: RangeIndex(start=0, stop=3, step=1)
print(df.columns)  # Output: Index(['Name', 'Age', 'Grade'], dtype='object') 
Our dataset contains row labels (index) from 0 to 2 and column labels (columns) of 'Name', 'Age', and 'Grade'.
```

## Accessing DataFrame Columns
One of the useful features of pandas DataFrame is its flexibility in accessing individual columns of data. You can select a single column, much like how you access a dictionary item by its key. Let's use our student_data DataFrame again:

```Python

print(df['Name'])

'''Output:
0    Sara
1     Ray
2    John
Name: Name, dtype: object
'''
```
As you can see, we now only have the 'Name' column content. Notice that pandas kept the index intact to retain information about the original rows.

To access multiple columns at once, pass a list with column names:

```Python

print(df[['Name', 'Grade']])

'''Output:
   Name  Grade
0  Sara      9
1   Ray     10
2  John     11
'''
```
Adding a list of columns as input, we obtain a new DataFrame that only includes the students' 'Name' and 'Grade'.

Remember: when handling a single column, pandas will return a Series. When dealing with multiple columns, pandas will return a DataFrame. Any new DataFrame or Series changes will not affect the original data.

## Understanding Data Types

The strength of a DataFrame lies in its ability to accommodate multiple data types. Using the DataFrame.dtypes property, we can ascertain the data type of each column. Let's look at the data types of out DataFrame:

```Python

print(df.dtypes)

Name     object
Age       int64
Grade     int64
dtype: object
```
Note, that strings are represented as the object data type.

Unlike NumPy arrays, which harbor single-type data, pandas DataFrames can handle and manipulate different data types.

