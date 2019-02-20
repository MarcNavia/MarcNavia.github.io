---
title: "Gender Prediction"
date: 2018-06-15
tags: [Jupyter, Python]
header:
    image: "/images/"
excerpt: "This is the excerpt"
mathjax: "true"
---

## Sound it out!
<p>Grey and Gray. Colour and Color. Words like these have been the cause of many heated arguments between Brits and Americans. Accents (and jokes) aside, there are many words that are pronounced the same way but have different spellings. While it is easy for us to realize their equivalence, basic programming commands will fail to equate such two strings. </p>
<p>More extreme than word spellings are names because people have more flexibility in choosing to spell a name in a certain way. To some extent, tradition sometimes governs the way a name is spelled, which limits the number of variations of any given English name. But if we consider global names and their associated English spellings, you can only imagine how many ways they can be spelled out. </p>
<p>One way to tackle this challenge is to write a program that checks if two strings sound the same, instead of checking for equivalence in spellings. We'll do that here using fuzzy name matching.</p>


```python
# Importing the fuzzy package
import fuzzy
#import seaborn as sns

# Exploring the output of fuzzy.nysiis
print(fuzzy.nysiis('Navia'))

# Testing equivalence of similar sounding words
fuzzy.nysiis('tommorow') == fuzzy.nysiis('tomorow')
```

    NAV





    True



## Authoring the authors
<p>The New York Times puts out a weekly list of best-selling books from different genres, and which has been published since the 1930’s.  We’ll focus on Children’s Picture Books, and analyze the gender distribution of authors to see if there have been changes over time. We'll begin by reading in the data on the best selling authors from 2008 to 2017.</p>


```python
# Importing the pandas module
import pandas as pd

# Reading in datasets/nytkids_yearly.csv, which is semicolon delimited.
author_df = pd.read_csv('datasets/nytkids_yearly.csv', sep=';' )

# Looping through author_df['Author'] to extract the authors first names
first_name = []
for name in author_df['Author']:
    first_name.append(name.split()[0])

# Adding first_name as a column to author_df
author_df['first_name'] = first_name

# Checking out the first few rows of author_df
author_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Book Title</th>
      <th>Author</th>
      <th>Besteller this year</th>
      <th>first_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017</td>
      <td>DRAGONS LOVE TACOS</td>
      <td>Adam Rubin</td>
      <td>49</td>
      <td>Adam</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017</td>
      <td>THE WONDERFUL THINGS YOU WILL BE</td>
      <td>Emily Winfield Martin</td>
      <td>48</td>
      <td>Emily</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017</td>
      <td>THE DAY THE CRAYONS QUIT</td>
      <td>Drew Daywalt</td>
      <td>44</td>
      <td>Drew</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>ROSIE REVERE, ENGINEER</td>
      <td>Andrea Beaty</td>
      <td>38</td>
      <td>Andrea</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017</td>
      <td>ADA TWIST, SCIENTIST</td>
      <td>Andrea Beaty</td>
      <td>28</td>
      <td>Andrea</td>
    </tr>
  </tbody>
</table>
</div>



## It's time to bring on the phonics... _again_!
<p>When we were young children, we were taught to read using phonics; sounding out the letters that compose words. So let's relive history and do that again, but using python this time. We will now create a new column or list that contains the phonetic equivalent of every first name that we just extracted. </p>
<p>To make sure we're on the right track, let's compare the number of unique values in the <code>first_name</code> column and the number of unique values in the nysiis coded column. As a rule of thumb, the number of unique nysiis first names should be less than or equal to the number of actual first names.</p>


```python
# Importing numpy
import numpy as np

# Looping through author's first names to create the nysiis (fuzzy) equivalent
nysiis_name = []
for firstname in author_df['first_name']:
    nysiis_name.append(fuzzy.nysiis(firstname))

# Adding nysiis_name as a column to author_df
author_df['nysiis_name'] = nysiis_name

