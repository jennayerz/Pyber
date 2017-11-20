

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import os
```

Analysis
1. Most of the drivers are located in the Urban city type. And in turn, they make the most in total fares and rides as indicated by the red areas in the pie charts.
2. The Rural city type has the smallest amount of drivers, but the percent of total fares surpasses the percent of drivers. This could mean that they make more money driving around than compared to the Urban city type. In the Urban city type, the percentage of drivers is way higher but their percent in total fares is lower than the percent of drivers, meaning that the Urban area is more saturated with drivers.
3. On the scatter plot, most of the cluster is near the bottom between 20-30 rides for every city and an average fare of about $20-30.


```python
# Read both data files
filepath = os.path.join('..', 'Pyber', 'city_data.csv')
city_data_df = pd.read_csv(filepath)
city_data_df.head()

filepath2 = os.path.join('..', 'Pyber', 'ride_data.csv')
ride_data_df = pd.read_csv(filepath2)
ride_data_df.head()

# Merge files together
merge_data_df = pd.merge(ride_data_df, city_data_df, on='city', how='left')
merge_data_df.head()
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
      <td>46</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
      <td>35</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
      <td>55</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
      <td>68</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# GRAPH 'Percent of total fares by city type'
# Calculate total number of fares per city type
city_type_fare = merge_data_df.groupby('type')['fare'].sum()
city_type_fare_df = pd.DataFrame(city_type_fare)
city_type_fare_df

# Graph
labels = ['Rural', 'Suburban', 'Urban']
sizes = [4255.09, 20335.69, 40078.34]

colors = ['yellow', 'blue', 'red']
explode = [0, 0, 0.1]

plt.pie(sizes, labels=labels, colors=colors, explode=explode,
        autopct="{0:1.1f}%".format, shadow=True, startangle=140)
plt.axis('equal')
plt.title('% of Total Fares by City Type')
plt.show()
```


![png](output_3_0.png)



```python
# GRAPH 'Percent of total rides by city type'
# Calculate total number of rides per city type
city_type_ride = merge_data_df.groupby('type')['ride_id'].count()
city_type_ride_df = pd.DataFrame(city_type_ride)
city_type_ride_df

# Graph
labels = ['Rural', 'Suburban', 'Urban']
sizes = [125, 657, 1625]

colors = ['yellow', 'blue', 'red']
explode = [0, 0, 0.1]

plt.pie(sizes, labels=labels, colors=colors, explode=explode,
        autopct="{0:1.1f}%".format, shadow=True, startangle=140)
plt.axis('equal')
plt.title('% of Total Rides by City Type')
plt.show()
```


![png](output_4_0.png)



```python
# GRAPH 'Percent of total drivers by city type'
#Calculate total number of drivers per city type
city_type_driver = city_data_df.groupby('type')['driver_count'].sum()
city_type_driver_df = pd.DataFrame(city_type_driver)
city_type_driver_df

# Graph
labels = ['Rural', 'Suburban', 'Urban']
sizes = [104, 638, 2607]

colors = ['yellow', 'blue', 'red']
explode = [0, 0, 0.1]

plt.pie(sizes, labels=labels, colors=colors, explode=explode,
        autopct="{0:1.1f}%".format, shadow=True, startangle=140)
plt.axis('equal')
plt.title('% of Total Drivers by City Type')
plt.show()
```


![png](output_5_0.png)



```python
# Calculate 'Average fare per city'
avg_fare_city = merge_data_df.groupby('city')['fare'].mean()
avg_fare_city_df = pd.DataFrame(avg_fare_city)
avg_fare_city_df.head()
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
      <th>fare</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>23.928710</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.609615</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.315556</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.625000</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.981579</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Calculate 'Total rides per city'
total_rides = merge_data_df.groupby('city')['fare'].count()
total_rides_df = pd.DataFrame(total_rides)
updated_total_rides_df = total_rides_df.rename(columns={'fare': 'total rides'})
updated_total_rides_df.head()
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
      <th>total rides</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Calculate 'Total # of drivers by city'
total_drivers = merge_data_df.groupby('city')['driver_count'].value_counts()
total_drivers_df = pd.DataFrame(total_drivers)
total_drivers_df1 = total_drivers_df.rename(columns={'driver_count': 'total rides'})
total_drivers_df1.reset_index().head()
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
      <th>city</th>
      <th>driver_count</th>
      <th>total rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Calculate 'Rides per city per city type'
rides_per_city_type = merge_data_df.groupby('type')['city'].value_counts()
rides_per_city_type_df = pd.DataFrame(rides_per_city_type)
rides_per_city_type_df1 = rides_per_city_type_df.rename(columns={'city': "# of rides"})
rides_per_city_type_df1.reset_index().head()

# Set index to 'city type'
#index_city_type_df = rides_per_city_type_df.set_index('type')
#index_city_type_df
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
      <th>type</th>
      <th>city</th>
      <th># of rides</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Rural</td>
      <td>South Joseph</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Rural</td>
      <td>East Leslie</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Rural</td>
      <td>East Stephen</td>
      <td>10</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Rural</td>
      <td>Kennethburgh</td>
      <td>10</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rural</td>
      <td>North Whitney</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
</div>




```python
# GRAPH 'Total # of Rides (per City) vs Average Fare($)'
# Dot size correlates to # of drivers per city
x_values = total_rides
y_values = avg_fare_city

plt.scatter(x_values, y_values,
            marker='o',
            sizes=total_drivers, alpha = 0.50)
plt.xlabel('Total # of Rides (per City)')
plt.ylabel('Average Fare ($)')
plt.title('Pyber Ride Sharing Data 2016')
plt.show()
```


![png](output_10_0.png)

