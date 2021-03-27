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
    
# Reading CSV files 
Comma Seperated Values

        df_sales=pd.read_csv('sales.csv.zip')
        df_sales.head().iloc[:,0:5]

output:

            Region	Country	Item Type	Sales Channel	Order Priority
        0	Sub-Saharan Africa	Chad	Office Supplies	Online	L
        1	Europe	Latvia	Beverages	Online	C
        2	Middle East and North Africa	Pakistan	Vegetables	Offline	C
        3	Sub-Saharan Africa	Democratic Republic of the Congo	Household	Online	C
        4	Europe	Czech Republic	Beverages	Online	C
        
## some operations with csv files

info

        df_sales.info()

output

        <class 'pandas.core.frame.DataFrame'>
        RangeIndex: 10000 entries, 0 to 9999
        Data columns (total 14 columns):
         #   Column          Non-Null Count  Dtype  
        ---  ------          --------------  -----  
         0   Region          10000 non-null  object 
         1   Country         10000 non-null  object 
         2   Item Type       10000 non-null  object 
         3   Sales Channel   10000 non-null  object 
         4   Order Priority  10000 non-null  object 
         5   Order Date      10000 non-null  object 
         6   Order ID        10000 non-null  int64  
         7   Ship Date       10000 non-null  object 
         8   Units Sold      10000 non-null  int64  
         9   Unit Price      10000 non-null  float64
         10  Unit Cost       10000 non-null  float64
         11  Total Revenue   10000 non-null  float64
         12  Total Cost      10000 non-null  float64
         13  Total Profit    10000 non-null  float64
        dtypes: float64(5), int64(2), object(7)
        memory usage: 1.1+ MB

describe

        df_sales.describe().head()

output  


        Order ID	Units Sold	Unit Price	Unit Cost	Total Revenue	Total Cost	Total Profit
        count	1.000000e+04	10000.000000	10000.000000	10000.000000	1.000000e+04	1.000000e+04	10000.000000
        mean	5.498719e+08	5002.855900	268.143139	188.806639	1.333355e+06	9.382658e+05	395089.347193
        std	2.607835e+08	2873.246454	217.944092	176.445907	1.465026e+06	1.145914e+06	377554.960738
        min	1.000892e+08	2.000000	9.330000	6.920000	1.679400e+02	1.245600e+02	43.380000
        25%	3.218067e+08	2530.750000	109.280000	56.670000	2.885511e+05	1.647855e+05	98329.140000

## Making csv files

        from io import StringIO
        str_data= ('col1,col2,col3,col4,col5\n'
                  'A,1,2,3,4\n'
                  'B,4,5,6,7\n'
                  'C,7,8,9,10\n'
                  'D,10,11,,12')
        df_str=pd.read_csv(StringIO(str_data))

        df_str

output

            col1	col2	col3	col4	col5
        0	A	1	2	3.0	4
        1	B	4	5	6.0	7
        2	C	7	8	9.0	10
        3	D	10	11	NaN	12

## parameters

Code

        df_test1=pd.read_csv(StringIO(str_data),index_col=0, usecols=['col1','col2','col4','col5'],dtype=object)

        print(df_test1, "\n", "col2, 1st index is", df_test1['col2'][1], "and its type is",(type(df_test1['col2'][1])))

output

             col2 col4 col5
        col1               
        A       1    3    4
        B       4    6    7
        C       7    9   10
        D      10  NaN   12 
         col2, 1st index is 4 and its type is <class 'str'>
         
Code for type int

        df_test2=pd.read_csv(StringIO(str_data),usecols=['col3','col2','col5'],dtype=int) #col1 has alphabets and col4 has 1 NA value which cant be int

        print(df_test2, "\n", "col2, 1st index is", df_test2['col2'][1], "and its type is",(type(df_test2['col2'][1])))
        
output

           col2  col3  col5
        0     1     2     4
        1     4     5     7
        2     7     8    10
        3    10    11    12 
         col2, 1st index is 4 and its type is <class 'numpy.int32'>
         
Code for all column different types

        df_test3=pd.read_csv(StringIO(str_data), usecols=['col1','col2','col3','col5'],index_col=None, dtype={'col1':object,'col2':float,'col3':int,'col5':'Int64'})

        print(df_test3)
        print("col1, 1st index is", df_test3['col1'][1], "and its type is",(type(df_test3['col1'][1])))
        print("col2, 1st index is", df_test3['col2'][1], "and its type is",(type(df_test3['col2'][1])))
        print("col3, 1st index is", df_test3['col3'][1], "and its type is",(type(df_test3['col3'][1])))
        print("col5, 1st index is", df_test3['col5'][1], "and its type is",(type(df_test3['col5'][1])))
        
output

          col1  col2  col3  col5
        0    A   1.0     2     4
        1    B   4.0     5     7
        2    C   7.0     8    10
        3    D  10.0    11    12
        col1, 1st index is B and its type is <class 'str'>
        col2, 1st index is 4.0 and its type is <class 'numpy.float64'>
        col3, 1st index is 5 and its type is <class 'numpy.int32'>
        col5, 1st index is 7 and its type is <class 'numpy.int64'>
        
