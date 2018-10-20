# pandas-quick-reference-guide [wip]
Cheat sheet for performing analysis in pandas and related packages

## Pandas setup

    import pandas as pd
    from pandas import Series, DataFrame

Set up a series with specific values and indexes

    pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
    pd.Series(my_dictionary) # creates with keys as indexes, values as values

Set up a dataframe with specific values and indexes

    data = {'index_1': ['value','value'], 
		    'index_2': ['value','value'], 
		    'index_3': ['value','value']} 
    frame = pd.DataFrame(data, columns = ['name','name'])

If a nested dict is passed to the DataFrame, pandas will interpret the outer dict keys as the columns and the inner keys as the row indices.

**Accessing Elements:**
Accessing rows

    my_df.ix['col_name']
Accessing columns

    my_df.iloc[2] # get the second column
    my_df.loc['column_name']
Accessing values

    df.loc['col_name', 'index_name']
    df.at['col_name', 'index_name']

Accessing and changing index

    df.set_index('new_name', inplace=True)
    df.index  # get list of index 
    df.index.values # get list of values

Accessing and changing columns

    df.columns = ['new_name1','new_name2']
    df.columns.values # get names of columns
Creating a boolean column

    df['bool'] = df['column'] == value

Deleting columns and rows

    del df['column_name']
    new_df = df.drop('index_name')
    new_df = df.drop('column_name', axis=1)

## Filtering
Filtering series:

    new_series = my_series > 0

Filtering dataframe: 

    filtered = my_df[my_df['col_name'] > 0]

**Missing values:**
Find missing elements

    missing_series.isnull()
    has_values.notnull()
    pd.isnull(test_series)
    pd.notnull(test_series)

Drop missing elements

    missing_series.dropna()

Fill missing values

    missing_series.fillna(-1)

**Dropping duplicates:**

    data.drop_duplicates()
**Converting columns from string to numeric:**

    my_df['new_column'] = pd.to_numeric(my_df['column_name'], errors='coerce')
    # 'coerce' makes any errors NaN
    # 'raise' raises and exception
    # 'ignore' returns input

**Adding conditional columns using mask:**

    my_df['new_column'] = 0
    mask = (my_df['column'] == 0) & (my_df['another_column'] == 1)
    my_df.ix[mask,'new_column'] = 1

## Transformations
**To flip the index and columns:**
T is short-form for "transpose", which flips rows and columns of a matrix

    my_df.T 

**Reindex:**
Sorts dataframe based on new index and creates missing value rows for new indexes.

    my_df.reindex(['a', 'b', 'c', 'd', 'e']) #reindex indexes
    my_df.reindex(columns=new_col_list) #reindex columns

**Sorting:**
Sort the DataFrame by its index.

    df.sort_index()
    df.sort_index(axis=1) #sort columns
Sort the DataFrame by value

    df.sort_values(by='column_name', ascending = True)

**Ranking:**
Rank the values in order and assign values

    rank = my_df['col_name'].rank(ascending=False)

**Applying functions to rows and columns of dataframes:**

    def function_name(value):
    	# do something
    	return value
    df['new_column'] = df['col_name'].apply(function_name)
    OR 
    df.loc['total'] = df.apply(function_name, axis='columns')
    df.applymap(function_name) # for element-wise functions

**Value counts:**
To get counts of various values in a row or column

    df['col_name'].value_counts()

**Descriptive statistics:**

    df.describe()
    df['column_name'].describe()

**Find max of column or row:**
To get the maximum value: `df.max()`
To get the maximum index or label: `df.idxmax()`
To get column maxes, easiest to transform with `.T` then use `max()` or `idxmax()`.

**Find mean of column or row:**

    df.mean(axis='columns', skipna=False)

**Get percentiles via qcut:**

    pd.qcut(df['col_name'], 10) # gets cutoff value for the 10th percentile

**Creating quartiles:**

    quartiles = pd.cut(df['column_name'], 4) # gives 4 equal size buckets

**Creating bins of values:**

    bins = [0, 5, 10, 15, 20]
    my_df['bins'] = pd.cut(data, bins)

**Replacing values in a column with new values:**

    my_df[‘col_name’].replace([‘name_1’,’name_2’],[‘new_1’,’new_2’])

**Adding columns, rows or series**
Simply use `df['a'] + df['b']` but know that any null values in one will result in a null result, unless you fill nulls with 0 first.

To get around this, use the add function:

    df1.add(df2, fill_value=0)

**Transforming text:**

    my_df['column_name'].str.lower()

## Merge, pivot table and groupby
### Merge
pandas.merge connects rows in DataFrames based on one or more keys. Similar to join operations in SQL

    pd.merge(df1, df2, on='key')
    pd.merge(df3, df4, left_on='lkey', right_on='rkey', suffixes=('_left', '_right'))
    pd.merge(df1, df2, how='outer')
    # options for how include inner, outer, left and right

In some cases, the merge key(s) in a DataFrame will be found in its index. In this case, you can pass left_index=True or right_index=True (or both) to indicate that the index should be used as the merge key

### Join

    left2.join(right2, how='outer', lsuffix='', rsuffix='', sort=False)

