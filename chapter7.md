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
df['result'] = df['result'].map(lambda x: x.lstrip('+-').rstrip('ls'))

# Check out the result again
print(df)

```

*** =sct
```{python}

```
