---
layout:     post
title:      Python For Data Analysis Pandas
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

Try it, see the compile results!!!