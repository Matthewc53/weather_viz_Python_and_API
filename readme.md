

```python

import matplotlib.pyplot as plt
import pandas as pd
import json
import requests as req
from citipy import citipy
import numpy as np
import random
import time
import seaborn as sns 
```

# 3 Observations

#1. WE can see that latitude does have a drastic effect on lowering world temperatures when venturing out from the equator,
especially when reaching the higher latitudes because there are many more cities in the northern hemisphere near the poles. 

#2. The likelihood of more windspeed does increase once leaving the equator. However,
the vast majority of points only exist between 0-5 mph. 

#3. Humidity has a lot of variation in relation to latitude, but near the equator the humidity is the highest. 




```python
lat=[]
long=[]
citylist= pd.read_csv('/Users/Shuff/Downloads/citipy-0.0.5/citipy/worldcities.csv')
url='http://api.openweathermap.org/data/2.5/weather?q=Austin&APPID=fd231f3e638d1803fc1c8af238fcd5b7'
key='fd231f3e638d1803fc1c8af238fcd5b7'

#cityweatherhw random coords<citypylng,lat query city name on api, parse lat, long
for x in range(0,1500):
    lat.append(np.random.uniform(low=-90, high=90.00))
    long.append(np.random.uniform(low=-180.00, high = 180.00))

df=pd.DataFrame(columns=['Lat','Long'])

df['Lat']=lat
df['Long']=long

df


```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lat</th>
      <th>Long</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-54.137622</td>
      <td>97.608453</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17.823302</td>
      <td>-48.914330</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12.581607</td>
      <td>-127.457439</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41.110217</td>
      <td>-168.890156</td>
    </tr>
    <tr>
      <th>4</th>
      <td>61.861770</td>
      <td>112.286947</td>
    </tr>
    <tr>
      <th>5</th>
      <td>83.181403</td>
      <td>-1.421027</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6.269226</td>
      <td>53.646426</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-10.032597</td>
      <td>84.378195</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5.125922</td>
      <td>21.038165</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-34.802676</td>
      <td>160.225070</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11.973629</td>
      <td>108.069129</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-36.801256</td>
      <td>153.726832</td>
    </tr>
    <tr>
      <th>12</th>
      <td>52.000811</td>
      <td>163.701842</td>
    </tr>
    <tr>
      <th>13</th>
      <td>61.681544</td>
      <td>170.027348</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-56.664968</td>
      <td>-101.937143</td>
    </tr>
    <tr>
      <th>15</th>
      <td>31.690582</td>
      <td>-117.974228</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-31.216697</td>
      <td>-110.511285</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-88.257033</td>
      <td>-179.685055</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-24.493766</td>
      <td>-119.537077</td>
    </tr>
    <tr>
      <th>19</th>
      <td>11.659377</td>
      <td>151.347240</td>
    </tr>
    <tr>
      <th>20</th>
      <td>28.755731</td>
      <td>88.115975</td>
    </tr>
    <tr>
      <th>21</th>
      <td>-53.913888</td>
      <td>-148.627401</td>
    </tr>
    <tr>
      <th>22</th>
      <td>20.731314</td>
      <td>-55.502211</td>
    </tr>
    <tr>
      <th>23</th>
      <td>-37.537728</td>
      <td>130.599422</td>
    </tr>
    <tr>
      <th>24</th>
      <td>-48.159021</td>
      <td>-3.980654</td>
    </tr>
    <tr>
      <th>25</th>
      <td>65.897834</td>
      <td>-85.412038</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-38.926815</td>
      <td>12.167547</td>
    </tr>
    <tr>
      <th>27</th>
      <td>69.506102</td>
      <td>-147.594035</td>
    </tr>
    <tr>
      <th>28</th>
      <td>5.568890</td>
      <td>-176.092626</td>
    </tr>
    <tr>
      <th>29</th>
      <td>45.775099</td>
      <td>-44.938202</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1470</th>
      <td>68.513387</td>
      <td>134.331697</td>
    </tr>
    <tr>
      <th>1471</th>
      <td>31.817503</td>
      <td>-13.532846</td>
    </tr>
    <tr>
      <th>1472</th>
      <td>-82.170348</td>
      <td>136.353740</td>
    </tr>
    <tr>
      <th>1473</th>
      <td>4.960614</td>
      <td>-31.206515</td>
    </tr>
    <tr>
      <th>1474</th>
      <td>67.861846</td>
      <td>-132.105707</td>
    </tr>
    <tr>
      <th>1475</th>
      <td>-6.441851</td>
      <td>-57.689455</td>
    </tr>
    <tr>
      <th>1476</th>
      <td>13.378999</td>
      <td>-54.978847</td>
    </tr>
    <tr>
      <th>1477</th>
      <td>-66.708568</td>
      <td>92.703618</td>
    </tr>
    <tr>
      <th>1478</th>
      <td>71.188719</td>
      <td>179.111739</td>
    </tr>
    <tr>
      <th>1479</th>
      <td>-83.667874</td>
      <td>-73.153664</td>
    </tr>
    <tr>
      <th>1480</th>
      <td>62.642215</td>
      <td>160.649989</td>
    </tr>
    <tr>
      <th>1481</th>
      <td>89.292278</td>
      <td>-79.305644</td>
    </tr>
    <tr>
      <th>1482</th>
      <td>39.714408</td>
      <td>149.452477</td>
    </tr>
    <tr>
      <th>1483</th>
      <td>-5.479925</td>
      <td>19.998529</td>
    </tr>
    <tr>
      <th>1484</th>
      <td>34.494239</td>
      <td>-143.116830</td>
    </tr>
    <tr>
      <th>1485</th>
      <td>-81.773543</td>
      <td>178.210807</td>
    </tr>
    <tr>
      <th>1486</th>
      <td>-5.714745</td>
      <td>108.970708</td>
    </tr>
    <tr>
      <th>1487</th>
      <td>52.643087</td>
      <td>163.194965</td>
    </tr>
    <tr>
      <th>1488</th>
      <td>-85.026737</td>
      <td>-36.996960</td>
    </tr>
    <tr>
      <th>1489</th>
      <td>51.399569</td>
      <td>64.322964</td>
    </tr>
    <tr>
      <th>1490</th>
      <td>-33.506347</td>
      <td>68.602460</td>
    </tr>
    <tr>
      <th>1491</th>
      <td>-30.021210</td>
      <td>-25.082545</td>
    </tr>
    <tr>
      <th>1492</th>
      <td>-79.196470</td>
      <td>-13.871906</td>
    </tr>
    <tr>
      <th>1493</th>
      <td>26.461477</td>
      <td>170.262833</td>
    </tr>
    <tr>
      <th>1494</th>
      <td>-86.622496</td>
      <td>143.751508</td>
    </tr>
    <tr>
      <th>1495</th>
      <td>77.298395</td>
      <td>159.802530</td>
    </tr>
    <tr>
      <th>1496</th>
      <td>33.427875</td>
      <td>112.775613</td>
    </tr>
    <tr>
      <th>1497</th>
      <td>63.810970</td>
      <td>-84.917791</td>
    </tr>
    <tr>
      <th>1498</th>
      <td>50.507884</td>
      <td>-116.826943</td>
    </tr>
    <tr>
      <th>1499</th>
      <td>-62.773597</td>
      <td>-98.204078</td>
    </tr>
  </tbody>
