

```python
import pandas as pd
import matplotlib as plt
```


```python
!wget http://files.zillowstatic.com/research/public/Zip/Zip_MedianValuePerSqft_AllHomes.csv
```

    --2019-08-17 22:37:02--  http://files.zillowstatic.com/research/public/Zip/Zip_MedianValuePerSqft_AllHomes.csv
    Resolving files.zillowstatic.com (files.zillowstatic.com)... 99.84.181.11, 99.84.181.89, 99.84.181.98, ...
    Connecting to files.zillowstatic.com (files.zillowstatic.com)|99.84.181.11|:80... connected.
    HTTP request sent, awaiting response... 200 OK
    Length: 15155733 (14M) [binary/octet-stream]
    Saving to: ‘Zip_MedianValuePerSqft_AllHomes.csv’
    
    Zip_MedianValuePerS 100%[===================>]  14.45M  7.33MB/s    in 2.0s    
    
    2019-08-17 22:37:04 (7.33 MB/s) - ‘Zip_MedianValuePerSqft_AllHomes.csv’ saved [15155733/15155733]
    



```python
zip_prices = pd.read_csv('Zip_MedianValuePerSqft_AllHomes.csv', engine = 'python')
```


```python
zip_prices.head(5)
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
      <th>RegionID</th>
      <th>RegionName</th>
      <th>City</th>
      <th>State</th>
      <th>Metro</th>
      <th>CountyName</th>
      <th>SizeRank</th>
      <th>1996-04</th>
      <th>1996-05</th>
      <th>1996-06</th>
      <th>...</th>
      <th>2018-10</th>
      <th>2018-11</th>
      <th>2018-12</th>
      <th>2019-01</th>
      <th>2019-02</th>
      <th>2019-03</th>
      <th>2019-04</th>
      <th>2019-05</th>
      <th>2019-06</th>
      <th>2019-07</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>61639</td>
      <td>10025</td>
      <td>New York</td>
      <td>NY</td>
      <td>New York-Newark-Jersey City</td>
      <td>New York County</td>
      <td>1</td>
      <td>200.0</td>
      <td>200.0</td>
      <td>201.0</td>
      <td>...</td>
      <td>1323</td>
      <td>1316</td>
      <td>1305</td>
      <td>1290</td>
      <td>1288</td>
      <td>1286</td>
      <td>1272</td>
      <td>1258</td>
      <td>1253</td>
      <td>1246</td>
    </tr>
    <tr>
      <th>1</th>
      <td>84654</td>
      <td>60657</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>Chicago-Naperville-Elgin</td>
      <td>Cook County</td>
      <td>2</td>
      <td>156.0</td>
      <td>157.0</td>
      <td>157.0</td>
      <td>...</td>
      <td>477</td>
      <td>478</td>
      <td>479</td>
      <td>481</td>
      <td>482</td>
      <td>487</td>
      <td>492</td>
      <td>492</td>
      <td>486</td>
      <td>481</td>
    </tr>
    <tr>
      <th>2</th>
      <td>61637</td>
      <td>10023</td>
      <td>New York</td>
      <td>NY</td>
      <td>New York-Newark-Jersey City</td>
      <td>New York County</td>
      <td>3</td>
      <td>359.0</td>
      <td>359.0</td>
      <td>359.0</td>
      <td>...</td>
      <td>1591</td>
      <td>1582</td>
      <td>1572</td>
      <td>1556</td>
      <td>1539</td>
      <td>1519</td>
      <td>1496</td>
      <td>1485</td>
      <td>1483</td>
      <td>1476</td>
    </tr>
    <tr>
      <th>3</th>
      <td>91982</td>
      <td>77494</td>
      <td>Katy</td>
      <td>TX</td>
      <td>Houston-The Woodlands-Sugar Land</td>
      <td>Harris County</td>
      <td>4</td>
      <td>67.0</td>
      <td>68.0</td>
      <td>68.0</td>
      <td>...</td>
      <td>113</td>
      <td>113</td>
      <td>114</td>
      <td>114</td>
      <td>114</td>
      <td>114</td>
      <td>114</td>
      <td>114</td>
      <td>114</td>
      <td>113</td>
    </tr>
    <tr>
      <th>4</th>
      <td>84616</td>
      <td>60614</td>
      <td>Chicago</td>
      <td>IL</td>
      <td>Chicago-Naperville-Elgin</td>
      <td>Cook County</td>
      <td>5</td>
      <td>199.0</td>
      <td>200.0</td>
      <td>201.0</td>
      <td>...</td>
      <td>523</td>
      <td>525</td>
      <td>527</td>
      <td>529</td>
      <td>530</td>
      <td>533</td>
      <td>534</td>
      <td>530</td>
      <td>522</td>
      <td>515</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 287 columns</p>
</div>




```python
zip_prices[zip_prices.columns[zip_prices.columns.str.contains('RegionName|\-')]].set_index('RegionName').head(10).transpose().plot()

```




    <matplotlib.axes._subplots.AxesSubplot at 0x12a5a5978>




![png](Analyze%20zip%20codes_files/Analyze%20zip%20codes_4_1.png)