escape char code

        str_esc=('col1,col2\n hey/, use escape here,  GG')

        df_esc=(pd.read_csv(StringIO(str_esc),escapechar='/'))

        df_esc
        
output


                            col1	col2
        0	hey, use escape here	GG
        
# Read json to csv

        Raw_Data = '{"Name" : "Pranav Sharma" , "email" : "pranavsharma@ABC.123" , "profile" : [{"Title1" : "team leader" , "Title2" : "Sr. developer"}]}'

        df_raw= pd.read_json(Raw_Data)
        df_wine=pd.read_csv('https://archive.ics.uci.edu/ml/machine-learning-databases/wine/wine.data',header=None)

        df_wine.head()
        
output

            0	1	    2	    3	    4	    5	6	    7	    8	    9	    10	    11	    12	    13
        0	1	14.23	1.71	2.43	15.6	127	2.80	3.06	0.28	2.29	5.64	1.04	3.92	1065
        1	1	13.20	1.78	2.14	11.2	100	2.65	2.76	0.26	1.28	4.38	1.05	3.40	1050
        2	1	13.16	2.36	2.67	18.6	101	2.80	3.24	0.30	2.81	5.68	1.03	3.17	1185
        3	1	14.37	1.95	2.50	16.8	113	3.85	3.49	0.24	2.18	7.80	0.86	3.45	1480
        4	1	13.24	2.59	2.87	21.0	118	2.80	2.69	0.39	1.82	4.32	1.04	2.93	735
json to csv

        df_wine.to_csv('wine.csv')
        df_raw.to_json()
        
output

        '{"Name":{"0":"Pranav Sharma"},"email":{"0":"pranavsharma@ABC.123"},"profile":{"0":{"Title1":"team leader","Title2":"Sr. developer"}}}'

without the orient parameter key value pairs are made with columns but they should be made with respect to records 

        df_raw.to_json(orient='records')

output

        '[{"Name":"Pranav Sharma","email":"pranavsharma@ABC.123","profile":{"Title1":"team leader","Title2":"Sr. developer"}}]'
        
# Reading HTML pages

FAILED BANK LIST

        url= 'https://www.fdic.gov/resources/resolutions/bank-failures/failed-bank-list/'

        dfs=pd.read_html(url, match= 'State', header= None,index_col= 4)
        print(dfs[0].head())

output

                                                           Bank Name  \
        Acquiring Institution                                          
        Equity Bank                                Almena State Bank   
        United Fidelity Bank, fsb         First City Bank of Florida   
        MVB Bank, Inc.                          The First State Bank   
        Farmers and Merchants Bank                Ericson State Bank   
        Industrial Bank             City National Bank of New Jersey   

                                                 City State   Cert       Closing Date  
        Acquiring Institution                                                          
        Equity Bank                            Almena    KS  15426   October 23, 2020  
        United Fidelity Bank, fsb   Fort Walton Beach    FL  16748   October 16, 2020  
        MVB Bank, Inc.                  Barboursville    WV  14361      April 3, 2020  
        Farmers and Merchants Bank            Ericson    NE  18265  February 14, 2020  
        
COUNTRY NUMBER CODES

        url2= 'https://countrycode.org/'

        dfs2=pd.read_html(url2, index_col= 0)
        print(dfs2[0].head())
        
output

                       COUNTRY CODE ISO CODES  POPULATION  AREA KM2       GDP $USD
        COUNTRY                                                                   
        Afghanistan              93  AF / AFG    29121286    647500  20.65 Billion
        Albania                 355  AL / ALB     2986952     28748   12.8 Billion
        Algeria                 213  DZ / DZA    34586184   2381740  215.7 Billion
        American Samoa        1-684  AS / ASM       57881       199  462.2 Million
        Andorra                 376  AD / AND       84000       468    4.8 Billion
        
        
        
# Reading excel files

accessing a local excel file

        df_excel=pd.read_excel('Book1.xlsx')
        df_excel

output

          pranav  1  2  3   4    5
        0    mom  3  4  5   6  7.0
        1    dad  5  6  7   8  9.0
        2    sid  7  8  9  10  NaN
        
        
# Pickling
updatting the locally accesable excel sheet 

        df_excel.iloc[-2:-1,:]=0
        print(df_excel)

output

          pranav  1  2  3   4    5
        0    mom  3  4  5   6  7.0
        1      0  0  0  0   0  0.0
        2    sid  7  8  9  10  NaN

pickling


        df_excel.to_pickle('excl_sheet')

        pd.read_pickle("excl_sheet")

output

          pranav  1  2  3   4    5
        0    mom  3  4  5   6  7.0
        1      0  0  0  0   0  0.0
        2    sid  7  8  9  10  NaN