</table>
<p>1500 rows × 2 columns</p>
</div>




```python
cities=[]

for index, row in df.iterrows():
    city=citipy.nearest_city(row['Lat'],row['Long'])
    cities.append(city.city_name)
df['city']=cities
df
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lat</th>
      <th>Long</th>
      <th>city</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-54.137622</td>
      <td>97.608453</td>
      <td>busselton</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17.823302</td>
      <td>-48.914330</td>
      <td>bathsheba</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12.581607</td>
      <td>-127.457439</td>
      <td>constitucion</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41.110217</td>
      <td>-168.890156</td>
      <td>bethel</td>
    </tr>
    <tr>
      <th>4</th>
      <td>61.861770</td>
      <td>112.286947</td>
      <td>chernyshevskiy</td>
    </tr>
    <tr>
      <th>5</th>
      <td>83.181403</td>
      <td>-1.421027</td>
      <td>barentsburg</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6.269226</td>
      <td>53.646426</td>
      <td>eyl</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-10.032597</td>
      <td>84.378195</td>
      <td>hithadhoo</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5.125922</td>
      <td>21.038165</td>
      <td>alindao</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-34.802676</td>
      <td>160.225070</td>
      <td>port macquarie</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11.973629</td>
      <td>108.069129</td>
      <td>da lat</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-36.801256</td>
      <td>153.726832</td>
      <td>ulladulla</td>
    </tr>
    <tr>
      <th>12</th>
      <td>52.000811</td>
      <td>163.701842</td>
      <td>nikolskoye</td>
    </tr>
    <tr>
      <th>13</th>
      <td>61.681544</td>
      <td>170.027348</td>
      <td>kamenskoye</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-56.664968</td>
      <td>-101.937143</td>
      <td>punta arenas</td>
    </tr>
    <tr>
      <th>15</th>
      <td>31.690582</td>
      <td>-117.974228</td>
      <td>rosarito</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-31.216697</td>
      <td>-110.511285</td>
      <td>rikitea</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-88.257033</td>
      <td>-179.685055</td>
      <td>vaini</td>
    </tr>
    <tr>
      <th>18</th>
      <td>-24.493766</td>
      <td>-119.537077</td>
      <td>rikitea</td>
    </tr>
    <tr>
      <th>19</th>
      <td>11.659377</td>
      <td>151.347240</td>
      <td>kavieng</td>
    </tr>
    <tr>
      <th>20</th>
      <td>28.755731</td>
      <td>88.115975</td>
      <td>mangan</td>
    </tr>
    <tr>
      <th>21</th>
      <td>-53.913888</td>
      <td>-148.627401</td>
      <td>mataura</td>
    </tr>
    <tr>
      <th>22</th>
      <td>20.731314</td>
      <td>-55.502211</td>
      <td>codrington</td>
    </tr>
    <tr>
      <th>23</th>
      <td>-37.537728</td>
      <td>130.599422</td>
      <td>flinders</td>
    </tr>
    <tr>
      <th>24</th>
      <td>-48.159021</td>
      <td>-3.980654</td>
      <td>cape town</td>
    </tr>
    <tr>
      <th>25</th>
      <td>65.897834</td>
      <td>-85.412038</td>
      <td>attawapiskat</td>
    </tr>
    <tr>
      <th>26</th>
      <td>-38.926815</td>
      <td>12.167547</td>
      <td>cape town</td>
    </tr>
    <tr>
      <th>27</th>
      <td>69.506102</td>
      <td>-147.594035</td>
      <td>college</td>
    </tr>
    <tr>
      <th>28</th>
      <td>5.568890</td>
      <td>-176.092626</td>
      <td>vaitupu</td>
    </tr>
    <tr>
      <th>29</th>
      <td>45.775099</td>
      <td>-44.938202</td>
      <td>torbay</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1470</th>
      <td>68.513387</td>
      <td>134.331697</td>
      <td>batagay</td>
    </tr>
    <tr>
      <th>1471</th>
      <td>31.817503</td>
      <td>-13.532846</td>
      <td>teguise</td>
    </tr>
    <tr>
      <th>1472</th>
      <td>-82.170348</td>
      <td>136.353740</td>
      <td>hobart</td>
    </tr>
    <tr>
      <th>1473</th>
      <td>4.960614</td>
      <td>-31.206515</td>
      <td>touros</td>
    </tr>
    <tr>
      <th>1474</th>
      <td>67.861846</td>
      <td>-132.105707</td>
      <td>inuvik</td>
    </tr>
    <tr>
      <th>1475</th>
      <td>-6.441851</td>
      <td>-57.689455</td>
      <td>jacareacanga</td>
    </tr>
    <tr>
      <th>1476</th>
      <td>13.378999</td>
      <td>-54.978847</td>
      <td>bathsheba</td>
    </tr>
    <tr>
      <th>1477</th>
      <td>-66.708568</td>
      <td>92.703618</td>
      <td>busselton</td>
    </tr>
    <tr>
      <th>1478</th>
      <td>71.188719</td>
      <td>179.111739</td>
      <td>leningradskiy</td>
    </tr>
    <tr>
      <th>1479</th>
      <td>-83.667874</td>
      <td>-73.153664</td>
      <td>ushuaia</td>
    </tr>
    <tr>
      <th>1480</th>
      <td>62.642215</td>
      <td>160.649989</td>
      <td>evensk</td>
    </tr>
    <tr>
      <th>1481</th>
      <td>89.292278</td>
      <td>-79.305644</td>
      <td>qaanaaq</td>
    </tr>
    <tr>
      <th>1482</th>
      <td>39.714408</td>
      <td>149.452477</td>
      <td>nemuro</td>
    </tr>
    <tr>
      <th>1483</th>
      <td>-5.479925</td>
      <td>19.998529</td>
      <td>tshikapa</td>
    </tr>
    <tr>
      <th>1484</th>
      <td>34.494239</td>
      <td>-143.116830</td>
      <td>hilo</td>
    </tr>
    <tr>
      <th>1485</th>
      <td>-81.773543</td>
      <td>178.210807</td>
      <td>kaitangata</td>
    </tr>
    <tr>
      <th>1486</th>
      <td>-5.714745</td>
      <td>108.970708</td>
      <td>indramayu</td>
    </tr>
    <tr>
      <th>1487</th>
      <td>52.643087</td>
      <td>163.194965</td>
      <td>ust-kamchatsk</td>
    </tr>
    <tr>
      <th>1488</th>
      <td>-85.026737</td>
      <td>-36.996960</td>
      <td>ushuaia</td>
    </tr>
    <tr>
      <th>1489</th>
      <td>51.399569</td>
      <td>64.322964</td>
      <td>kushmurun</td>
    </tr>
    <tr>
      <th>1490</th>
      <td>-33.506347</td>
      <td>68.602460</td>
      <td>mahebourg</td>
    </tr>
    <tr>
      <th>1491</th>
      <td>-30.021210</td>
      <td>-25.082545</td>
      <td>vila velha</td>
    </tr>
    <tr>
      <th>1492</th>
      <td>-79.196470</td>
      <td>-13.871906</td>
      <td>cape town</td>
    </tr>
    <tr>
      <th>1493</th>
      <td>26.461477</td>
      <td>170.262833</td>
      <td>butaritari</td>
    </tr>
    <tr>
      <th>1494</th>
      <td>-86.622496</td>
      <td>143.751508</td>
      <td>hobart</td>
    </tr>
    <tr>
      <th>1495</th>
      <td>77.298395</td>
      <td>159.802530</td>
      <td>cherskiy</td>
    </tr>
    <tr>
      <th>1496</th>
      <td>33.427875</td>
      <td>112.775613</td>
      <td>yunyang</td>
    </tr>
    <tr>
      <th>1497</th>
      <td>63.810970</td>
      <td>-84.917791</td>
      <td>attawapiskat</td>
    </tr>
    <tr>
      <th>1498</th>
      <td>50.507884</td>
      <td>-116.826943</td>
      <td>invermere</td>
    </tr>
    <tr>
      <th>1499</th>
      <td>-62.773597</td>
      <td>-98.204078</td>
      <td>punta arenas</td>
    </tr>
  </tbody>
</table>
<p>1500 rows × 3 columns</p>
</div>




```python
df=df.drop_duplicates('city',keep='first')
len(df)
```




    605




```python
temp=[]
humidity=[]
clouds=[]
windspeed=[]

