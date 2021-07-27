## Analytics on Gas prices over the world in USD



```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```


```python
gas = pd.read_csv("gas_prices.csv").fillna(0)
gas.head(7)
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
      <th>Year</th>
      <th>Australia</th>
      <th>Canada</th>
      <th>France</th>
      <th>Germany</th>
      <th>Italy</th>
      <th>Japan</th>
      <th>Mexico</th>
      <th>South Korea</th>
      <th>UK</th>
      <th>USA</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1990</td>
      <td>0.00</td>
      <td>1.87</td>
      <td>3.63</td>
      <td>2.65</td>
      <td>4.59</td>
      <td>3.16</td>
      <td>1.00</td>
      <td>2.05</td>
      <td>2.82</td>
      <td>1.16</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1991</td>
      <td>1.96</td>
      <td>1.92</td>
      <td>3.45</td>
      <td>2.90</td>
      <td>4.50</td>
      <td>3.46</td>
      <td>1.30</td>
      <td>2.49</td>
      <td>3.01</td>
      <td>1.14</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1992</td>
      <td>1.89</td>
      <td>1.73</td>
      <td>3.56</td>
      <td>3.27</td>
      <td>4.53</td>
      <td>3.58</td>
      <td>1.50</td>
      <td>2.65</td>
      <td>3.06</td>
      <td>1.13</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1993</td>
      <td>1.73</td>
      <td>1.57</td>
      <td>3.41</td>
      <td>3.07</td>
      <td>3.68</td>
      <td>4.16</td>
      <td>1.56</td>
      <td>2.88</td>
      <td>2.84</td>
      <td>1.11</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1994</td>
      <td>1.84</td>
      <td>1.45</td>
      <td>3.59</td>
      <td>3.52</td>
      <td>3.70</td>
      <td>4.36</td>
      <td>1.48</td>
      <td>2.87</td>
      <td>2.99</td>
      <td>1.11</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1995</td>
      <td>1.95</td>
      <td>1.53</td>
      <td>4.26</td>
      <td>3.96</td>
      <td>4.00</td>
      <td>4.43</td>
      <td>1.11</td>
      <td>2.94</td>
      <td>3.21</td>
      <td>1.15</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1996</td>
      <td>2.12</td>
      <td>1.61</td>
      <td>4.41</td>
      <td>3.94</td>
      <td>4.39</td>
      <td>3.64</td>
      <td>1.25</td>
      <td>3.18</td>
      <td>3.34</td>
      <td>1.23</td>
    </tr>
  </tbody>
</table>
</div>




```python
gas.index=gas["Year"]
gas.head(7)
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
      <th>Year</th>
      <th>Australia</th>
      <th>Canada</th>
      <th>France</th>
      <th>Germany</th>
      <th>Italy</th>
      <th>Japan</th>
      <th>Mexico</th>
      <th>South Korea</th>
      <th>UK</th>
      <th>USA</th>
    </tr>
    <tr>
      <th>Year</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1990</th>
      <td>1990</td>
      <td>0.00</td>
      <td>1.87</td>
      <td>3.63</td>
      <td>2.65</td>
      <td>4.59</td>
      <td>3.16</td>
      <td>1.00</td>
      <td>2.05</td>
      <td>2.82</td>
      <td>1.16</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>1991</td>
      <td>1.96</td>
      <td>1.92</td>
      <td>3.45</td>
      <td>2.90</td>
      <td>4.50</td>
      <td>3.46</td>
      <td>1.30</td>
      <td>2.49</td>
      <td>3.01</td>
      <td>1.14</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>1992</td>
      <td>1.89</td>
      <td>1.73</td>
      <td>3.56</td>
      <td>3.27</td>
      <td>4.53</td>
      <td>3.58</td>
      <td>1.50</td>
      <td>2.65</td>
      <td>3.06</td>
      <td>1.13</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>1993</td>
      <td>1.73</td>
      <td>1.57</td>
      <td>3.41</td>
      <td>3.07</td>
      <td>3.68</td>
      <td>4.16</td>
      <td>1.56</td>
      <td>2.88</td>
      <td>2.84</td>
      <td>1.11</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>1994</td>
      <td>1.84</td>
      <td>1.45</td>
      <td>3.59</td>
      <td>3.52</td>
      <td>3.70</td>
      <td>4.36</td>
      <td>1.48</td>
      <td>2.87</td>
      <td>2.99</td>
      <td>1.11</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>1995</td>
      <td>1.95</td>
      <td>1.53</td>
      <td>4.26</td>
      <td>3.96</td>
      <td>4.00</td>
      <td>4.43</td>
      <td>1.11</td>
      <td>2.94</td>
      <td>3.21</td>
      <td>1.15</td>
    </tr>
    <tr>
      <th>1996</th>
      <td>1996</td>
      <td>2.12</td>
      <td>1.61</td>
      <td>4.41</td>
      <td>3.94</td>
      <td>4.39</td>
      <td>3.64</td>
      <td>1.25</td>
      <td>3.18</td>
      <td>3.34</td>
      <td>1.23</td>
    </tr>
  </tbody>
</table>
</div>



### European Countries


```python
plt.figure(figsize=(8,5), dpi=120)
plt.plot(gas.Year,gas["France"], 'y.-', label="France")
plt.plot(gas.Year,gas["Germany"],"b.-", label="Germany")
plt.plot(gas.Year,gas["Italy"], "g.-", label="Italy")
plt.legend()
plt.xticks(gas.Year[::2])
plt.title("Gas Prices over Time (in USD)")
plt.xlabel("Year")
plt.ylabel("US Dollars")
plt.show()
```


    
![png](output_5_0.png)
    


## Continental countries


```python
countries = ["USA","Canada","Germany","Japan","Australia","South Korea"]
font = fontdict={"fontname":"Verdana","fontsize":13}
plt.figure(figsize=(8,5), dpi=120)
plt.title("Gas Prices over time (in USD) ", font)
for country in gas:
    if country in countries:
        plt.plot(gas.Year,gas[country], marker=".",label=country)
plt.xticks(gas.Year[::2].tolist()+[2010])
plt.legend()
plt.xlabel("Year", font)
plt.ylabel("US Dollars", font)
plt.show()
#save the graph: plt.figsave("gas_prices.png", dpi=200)
        
```


    
![png](output_7_0.png)
    



```python
gas.loc[1998,["Japan","USA","Germany"]]
```




    Japan      2.82
    USA        1.06
    Germany    3.34
    Name: 1998, dtype: float64


