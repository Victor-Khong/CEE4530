```python
from aguaclara.core.units import unit_registry as u
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from scipy import stats

#Importing file
df = pd.read_csv('lab1.csv',delimiter = ',')
print(df)

#Columns
list(df)
columns = df.columns
print(columns)

#Defining variables
x = df[list(df)[0]].values
x = df.iloc[:,0].values * u.mg/u.L
x
y = df[list(df)[1]].values
y = df.iloc[:,1].values * u.volt
y

#Equation
slope, intercept, r_value, p_value, std_err = stats.linregress(x,y)
intercept = intercept * y.units
print(intercept)
slope = slope * y.units/x.units
print(slope)
#Figure
fig, ax = plt.subplots()
ax.plot(x, y, 'ro', )
ax.plot(x, slope * x + intercept, 'k-', )
ax.set(xlabel=list(df)[0])
ax.set(ylabel=list(df)[1])
ax.legend(['Measured', 'Linear regression'])
ax.grid(True)
plt.savefig('linear')
plt.show()
```
![linear](https://github.com/Victor-Khong/CEE4530/blob/master/linear.png?raw=true)
$$Voltage=-0.2466*Concentration+3.289 (volt)$$
