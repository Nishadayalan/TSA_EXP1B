# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 17-08-2025

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
```
```
data = pd.read_csv('/content/plane_crash.csv')
```
```
data['Date'] = pd.to_datetime(data['Date'], errors='coerce')
data.set_index('Date', inplace=True)
```
```
data = data['Fatalities'].resample('Y').sum().to_frame(name='Fatalities')
```
```
data['fatalities_diff'] = data['Fatalities'] - data['Fatalities'].shift(1)
```
```
result = seasonal_decompose(data['Fatalities'].dropna(), model='additive', period=12)
data['fatalities_sea_diff'] = result.resid
```
```
data['fatalities_log'] = np.log(data['Fatalities'].replace(0, np.nan))
```
```
data['fatalities_log_diff'] = data['fatalities_log'] - data['fatalities_log'].shift(1)
```
```
plt.figure(figsize=(16, 16))
```
```
plt.subplot(6, 1, 1)
plt.plot(data['Fatalities'], label='Original', color='blue')
plt.legend(loc='upper left', bbox_to_anchor=(1.0, 1.0))   # move outside
plt.title('Original Data')
plt.xlabel('Year')
plt.ylabel('Fatalities')

```
```

plt.subplot(6, 1, 2)
plt.plot(data['fatalities_diff'], label='Regular Difference', color='orange')
plt.legend(loc='upper left', bbox_to_anchor=(1.0, 1.0))   # moved legend outside
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Diff(Fatalities)')
```
```
plt.subplot(6, 1, 3)
plt.plot(data['fatalities_sea_diff'], label='Seasonal Adjustment', color='green')
plt.legend(loc='upper left', bbox_to_anchor=(1.0, 1.0))
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Fatalities')
```
```
plt.subplot(6, 1, 4)
plt.plot(data['fatalities_log'], label='Log Transformation', color='red')
plt.legend(loc='upper left', bbox_to_anchor=(1.0, 1.0))
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Fatalities)')
```
```
plt.subplot(6, 1, 6)
plt.plot(data['fatalities_log_seasonal_diff'], label='Log + Regular + Seasonal Differencing', color='brown')
plt.legend(loc='upper left', bbox_to_anchor=(1.0, 1.0))
plt.title('Log Transformation + Regular Differencing + Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('SDiff(RDiff(Log(Fatalities)))')
```



### OUTPUT:
<img width="955" height="228" alt="image" src="https://github.com/user-attachments/assets/74d653d4-8f78-434e-8d2f-9a517e3fded8" />



REGULAR DIFFERENCING:
<img width="1111" height="226" alt="image" src="https://github.com/user-attachments/assets/382fd7b2-3a3e-4635-a873-51f962c55cce" />




SEASONAL ADJUSTMENT:
<img width="1110" height="232" alt="image" src="https://github.com/user-attachments/assets/d6098396-3030-4cdf-b35d-c3bca11455f1" />



LOG TRANSFORMATION:
<img width="1055" height="218" alt="image" src="https://github.com/user-attachments/assets/9c0e1f7f-5fc5-4a94-a2dd-67d392fbd38e" />



Log Transformation + Regular Differencing + Seasonal Differencing:
<img width="1317" height="240" alt="image" src="https://github.com/user-attachments/assets/f376fea4-6ec2-4934-96c0-51b95fccab7a" />


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
