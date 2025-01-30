# Mastering Row Manipulation in Pandas DataFrame

## Introduction to Adding and Removing Rows in a Pandas DataFrame

```Python

import pandas as pd
```

## Quick Recap on Rows in a DataFrame

A DataFrame, a central data structure in Pandas, is a tool for storing data in table form. Each row contains values correlated to an individual entry in our data. For instance, each row of a grocery list might represent a unique grocery item.

Each row features an index, a unique identifier. Now, let's create a DataFrame:

```Python

import pandas as pd

data = {
    'Grocery Item': ['Apples', 'Oranges', 'Bananas', 'Grapes'],
    'Price per kg': [3.25, 4.50, 2.75, 5.00]
}

grocery_df = pd.DataFrame(data)

print(grocery_df)
'''Output:
  Grocery Item  Price per kg
0       Apples          3.25
1      Oranges          4.50
2      Bananas          2.75
3       Grapes          5.00
'''
```

## Adding a Row to a DataFrame

Multiple scenarios might necessitate adding new entries to our DataFrame. Let's explore how to accomplish that:

In modern pandas, we use pd.concat() function to incorporate new rows. If you forgot to add 'Pears' to your grocery list, here’s how to do it:

```Python

new_row = pd.DataFrame({'Grocery Item': ['Pears'], 'Price per kg': [4.00]})

grocery_df = pd.concat([grocery_df, new_row]).reset_index(drop=True)

print(grocery_df)
'''Output:
  Grocery Item  Price per kg
0       Apples          3.25
1      Oranges          4.50
2      Bananas          2.75
3       Grapes          5.00
4        Pears          4.00
'''
```
Setting reset_index(drop=True) resets the index to default integers. Without this step, pandas will save the original dataframes' indices, resulting in both 'Pears' and 'Apples' sharing the same index 0.

## Adding Multiple Rows to a DataFrame
For multiple rows, you can concatenate them by creating a DataFrame and adding it to the original one:

```Python

new_rows = pd.DataFrame({
    'Grocery Item': ['Avocados', 'Blueberries'],
    'Price per kg': [2.5, 10.0]
})

grocery_df = pd.concat([grocery_df, new_rows]).reset_index(drop=True)

print(grocery_df)
'''Output:
  Grocery Item  Price per kg
0       Apples          3.25
1      Oranges          4.50
2      Bananas          2.75
3       Grapes          5.00
4     Avocados          2.50
5  Blueberries         10.00
'''
```
You may wonder why we don't include these rows in the original dataframe. Well, it is only sometimes possible. Imagine we have two separate grocery lists coming from different sources, for instance, from separate files. In this case, the only way to combine them into one is to use pd.concat()

Removing Rows from a DataFrame
Frequently, we must delete rows from a DataFrame. To facilitate this, Pandas provides the drop() function. Suppose you want to remove 'Grapes' or both 'Apples' and 'Oranges' from your list. Here's how:

Python
Copy to clipboard
index_to_delete = grocery_df[grocery_df['Grocery Item'] == 'Grapes'].index

grocery_df = grocery_df.drop(index_to_delete)

print(grocery_df)
'''Output:
  Grocery Item  Price per kg
0       Apples          3.25
1      Oranges          4.50
2      Bananas          2.75
'''
Note that the .drop() method returns a new updated DataFrame instead of changing the original one. It allows you to modify the data while keeping its original state to return to it if necessary.

Removing Multiple Rows
There will be times when you will have to remove multiple rows in one go. For example, let's say you were informed that 'Apples' and 'Oranges' are out of stock, so you need to remove them from your grocery list. The drop() function allows you to do this too.

When removing multiple rows, we utilize the .isin() function, which checks if a value exists in a particular DataFrame column. You provide it with the values you want to remove, and it outputs the indices of those rows. Let's see it in action:

Python
Copy to clipboard
indices_to_delete = grocery_df[grocery_df['Grocery Item'].isin(['Apples', 'Oranges'])].index

grocery_df = grocery_df.drop(indices_to_delete)

print(grocery_df)
'''Output:
  Grocery Item  Price per kg
2      Bananas          2.75
3       Grapes          5.00
'''
In this block of code, the variable indices_to_delete holds the indices of the rows where the 'Grocery Item' is either 'Apples' or 'Oranges'. We then pass indices_to_delete to the drop() function, which removes the corresponding rows from the DataFrame.

Keep in mind, just as with removing a single row, the drop() function here doesn't change the original DataFrame. Instead, it returns a new DataFrame with the specified rows removed. This way, you can always revert back to the original data if needed.
