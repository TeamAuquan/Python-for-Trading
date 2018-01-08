---
title       : Introduction to Pandas
description : Next to Matplotlib and NumPy, Pandas is one of the most widely used Python libraries in data science. It is one of the most powerful and flexible open source data analysis and manipulation tool available in any language.
--- type:NormalExercise lang:python xp:100 skills:2 key:a1191442b4
## Introduction to DataFrames

Data frames in Python are very similar are defined as a two-dimensional labeled data structures with columns of potentially different types.
In general, you could say that the Pandas data frame consists of three main components: the data, the index, and the columns.
Firstly, the DataFrame can contain data that is:

- a Pandas DataFrame
- a Pandas Series: a one-dimensional labeled array capable of holding any data type with axis labels or index. An example of a Series object is one column from a DataFrame.
- a Numpy ndarray, which can be a record or structured
- a two-dimensional ndarray
- dictionaries of one-dimensional ndarrays, lists, dictionaries or Series.

Note that np.ndarray is the actual data type, while np.array() is a function to make arrays from other data structures.
Structured arrays allow users to manipulate the data by named fields: in the example below, a structured array of three tuples is created. The first element of each tuple will be called ‘foo’ and will be of type int, while the second element will be named ‘bar’ and will be a float.

*** =instructions
Print the value of 'foo' from structured array
*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np

```

*** =sample_code
```{python}
# A structured array
my_array = np.ones(3, dtype=([('foo', int), ('bar', float)]))
# Print the structured array


```

*** =solution
```{python}
print(my_array['foo'])
```

*** =sct
```{python}

```



--- type:VideoExercise lang:python xp:50 skills:2 key:006c9bc8ed
## Index and Columns in DataFrames

Besides the data that your DataFrame needs to contain, you can also specify the index and column names. The index labels the rows, while the column names label different columns. We will see later that these two components of the DataFrame are handy when you’re manipulating your data.

If you’re in doubt about Pandas DataFrames and how they differ from other data structures such as the NumPy array or a Series, you can watch the small presentation below:


*** =video_link
//player.vimeo.com/video/154783078

--- type:NormalExercise lang:python xp:100 skills:2 key:7aa97bf603
## How To Create a Pandas DataFrame
Obviously, making your DataFrames is your first step in almost anything that you want to do. Maybe you want to start from scratch to make a data frame, but you can also convert other data structures.
Note that the data inputted to the data frame can vary!
This section will only cover making a Pandas DataFrame from other data structures, such as NumPy arrays.
To read more on making empty dataframes that you can fill up with data later, part 8.
Among the many things that can serve as input to make a ‘DataFrame’, a NumPy ndarray is one of them. To make a data frame from a NumPy array, you can just pass it to the DataFrame() function in the data argument.

Note how the code chunks select elements from the NumPy array to construct the DataFrame: you first select the values that are contained in the lists that start with Row1 and Row2, then you select the index or row numbers Row1 and Row2 and then the column names Col1 and Col2.

This approach to making data frames will be the same for all the structures that DataFrame() can take on as input.

*** =instructions

Create dataframes from different structures provided

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
                  

# Take a 2D array as input to your DataFrame 
my_2darray = np.array([[1, 2, 3], [4, 5, 6]])
print(________________)

# Take a dictionary as input to your DataFrame 
my_dict = {1: ['1', '3'], 2: ['1', '2'], 3: ['2', '4']}
print(________________)

# Take a DataFrame as input to your DataFrame 
my_df = pd.DataFrame(data=[4,5,6,7], index=range(0,4), columns=['A'])
print(________________)

# Take a Series as input to your DataFrame
my_series = pd.Series({"Belgium":"Brussels", "India":"New Delhi", "United Kingdom":"London", "United States":"Washington"})
print(________________)
```

*** =solution
```{python}
# Take a 2D array as input to your DataFrame 
my_2darray = np.array([[1, 2, 3], [4, 5, 6]])
print(pd.DataFrame(my_2darray))

# Take a dictionary as input to your DataFrame 
my_dict = {1: ['1', '3'], 2: ['1', '2'], 3: ['2', '4']}
print(pd.DataFrame(my_dict))

# Take a DataFrame as input to your DataFrame 
my_df = pd.DataFrame(data=[4,5,6,7], index=range(0,4), columns=['A'])
print(my_df)

# Take a Series as input to your DataFrame
my_series = pd.Series({"Belgium":"Brussels", "India":"New Delhi", "United Kingdom":"London", "United States":"Washington"})
print(pd.DataFrame(my_series))
```

*** =sct
```{python}

```



--- type:NormalExercise lang:python xp:100 skills:2 key:f1890374fd
## DataFrame Shapre
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
print(df.shape)
print(len(df.index))
```

*** =sct
```{python}

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

```
