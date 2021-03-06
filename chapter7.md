---
title_meta  : Chapter 7
title       : Advanced Pandas
description :  Now that you have an introduction to Pandas, it’s time to go beyond the basics and get our hands dirty for real. Because there is far more to DataFrames than what you have seen in the first section.




--- type:NormalExercise lang:python xp:100 skills:2 key:f4876d2a78
## Format Data: Replacing All Occurrences of a String in a DataFrame

To replace certain Strings in your DataFrame, you can easily use `replace()`: pass the values that you would like to change, followed by the values you want to replace them by.

There is also a `regex` argument that can help you out tremendously when you’re faced with strange string combinations

*** =instructions
We have data for three stocks but the data got corrupted. convert all 'H' to lowercase 'h' and then replace strings by numerical values, high by 0 and low by 1

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np

```

*** =sample_code
```{python}
df = pd.DataFrame(data=np.array([['higH', 'low', 'low'], ['low', 'High', 'high']]), columns=['S1', 'S2', 'S3'])

print(df)

# Replace strings by others with `regex`


# Replace the strings by numerical values (0-1)



print(df)

```

*** =solution
```{python}
df = pd.DataFrame(data=np.array([['higH', 'low', 'low'], ['low', 'High', 'high']]), columns=['S1', 'S2', 'S3'])

print(df)

# Replace strings by others with `regex`
df = df.replace({'H': 'h'}, regex=True)
print(df)

# Replace the strings by numerical values (0-1)
df = df.replace(['high', 'low'], [0, 1]) 
print(df)

```

*** =sct
```{python}

test_object("df")
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:d23c3ea18c
## Removing Parts From Strings in the Cells of Your DataFrame

Removing unwanted parts of strings is cumbersome work. Luckily, there is a solution in place!

Look at the dataframe to the right. We want to remove the extra symbols in the column 'position'. 

You can create a `lambda` function takes a string value and strips the `+` or `-` that’s located on the left using `lstrip()`, and also strips away any of `ls` on the right using `rstrip()`. Then use `map()` on the column position to apply the `lambda` function over each element or element-wise of the column.

*** =instructions
Use the hint above to convert the data in column `position` into numbers
*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np

```

*** =sample_code
```{python}
df = pd.DataFrame(data=np.array([['500', '+50l'], ['250', '-35s'], ['-400', '-25s']]), index=['S1', 'S2', 'S3'], columns=['pnl','position'])

print(df)

# Delete unwanted parts from the strings in the `position` column


print(df)
```

*** =solution
```{python}
df = pd.DataFrame(data=np.array([['500', '+50l'], ['250', '-35s'], ['-400', '-25s']]), index=['S1', 'S2', 'S3'], columns=['pnl','position'])

# Delete unwanted parts from the strings in the `result` column
df['position'] = df['position'].map(lambda x: x.lstrip('+-').rstrip('ls'))

# Check out the result again
print(df)

```

*** =sct
```{python}
test_object("df")
success_msg("Great job!")

```
--- type:NormalExercise lang:python xp:100 skills:2 key:728a29687f
## Reshape Pandas DataFrame
Reshaping your DataFrame is basically transforming it so that the resulting structure makes it more suitable for your data analysis.
In other words, reshaping is not so much concerned with formatting the values that are contained within the DataFrame, but more about transforming the shape of it.

There are three ways of reshaping: pivoting, stacking and unstacking and melting. Let's look at stacking. 

When you stack a DataFrame, you make it taller. You move the innermost column index to become the innermost row index. You return a DataFrame with an index with a new inner-most level of row labels.

The inverse of stacking is called unstacking. Much like `stack()`, you use `unstack()` to move the innermost row index to become the innermost column index.


*** =instructions

*** =hint

*** =pre_exercise_code
```{python}

```

*** =sample_code
```{python}

```

*** =solution
```{python}

```

*** =sct
```{python}

```

--- type:NormalExercise lang:python xp:100 skills:2 key:a1b169c2d9
## Splitting Text in a Column into Multiple Rows in a DataFrame

We run into this situation frequently when dealing with exchange data. Splitting your text into multiple rows is quite complex. 

In our dataframe, some of our data has not split into rows properly (probably because of dividend). Let's see how we can fix this.

- You take the `price diff` column from the DataFrame `df` and break the string on the space using `.str.split()`. This will make sure that the two differences will end up in two separate rows in the end. 
- This will result in `NaN` values. So you have to convert it to series and stack the Series to make sure you don’t have any NaN values in the resulting Series. Use `.apply()` to convert to series and `.stack()` to stack them.
- Finally, reindex and drop a level to line up with rest of the DataFrame. Levels are dropped by `.droplevel(-1)`
- Now you can join it back to your initial DataFrame. However, to avoid having any duplicates in your DataFrame, you can delete the original `price diff` column.

Applying A Function to Your Pandas DataFrame’s Columns or Rows: We can select a row or column of the dataframe using `loc` or `iloc` and use `.apply()` with the function as parameter. If, however, you want to apply it to each element or element-wise, you can make use of the map() function. 


*** =instructions
Use the above instructions to split the text in `price diff` column into Multiple Rows

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}
df = pd.DataFrame(data=np.array([['S1', 'N', '0.32'], ['S2', 'N', '0.25'], ['S3', 'N', '0.22'], ['S4', 'Y', '0.32 0.12']]), columns=['Stock', 'Divs', 'price diff'])

print(df)

# Split out the two values in the third row


# Make it a Series


# Stack the values

# Get rid of the stack:
# Drop the level to line up with the DataFrame

# Make series a dataframe 

# Delete the `price diff` column from your DataFrame

# Join the `dataframe` DataFrame to `df`


# Check out the new `df`
print(df)

```

