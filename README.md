# Ex.No: 1B CONVERSION OF NON STATIONARY TO STATIONARY DATA
## Date: 
## AIM:
To perform regular differncing,seasonal adjustment and log transformation on daily website visitors data.
## ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
## PROGRAM:
### Name: RONICK AAKSHATH P
### Reg. No.: 212222240084
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import statsmodels.api as sm

df = pd.read_csv('daily_website_visitors.csv')
df.head()

df['Date'] = pd.to_datetime(df['Date'])
df.set_index('Date', inplace=True)
df['Page.Loads'] = pd.to_numeric(df['Page.Loads'].str.replace(',', ''), errors='coerce')
df.dropna(inplace=True)

df['Log_Page_Loads'] = np.log(df['Page.Loads'])

df['Diff_Log_Page_Loads'] = df['Log_Page_Loads'].diff()

decomposition = sm.tsa.seasonal_decompose(df['Log_Page_Loads'], model='additive')
seasonal_adjusted = df['Log_Page_Loads'] - decomposition.seasonal
df['Seasonal_Adjusted'] = seasonal_adjusted

plt.figure(figsize=(14, 10))

plt.subplot(4, 1, 1)
plt.plot(df['Page.Loads'], label='Original Data', color='blue')
plt.title('Original Page Loads')
plt.legend()

plt.subplot(4, 1, 2)
plt.plot(df['Log_Page_Loads'], label='Log Transformed Data', color='orange')
plt.title('Log Transformed Page Loads')
plt.legend()

plt.subplot(4, 1, 3)
plt.plot(df['Diff_Log_Page_Loads'], label='Differenced Log Data', color='green')
plt.title('Differenced Log Page Loads')
plt.legend()

plt.subplot(4, 1, 4)
plt.plot(df['Seasonal_Adjusted'], label='Seasonal Adjusted Data', color='red')
plt.title('Seasonally Adjusted Page Loads')
plt.legend()

plt.tight_layout()
plt.show()
```
## OUTPUT:
![image](https://github.com/user-attachments/assets/df304c51-eae9-4157-a232-47eca7135308)

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on daily website visitors data.
