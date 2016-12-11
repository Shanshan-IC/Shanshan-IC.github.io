---
layout:     post
title:      Python For Data Analysis Introduction to Pandas
category:   [Python] 
tags:		[Python, Data Analysis, Pandas]
---

It is learned from [Jupyter](http://nbviewer.jupyter.org/urls/gist.github.com/fonnesbeck/5850375/raw/c18cfcd9580d382cb6d14e4708aab33a0916ff3e/1.+Introduction+to+Pandas.ipynb)

{% highlight Python %}
import pandas as pd
import numpy as np

print "------------ Index 1 ---------------------"
# Series is a single vector
counts = pd.Series([632, 1322, 242, 1232])
print counts
print counts.values
print counts.index

print "------------ Index 2 ---------------------"
bacteria = pd.Series([632, 1322, 242, 1232],
                     index = ['Firmicutes', 'Proteobacteria', 'Actinobacteria', 'Bacteroidetes'])
print bacteria
print bacteria['Actinobacteria']
print bacteria[[name.endswith('bacteria') for name in bacteria.index]]
print bacteria[0]

# here we still can use the math functions in the numpy
np.log(bacteria)
print(bacteria)

print bacteria[bacteria > 10]

print "------------ Index 3 ---------------------"
# we can also create a dict for the series
bacteria_dict = {'Firmicutes': 632, 'Proteobacteria': 1638, 'Actinobacteria': 569, 'Bacteroidetes': 115}
print pd.Series(bacteria_dict)

bacteria2 = pd.Series(bacteria_dict, index=['Cyanobacteria','Firmicutes','Proteobacteria','Actinobacteria'])
print bacteria2
# check null
print bacteria2.isnull()
# align data
print bacteria + bacteria2

print "------------ Index 4 ---------------------"
# Data Frame another data structure
data = pd.DataFrame({'value':[632, 1638, 569, 115, 433, 1130, 754, 555],
                     'patient':[1, 1, 1, 1, 2, 2, 2, 2],
                     'phylum':['Firmicutes', 'Proteobacteria', 'Actinobacteria',
    'Bacteroidetes', 'Firmicutes', 'Proteobacteria', 'Actinobacteria', 'Bacteroidetes']})
print data
print data.columns
print data['value']
print type(data.value)
print type(data[['value']])

print "------------ Index 5 ---------------------"
#create a DataFrame with a dict of dicts
data2 = pd.DataFrame({0: {'patient': 1, 'phylum': 'Firmicutes', 'value': 632},
                    1: {'patient': 1, 'phylum': 'Proteobacteria', 'value': 1638},
                    2: {'patient': 1, 'phylum': 'Actinobacteria', 'value': 569},
                    3: {'patient': 1, 'phylum': 'Bacteroidetes', 'value': 115},
                    4: {'patient': 2, 'phylum': 'Firmicutes', 'value': 433},
                    5: {'patient': 2, 'phylum': 'Proteobacteria', 'value': 1130},
                    6: {'patient': 2, 'phylum': 'Actinobacteria', 'value': 754},
                    7: {'patient': 2, 'phylum': 'Bacteroidetes', 'value': 555}})
print data2
data2 = data2.T
# Its important to note that the Series returned
# when a DataFrame is indexted is merely a view on the DataFrame,
# and not a copy of the data itself. So you must be cautious when manipulating this data:
vals = data2.value
print vals
vals[5] = 0
print data2
# it will be changed into 0 also , so you have to do
vals = data2.value.copy()
vals[5] = 100 #in this way, it wont be changed

print "------------ Index 6 ---------------------"
# Add new columns
data2['month'] = ['Jan'] * len(data2)
print data2
# delete the columns
del data2['month']
print data2

print "------------ Index 7 ---------------------"
# because of the mix of string and integer (and NaN) values, the dtype of the array is object.
# The dtype will automatically be chosen to be as general as needed to accomodate all the columns.
df = pd.DataFrame({'foo': [1,2,3], 'bar':[0.4, -1.0, 4.5]})
print df.values

print "------------ Index 8 ---------------------"
bacteria2.index = bacteria.index
print bacteria2

print "------------ Index 9 ---------------------"
#import data
mb = pd.read_csv("data/microbiome.csv").head(5)
print mb
mb = pd.read_table("data/microbiome.csv", sep=',')
# only read some columns you need
mb = pd.read_csv("data/microbiome.csv", index_col=['Taxon','Patient'])
print mb.head()
# skip some rows
print pd.read_csv("data/microbiome.csv", skiprows=[3,4,6]).head()

print "------------ Index 10 ---------------------"
# import excel
mb2 = pd.read_excel('data/microbiome/MID2.xls', sheetname='Sheet 1', header=None)
print mb2.head()

print "------------ Index 11 ---------------------"
# pandas
baseball = pd.read_csv("data/baseball.csv")
print baseball.head()
player_id = baseball.player + baseball.year.astype(str)
baseball_newind = baseball.copy()
baseball_newind.index = player_id
print baseball_newind.head()

print baseball_newind.index.is_unique
pd.Series(baseball_newind.index).value_counts()

# we can change the order of index
print baseball.reindex(baseball.index[::-1]).head()
# when the index is not sequential, we can use the range to fill them using Nan
id_range = range(baseball.index.values.min(), baseball.index.values.max())
print baseball.reindex(id_range).head()
# maybe not use nan to fill in, use the value you want
baseball.reindex(id_range, method='ffill', columns=['player','year']).head()
print baseball.shape
# delete columns
baseball.drop(['ibb','hbp'], axis=1)
print baseball_newind[baseball_newind.ab>500]
# print baseball_newind.ix['gonzalu01ARI2006', ['h','X2b', 'X3b', 'hr']]

print "------------ Index 12 ---------------------"
# Some Operations
# print baseball.ix[89521]["player"]
print baseball.hr - baseball.hr.max()

# we can use apply to each column or row of dataframe
stats = baseball[['h','X2b', 'X3b', 'hr']]
print stats
diff = stats - stats.xs(7)
print diff[:10]
print stats.apply(np.median)
stat_range = lambda x: x.max() - x.min()
stats.apply(stat_range)

slg = lambda x: (x['h']-x['X2b']-x['X3b']-x['hr'] + 2*x['X2b'] + 3*x['X3b'] + 4*x['hr'])/(x['ab']+1e-6)
baseball.apply(slg, axis=1).apply(lambda x: '%.3f' % x)

print "------------ Index 13 ---------------------"
# sorting and ranking
# sorting
print baseball_newind.sort_index().head()
print baseball_newind.sort_index(ascending=False).head()
print baseball.hr.order(ascending=False)
# multiple sort
print baseball[['player','sb','cs']].sort_index(ascending=[False,True], by=['sb', 'cs']).head(10)

# ranking
# Ranking does not re-arrange data, but instead returns an index that ranks each value relative to others in the Series.
print baseball.hr.rank()
# Calling the DataFrame's rank method results in the ranks of all columns:
baseball.rank(ascending=False).head()

print "------------ Index 14 ---------------------"
# Hierarchical indexing
baseball_h = baseball.set_index(['year', 'team', 'player'])
print baseball_h
print baseball_h.index.is_unique

frame = pd.DataFrame(np.arange(12).reshape((4, 3)),
                index = [['a', 'a', 'b', 'b'], [1, 2, 1, 2]],
                columns = [['Ohio', 'Ohio', 'Colorado'], ['Green', 'Red', 'Green']])
print frame

print "------------ Index 15 ---------------------"
# Missing Data
foo = pd.Series([None, -3, None, 'foobar'])
print foo
print foo.isnull()

print bacteria2
bacteria2.dropna()
print bacteria2
# This can be overridden by passing the how='all' argument, which only drops a row when every field is a missing value.
bacteria2.dropna(how='all')
# fill 0 in the nan field
bacteria2.fillna(0)

print "------------ Index 16 ---------------------"
# Data Summaries
print baseball.sum()
print baseball.mean()
print baseball.mean(skipna=False)
# a useful summary used
print baseball.describe()
# correlation and covariance
print baseball.hr.cov(baseball.X2b)
print baseball.hr.corr(baseball.X2b)
print baseball.corr()

print mb.sum(level='Taxon')

print "------------ Index 17 ---------------------"
# wrint data
mb.to_csv("mb.csv")
# An efficient way of storing data to disk is in binary format
baseball.to_pickle("baseball_pickle")
# The complement to to_pickle is the read_pickle function, which restores the pickle to a DataFrame or Series:
pd.read_pickle("baseball_pickle")

{% endhighlight %}

Output 

{% highlight Python %}
/System/Library/Frameworks/Python.framework/Versions/2.7/bin/python2.7 /Users/fushanshan/PycharmProjects/Data/DataAnalysis/Tut1.py
------------ Index 1 ---------------------
0     632
1    1322
2     242
3    1232
dtype: int64
[ 632 1322  242 1232]
RangeIndex(start=0, stop=4, step=1)
------------ Index 2 ---------------------
Firmicutes         632
Proteobacteria    1322
Actinobacteria     242
Bacteroidetes     1232
dtype: int64
242
Proteobacteria    1322
Actinobacteria     242
dtype: int64
632
Firmicutes         632
Proteobacteria    1322
Actinobacteria     242
Bacteroidetes     1232
dtype: int64
Firmicutes         632
Proteobacteria    1322
Actinobacteria     242
Bacteroidetes     1232
dtype: int64
------------ Index 3 ---------------------
Actinobacteria     569
Bacteroidetes      115
Firmicutes         632
Proteobacteria    1638
dtype: int64
Cyanobacteria        NaN
Firmicutes         632.0
Proteobacteria    1638.0
Actinobacteria     569.0
dtype: float64
Cyanobacteria      True
Firmicutes        False
Proteobacteria    False
Actinobacteria    False
dtype: bool
Actinobacteria     811.0
Bacteroidetes        NaN
Cyanobacteria        NaN
Firmicutes        1264.0
Proteobacteria    2960.0
dtype: float64
------------ Index 4 ---------------------
   patient          phylum  value
0        1      Firmicutes    632
1        1  Proteobacteria   1638
2        1  Actinobacteria    569
3        1   Bacteroidetes    115
4        2      Firmicutes    433
5        2  Proteobacteria   1130
6        2  Actinobacteria    754
7        2   Bacteroidetes    555
Index([u'patient', u'phylum', u'value'], dtype='object')
0     632
1    1638
2     569
3     115
4     433
5    1130
6     754
7     555
Name: value, dtype: int64
<class 'pandas.core.series.Series'>
<class 'pandas.core.frame.DataFrame'>
------------ Index 5 ---------------------
                  0               1               2              3  \
patient           1               1               1              1   
phylum   Firmicutes  Proteobacteria  Actinobacteria  Bacteroidetes   
value           632            1638             569            115   

                  4               5               6              7  
patient           2               2               2              2  
phylum   Firmicutes  Proteobacteria  Actinobacteria  Bacteroidetes  
value           433            1130             754            555  
0     632
1    1638
2     569
3     115
4     433
5    1130
6     754
7     555
Name: value, dtype: object
  patient          phylum value
0       1      Firmicutes   632
1       1  Proteobacteria  1638
2       1  Actinobacteria   569
3       1   Bacteroidetes   115
4       2      Firmicutes   433
5       2  Proteobacteria     0
6       2  Actinobacteria   754
7       2   Bacteroidetes   555
------------ Index 6 ---------------------
  patient          phylum value month
0       1      Firmicutes   632   Jan
1       1  Proteobacteria  1638   Jan
2       1  Actinobacteria   569   Jan
3       1   Bacteroidetes   115   Jan
4       2      Firmicutes   433   Jan
5       2  Proteobacteria     0   Jan
6       2  Actinobacteria   754   Jan
7       2   Bacteroidetes   555   Jan
  patient          phylum value
0       1      Firmicutes   632
1       1  Proteobacteria  1638
2       1  Actinobacteria   569
3       1   Bacteroidetes   115
4       2      Firmicutes   433
5       2  Proteobacteria     0
6       2  Actinobacteria   754
7       2   Bacteroidetes   555
------------ Index 7 ---------------------
[[ 0.4  1. ]
 [-1.   2. ]
 [ 4.5  3. ]]
------------ Index 8 ---------------------
Firmicutes           NaN
Proteobacteria     632.0
Actinobacteria    1638.0
Bacteroidetes      569.0
dtype: float64
------------ Index 9 ---------------------
        Taxon  Patient  Tissue  Stool
0  Firmicutes        1     632    305
1  Firmicutes        2     136   4182
2  Firmicutes        3    1174    703
3  Firmicutes        4     408   3946
4  Firmicutes        5     831   8605
                    Tissue  Stool
Taxon      Patient               
Firmicutes 1           632    305
           2           136   4182
           3          1174    703
           4           408   3946
           5           831   8605
        Taxon  Patient  Tissue  Stool
0  Firmicutes        1     632    305
1  Firmicutes        2     136   4182
2  Firmicutes        5     831   8605
3  Firmicutes        7     718    717
4  Firmicutes        8     173     33
------------ Index 10 ---------------------
                                                   0   1
0  Archaea "Crenarchaeota" Thermoprotei Acidiloba...   2
1  Archaea "Crenarchaeota" Thermoprotei Acidiloba...  14
2  Archaea "Crenarchaeota" Thermoprotei Desulfuro...  23
3  Archaea "Crenarchaeota" Thermoprotei Desulfuro...   1
4  Archaea "Crenarchaeota" Thermoprotei Desulfuro...   2
------------ Index 11 ---------------------
      id     player  year  stint team  lg   g  ab  r   h  ...   rbi   sb   cs  \
0  88641  womacto01  2006      2  CHN  NL  19  50  6  14  ...   2.0  1.0  1.0   
1  88643  schilcu01  2006      1  BOS  AL  31   2  0   1  ...   0.0  0.0  0.0   
2  88645  myersmi01  2006      1  NYA  AL  62   0  0   0  ...   0.0  0.0  0.0   
3  88649  helliri01  2006      1  MIL  NL  20   3  0   0  ...   0.0  0.0  0.0   
4  88650  johnsra05  2006      1  NYA  AL  33   6  0   1  ...   0.0  0.0  0.0   

   bb   so  ibb  hbp   sh   sf  gidp  
0   4  4.0  0.0  0.0  3.0  0.0   0.0  
1   0  1.0  0.0  0.0  0.0  0.0   0.0  
2   0  0.0  0.0  0.0  0.0  0.0   0.0  
3   0  2.0  0.0  0.0  0.0  0.0   0.0  
4   0  4.0  0.0  0.0  0.0  0.0   0.0  

[5 rows x 23 columns]
                  id     player  year  stint team  lg   g  ab  r   h  ...   \
womacto012006  88641  womacto01  2006      2  CHN  NL  19  50  6  14  ...    
schilcu012006  88643  schilcu01  2006      1  BOS  AL  31   2  0   1  ...    
myersmi012006  88645  myersmi01  2006      1  NYA  AL  62   0  0   0  ...    
helliri012006  88649  helliri01  2006      1  MIL  NL  20   3  0   0  ...    
johnsra052006  88650  johnsra05  2006      1  NYA  AL  33   6  0   1  ...    

               rbi   sb   cs  bb   so  ibb  hbp   sh   sf  gidp  
womacto012006  2.0  1.0  1.0   4  4.0  0.0  0.0  3.0  0.0   0.0  
schilcu012006  0.0  0.0  0.0   0  1.0  0.0  0.0  0.0  0.0   0.0  
myersmi012006  0.0  0.0  0.0   0  0.0  0.0  0.0  0.0  0.0   0.0  
helliri012006  0.0  0.0  0.0   0  2.0  0.0  0.0  0.0  0.0   0.0  
johnsra052006  0.0  0.0  0.0   0  4.0  0.0  0.0  0.0  0.0   0.0  

[5 rows x 23 columns]
False
       id     player  year  stint team  lg    g   ab   r    h  ...    rbi  \
99  89534  alomasa02  2007      1  NYN  NL    8   22   1    3  ...    0.0   
98  89533   aloumo01  2007      1  NYN  NL   87  328  51  112  ...   49.0   
97  89530  ausmubr01  2007      1  HOU  NL  117  349  38   82  ...   25.0   
96  89526  benitar01  2007      1  SFN  NL   19    0   0    0  ...    0.0   
95  89525  benitar01  2007      2  FLO  NL   34    0   0    0  ...    0.0   

     sb   cs  bb    so  ibb  hbp   sh   sf  gidp  
99  0.0  0.0   0   3.0  0.0  0.0  0.0  0.0   0.0  
98  3.0  0.0  27  30.0  5.0  2.0  0.0  3.0  13.0  
97  6.0  1.0  37  74.0  3.0  6.0  4.0  1.0  11.0  
96  0.0  0.0   0   0.0  0.0  0.0  0.0  0.0   0.0  
95  0.0  0.0   0   0.0  0.0  0.0  0.0  0.0   0.0  

[5 rows x 23 columns]
      id     player  year  stint team  lg   g  ab  r   h  ...   rbi   sb   cs  \
0  88641  womacto01  2006      2  CHN  NL  19  50  6  14  ...   2.0  1.0  1.0   
1  88643  schilcu01  2006      1  BOS  AL  31   2  0   1  ...   0.0  0.0  0.0   
2  88645  myersmi01  2006      1  NYA  AL  62   0  0   0  ...   0.0  0.0  0.0   
3  88649  helliri01  2006      1  MIL  NL  20   3  0   0  ...   0.0  0.0  0.0   
4  88650  johnsra05  2006      1  NYA  AL  33   6  0   1  ...   0.0  0.0  0.0   

   bb   so  ibb  hbp   sh   sf  gidp  
0   4  4.0  0.0  0.0  3.0  0.0   0.0  
1   0  1.0  0.0  0.0  0.0  0.0   0.0  
2   0  0.0  0.0  0.0  0.0  0.0   0.0  
3   0  2.0  0.0  0.0  0.0  0.0   0.0  
4   0  4.0  0.0  0.0  0.0  0.0   0.0  

[5 rows x 23 columns]
(100, 23)
                  id     player  year  stint team  lg    g   ab   r    h  \
gonzalu012006  88653  gonzalu01  2006      1  ARI  NL  153  586  93  159   
vizquom012007  89347  vizquom01  2007      1  SFN  NL  145  513  54  126   
thomafr042007  89361  thomafr04  2007      1  TOR  AL  155  531  63  147   
rodriiv012007  89389  rodriiv01  2007      1  DET  AL  129  502  50  141   
griffke022007  89462  griffke02  2007      1  CIN  NL  144  528  78  146   
delgaca012007  89489  delgaca01  2007      1  NYN  NL  139  538  71  139   
biggicr012007  89523  biggicr01  2007      1  HOU  NL  141  517  68  130   

               ...    rbi    sb   cs  bb     so   ibb   hbp    sh   sf  gidp  
gonzalu012006  ...   73.0   0.0  1.0  69   58.0  10.0   7.0   0.0  6.0  14.0  
vizquom012007  ...   51.0  14.0  6.0  44   48.0   6.0   1.0  14.0  3.0  14.0  
thomafr042007  ...   95.0   0.0  0.0  81   94.0   3.0   7.0   0.0  5.0  14.0  
rodriiv012007  ...   63.0   2.0  2.0   9   96.0   1.0   1.0   1.0  2.0  16.0  
griffke022007  ...   93.0   6.0  1.0  85   99.0  14.0   1.0   0.0  9.0  14.0  
delgaca012007  ...   87.0   4.0  0.0  52  118.0   8.0  11.0   0.0  6.0  12.0  
biggicr012007  ...   50.0   4.0  3.0  23  112.0   0.0   3.0   7.0  5.0   5.0  

[7 rows x 23 columns]
------------ Index 12 ---------------------
0    -34
1    -35
2    -35
3    -35
4    -35
5    -29
6    -20
7    -35
8    -35
9    -34
10   -25
11   -35
12   -34
13   -35
14   -35
15   -31
16   -35
17   -35
18   -35
19   -35
20   -35
21   -35
22   -31
23   -35
24   -32
25   -35
26   -35
27   -35
28     0
29    -9
      ..
70   -35
71    -5
72   -25
73   -26
74   -35
75   -20
76   -35
77   -34
78   -35
79   -26
80   -34
81   -35
82   -23
83   -25
84   -11
85   -35
86   -35
87   -29
88   -35
89   -35
90   -34
91   -35
92   -33
93    -7
94   -25
95   -35
96   -35
97   -32
98   -22
99   -35
Name: hr, dtype: int64
      h  X2b  X3b  hr
0    14    1    0   1
1     1    0    0   0
2     0    0    0   0
3     0    0    0   0
4     1    0    0   0
5   105   21   12   6
6   159   52    2  15
7     5    1    0   0
8    10    3    0   0
9    10    0    0   1
10   80   24    1  10
11    0    0    0   0
12    6    0    0   1
13    0    0    0   0
14    0    0    0   0
15   19    4    0   4
16    0    0    0   0
17    4    1    0   0
18    4    0    0   0
19    0    0    0   0
20   13    1    0   0
21    0    0    0   0
22  126   18    3   4
23    0    0    0   0
24   40   11    1   3
25    1    0    0   0
26    0    0    0   0
27    0    0    0   0
28  119   19    0  35
29  147   30    0  26
..  ...  ...  ...  ..
70    0    0    0   0
71  146   24    1  30
72  130   30    1  10
73   55    8    0   9
74    0    0    0   0
75  129   23    2  15
76   15    2    0   0
77   51   10    1   1
78   12    1    0   0
79   80   10    1   9
80   17    3    0   1
81    0    0    0   0
82   92   15    2  12
83   54    6    0  10
84  139   30    0  24
85    0    0    0   0
86    8    2    0   0
87   57   11    1   6
88    1    0    0   0
89    0    0    0   0
90   48   14    0   1
91    8    4    0   0
92   40    9    2   2
93   94   14    0  28
94  130   31    3  10
95    0    0    0   0
96    0    0    0   0
97   82   16    3   3
98  112   19    1  13
99    3    1    0   0

[100 rows x 4 columns]
     h  X2b  X3b  hr
0    9    0    0   1
1   -4   -1    0   0
2   -5   -1    0   0
3   -5   -1    0   0
4   -4   -1    0   0
5  100   20   12   6
6  154   51    2  15
7    0    0    0   0
8    5    2    0   0
9    5   -1    0   1
h      8.0
X2b    1.0
X3b    0.0
hr     0.0
dtype: float64
------------ Index 13 ---------------------
                  id     player  year  stint team  lg    g   ab   r    h  \
alomasa022007  89534  alomasa02  2007      1  NYN  NL    8   22   1    3   
aloumo012007   89533   aloumo01  2007      1  NYN  NL   87  328  51  112   
ausmubr012007  89530  ausmubr01  2007      1  HOU  NL  117  349  38   82   
benitar012007  89525  benitar01  2007      2  FLO  NL   34    0   0    0   
benitar012007  89526  benitar01  2007      1  SFN  NL   19    0   0    0   

               ...    rbi   sb   cs  bb    so  ibb  hbp   sh   sf  gidp  
alomasa022007  ...    0.0  0.0  0.0   0   3.0  0.0  0.0  0.0  0.0   0.0  
aloumo012007   ...   49.0  3.0  0.0  27  30.0  5.0  2.0  0.0  3.0  13.0  
ausmubr012007  ...   25.0  6.0  1.0  37  74.0  3.0  6.0  4.0  1.0  11.0  
benitar012007  ...    0.0  0.0  0.0   0   0.0  0.0  0.0  0.0  0.0   0.0  
benitar012007  ...    0.0  0.0  0.0   0   0.0  0.0  0.0  0.0  0.0   0.0  

[5 rows x 23 columns]
                  id     player  year  stint team  lg    g   ab   r   h  ...   \
zaungr012007   89330   zaungr01  2007      1  TOR  AL  110  331  43  80  ...    
womacto012006  88641  womacto01  2006      2  CHN  NL   19   50   6  14  ...    
witasja012007  89333  witasja01  2007      1  TBA  AL    3    0   0   0  ...    
williwo022007  89334  williwo02  2007      1  HOU  NL   33   59   3   6  ...    
wickmbo012007  89335  wickmbo01  2007      2  ARI  NL    8    0   0   0  ...    

                rbi   sb   cs  bb    so  ibb  hbp   sh   sf  gidp  
zaungr012007   52.0  0.0  0.0  51  55.0  8.0  2.0  1.0  6.0   9.0  
womacto012006   2.0  1.0  1.0   4   4.0  0.0  0.0  3.0  0.0   0.0  
witasja012007   0.0  0.0  0.0   0   0.0  0.0  0.0  0.0  0.0   0.0  
williwo022007   2.0  0.0  0.0   0  25.0  0.0  0.0  5.0  0.0   1.0  
wickmbo012007   0.0  0.0  0.0   0   0.0  0.0  0.0  0.0  0.0   0.0  

[5 rows x 23 columns]
/Users/fushanshan/PycharmProjects/Data/DataAnalysis/Tut1.py:153: FutureWarning: order is deprecated, use sort_values(...)
  print baseball.hr.order(ascending=False)
28    35
71    30
93    28
29    26
40    25
84    24
36    21
38    21
48    20
64    20
6     15
75    15
98    13
82    12
47    11
94    10
10    10
72    10
83    10
73     9
79     9
49     8
61     7
5      6
87     6
63     6
22     4
15     4
24     3
97     3
      ..
60     0
58     0
68     0
57     0
56     0
55     0
54     0
53     0
52     0
51     0
62     0
65     0
66     0
67     0
46     0
44     0
30     0
69     0
42     0
41     0
70     0
39     0
74     0
37     0
76     0
35     0
33     0
78     0
31     0
99     0
Name: hr, dtype: int64
/Users/fushanshan/PycharmProjects/Data/DataAnalysis/Tut1.py:155: FutureWarning: by argument to sort_index is deprecated, pls use .sort_values(by=...)
  print baseball[['player','sb','cs']].sort_index(ascending=[False,True], by=['sb', 'cs']).head(10)
       player    sb   cs
40  sheffga01  22.0  5.0
61  loftoke01  21.0  4.0
22  vizquom01  14.0  6.0
72  greensh01  11.0  1.0
5   finlest01   7.0  0.0
71  griffke02   6.0  1.0
97  ausmubr01   6.0  1.0
75  gonzalu01   6.0  2.0
93  bondsba01   5.0  0.0
63  kleskry01   5.0  1.0
0      62.5
1      29.0
2      29.0
3      29.0
4      29.0
5      76.0
6      89.5
7      29.0
8      29.0
9      62.5
10     83.5
11     29.0
12     62.5
13     29.0
14     29.0
15     73.5
16     29.0
17     29.0
18     29.0
19     29.0
20     29.0
21     29.0
22     73.5
23     29.0
24     71.5
25     29.0
26     29.0
27     29.0
28    100.0
29     97.0
      ...  
70     29.0
71     99.0
72     83.5
73     80.5
74     29.0
75     89.5
76     29.0
77     62.5
78     29.0
79     80.5
80     62.5
81     29.0
82     87.0
83     83.5
84     95.0
85     29.0
86     29.0
87     76.0
88     29.0
89     29.0
90     62.5
91     29.0
92     69.0
93     98.0
94     83.5
95     29.0
96     29.0
97     71.5
98     88.0
99     29.0
Name: hr, dtype: float64
------------ Index 14 ---------------------
                        id  stint  lg    g   ab   r    h  X2b  X3b  hr   rbi  \
year team player                                                               
2006 CHN  womacto01  88641      2  NL   19   50   6   14    1    0   1   2.0   
     BOS  schilcu01  88643      1  AL   31    2   0    1    0    0   0   0.0   
     NYA  myersmi01  88645      1  AL   62    0   0    0    0    0   0   0.0   
     MIL  helliri01  88649      1  NL   20    3   0    0    0    0   0   0.0   
     NYA  johnsra05  88650      1  AL   33    6   0    1    0    0   0   0.0   
     SFN  finlest01  88652      1  NL  139  426  66  105   21   12   6  40.0   
     ARI  gonzalu01  88653      1  NL  153  586  93  159   52    2  15  73.0   
     LAN  seleaa01   88662      1  NL   28   26   2    5    1    0   0   0.0   
2007 ATL  francju01  89177      2  NL   15   40   1   10    3    0   0   8.0   
     NYN  francju01  89178      1  NL   40   50   7   10    0    0   1   8.0   
     TOR  zaungr01   89330      1  AL  110  331  43   80   24    1  10  52.0   
     TBA  witasja01  89333      1  AL    3    0   0    0    0    0   0   0.0   
     HOU  williwo02  89334      1  NL   33   59   3    6    0    0   1   2.0   
     ARI  wickmbo01  89335      2  NL    8    0   0    0    0    0   0   0.0   
     ATL  wickmbo01  89336      1  NL   47    0   0    0    0    0   0   0.0   
     MIN  whitero02  89337      1  AL   38  109   8   19    4    0   4  20.0   
     HOU  whiteri01  89338      1  NL   20    1   0    0    0    0   0   0.0   
     LAN  wellsda01  89339      2  NL    7   15   2    4    1    0   0   1.0   
     SDN  wellsda01  89340      1  NL   22   38   1    4    0    0   0   0.0   
     CIN  weathda01  89341      1  NL   67    0   0    0    0    0   0   0.0   
     OAK  walketo04  89343      1  AL   18   48   5   13    1    0   0   4.0   
     BOS  wakefti01  89345      1  AL    1    2   0    0    0    0   0   0.0   
     SFN  vizquom01  89347      1  NL  145  513  54  126   18    3   4  51.0   
     NYA  villoro01  89348      1  AL    6    0   0    0    0    0   0   0.0   
     NYN  valenjo03  89352      1  NL   51  166  18   40   11    1   3  18.0   
     CHN  trachst01  89354      2  NL    4    7   0    1    0    0   0   0.0   
     BAL  trachst01  89355      1  AL    3    5   0    0    0    0   0   0.0   
     BOS  timlimi01  89359      1  AL    4    0   0    0    0    0   0   0.0   
     CHA  thomeji01  89360      1  AL  130  432  79  119   19    0  35  96.0   
     TOR  thomafr04  89361      1  AL  155  531  63  147   30    0  26  95.0   
...                    ...    ...  ..  ...  ...  ..  ...  ...  ...  ..   ...   
     CIN  guarded01  89460      1  NL   15    0   0    0    0    0   0   0.0   
          griffke02  89462      1  NL  144  528  78  146   24    1  30  93.0   
     NYN  greensh01  89463      1  NL  130  446  62  130   30    1  10  46.0   
     MIL  graffto01  89464      1  NL   86  231  34   55    8    0   9  30.0   
     PHI  gordoto01  89465      1  NL   44    0   0    0    0    0   0   0.0   
     LAN  gonzalu01  89466      1  NL  139  464  70  129   23    2  15  68.0   
     CLE  gomezch02  89467      2  AL   19   53   4   15    2    0   0   5.0   
     BAL  gomezch02  89468      1  AL   73  169  17   51   10    1   1  16.0   
     NYN  glavito02  89469      1  NL   33   56   3   12    1    0   0   4.0   
     CHN  floydcl01  89473      1  NL  108  282  40   80   10    1   9  45.0   
     COL  finlest01  89474      1  NL   43   94   9   17    3    0   1   2.0   
     OAK  embreal01  89480      1  AL    4    0   0    0    0    0   0   0.0   
     SLN  edmonji01  89481      1  NL  117  365  39   92   15    2  12  53.0   
     NYN  easleda01  89482      1  NL   76  193  24   54    6    0  10  26.0   
          delgaca01  89489      1  NL  139  538  71  139   30    0  24  87.0   
     CIN  cormirh01  89493      1  NL    6    0   0    0    0    0   0   0.0   
     NYN  coninje01  89494      2  NL   21   41   2    8    2    0   0   5.0   
     CIN  coninje01  89495      1  NL   80  215  23   57   11    1   6  32.0   
     NYA  clemero02  89497      1  AL    2    2   0    1    0    0   0   0.0   
     BOS  claytro01  89498      2  AL    8    6   1    0    0    0   0   0.0   
     TOR  claytro01  89499      1  AL   69  189  23   48   14    0   1  12.0   
     ARI  cirilje01  89501      2  NL   28   40   6    8    4    0   0   6.0   
     MIN  cirilje01  89502      1  AL   50  153  18   40    9    2   2  21.0   
     SFN  bondsba01  89521      1  NL  126  340  75   94   14    0  28  66.0   
     HOU  biggicr01  89523      1  NL  141  517  68  130   31    3  10  50.0   
     FLO  benitar01  89525      2  NL   34    0   0    0    0    0   0   0.0   
     SFN  benitar01  89526      1  NL   19    0   0    0    0    0   0   0.0   
     HOU  ausmubr01  89530      1  NL  117  349  38   82   16    3   3  25.0   
     NYN  aloumo01   89533      1  NL   87  328  51  112   19    1  13  49.0   
          alomasa02  89534      1  NL    8   22   1    3    1    0   0   0.0   

                       sb   cs   bb     so   ibb   hbp    sh   sf  gidp  
year team player                                                         
2006 CHN  womacto01   1.0  1.0    4    4.0   0.0   0.0   3.0  0.0   0.0  
     BOS  schilcu01   0.0  0.0    0    1.0   0.0   0.0   0.0  0.0   0.0  
     NYA  myersmi01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     MIL  helliri01   0.0  0.0    0    2.0   0.0   0.0   0.0  0.0   0.0  
     NYA  johnsra05   0.0  0.0    0    4.0   0.0   0.0   0.0  0.0   0.0  
     SFN  finlest01   7.0  0.0   46   55.0   2.0   2.0   3.0  4.0   6.0  
     ARI  gonzalu01   0.0  1.0   69   58.0  10.0   7.0   0.0  6.0  14.0  
     LAN  seleaa01    0.0  0.0    1    7.0   0.0   0.0   6.0  0.0   1.0  
2007 ATL  francju01   0.0  0.0    4   10.0   1.0   0.0   0.0  1.0   1.0  
     NYN  francju01   2.0  1.0   10   13.0   0.0   0.0   0.0  1.0   1.0  
     TOR  zaungr01    0.0  0.0   51   55.0   8.0   2.0   1.0  6.0   9.0  
     TBA  witasja01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     HOU  williwo02   0.0  0.0    0   25.0   0.0   0.0   5.0  0.0   1.0  
     ARI  wickmbo01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     ATL  wickmbo01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     MIN  whitero02   0.0  0.0    6   19.0   0.0   3.0   0.0  1.0   2.0  
     HOU  whiteri01   0.0  0.0    0    1.0   0.0   0.0   0.0  0.0   0.0  
     LAN  wellsda01   0.0  0.0    0    6.0   0.0   0.0   0.0  0.0   0.0  
     SDN  wellsda01   0.0  0.0    0   12.0   0.0   0.0   4.0  0.0   0.0  
     CIN  weathda01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     OAK  walketo04   0.0  0.0    2    4.0   0.0   0.0   0.0  2.0   2.0  
     BOS  wakefti01   0.0  0.0    0    2.0   0.0   0.0   0.0  0.0   0.0  
     SFN  vizquom01  14.0  6.0   44   48.0   6.0   1.0  14.0  3.0  14.0  
     NYA  villoro01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     NYN  valenjo03   2.0  1.0   15   28.0   4.0   0.0   1.0  1.0   5.0  
     CHN  trachst01   0.0  0.0    0    1.0   0.0   0.0   0.0  0.0   0.0  
     BAL  trachst01   0.0  0.0    0    3.0   0.0   0.0   0.0  0.0   0.0  
     BOS  timlimi01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     CHA  thomeji01   0.0  1.0   95  134.0  11.0   6.0   0.0  3.0  10.0  
     TOR  thomafr04   0.0  0.0   81   94.0   3.0   7.0   0.0  5.0  14.0  
...                   ...  ...  ...    ...   ...   ...   ...  ...   ...  
     CIN  guarded01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
          griffke02   6.0  1.0   85   99.0  14.0   1.0   0.0  9.0  14.0  
     NYN  greensh01  11.0  1.0   37   62.0   4.0   5.0   1.0  1.0  14.0  
     MIL  graffto01   0.0  1.0   24   44.0   6.0   3.0   0.0  2.0   7.0  
     PHI  gordoto01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     LAN  gonzalu01   6.0  2.0   56   56.0   4.0   4.0   0.0  2.0  11.0  
     CLE  gomezch02   0.0  0.0    0    6.0   0.0   0.0   1.0  1.0   1.0  
     BAL  gomezch02   1.0  2.0   10   20.0   1.0   0.0   5.0  1.0   5.0  
     NYN  glavito02   0.0  0.0    6    5.0   0.0   0.0  12.0  1.0   0.0  
     CHN  floydcl01   0.0  0.0   35   47.0   5.0   5.0   0.0  0.0   6.0  
     COL  finlest01   0.0  0.0    8    4.0   1.0   0.0   0.0  0.0   2.0  
     OAK  embreal01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     SLN  edmonji01   0.0  2.0   41   75.0   2.0   0.0   2.0  3.0   9.0  
     NYN  easleda01   0.0  1.0   19   35.0   1.0   5.0   0.0  1.0   2.0  
          delgaca01   4.0  0.0   52  118.0   8.0  11.0   0.0  6.0  12.0  
     CIN  cormirh01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     NYN  coninje01   0.0  0.0    7    8.0   2.0   0.0   1.0  1.0   1.0  
     CIN  coninje01   4.0  0.0   20   28.0   0.0   0.0   1.0  6.0   4.0  
     NYA  clemero02   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     BOS  claytro01   0.0  0.0    0    3.0   0.0   0.0   0.0  0.0   2.0  
     TOR  claytro01   2.0  1.0   14   50.0   0.0   1.0   3.0  3.0   8.0  
     ARI  cirilje01   0.0  0.0    4    6.0   0.0   0.0   0.0  0.0   1.0  
     MIN  cirilje01   2.0  0.0   15   13.0   0.0   1.0   3.0  2.0   9.0  
     SFN  bondsba01   5.0  0.0  132   54.0  43.0   3.0   0.0  2.0  13.0  
     HOU  biggicr01   4.0  3.0   23  112.0   0.0   3.0   7.0  5.0   5.0  
     FLO  benitar01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     SFN  benitar01   0.0  0.0    0    0.0   0.0   0.0   0.0  0.0   0.0  
     HOU  ausmubr01   6.0  1.0   37   74.0   3.0   6.0   4.0  1.0  11.0  
     NYN  aloumo01    3.0  0.0   27   30.0   5.0   2.0   0.0  3.0  13.0  
          alomasa02   0.0  0.0    0    3.0   0.0   0.0   0.0  0.0   0.0  

[100 rows x 20 columns]
True
     Ohio     Colorado
    Green Red    Green
a 1     0   1        2
  2     3   4        5
b 1     6   7        8
  2     9  10       11
------------ Index 15 ---------------------
0      None
1        -3
2      None
3    foobar
dtype: object
0     True
1    False
2     True
3    False
dtype: bool
Firmicutes           NaN
Proteobacteria     632.0
Actinobacteria    1638.0
Bacteroidetes      569.0
dtype: float64
Firmicutes           NaN
Proteobacteria     632.0
Actinobacteria    1638.0
Bacteroidetes      569.0
dtype: float64
------------ Index 16 ---------------------
id                                                  8935266
player    womacto01schilcu01myersmi01helliri01johnsra05f...
year                                                 200692
stint                                                   113
team      CHNBOSNYAMILNYASFNARILANATLNYNTORTBAHOUARIATLM...
lg        NLALALNLALNLNLNLNLNLALALNLNLNLALNLNLNLNLALALNL...
g                                                      5238
ab                                                    13654
r                                                      1869
h                                                      3582
X2b                                                     739
X3b                                                      55
hr                                                      437
rbi                                                    1847
sb                                                      138
cs                                                       46
bb                                                     1549
so                                                     2408
ibb                                                     177
hbp                                                     112
sh                                                      138
sf                                                      120
gidp                                                    354
dtype: object
id       89352.66
year      2006.92
stint        1.13
g           52.38
ab         136.54
r           18.69
h           35.82
X2b          7.39
X3b          0.55
hr           4.37
rbi         18.47
sb           1.38
cs           0.46
bb          15.49
so          24.08
ibb          1.77
hbp          1.12
sh           1.38
sf           1.20
gidp         3.54
dtype: float64
id       89352.66
year      2006.92
stint        1.13
g           52.38
ab         136.54
r           18.69
h           35.82
X2b          7.39
X3b          0.55
hr           4.37
rbi         18.47
sb           1.38
cs           0.46
bb          15.49
so          24.08
ibb          1.77
hbp          1.12
sh           1.38
sf           1.20
gidp         3.54
dtype: float64
                 id        year       stint           g          ab  \
count    100.000000   100.00000  100.000000  100.000000  100.000000   
mean   89352.660000  2006.92000    1.130000   52.380000  136.540000   
std      218.910859     0.27266    0.337998   48.031299  181.936853   
min    88641.000000  2006.00000    1.000000    1.000000    0.000000   
25%    89353.500000  2007.00000    1.000000    9.500000    2.000000   
50%    89399.000000  2007.00000    1.000000   33.000000   40.500000   
75%    89465.250000  2007.00000    1.000000   83.250000  243.750000   
max    89534.000000  2007.00000    2.000000  155.000000  586.000000   

               r           h         X2b         X3b          hr        rbi  \
count  100.00000  100.000000  100.000000  100.000000  100.000000  100.00000   
mean    18.69000   35.820000    7.390000    0.550000    4.370000   18.47000   
std     27.77496   50.221807   11.117277    1.445124    7.975537   28.34793   
min      0.00000    0.000000    0.000000    0.000000    0.000000    0.00000   
25%      0.00000    0.000000    0.000000    0.000000    0.000000    0.00000   
50%      2.00000    8.000000    1.000000    0.000000    0.000000    2.00000   
75%     33.25000   62.750000   11.750000    1.000000    6.000000   27.00000   
max    107.00000  159.000000   52.000000   12.000000   35.000000   96.00000   

               sb          cs          bb          so         ibb        hbp  \
count  100.000000  100.000000  100.000000  100.000000  100.000000  100.00000   
mean     1.380000    0.460000   15.490000   24.080000    1.770000    1.12000   
std      3.694878    1.067613   25.812649   32.804496    5.042957    2.23055   
min      0.000000    0.000000    0.000000    0.000000    0.000000    0.00000   
25%      0.000000    0.000000    0.000000    1.000000    0.000000    0.00000   
50%      0.000000    0.000000    1.000000    7.000000    0.000000    0.00000   
75%      1.000000    0.000000   19.250000   37.250000    1.250000    1.00000   
max     22.000000    6.000000  132.000000  134.000000   43.000000   11.00000   

               sh          sf        gidp  
count  100.000000  100.000000  100.000000  
mean     1.380000    1.200000    3.540000  
std      2.919042    2.035046    5.201826  
min      0.000000    0.000000    0.000000  
25%      0.000000    0.000000    0.000000  
50%      0.000000    0.000000    1.000000  
75%      1.000000    2.000000    6.000000  
max     14.000000    9.000000   21.000000  
69.0764646465
0.779061518254
             id      year     stint         g        ab         r         h  \
id     1.000000  0.952133 -0.001171  0.000011  0.049978  0.028459  0.055694   
year   0.952133  1.000000  0.004384 -0.050874 -0.001360 -0.023315  0.001151   
stint -0.001171  0.004384  1.000000 -0.257552 -0.216333 -0.209781 -0.206878   
g      0.000011 -0.050874 -0.257552  1.000000  0.935910  0.910262  0.929292   
ab     0.049978 -0.001360 -0.216333  0.935910  1.000000  0.965609  0.994217   
r      0.028459 -0.023315 -0.209781  0.910262  0.965609  1.000000  0.970560   
h      0.055694  0.001151 -0.206878  0.929292  0.994217  0.970560  1.000000   
X2b   -0.004195 -0.052917 -0.196423  0.885847  0.952249  0.923508  0.957275   
X3b   -0.197270 -0.246099 -0.085821  0.518663  0.535986  0.500807  0.514245   
hr     0.091373  0.060199 -0.209124  0.802014  0.843308  0.890060  0.855163   
rbi    0.073826  0.042812 -0.205688  0.891563  0.947911  0.941483  0.952320   
sb     0.056308  0.030480 -0.120837  0.492362  0.533536  0.596343  0.530018   
cs     0.066068  0.058296 -0.055425  0.520923  0.577192  0.576454  0.571629   
bb     0.047443  0.005626 -0.190301  0.828572  0.850803  0.915010  0.853384   
so     0.103113  0.069610 -0.214121  0.866499  0.923926  0.879375  0.906966   
ibb    0.065039  0.015868 -0.118580  0.514423  0.506398  0.588882  0.513009   
hbp    0.042430 -0.000664 -0.195074  0.730161  0.767210  0.806523  0.767449   
sh    -0.004001 -0.012184 -0.091527  0.079361  0.094537 -0.001273  0.045533   
sf     0.026750 -0.007282 -0.155662  0.767543  0.840361  0.839592  0.839737   
gidp   0.104824  0.052131 -0.224173  0.863041  0.926632  0.894724  0.935525   

            X2b       X3b        hr       rbi        sb        cs        bb  \
id    -0.004195 -0.197270  0.091373  0.073826  0.056308  0.066068  0.047443   
year  -0.052917 -0.246099  0.060199  0.042812  0.030480  0.058296  0.005626   
stint -0.196423 -0.085821 -0.209124 -0.205688 -0.120837 -0.055425 -0.190301   
g      0.885847  0.518663  0.802014  0.891563  0.492362  0.520923  0.828572   
ab     0.952249  0.535986  0.843308  0.947911  0.533536  0.577192  0.850803   
r      0.923508  0.500807  0.890060  0.941483  0.596343  0.576454  0.915010   
h      0.957275  0.514245  0.855163  0.952320  0.530018  0.571629  0.853384   
X2b    1.000000  0.493267  0.779062  0.901751  0.413655  0.477487  0.780012   
X3b    0.493267  1.000000  0.210028  0.369890  0.450421  0.384312  0.350682   
hr     0.779062  0.210028  1.000000  0.948787  0.364346  0.345187  0.916774   
rbi    0.901751  0.369890  0.948787  1.000000  0.394633  0.435011  0.893945   
sb     0.413655  0.450421  0.364346  0.394633  1.000000  0.743921  0.491351   
cs     0.477487  0.384312  0.345187  0.435011  0.743921  1.000000  0.425352   
bb     0.780012  0.350682  0.916774  0.893945  0.491351  0.425352  1.000000   
so     0.862149  0.408800  0.865929  0.929410  0.365841  0.426658  0.795751   
ibb    0.453301  0.090993  0.673691  0.582982  0.209110  0.106152  0.792057   
hbp    0.738226  0.217474  0.767411  0.780899  0.413570  0.337129  0.742118   
sh     0.005659  0.187012 -0.145374 -0.054670  0.171910  0.293397 -0.044992   
sf     0.819361  0.394987  0.782038  0.855260  0.412947  0.422146  0.760932   
gidp   0.906860  0.411577  0.798350  0.906908  0.431198  0.456820  0.823631   

             so       ibb       hbp        sh        sf      gidp  
id     0.103113  0.065039  0.042430 -0.004001  0.026750  0.104824  
year   0.069610  0.015868 -0.000664 -0.012184 -0.007282  0.052131  
stint -0.214121 -0.118580 -0.195074 -0.091527 -0.155662 -0.224173  
g      0.866499  0.514423  0.730161  0.079361  0.767543  0.863041  
ab     0.923926  0.506398  0.767210  0.094537  0.840361  0.926632  
r      0.879375  0.588882  0.806523 -0.001273  0.839592  0.894724  
h      0.906966  0.513009  0.767449  0.045533  0.839737  0.935525  
X2b    0.862149  0.453301  0.738226  0.005659  0.819361  0.906860  
X3b    0.408800  0.090993  0.217474  0.187012  0.394987  0.411577  
hr     0.865929  0.673691  0.767411 -0.145374  0.782038  0.798350  
rbi    0.929410  0.582982  0.780899 -0.054670  0.855260  0.906908  
sb     0.365841  0.209110  0.413570  0.171910  0.412947  0.431198  
cs     0.426658  0.106152  0.337129  0.293397  0.422146  0.456820  
bb     0.795751  0.792057  0.742118 -0.044992  0.760932  0.823631  
so     1.000000  0.476613  0.742547  0.073624  0.782314  0.846629  
ibb    0.476613  1.000000  0.431714 -0.075658  0.451377  0.572355  
hbp    0.742547  0.431714  1.000000 -0.104810  0.648882  0.700380  
sh     0.073624 -0.075658 -0.104810  1.000000 -0.002721  0.028924  
sf     0.782314  0.451377  0.648882 -0.002721  1.000000  0.785489  
gidp   0.846629  0.572355  0.700380  0.028924  0.785489  1.000000  
                Tissue  Stool
Taxon                        
Actinobacteria    6736   2263
Bacteroidetes     8995   4656
Firmicutes       10266  30477
Other             2982    519
Proteobacteria   44146  16369
------------ Index 17 ---------------------

Process finished with exit code 0
{% endhighlight %}