*** =solution
```{python}
df = pd.DataFrame(data=np.array([['S1', 'N', '0.32'], ['S2', 'N', '0.25'], ['S3', 'N', '0.22'], ['S4', 'Y', '0.32 0.12']]), columns=['Stock', 'Divs', 'price diff'])

print(df)

# Split out the two values in the third row
pdiff = df['price diff'].str.split(' ')

# Make it a Series
pdiff_series = pdiff.apply(pd.Series, 1)

# Stack the values
pdiff_series_clean = pdiff_series.stack()

# Get rid of the stack:
# Drop the level to line up with the DataFrame
pdiff_series_clean.index = pdiff_series_clean.index.droplevel(-1)

# Make your `ticket_series` a dataframe 
pdiffdf = pd.DataFrame(pdiff_series_clean)

# Delete the `Ticket` column from your DataFrame
del df['price diff']

# Join the `ticketdf` DataFrame to `df`
df = df.join(pdiffdf)

# Check out the new `df`
print(df)

```

*** =sct
```{python}
test_object("df")
success_msg("Great job!")

```

--- type:NormalExercise lang:python xp:100 skills:2 key:be415ef317
## Initializing an Empty DataFrame
Pandas `Dataframe()` function requires you to pass the data that you want to put in, the indices and the columns. Remember that the data that is contained within the data frame doesn’t have to be homogenous.
There are several ways in which you can use this function to make an empty data frame.
Firstly, you can use `numpy.nan` to initialize your data frame with `NaN`s. Note that `numpy.nan` has type `float`.
The data type of the data frame is inferred by default: because `numpy.nan` has type float, the data frame will also contain values of type float. You can, however, also force the data frame to be of a certain type by adding the attribute `dtype` and filling in the desired type.
Note that if you don’t specify the axis labels or index, they will be constructed from the input data based on common sense rules.

*** =instructions

Create an empty dataframe `df` with index=[0,1,2,3], single columns='A' and dtype=`int`
*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}


```

*** =solution
```{python}
df = pd.DataFrame(index=range(0,4),columns=['A'], dtype='int')
print(df)
```

*** =sct
```{python}
test_object("df")
success_msg("Great job!")
```

--- type:NormalExercise lang:python xp:100 skills:2 key:0d73b6c433
## Importing Data (especially with dates)

You can use the `.read_csv()` method to read data from a csv files directly into a DataFrame. If your data contains dates (as financial data will), add the argument `parse_dates`. There are, however, always weird date-time formats.

In such cases, you can construct your own parser to deal with this. You could, for example, make a `lambda` function that takes your DateTime and controls it with a format string.

*** =instructions
'AAPL.csv' file contains dates in the format '%Y-%m-%d'.
The filelocation is stored in a variable `fileLocation`
Write a custom date parser and import the data into a dataframe `df`
*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
fileLocation = 'https://s3.amazonaws.com/assets.datacamp.com/production/course_6523/datasets/AAPL.csv'
```

*** =sample_code
```{python}

```

*** =solution
```{python}
dateparser = lambda x: pd.datetime.strptime(x, '%Y-%m-%d')

df = pd.read_csv(fileLocation, parse_dates=True, date_parser=dateparser)

```

*** =sct
```{python}
test_object("df")
success_msg("Great job!")

```

--- type:NormalExercise lang:python xp:100 skills:2 key:9b04700610
## Iterate Over a Pandas DataFrame

You can iterate over the rows of your DataFrame with the help of a `for` loop in combination with an `iterrows()` call on your DataFrame. `iterrows()` allows you to efficiently loop over your DataFrame rows as (index, Series) pairs. In other words, it gives you (index, row) tuples as a result.


*** =instructions
Iterate over all rows of the dataframe and print values in column A and column B, one row per line.

*** =hint

*** =pre_exercise_code
```{python}
import pandas as pd
import numpy as np
```

*** =sample_code
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A', 'B', 'C'])


```

*** =solution
```{python}
df = pd.DataFrame(data=np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]]), columns=['A', 'B', 'C'])

for index, row in df.iterrows() :
    print(row['A'], row['B'])

```

*** =sct
```{python}
test_student_typed("df.iterrows()")
success_msg("Great job!")

```
