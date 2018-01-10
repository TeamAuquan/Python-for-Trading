---
title_meta  : Chapter 6
title       : Introduction to Pandas
description :  Pandas is one of the most widely used Python libraries in data science. It is one of the most powerful and flexible open source data analysis and manipulation tool available in any language.


---
## Creating a Dataframe

```yaml
type: NormalExercise
key: a7dcdc4bb3
lang: python
xp: 100
skills: 2
```

Data frames in Python are a two-dimensional labeled data structures with columns of potentially different types.

In general, you could say that the Pandas data frame consists of three main components: the data, the index, and the columns.

Firstly, the DataFrame can contain data that is:

- a Pandas DataFrame
- a Pandas Series: a one-dimensional labeled array capable of holding any data type with axis labels or index. An example of a Series object is one column from a DataFrame.
- a Numpy ndarray, which can be a record or structured
- a two-dimensional ndarray
- dictionaries of one-dimensional ndarrays, lists, dictionaries or Series.

Note that np.ndarray is the actual data type, while `np.array()` is a function to make arrays from other data structures.
To make a data frame from a NumPy array, you can just pass it to the `DataFrame()` function in the data argument.

Note how the code chunks select elements from the NumPy array to construct the DataFrame: you first select the values that are contained in the lists that start with Row1 and Row2, then you select the index or row numbers Row1 and Row2 and then the column names Col1 and Col2.

This approach to making data frames will be the same for all the structures that `DataFrame()` can take on as input.

*** =instructions

Create and print a dataframe `df` from each of the different structures provided

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np

```

*** =sample_code
```{python}
data = np.array([['','Col1','Col2'],
                ['Row1',1,2],
                ['Row2',3,4]])
                
print(pd.DataFrame(data=data[1:,1:],
                  index=data[1:,0],
                  columns=data[0,1:]))
                  

# Take a 2D array as input to your DataFrame df1
my_2darray = np.array([[1, 2, 3], [4, 5, 6]]) 
df1 = None
print(________________)

# Take a dictionary as input to your DataFrame df2
my_dict = {1: ['1', '3'], 2: ['1', '2'], 3: ['2', '4']}
df2 = None
print(________________)

# Take a DataFrame as input to your DataFrame df3
my_df = pd.DataFrame(data=[4,5,6,7], index=range(0,4), columns=['A'])
df3 = None
print(________________)

# Take a Series as input to your DataFrame df4
my_series = pd.Series({"Belgium":"Brussels", "India":"New Delhi", "United Kingdom":"London", "United States":"Washington"})
df4 = None
print(________________)
```

*** =solution
```{python}
# Take a 2D array as input to your DataFrame 
my_2darray = np.array([[1, 2, 3], [4, 5, 6]])
df1 = pd.DataFrame(my_2darray)
print(df1)

# Take a dictionary as input to your DataFrame 
my_dict = {1: ['1', '3'], 2: ['1', '2'], 3: ['2', '4']}
df2 = pd.DataFrame(my_dict)
print(df2)

# Take a DataFrame as input to your DataFrame 
my_df = pd.DataFrame(data=[4,5,6,7], index=range(0,4), columns=['A'])
df3 = my_df
print(df3)

# Take a Series as input to your DataFrame
my_series = pd.Series({"Belgium":"Brussels", "India":"New Delhi", "United Kingdom":"London", "United States":"Washington"})
df4 = pd.DataFrame(my_series)
print(df4)
```

*** =sct
```{python}
test_object("df1")
test_object("df2")
test_object("df3")
test_object("df4")