# Printing out the difference between unique firstnames and unique nysiis_names:
difference = len(np.unique(first_name)) - len(np.unique(nysiis_name))
print('The difference between unique firstnames and unique nysiis_names is ' + str(difference))
author_df.head()
```

    The difference between unique firstnames and unique nysiis_names is 25





<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Book Title</th>
      <th>Author</th>
      <th>Besteller this year</th>
      <th>first_name</th>
      <th>nysiis_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2017</td>
      <td>DRAGONS LOVE TACOS</td>
      <td>Adam Rubin</td>
      <td>49</td>
      <td>Adam</td>
      <td>ADAN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2017</td>
      <td>THE WONDERFUL THINGS YOU WILL BE</td>
      <td>Emily Winfield Martin</td>
      <td>48</td>
      <td>Emily</td>
      <td>ENALY</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017</td>
      <td>THE DAY THE CRAYONS QUIT</td>
      <td>Drew Daywalt</td>
      <td>44</td>
      <td>Drew</td>
      <td>DR</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>ROSIE REVERE, ENGINEER</td>
      <td>Andrea Beaty</td>
      <td>38</td>
      <td>Andrea</td>
      <td>ANDR</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2017</td>
      <td>ADA TWIST, SCIENTIST</td>
      <td>Andrea Beaty</td>
      <td>28</td>
      <td>Andrea</td>
      <td>ANDR</td>
    </tr>
  </tbody>
</table>
</div>



## The inbetweeners
<p>We'll use <code>babynames_nysiis.csv</code>, a dataset that is derived from <a href="https://www.ssa.gov/oact/babynames/limits.html">the Social Security Administration’s baby name data</a>, to identify author genders. The dataset contains unique NYSIIS versions of baby names, and also includes the percentage of times the name appeared as a female name (<code>perc_female</code>) and the percentage of times it appeared as a male name (<code>perc_male</code>). </p>
<p>We'll use this data to create a list of <code>gender</code>. Let's make the following simplifying assumption: For each name, if <code>perc_female</code> is greater than <code>perc_male</code> then assume the name is female, if <code>perc_female</code> is less than <code>perc_male</code> then assume it is a male name, and if the percentages are equal then it's a "neutral" name.</p>


```python
# Reading in datasets/babynames_nysiis.csv, which is semicolon delimited.
babies_df = pd.read_csv('datasets/babynames_nysiis.csv', sep=';')

# Looping through babies_df to and filling up gender
gender = []
babies_df.head()
for idx in range(len(babies_df)):
    if babies_df.perc_female[idx] < babies_df.perc_male[idx]:
        gender.append('M')
    elif babies_df.perc_female[idx] == babies_df.perc_male[idx]:
        gender.append('N')
    else:
        gender.append('F')

# creating a new column gender
babies_df['gender'] = gender

# Printing out the first few rows of babies_df
print(babies_df[0:10])
```

      babynysiis  perc_female  perc_male gender
    0        NaN        62.50      37.50      F
    1        RAX        63.64      36.36      F
    2       ESAR        44.44      55.56      M
    3      DJANG         0.00     100.00      M
    4     PARCAL        25.00      75.00      M
    5    VALCARY       100.00       0.00      F
    6   FRANCASC        63.64      36.36      F
    7      CABAT        50.00      50.00      N
    8     XANDAR        16.67      83.33      M
    9     RACSAN        33.33      66.67      M


## Playing matchmaker
<p>Now that we have identified the likely genders of different names, let's find author genders by searching for each author's name in the <code>babies_df</code> DataFrame, and extracting the associated gender. </p>


```python
# This function returns the location of an element in a_list.
# Where an item does not exist, it returns -1.
def locate_in_list(a_list, element):
    loc_of_name = a_list.index(element) if element in a_list else -1
    return(loc_of_name)

