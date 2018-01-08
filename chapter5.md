---
title_meta  : Chapter 5
title       : Python Dictionary Comprehension
description : Learn all about Python dictionary comprehension- how you can use it to create dictionaries and loops and conditionals



---
## Initialize Dictionary

```yaml
type: NormalExercise
key: a7dcdc4bb3
lang: python
xp: 100
skills: 2
```

Dictionaries (or dict in Python) are a way of storing elements just like you would in a Python list. But, rather than accessing elements using its index, you assign a fixed key to it and access the element using the key. What you now deal with is a "key-value" pair, which is sometimes a more appropriate data structure for many problem instead of a simple list.

You can initialize a dictionary in Python as shown. In this case, apple is the key and fruit is the value. To assign a new key : value pair such as donught : snack, you simply add it as shown. You can access the value of any key also as shown.


`@instructions`
Try adding a new key value pair, tea : beverage and print the value of key 'cake'
`@hint`

`@pre_exercise_code`
```{python}
a = {'apple': 'fruit', 'beetroot': 'vegetable', 'cake': 'dessert'}
a['doughnut'] = 'snack'
print(a['apple'])

```

`@sample_code`
```{python}
a = {'apple': 'fruit', 'beetroot': 'vegetable', 'cake': 'dessert'}
a['doughnut'] = 'snack'
print(a['apple'])

```

`@solution`
```{python}
a['tea'] = 'beverage'
print(a['cake'])
```

`@sct`
```{python}

success_msg("Great! Moving on")

```


---
## More on initializing

```yaml
type: NormalExercise
key: 415ad65af4
lang: python
xp: 100
skills: 2
```
The items in a dictionary can have any data type. Check out some more examples of a dictionary to get a hang of it.
Each key in the dictionary needs to be unique, in case of duplicate keys Python will take the last instance of the key to be valid and simply ignore the first key-value pair.
Any key can be deleted by the `del ` command
The whole dictionary can be cleared by the `.clear()` command

`@instructions`
declare a new dictionary a with 
keys : one, two, three 
values: [1], [1,1], 3.0

change the value of key 'one' to a string 'One' and print the dictionary


`@hint`

a = {'one': [1], 'two': [1,1], 'three': 3.0}
a['one'] = 'One'
print(a)

`@pre_exercise_code`
```{python}
```

`@sample_code`
```{python}
a = {'one': 1, 'two': 'to', 'three': 3.0, 'four': [4,4.0]}
print(a)
del a['one']
print(a)
a.clear()
```

`@solution`
```{python}
a = {'one': [1], 'two': [1,1], 'three': 3.0}
a['one'] = 'One'
print(a)
```

`@sct`
```{python}
success_msg("Good Work")
```
---
## Python Dictionary Comprehension

```yaml
type: NormalExercise
key: 4d017df869
lang: python
xp: 100
skills: 2
```

Dictionary comprehension is a method for transforming one dictionary into another dictionary. During this transformation, items within the original dictionary can be conditionally included in the new dictionary and each item can be transformed as needed.

To do this, you need to access the keys and values. Dict keys are accessed as a list by `keys()` method and values by `values()` method.You can also access each key-value pair within a dictionary using the `items()` method.

`@instructions`
Create a python dictionary a = {'one': 1, 'two': 'to', 'three': 3.0, 'four': [4,4.0]}
Print all keys, all values and all key:value pairs

`@hint`

`@pre_exercise_code`
```{python}

```

`@sample_code`
```{python}

```

`@solution`
```{python}
a = {'one': 1, 'two': 'to', 'three': 3.0, 'four': [4,4.0]}
print(a.keys())
print(a.values())
print(a.items())
```

`@sct`
```{python}

```


---
## Simple Comprehension

```yaml
type: NormalExercise
key: c290f9ecd0
lang: python
xp: 100
skills: 2
```

This is the general template you can follow for dictionary comprehension in Python:
`dict_variable = {key:value for (key,value) in dictonary.items()}`
Look at a simple comprehension where we create a new dictionary with same keys and doubled values as original

`@instructions`
Create a new dictionary where the key is a number in the range of 0-10 and it's value is the square of the number. Print the keys
`@hint`

`@pre_exercise_code`
```{python}
numbers = range(10)
```

`@sample_code`
```{python}
dict1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5}
# Double each value in the dictionary
double_dict1 = {k:v*2 for (k,v) in dict1.items()}
print(double_dict1)
```

`@solution`
```{python}
new_dict_comp = {n:n**2 for n in numbers}

print(new_dict_comp)
```

`@sct`
```{python}

```

---
## Adding Conditionals to Dictionary Comprehension

```yaml
type: NormalExercise
key: f25aeede3d
lang: python
xp: 100
skills: 2
```

You often need to add conditions to a solution while tackling problems. Let's explore how you can add conditionals into dictionary comprehension to make it more powerful.
Let' say you want to create a new dictionary same as previous problem but now the key is a number divisible by 2 in a range of 0-10 and it's value is the square of the number.
`@instructions`
Create a new dictionary where key is a number in a range of 0-10 and it's value is the square of the number if number is even else the number itself.
Eg: 2:4 , 3: 3
`@hint`

`@pre_exercise_code`
```{python}

```

`@sample_code`
```{python}
numbers = range(10)
# Use dictionary comprehension with conditional
new_dict_comp = {n:n**2 for n in numbers if n%2 == 0}

print(new_dict_comp)

# Create a new dictionary

```

`@solution`
```{python}

numbers = range(10)
# Use dictionary comprehension with conditional
new_dict_comp = {n:(n**2 if n%2 == 0 else n) for n in numbers }

print(new_dict_comp)


```

`@sct`
```{python}

```


---
## Nested Dictionary Comprehension

```yaml
type: NormalExercise
key: 8d6826bb41
lang: python
xp: 100
skills: 2
```

Nesting is a programming concept where data is organized in layers, such as a nested 'if' structure, which is an if condition inside another if condition.
Similarly, dictionaries can be nested and thus their comprehensions can be nested as well.
Check out an example of a nested dictionary

`@instructions`

Write a nested code to create a new dictionary with same keys as the original dictionary and values of the first key of the correponding nested dictionary

For example, the first key : value pair should be : 'first':{1}
`@hint`
write a nested for loop, first loop over all items of the main dictionary as 
` {outer_k : (somevalue) for (outer_k, outer_v) in nested_dict.items()}`
and then loop over all itmes of the nested dictionary to get somevalue as 
`inner_v for (inner_k, inner_v) in outer_v.items()`


`@pre_exercise_code`
```{python}

```

`@sample_code`
```{python}
nested_dict = {'first':{'a':1}, 'second':{'b':2}}
```

`@solution`
```{python}
nested_dict = {'first':{'a':1}, 'second':{'b':2}}
float_dict = {outer_k: {inner_v for (inner_k, inner_v) in outer_v.items()} for (outer_k, outer_v) in nested_dict.items()}
print(float_dict)
```

`@sct`
```{python}

```