### Concatenate
pandas.concat concatenates or “stacks” together objects along an axis

    pd.concat([s1, s2]) # results in a long series
    pd.concat([s1, s2], axis=1) # results in a dataframe
    pd.concat([df1, df2]) # concatentate rows of two dataframes

Combining data with overlap

    s1.combine_first(s2)

### Pivot table
[Pivot table Documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.pivot_table.html)

    pivoted = pd.pivot_table(my_df, index='col_name', columns='col_name', values='count', aggfunc=sum, fill_value=0)

Apart from pivot_table(), there are two main ways to reshape the data:
-   stack, which "rotates" or pivots from columns to index, and
-   unstack, which does the opposite.

### Groupby
[Groupby Documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.groupby.html)

    my_df.groupby(by=['col_or_list_of_columns'], axis = 0, as_index = True)
    # axis = 0 is group by columns
    # as_index = True makes the index out of group by variables, as_index = False effectively does a SQL-style group by

Aggregating with functions:

    my_df.groupby(‘column_name’).mean()

Group aggregations - 
-   .mean()
-   .count()
-   .min()
-   .max()
-   Defining an aggregation function -
	- Define function that takes in a series (column) and returns one value
	- Apply the function in the groupby `my_df.groupby([‘col_1’,’col_2’])[[‘speed’]].agg(function_name)`
	- Apply multiple functions - `my_df.groupby([‘col_1’,’col_2’])[[‘speed’]].agg([‘mean’,’count’, funct_name])`

You can also group by python functions, such as:

    my_df['col_name]].groupby(len).count() # gets the number of rows with column character length

**Multilevel hierarchies:**
To unstack hierarchies, use `.unstack()`

If you need to swap the levels of a dataframe, use the level names or numbers

    frame.swaplevel('key1', 'key2')

Set index and reset index help you create and remove levels

    frame2 = frame.set_index(['c', 'd'])
    frame2.reset_index()

# Time Series Analysis

    From datetime import datetime

When reading a file with “time” into pandas, use parse_dates = True and set the index to the date column

Extracting from datetime -
-   Date_var.year 
-   Date_var.month
-   Date_var.day
-   Date_var.dayofweek
-   Date_var.quarter

The general solution to slicing is to create a range of dates and select a slice using that range. There are many options:
-   For calendar dates, use _date_range()_, with a common case being: `date_range(start_date, end_date, freq)`
-   The "freq" can be:
	- 'D' for daily
	-  'B' for each business day
	- 'W-MON', 'W-TUE', ... for once a week on Monday, Tuesday, ...
	- 'M' for monthly
	-  'WOM-3FRI' for third Friday of the month (usual for option expiry dates)

For percent changes (i.e. to see what the closing time was the day before), you can use `.shift(1)` which shifts values up 1 row

**Calculate percent changes:**

    df['column_name'].pct_change()

**Moving averages:**

    df['Close'].rolling(window=30, min_periods=10).mean()

-   df['Close']: use this time series
-   window=30: take a window of closes over the past 30 days
-   min_periods=10: If the past 30 days don't exist (say, today is the 25th day from the start of the time series), what do we do? This option says:
-   for the first 10 days of the time series, the moving average doesn't exist (NaN)
-   from the 10th to 30th day, take the average of as many days as are available (so for the 25th day, we average the past 25 days)
-   from the 30th day onwards, take the average of the past 30 days
-   mean(): Compute the mean for this rolling window

# Statistics
**Linspace for binning:**

    my_df.hist(ax=ax1, bins=np.linspace(100, 400, 20)) # Creates 20 bins from 100 to 400
    ax1.set_xlabel('x label')
     ax1.set_ylabel('y label')

 And a bell curve with exactly the same mean and standard deviation.

     x = np.linspace(60, 75, 100)

### Correlations

    my_df['col_1'].corr(my_df['col_2'])

*Tip: if the relationship is not quite linear, it can be helpful to compare correlation between the ranks of two variables (a.k.a. Spearman effect)*

### Regressions
**Least squares regression**

    pd.ols()

**Multiple regression**

    import statsmodels.api as sm
    from patsy import dmatrices

For multiple regression, we take two steps:
-   Create the design matrices, i.e., the DataFrames which say which variable we want to predict (called y), and which variable(s) we will use to predict y (called X)
-   Run the linear regression, and inspect the results

1.  Create design matrices

    y, X = dmatrices('Predicted_column ~ Explanatory_column', data=my_df, return_type='dataframe')

2.  Run the linear regression

    model = sm.OLS(y, X) # Set up the model
    result = model.fit() # Fit model (find the intercept and slopes)
    print result.summary()

*Regression on multiple variables*

    y, X = dmatrices('Predicted_column ~ Explanatory_column1 + Explanatory_column2', data=my_df, return_type='dataframe')

Dummy variables - if we have 5 variables, we need 4 dummy variables because one has to be set as the base variable





<!--stackedit_data:
eyJoaXN0b3J5IjpbODY2NzE0ODAzLDE2MTA0MTg0NjcsMTE2NT
U2NDE5OSwtMTg5NTM4MDgzNSwyMDUyNjg4MzEyLC0yMzc0ODUy
NCwxNzE2ODM2ODc4LDExNzI2NTYzNTEsLTE0MzQ1MTU1NDksLT
Q3MjIzNDM5NiwtMTc3MDU1NTIxOV19
-->