url='http://api.openweathermap.org/data/2.5/weather?q='
units='imperial'
for index, row in df.iterrows():
    try:
    

        target=url+row['city']+'&appid='+ key + '&units=' +units 
        response=req.get(target).json()
        temp.append(response['main']['temp'])
        humidity.append(response['main']['humidity'])
        clouds.append(response['clouds']['all'])
        windspeed.append(response['wind']['speed'])
        time.sleep(1)
    except:
        df.drop(index,inplace=True)
        pass
df['temp']=temp
df['humidity']=humidity
df['windspeed']=windspeed
df['clouds']=clouds

df

```

    /anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:20: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    /anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:22: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    /anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:23: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    /anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:24: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    /anaconda3/lib/python3.6/site-packages/ipykernel_launcher.py:25: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy





<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Lat</th>
      <th>Long</th>
      <th>city</th>
      <th>temp</th>
      <th>humidity</th>
      <th>windspeed</th>
      <th>clouds</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-54.137622</td>
      <td>97.608453</td>
      <td>busselton</td>
      <td>63.48</td>
      <td>100</td>
      <td>11.79</td>
      <td>48</td>
    </tr>
    <tr>
      <th>1</th>
      <td>17.823302</td>
      <td>-48.914330</td>
      <td>bathsheba</td>
      <td>75.54</td>
      <td>100</td>
      <td>14.92</td>
      <td>80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>12.581607</td>
      <td>-127.457439</td>
      <td>constitucion</td>
      <td>78.80</td>
      <td>15</td>
      <td>17.22</td>
      <td>40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>41.110217</td>
      <td>-168.890156</td>
      <td>bethel</td>
      <td>24.80</td>
      <td>62</td>
      <td>5.82</td>
      <td>75</td>
    </tr>
    <tr>
      <th>4</th>
      <td>61.861770</td>
      <td>112.286947</td>
      <td>chernyshevskiy</td>
      <td>-30.57</td>
      <td>49</td>
      <td>2.95</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6.269226</td>
      <td>53.646426</td>
      <td>eyl</td>
      <td>74.19</td>
      <td>100</td>
      <td>6.08</td>
      <td>44</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-10.032597</td>
      <td>84.378195</td>
      <td>hithadhoo</td>
      <td>80.67</td>
      <td>100</td>
      <td>7.99</td>
      <td>80</td>
    </tr>
    <tr>
      <th>8</th>
      <td>5.125922</td>
      <td>21.038165</td>
      <td>alindao</td>
      <td>69.20</td>
      <td>99</td>
      <td>4.07</td>
      <td>64</td>
    </tr>
    <tr>
      <th>9</th>
      <td>-34.802676</td>
      <td>160.225070</td>
      <td>port macquarie</td>
      <td>73.40</td>
      <td>64</td>
      <td>8.05</td>
      <td>40</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11.973629</td>
      <td>108.069129</td>
      <td>da lat</td>
      <td>62.76</td>
      <td>94</td>
      <td>2.06</td>
      <td>24</td>
    </tr>
    <tr>
      <th>11</th>
      <td>-36.801256</td>
      <td>153.726832</td>
      <td>ulladulla</td>
      <td>71.60</td>
      <td>60</td>
      <td>12.75</td>
      <td>40</td>
    </tr>
    <tr>
      <th>12</th>
      <td>52.000811</td>
      <td>163.701842</td>
      <td>nikolskoye</td>
      <td>1.40</td>
      <td>84</td>
      <td>2.24</td>
      <td>0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>-56.664968</td>
      <td>-101.937143</td>
      <td>punta arenas</td>
      <td>57.20</td>
      <td>54</td>
      <td>25.28</td>
      <td>0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>31.690582</td>
      <td>-117.974228</td>
      <td>rosarito</td>
      <td>76.62</td>
      <td>52</td>
      <td>6.93</td>
      <td>36</td>
    </tr>
    <tr>
      <th>16</th>
      <td>-31.216697</td>
      <td>-110.511285</td>
      <td>rikitea</td>
      <td>81.66</td>
      <td>98</td>
      <td>18.16</td>
      <td>0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>-88.257033</td>
      <td>-179.685055</td>
      <td>vaini</td>
      <td>59.25</td>
      <td>76</td>
      <td>2.28</td>
      <td>0</td>
    </tr>
    <tr>
      <th>19</th>
      <td>11.659377</td>
      <td>151.347240</td>
      <td>kavieng</td>
      <td>84.27</td>
      <td>100</td>
      <td>3.29</td>
      <td>12</td>
    </tr>
    <tr>
      <th>20</th>
      <td>28.755731</td>
      <td>88.115975</td>
      <td>mangan</td>
      <td>19.74</td>
      <td>68</td>
      <td>2.17</td>
      <td>0</td>
    </tr>
    <tr>
      <th>21</th>
      <td>-53.913888</td>
      <td>-148.627401</td>
      <td>mataura</td>
      <td>67.35</td>
      <td>94</td>
      <td>4.63</td>
      <td>100</td>
    </tr>
    <tr>
      <th>22</th>
      <td>20.731314</td>
      <td>-55.502211</td>
      <td>codrington</td>
      <td>70.77</td>
      <td>97</td>
      <td>3.85</td>
      <td>92</td>
    </tr>
    <tr>
      <th>23</th>
      <td>-37.537728</td>
      <td>130.599422</td>
      <td>flinders</td>
      <td>71.60</td>
      <td>60</td>
      <td>12.75</td>
      <td>40</td>
    </tr>
    <tr>
      <th>24</th>
      <td>-48.159021</td>
      <td>-3.980654</td>
      <td>cape town</td>
      <td>68.00</td>
      <td>64</td>
      <td>19.46</td>
      <td>0</td>
    </tr>
    <tr>
      <th>27</th>
      <td>69.506102</td>
      <td>-147.594035</td>
      <td>college</td>
      <td>0.75</td>
      <td>65</td>
      <td>10.29</td>
      <td>40</td>
    </tr>
    <tr>
      <th>29</th>
      <td>45.775099</td>
      <td>-44.938202</td>
      <td>torbay</td>
      <td>33.80</td>
      <td>100</td>
      <td>6.93</td>
      <td>75</td>
    </tr>
    <tr>
      <th>30</th>
      <td>-72.514341</td>
      <td>41.455829</td>
      <td>port alfred</td>
      <td>66.90</td>
      <td>97</td>
      <td>6.42</td>
      <td>92</td>
    </tr>
    <tr>
      <th>31</th>
      <td>-30.669160</td>
      <td>15.023131</td>
      <td>oranjemund</td>
      <td>62.54</td>
      <td>96</td>
      <td>18.72</td>
      <td>92</td>
    </tr>
    <tr>
      <th>32</th>
      <td>38.313229</td>
      <td>35.493839</td>
      <td>develi</td>
      <td>26.60</td>
      <td>86</td>
      <td>8.05</td>
      <td>0</td>
    </tr>
    <tr>
      <th>33</th>
      <td>56.094692</td>
      <td>-58.836619</td>
      <td>saint-augustin</td>
      <td>49.19</td>
      <td>93</td>
      <td>24.16</td>
      <td>75</td>
    </tr>
    <tr>
      <th>34</th>
      <td>46.085397</td>
      <td>-131.477431</td>
      <td>port hardy</td>
      <td>46.40</td>
      <td>65</td>
      <td>16.11</td>
      <td>40</td>
    </tr>
    <tr>
      <th>35</th>
      <td>-52.053863</td>
      <td>-165.309771</td>
      <td>avarua</td>
      <td>84.20</td>
      <td>74</td>
      <td>10.29</td>
      <td>40</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1393</th>
      <td>35.259933</td>
      <td>-81.752754</td>
      <td>gaffney</td>
      <td>57.20</td>
      <td>93</td>
      <td>5.82</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1398</th>
      <td>-0.860088</td>
      <td>-79.086345</td>
      <td>la mana</td>
      <td>62.60</td>
      <td>67</td>
      <td>6.93</td>
      <td>75</td>
    </tr>
    <tr>
      <th>1399</th>
      <td>51.782609</td>
      <td>-114.891116</td>
      <td>rocky mountain house</td>
      <td>18.80</td>
      <td>80</td>
      <td>6.64</td>
      <td>88</td>
    </tr>
    <tr>
      <th>1408</th>
      <td>19.718639</td>
      <td>74.568585</td>
      <td>shirdi</td>
      <td>69.51</td>
      <td>49</td>
      <td>5.86</td>
      <td>68</td>
    </tr>
    <tr>
      <th>1415</th>
      <td>27.178261</td>
      <td>136.731551</td>
      <td>shingu</td>
      <td>46.40</td>
      <td>49</td>
      <td>18.34</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1425</th>
      <td>50.160198</td>
      <td>-6.236318</td>
      <td>penzance</td>
      <td>37.40</td>
      <td>93</td>
      <td>33.33</td>
      <td>90</td>
    </tr>
    <tr>
      <th>1426</th>
      <td>68.530298</td>
      <td>58.971389</td>
      <td>inta</td>
      <td>11.10</td>
      <td>84</td>
      <td>5.75</td>
      <td>76</td>
    </tr>
    <tr>
      <th>1429</th>
      <td>-45.489106</td>
      <td>171.505382</td>
      <td>waitati</td>
      <td>67.53</td>
      <td>92</td>
      <td>4.29</td>
      <td>92</td>
    </tr>
    <tr>
      <th>1435</th>
      <td>16.368906</td>
      <td>2.757841</td>
      <td>filingue</td>
      <td>73.74</td>
      <td>20</td>
      <td>10.67</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1437</th>
      <td>10.390887</td>
      <td>118.080807</td>
      <td>bacungan</td>
      <td>77.00</td>
      <td>83</td>
      <td>4.70</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1438</th>
      <td>22.929809</td>
      <td>34.124816</td>
      <td>aswan</td>
      <td>68.00</td>
      <td>22</td>
      <td>5.82</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1439</th>
      <td>-7.727830</td>
      <td>2.915024</td>
      <td>gamba</td>
      <td>-4.38</td>
      <td>58</td>
      <td>1.28</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1441</th>
      <td>-23.938335</td>
      <td>-27.424232</td>
      <td>caravelas</td>
      <td>82.29</td>
      <td>99</td>
      <td>18.28</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1443</th>
      <td>44.042343</td>
      <td>28.353791</td>
      <td>mereni</td>
      <td>3.20</td>
      <td>84</td>
      <td>4.70</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1450</th>
      <td>-12.427768</td>
      <td>141.336305</td>
      <td>daru</td>
      <td>76.53</td>
      <td>70</td>
      <td>5.75</td>
      <td>64</td>
    </tr>
    <tr>
      <th>1452</th>
      <td>-3.780131</td>
      <td>143.571050</td>
      <td>wewak</td>
      <td>83.19</td>
      <td>78</td>
      <td>2.39</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1455</th>
      <td>48.552275</td>
      <td>-79.902161</td>
      <td>kirkland lake</td>
      <td>26.60</td>
      <td>63</td>
      <td>9.17</td>
      <td>75</td>
    </tr>
    <tr>
      <th>1461</th>
      <td>-37.370083</td>
      <td>146.058594</td>
      <td>healesville</td>
      <td>67.08</td>
      <td>60</td>
      <td>3.36</td>
      <td>40</td>
    </tr>
    <tr>
      <th>1462</th>
      <td>17.264520</td>
      <td>79.146216</td>
      <td>nalgonda</td>
      <td>62.58</td>
      <td>72</td>
      <td>2.73</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1466</th>
      <td>46.878126</td>
      <td>144.400562</td>
      <td>novikovo</td>
      <td>17.58</td>
      <td>100</td>
      <td>1.39</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1467</th>
      <td>14.341241</td>
      <td>98.496926</td>
      <td>dawei</td>
      <td>68.34</td>
      <td>90</td>
      <td>2.17</td>
      <td>8</td>
    </tr>
    <tr>
      <th>1468</th>
      <td>-29.070408</td>
      <td>-51.480046</td>
      <td>bento goncalves</td>
      <td>72.39</td>
      <td>84</td>
      <td>1.95</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1471</th>
      <td>31.817503</td>
      <td>-13.532846</td>
      <td>teguise</td>
      <td>62.60</td>
      <td>88</td>
      <td>3.36</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1473</th>
      <td>4.960614</td>
      <td>-31.206515</td>
      <td>touros</td>
      <td>73.07</td>
      <td>100</td>
      <td>5.19</td>
      <td>88</td>
    </tr>
    <tr>
      <th>1475</th>
      <td>-6.441851</td>
      <td>-57.689455</td>
      <td>jacareacanga</td>
      <td>78.92</td>
      <td>89</td>
      <td>2.39</td>
      <td>24</td>
    </tr>
    <tr>
      <th>1480</th>
      <td>62.642215</td>
      <td>160.649989</td>
      <td>evensk</td>
      <td>4.62</td>
      <td>100</td>
      <td>4.97</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1483</th>
      <td>-5.479925</td>
      <td>19.998529</td>
      <td>tshikapa</td>
      <td>70.10</td>
      <td>89</td>
      <td>2.95</td>
      <td>92</td>
    </tr>
    <tr>
      <th>1486</th>
      <td>-5.714745</td>
      <td>108.970708</td>
      <td>indramayu</td>
      <td>69.24</td>
      <td>94</td>
      <td>3.85</td>
      <td>20</td>
    </tr>
    <tr>
      <th>1496</th>
      <td>33.427875</td>
      <td>112.775613</td>
      <td>yunyang</td>
      <td>33.69</td>
      <td>93</td>
      <td>2.62</td>
      <td>44</td>
    </tr>
    <tr>
      <th>1498</th>
      <td>50.507884</td>
      <td>-116.826943</td>
      <td>invermere</td>
      <td>29.15</td>
      <td>64</td>
      <td>1.72</td>
      <td>68</td>
    </tr>
  </tbody>
</table>
<p>533 rows × 7 columns</p>
</div>




```python
len(df)
```




    533




```python
#Temperature (F) vs. Latitude
plt.scatter(df['Lat'],df['temp'],marker='o',alpha=.7, s=22)
plt.title('Latitude V Temperature')
plt.xlabel('Latitude')
plt.ylabel('Temperature(F)')