```


--- type:VideoExercise lang:python xp:50 skills:2 key:006c9bc8ed
## Index and Columns in DataFrames

Besides the data that your DataFrame needs to contain, you can also specify the index and column names. The index labels the rows, while the column names label different columns. We will see later that these two components of the DataFrame are handy when you’re manipulating your data.

If you’re in doubt about Pandas DataFrames and how they differ from other data structures such as the NumPy array or a Series, you can watch the small presentation below:


*** =video_link
//player.vimeo.com/video/154783078


*** =projector_key
ab521d54a14cd5c8c35afc52fbf750d9

--- type:NormalExercise lang:python xp:100 skills:2 key:f1890374fd
## DataFrame Shape
After you have created your DataFrame, you might want to know a little bit more about it. You can use the `shape` property or the `len()` function in combination with the `.index` property.

Note how these two options give you slightly different information on your DataFrame: the `shape` property will give you the dimensions of your DataFrame. So you will get to know the width and the height of your DataFrame. On the other hand, the `len()` function, in combination with the index property, will only give you information on the height of your DataFrame.
This all is totally not extraordinary, though, as you explicitly give in the `index` property.
You could also use `df[0].count()` to get to know more about the height of your DataFrame, but this will exclude the NaN values (if there are any). That is why calling `.count()` on your DataFrame is not always the better option.
If you want more information on your DataFrame columns, you can always execute `list(my_dataframe.columns.values)`

*** =instructions
Print the dataframe dimensions using the shape property
Print the height using len() function with index property

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}

df = pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6]]))

# Use the `shape` property
print(________)

# Or use the `len()` function with the `index` property
print(____________)

```

*** =solution
```{python}
df = pd.DataFrame(np.array([[1, 2, 3], [4, 5, 6]]))

print(df.shape)
print(len(df.index))
```

*** =sct
```{python}
test_function("print", index=1)
test_function("print", index=2)
success_msg("Great job!")
```


--- type:NormalExercise lang:python xp:100 skills:2 key:f520cc6b8f
## Selecting an Index or Column From a Pandas DataFrame

Before you start with adding, deleting and renaming the components of your DataFrame, you first need to know how you can select these elements.
Let’s say you have a DataFrame like this one

And you want to access the value that is at index 0, in column ‘A’.

The various options that exist to get your value 1 back are shown:
The most important ones to remember are, without a doubt, `loc` and `iloc`. The subtle differences between these two will be discussed in the next sections.

What about selecting rows and columns? Just use rowname with `iloc` or columnname with `loc` to select rows or columns

For now, it suffices to know that you can either access the values by calling them by their label or by their position in the index or column. If you don’t see this, look again at the slight differences in the commands: one time, you see [0][0], the other time, you see [0,'A'] to retrieve your value 1.

*** =instructions

Print row 0 and column A

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A','B','C'])
```

*** =sample_code
```{python}
#   A B C
# 0 1 2 3
# 1 4 5 6
# 2 7 8 9
# Using `iloc[]`
print(df.iloc[0][0])

# Using `loc[]`
print(df.loc[0]['A'])

# Using `at[]`
print(df.at[0,'A'])

# Using `iat[]`
print(df.iat[0,0])

# Using `get_value(index, column)`
print(df.get_value(0, 'A'))

# Use `iloc[]` to select row `0`
print()

# Use `loc[]` to select column `'A'`
print()

```

*** =solution
```{python}

# Use `iloc[]` to select row `0`
print(df.iloc[0])

# Use `loc[]` to select column `'A'`
print(df.loc[:,'A'])

```

*** =sct
```{python}
test_function("print", index=1)
test_function("print", index=2)
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:33c60edd54
## Adding an Index to a DataFrame

When you create a DataFrame, you have the option to add input to the ‘index’ argument to make sure that you have the index that you desire. When you don’t specify this, your DataFrame will have, by default, a numerically valued index that starts with 0 and continues until the last row of your DataFrame.
However, even when your index is specified for you automatically, you still have the power to re-use one of your columns and make it your index. You can easily do this by calling set_index() on your DataFrame.


*** =instructions

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A','B','C'])
```

*** =sample_code
```{python}

# Print out your DataFrame `df` to check it out
print(__)

# Set 'C' as the index of your DataFrame
df.______('C')

```

*** =solution
```{python}
print(df)
df.set_index('C')

```

*** =sct
```{python}
test_function("print", index=1)
test_student_typed(".set_index()")
test_object("df")
success_msg("Great job!")

