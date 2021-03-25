# pandas
## importing libraries 


    import pandas as pd
    import numpy as np
    
# making a data frame   
    randint= np.random.randint(0,20,20).reshape(4,5)
    df= pd.DataFrame(randint, index=['row1', 'row2', "row3", 'row4'],columns=['column1','column2','column3','column4','column5'])
    df
    
output

         column1	column2	column3	column4	column5
    row1	12	0	17	0	11
    row2	10	8	5	9	12
    row3	12	3	11	13	9
    row4	5	17	7	13	16
    
to save as csv file

        df.to_csv('comma_seperated')
        
# Accessing elements
### 1) .loc
location- focuses only on row indexes
### 2) .iloc
index location- involves both rows and columns indexes
d1

    print(df.loc[['row1','row2']])
    d1_type=type(df.loc['row1'])
    d1_type
output

          column1  column2  column3  column4  column5
    row1       15        7        3       13       11
    row2       11       16        5       10       18
    pandas.core.series.Series
d2

    print(df.iloc[0:1,:])
    d2_type=type(df.iloc[0:1,:])
    d2_type

output

          column1  column2  column3  column4  column5
    row1       15        7        3       13       11
    pandas.core.frame.DataFrame

d3

    print(df.iloc[0:1,0])
    d3_type=type(df.iloc[0:1,0])
    d3_type

output

    row1    15
    Name: column1, dtype: int32
    pandas.core.series.Series

d4

    print(df.iloc[0:2,2:])
    d4_type=type(df.iloc[0:2,2:])
    d4_type

output

          column3  column4  column5
    row1        3       13       11
    row2        5       10       18
    pandas.core.frame.DataFrame
    
# Converting dataframes to arrays

    df.iloc[1:3,1:4].values

output

    array([[12, 12,  0],
           [18, 12, 18]])
# operations in pandas

null

    df.isnull().sum() 

output

    column1    0
    column2    0
    column3    0
    column4    0
    column5    0
    dtype: int64

column values count

    df['column1'].value_counts()

output

    4     1
    10    1
    0     1
    8     1
    Name: column1, dtype: int64

column unique values

    df['column2'].unique
    
output

    <bound method Series.unique of row1     4
    row2    12
    row3    18
    row4     0
    Name: column2, dtype: int32>