sns.set()
plt.show()
```


![png](hw6weatherpy_files/hw6weatherpy_8_0.png)



```python
#Humidity (%) vs. Latitude
plt.scatter(df['Lat'],df['humidity'],marker='o', color='green', alpha=.5, s=24 )
plt.title('Humidity V Latitude (02/28/2018)')
plt.xlabel('Latitude')
plt.ylabel('Humidity%')

sns.set()
plt.show()
```


![png](hw6weatherpy_files/hw6weatherpy_9_0.png)



```python
#Cloudiness (%) vs. Latitude
plt.scatter(df['Lat'],df['clouds'],marker='o', color='purple', alpha=.5, s=27)
plt.title('Latitude V Cloudiness (02/28/2018)')
plt.xlabel('Latitude')
plt.ylabel('Cloudiness')

sns.set()
plt.show()


```


![png](hw6weatherpy_files/hw6weatherpy_10_0.png)



```python
#Wind Speed (mph) vs. Latitude
plt.scatter(df['Lat'],df['windspeed'],marker='o', color='black',alpha=.5, s=28)
plt.title('Windspeed V Latitude (02/28/2018)')
plt.xlabel('Latitude')
plt.ylabel('Windspeed')

sns.set()
plt.show()


```


![png](hw6weatherpy_files/hw6weatherpy_11_0.png)

