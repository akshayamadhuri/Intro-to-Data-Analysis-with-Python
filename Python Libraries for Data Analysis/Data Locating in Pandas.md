## Navigating DataFrames with Index Column and Data Locating in Pandas

Introduction and Lesson Overviews
Welcome, future data analyzers! Today, we're tackling Index Columns and Locating Elements in a Pandas DataFrame. We'll learn how to handle index columns, locate specific data, and strengthen our understanding of DataFrames. Ready, set, code!

Understanding the Index Column in a Pandas DataFrame
In a Pandas DataFrame, an index is assigned to each row, much like the numbers on books in a library. When a DataFrame is created, Pandas establishes a default index. Let's refer to an example:

Python
Copy to clipboard
import pandas as pd

data = {
    "Name": ["John", "Anna", "Peter", "Linda"],
    "Age": [28, 24, 35, 32],
    "City": ["New York", "Paris", "Berlin", "London"]
}

df = pd.DataFrame(data)

print(df)
"""Output:
    Name  Age      City
0   John   28  New York
1   Anna   24     Paris
2  Peter   35    Berlin
3  Linda   32    London
"""
The numbers on the left are the default index.

Setting and Modifying the Index Column
Occasionally, we might need to establish a custom index. The Pandas' set_index() function allows us to set a custom index. To reset the index to its default state, we use reset_index().

To better understand these functions, let's consider an example in which we create an index using unique IDs:

Python
Copy to clipboard
df['ID'] = [101, 102, 103, 104]    # Adding unique IDs
df.set_index('ID', inplace=True)   # Setting 'ID' as index

print(df)
"""Output:
      Name  Age      City
ID                       
101   John   28  New York
102   Anna   24     Paris
103  Peter   35    Berlin
104  Linda   32    London
"""
In this example, ID column is displayed as an index. Let's reset the index to return to the original state:

Python
Copy to clipboard
df.reset_index(inplace=True)       # Resetting index

print(df)
"""Output:
    ID   Name  Age      City
0  101   John   28  New York
1  102   Anna   24     Paris
2  103  Peter   35    Berlin
3  104  Linda   32    London
"""
By setting inplace parameter to True, we ask pandas to reset the index in the original df dataframe. Otherwise, pandas will create a copy of the data frame with a reset index, leaving the original df untouched.

Locating Elements in a DataFrame
Let's consider a dataframe with a custom index. If you want to select a specific row based on its index value (for example, ID = 102), you can do this:

Python
Copy to clipboard
import pandas as pd

data = {
    "Name": ["John", "Anna", "Peter", "Linda"],
    "Age": [28, 24, 35, 32],
    "City": ["New York", "Paris", "Berlin", "London"]
}

df = pd.DataFrame(data)
df['ID'] = [101, 102, 103, 104]    # Adding unique IDs
df.set_index('ID', inplace=True)   # Setting 'ID' as index

print(df.loc[102])
'''Output:
Name     Anna
Age        24
City    Paris
Name: 102, dtype: object
'''
Selecting Multiple Rows with `loc`
For multiple rows, simply use list of ids:

Python
Copy to clipboard
print(df.loc[[102, 104]])

'''Output:
      Name  Age    City
ID                     
102   Anna   24   Paris
104  Linda   32  London
'''
As you can see, the output of the .loc operation is some subset of the original dataframe.

Selecting Multiple Columns with `loc`
To select specific multiple columns for these rows, you can provide the column labels as well:

Python
Copy to clipboard
print(df.loc[[102, 104], ['Name', 'Age']])
'''Output:
      Name  Age
ID             
102   Anna   24
104  Linda   32
'''
Also you can select all rows for specific columns, providing : as a set of index labels:

Python
Copy to clipboard
print(df.loc[:, ['Name', 'Age']])
'''Output:
      Name  Age
ID             
101   John   28
102   Anna   24
103  Peter   35
104  Linda   32
'''
Using `iloc` for Location by Index Position
The iloc function enables us to select elements in a data frame based on their index positions. iloc works like the loc, but it expects the index number of the rows. For example, we can select the 3rd row:

Python
Copy to clipboard
print(df.iloc[3])
'''Output:
Name     Linda
Age         32
City    London
Name: 104, dtype: object
'''
You can also use slicing here:

Python
Copy to clipboard
print(df.iloc[1:3])
'''Output:
      Name  Age    City
ID                     
102   Anna   24   Paris
103  Peter   35  Berlin
'''
