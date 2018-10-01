# python-quick-reference-guide [wip]

**Iteration over list or dictionaries:**

    new_list = [ some_function(item) for item in old_list if some_condition(item) ]

Enumeration

    for index, value in enumerate(some_list):
    	new_list[value] = index

**String operations:**
split() a string into a list, or join() a list into a string

    val.split(',')

lstrip() and rstrip() to remove beginning and trailing characters

join elements in a list with a separator

    '::'.join(my_list)

**Regular expressions:**
[re python package](https://pypi.org/project/regex/)

- contains - Return boolean array if each string contains pattern/regex
- count - Count occurrences of pattern
- endswith and startswith
- findall
- match
- replace

**Datetime:**
[datetime documentation](https://docs.python.org/3/library/datetime.html)

    from datetime import datetime, date, time
    datetime.date() # gets date from an element
    datetime.time() # gets time from an element

The `strftime` method formats a datetime as a string

Strings can be converted (parsed) into datetime objects with the `strptime` function

**Lambdas functions:**
A way to write functions in a single statement that return a value. Particularly useful for data transformations.

    multiply_by_2 = lambda x: x * 2

**Statistical methods:**
- min, max, argmin and argmax (for index of min/max)
- cumsum (for cumulative sum of previous elements)
- cumprod (for cumulative product of previous elements)

**Psuedo-random functions:**
- NumPy random functions are useful for simulations and comparing to random various distributions 
- rand, randint, randn (from a normal distribution), binomial, uniform, etc.

<!--stackedit_data:
eyJoaXN0b3J5IjpbOTAyMzUxODgsMTIyMjI4MDU4MCwtMTcwNj
I1NTM2MV19
-->