```

--- type:NormalExercise lang:python xp:100 skills:2 key:6a6ce95589
## Adding Rows to a DataFrame

It's important to understand the concept of `loc` and how it differs from other indexing attributes such as `.iloc` and `.ix`:
- `loc` works on labels of your index. This means that if you give in `loc[2]`, you look for the values of your DataFrame that have an index labeled 2.
- `iloc` works on the positions in your index. This means that if you give in `iloc[2]`, you look for the values of your DataFrame that are at index ’2`.
- `ix` is a more complex case: when the index is integer-based, you pass a label to `ix`. `ix[2]` then means that you’re looking in your DataFrame for values that have an index labeled 2. This is just like `loc`! However, if your index is not solely integer-based, `ix` will work with positions, just like `iloc`

Look at the results of the sample code on the right to see the difference.

Now give adding rows to your DataFrame a go!
As a consequence of what has just been explained, you understand that the general recommendation is that you use `.loc` to insert rows in your DataFrame.
If you would use `df.ix[]`, you might try to reference a numerically valued index with the index value and accidentally overwrite an existing row of your DataFrame.


*** =instructions
 A new dataframe, df2 has been created.
1.  Change the index at position `2` to [60, 50, 40]
2. Make an index labeled `2` and add the new values [11, 12, 13]

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}

df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), index= [2, 'A', 4], columns=[48, 49, 50])

# Pass `2` to `loc`
print(df.loc[2])

# Pass `2` to `iloc`
print(df.iloc[2])

# Pass `2` to `ix`
print(df.ix[2])

df2 = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), index= [2.5, 12.6, 4.8], columns=[48, 49, 50])

# Change the index at position `2` to [60, 50, 40]

# Make an index labeled `2` and add the new values [11, 12, 13]

```

*** =solution
```{python}

df2 = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), index= [2.5, 12.6, 4.8], columns=[48, 49, 50])

# Change the index at position `2` to [60, 50, 40]
df2.ix[2] = [60, 50, 40]
print(df2)

# Make an index labeled `2` and add the new values [11, 12, 13]
df2.loc[2] = [11, 12, 13]
print(df2)
```

*** =sct
```{python}
test_object("df2")
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:36d041f848
## Adding a Column to Your DataFrame

In some cases, you want to make your index part of your DataFrame. You can easily do this by taking a column from your DataFrame or by referring to a column that you haven’t made yet and assigning it to the `.index` property. In sample code, we add a new column D which is same as the index.

However, if you want to append columns to your DataFrame, you could also follow the same approach as adding an index to your DataFrame: you use `loc` or `iloc`.

*** =instructions
Remember that you could consider a Series object much like a column of a DataFrame. Add a Series to an existing DataFrame with the help of `loc`

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A', 'B', 'C'])

# Use `.index`
df['D'] = df.index

print(df)

#create a new series S

S = pd.Series(['5', '6', '7'], index=df.index)

# Append S as a column to `df`. Name the column 'S'


# Print out `df` again to see the changes

```

*** =solution
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A', 'B', 'C'])
df['D'] = df.index

S = pd.Series(['5', '6', '7'], index=df.index)
df.loc[:, 'S'] = S

print(df)
```

*** =sct
```{python}
test_object("df")
success_msg("Great job!")

```

--- type:NormalExercise lang:python xp:100 skills:2 key:89cbbc4e51
## Resetting the Index of Your DataFrame

When your index doesn’t look entirely the way you want it to, you can opt to reset it. This can easily ben done with `.reset_index()`.
You can pass two arguments here depending on the usecase. Use the `drop` argument to indicate that you want to get rid of the index that was there. Use `inplace` to add the original index as an extra column to your DataFrame.

*** =instructions
Reset the index of the dataframe and add the original index as an extra column to your DataFrame

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), index= [2.5, 12.6, 4.8], columns=[48, 49, 50])
# Check out the weird index of your dataframe
print(df)

# Use `reset_index()` to reset the values. 
```

*** =solution
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), index= [2.5, 12.6, 4.8], columns=[48, 49, 50])
# Check out the weird index of your dataframe
print(df)

# Use `reset_index()` to reset the values. 
df.reset_index(level=0, inplace=True)

```