# Looping through author_df['nysiis_name'] and appending the gender of each
# author to author_gender.
author_gender = []
for idx, name in author_df.iterrows():
    i = locate_in_list(list(babies_df['babynysiis']), name['nysiis_name'])
    if i >= 0:
        author_gender.append(babies_df.iloc[i]['gender'])
    else:
        author_gender.append('Unknown')


# Adding author_gender to the author_df
author_df['author_gender'] = author_gender

# Counting the author's genders
print(author_df['author_gender'].value_counts())
```

    F          395
    M          191
    Unknown      9
    N            8
    Name: author_gender, dtype: int64


## Tally up
<p>From the results above see that there are more female authors on the New York Times best seller's list than male authors. Our dataset spans 2008 to 2017. Let's find out if there have been changes over time.</p>


```python
# Creating a list of unique years, sorted in ascending order.
years = [2008, 2009, 2010, 2011, 2012, 2013, 2014 , 2015, 2016, 2017]

# Initializing lists
males_by_yr = []
females_by_yr = []
unknown_by_yr = []

# Looping through years to find the number of male, female and unknown authors per year
for x in years:
    males_by_yr.append(len(author_df[(author_df['author_gender'] =='M') & (author_df['Year'] == x)]))
    females_by_yr.append(len(author_df[(author_df['author_gender'] =='F') & (author_df['Year'] == x)]))
    unknown_by_yr.append(len(author_df[(author_df['author_gender'] =='N') & (author_df['Year'] == x)]))

# Printing out yearly values to examine changes over time
data = np.array([males_by_yr, females_by_yr, unknown_by_yr])
headers = ['males', 'females', 'unknowns']
changes = pd.DataFrame(data, headers, years)

print(changes)
```

              2008  2009  2010  2011  2012  2013  2014  2015  2016  2017
    males        8    19    27    21    21    11    21    18    25    20
    females     15    45    48    51    46    51    34    30    32    43
    unknowns     1     0     1     1     2     1     1     0     1     0


## Foreign-born authors?
<p>Our gender data comes from social security applications of individuals born in the US. Hence, one possible explanation for why there are "unknown" genders associated with some author names is because these authors were foreign-born. While making this assumption, we should note that these are only a subset of foreign-born authors as others will have names that have a match in <code>baby_df</code> (and in the social security dataset). </p>
<p>Using a bar chart, let's explore the trend of foreign-born authors with no name matches in the social security dataset.</p>


```python
# Importing matplotlib
import matplotlib.pyplot as plt

# This makes plots appear in the notebook
%matplotlib inline
#sns.set()

# Plotting the bar chart
_= plt.bar(years, unknown_by_yr)

# Setting a title, and axes labels
_= plt.xlabel('Year')
_= plt.ylabel('Count')
_= plt.title('Foreign-born authors')
_= plt.yticks(np.arange(0, 3, 1))
```


<img src="{{ site.url }}{{ site.baseurl }}/images/GenderPrediction/output_13_0.svg" alt="Test">


## Raising the bar
<p>What’s more exciting than a bar chart is a grouped bar chart. This type of chart is good for displaying <em>changes</em> over time while also <em>comparing</em> two or more groups. Let’s use a grouped bar chart to look at the distribution of male and female authors over time.</p>


```python
# Creating a new list, where 0.25 is added to each year
years_shifted = [year + 0.25 for year in years]

# Plotting males_by_yr by year
_= plt.bar(years, males_by_yr, width=0.25, color='lightblue', label='Male')

# Plotting females_by_yr by years_shifted
_= plt.bar(years_shifted, females_by_yr, width=0.25, color='pink', label='Female')

# Adding relevant Axes labels and Chart Title
_= plt.xlabel('year')
_= plt.ylabel('Authors')
_= plt.title('Male vs. Female')
_= plt.legend()
```


<img src="{{ site.url }}{{ site.baseurl }}/images/GenderPrediction/output_15_0.svg" alt="Test">
