# Paired T-test
<br><br>
**Goal**: test if the mean of a population in two different moments is the same.
<br><br>
## Example : The new diet

A population was exposed to a new diet, our goal is to figure out if:
<br><br>
H1: The diet had an effect on the weight ( mean_ater_diet != mean_before_diet )<br>
H0: The diet has no effect on the weight ( mean_ater_diet == mean_before_diet )<br>
<br><br>
**Assumptions**
<br><br>
1 - The dependent variable should be measured on a continuous scale<br>
2 - Observations should be independent of each other<br>
3 - There should be no significant outliers<br>
4 - The dependent variable has a normal distribution<br>


```python
import pandas as pd
from scipy import stats
```


```python
# Import dataset:

df = pd.read_csv("diet_dataset.csv", decimal=',')
df.head()
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
      <th>id_participante</th>
      <th>peso_antes</th>
      <th>peso_depois</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>id1</td>
      <td>74.6</td>
      <td>73.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>id2</td>
      <td>104.0</td>
      <td>100.6</td>
    </tr>
    <tr>
      <th>2</th>
      <td>id3</td>
      <td>96.0</td>
      <td>92.7</td>
    </tr>
    <tr>
      <th>3</th>
      <td>id4</td>
      <td>96.3</td>
      <td>96.4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>id5</td>
      <td>106.2</td>
      <td>105.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dtypes
```




    id_participante     object
    peso_antes         float64
    peso_depois        float64
    dtype: object




```python
df.describe()
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
      <th>peso_antes</th>
      <th>peso_depois</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>100.00000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>96.58000</td>
      <td>94.473000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>11.13757</td>
      <td>11.132525</td>
    </tr>
    <tr>
      <th>min</th>
      <td>72.00000</td>
      <td>67.700000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>86.67500</td>
      <td>85.700000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>96.80000</td>
      <td>95.050000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>106.05000</td>
      <td>104.375000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>113.00000</td>
      <td>111.500000</td>
    </tr>
  </tbody>
</table>
</div>



The mean after the diet is more then 2 kilos smaller than the mean before. Let's check if these results have statistical significance:


```python
# weight before diet:
a = df.peso_antes

#weight after diet:
b = df.peso_depois

#Paired sample-test:
tStat, pValue =  stats.ttest_rel(a, b)

print("P-Value:{0} T-Statistic:{1}".format(pValue,tStat))
```

    P-Value:7.122999470178242e-27 T-Statistic:14.820165521870756


*Result: Our p-value is smaller than 0.05, so we reject the null hypothesis* and we confirm that this diet helps to loose weight.