*** =sct
```{python}
test_object("df")
success_msg("Great job!")

```

--- type:NormalExercise lang:python xp:100 skills:2 key:47723735a8
## Delete Indices, Rows or Columns From a Pandas Data Frame

- Deleting an Index from Your DataFrame

If you want to remove the index from your DataFrame, you should reconsider.Because DataFrames and Series always have an index.
What you can do is:
- resetting the index of your DataFrame (go back to the previous section to see how it is done) or
- remove the index name, if there is any, by executing `del df.index.name`,
- remove duplicate index values by resetting the index, dropping the duplicates of the index column that has been added to your DataFrame and reinstating that duplicateless column again as the index

Deleting a Column from Your DataFrame

To get rid of (a selection of) columns from your DataFrame, you can use the `drop()` method. There are some extra arguments that are passsed to the `drop()` method!
- The axis argument is either 0 when it indicates rows and 1 when it is used to drop columns.
- You can set `inplace` to `True` to delete the column without having to reassign the DataFrame.

Note that you can also delete duplicate values from column with `drop_duplicates()`

Removing a Row from Your DataFrame

You can remove duplicate rows from your DataFrame by executing `df.drop_duplicates()`. You can also remove rows from your DataFrame, taking into account only the duplicate values that exist in one column.

If there is no uniqueness criterion to the deletion that you want to perform, you can use the `drop()` method, where you use the index property to specify the index of which rows you want to remove from your DataFrame.

After this command, you might want to reset the index again.


*** =instructions

Check out the dataframe in the window
1. Drop duplicate index values and reinstate the index back
2. Drop the column with label 48 inplace 
3. Drop the third row


*** =hint

Use `.reset_index()` to convert index to a column, `.drop_duplicates(subset='index', keep='last')` to drop duplicates from that column and `.set_index('index')` to set it back as index

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}

df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [40, 50, 60], [23, 35, 37]]), 
                  index= [2.5, 12.6, 4.8, 4.8, 2.5], 
                  columns=[48, 49, 50])
                  
# Drop duplicate index values



# Drop the column with label 48 inplace                 


# Drop the third row (index at position 1)


print(df)

```

*** =solution
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9], [40, 50, 60], [23, 35, 37]]), 
                  index= [2.5, 12.6, 4.8, 4.8, 2.5], 
                  columns=[48, 49, 50])
                  
# Drop duplicate index values

df.reset_index().drop_duplicates(subset='index', keep='last').set_index('index')

# Drop the column with label 48 inplace                 
df.drop(48, axis=1, inplace=True)

# Drop the third row (index at position 1)
df.drop(df.index[1])

print(df)

```

*** =sct
```{python}
test_function("df.reset_index", do_eval = False)
test_function("print")
test_object("df")
success_msg("Great job!")

```

--- type:NormalExercise lang:python xp:100 skills:2 key:b645cefed1
## Rename the Index or Columns of a Pandas DataFrame

To give the columns or your index values of your dataframe a different value, it’s best to use the `.rename()` method.

*** =instructions

1. Change the column names to c1, c2, c3 inplace. The dict variable to pass to `.rename()` has already been created for you
2. Change the second index label 1 to 'a'

Note that the DataFrame hasn’t been reassigned when renaming the index. As a result,  if you print the DataFrame df, you'll see the column names are changed but index names are not.

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np

```

*** =sample_code
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A','B','C'])

# Define the new names of your columns
newcols = {'A': 'c1', 'B': 'c2', 'C': 'c3'}

# Use `rename()` to rename your columns inplace


# Use `rename()` to your index


print(df)
```

*** =solution
```{python}

df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A','B','C'])

# Define the new names of your columns
newcols = {'A': 'c1', 'B': 'c2', 'C': 'c3'}

# Use `rename()` to rename your columns inplace
df.rename(columns=newcols, inplace=True)

# Use `rename()` to your index
df.rename(index={1: 'a'})

print(df)

```

*** =sct
```{python}
test_function("df.rename", do_eval = False)
test_object("df")
success_msg("Great job!")

```
