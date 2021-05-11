# Chi-squared test

A chi-squared test exists to test the association between two categorical variables.

We are ging to use another example from AGRESTI and FINLAY (2012). In this example, we want to see if party association has any gender bias. Therefore our hypothesis are: <br><br>

H0 : Gender does not influenciate political prerfernces<br>
H1: Gender influenciates political preferences<br><br>


First we need to form a contingency table in which each row is the independent variable and each column is the dependent variable.
We are going to use the contingency table (e.g. already grouped) from the book:



```python
import numpy as np
import pandas as pd
from scipy import stats
```


```python
gender = ['women', 'men', 'total']

df = {'democrats' : [573, 386, 959],
       'independent': [516, 475, 991],
       'republicans': [422, 399, 821],
       'total': [1511, 1260, 2771]}

df = pd.DataFrame(df, index = gender)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>democrats</th>
      <th>independent</th>
      <th>republicans</th>
      <th>total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>women</th>
      <td>573</td>
      <td>516</td>
      <td>422</td>
      <td>1511</td>
    </tr>
    <tr>
      <th>men</th>
      <td>386</td>
      <td>475</td>
      <td>399</td>
      <td>1260</td>
    </tr>
    <tr>
      <th>total</th>
      <td>959</td>
      <td>991</td>
      <td>821</td>
      <td>2771</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Let's do the test

#first, getting the totals:
df = df.iloc[:2]

data = df[['democrats', 'independent', 'republicans']].to_numpy()
data
```




    array([[573, 516, 422],
           [386, 475, 399]])




```python
#Chi-suqared test

chi2_stat, p_val, dof, ex = stats.chi2_contingency(data)

print("===Chi2 Stat===")
print(chi2_stat)
print("\n")
print("===Degrees of Freedom===")
print(dof)
print("\n")
print("===P-Value===")
print(p_val)
print("\n")
print("===Contingency Table===")
print(ex)
```

    ===Chi2 Stat===
    16.201726038971145
    
    
    ===Degrees of Freedom===
    2
    
    
    ===P-Value===
    0.0003032772908939342
    
    
    ===Contingency Table===
    [[522.93359798 540.38289426 447.68350776]
     [436.06640202 450.61710574 373.31649224]]


Our p-value is lower than 0.05, which means that we can reject the null hypothesis and assume that there is a gender bias in political preferences
