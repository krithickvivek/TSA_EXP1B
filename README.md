# Ex.No: 1-B CONVERSION OF NON STATIONARY TO STATIONARY DATA
### Date: 

## AIM
To perform regular differencing, seasonal adjustment, and log transformation on Apple revenue time series data.
## DATASET
Apple 2009-2005
## SOFTWARE REQUIRED
Google Colab
## ALGORITHM
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM
```python
from matplotlib import pyplot as plt
import pandas as pd
import numpy as np

data = pd.read_csv('Apple 2009-2024.csv')
data.head()

for col in data.columns:
    if data[col].dtype == 'object':
        data[col] = data[col].str.replace(',', '').str.replace('$', '').str.replace('%', '').astype(float)
data.describe()

# Clean column names
data.columns = data.columns.str.strip()

# Create Year column (since it's not present)
data['Year'] = range(2009, 2009 + len(data))

# Convert to datetime
data['Year'] = pd.to_datetime(data['Year'], format='%Y')

# Set index
data.set_index('Year', inplace=True)

# -------- DIFFERENCING --------
data['diff'] = data['Revenue (millions)'] - data['Revenue (millions)'].shift(1)

# -------- SEASONAL DIFFERENCING (lag = 4 for yearly trend example) --------
data['seasonal_diff'] = data['Revenue (millions)'] - data['Revenue (millions)'].shift(4)

# -------- LOG TRANSFORM --------
data['log'] = np.log(data['Revenue (millions)'])

plt.figure(figsize=(18, 18))

plt.plot(data['diff'])
plt.title('Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Revenue')
plt.grid(alpha=0.9)

plt.plot(data['seasonal_diff'])
plt.title('Seasonal Differencing')
plt.xlabel('Year')
plt.ylabel('Seasonal Differenced Revenue')
plt.grid(alpha=0.9)

plt.plot(data['log'])
plt.title('Log Transform')
plt.xlabel('Year')
plt.ylabel('Log Revenue')
plt.grid(alpha=0.9)
```

## OUTPUT

### REGULAR DIFFERENCING
<img width="694" height="496" alt="image" src="https://github.com/user-attachments/assets/d35c0aed-fe00-40be-9878-c28157922896" />

### SEASONAL ADJUSTMENT
<img width="699" height="493" alt="image" src="https://github.com/user-attachments/assets/70656fb2-bebf-4887-8d25-84986af4d11a" />

### LOG TRANSFORMATION
<img width="699" height="508" alt="image" src="https://github.com/user-attachments/assets/d7046250-6287-4919-9a07-e5df147ecb9b" />

## RESULT:
Thus, we have successfully created the Python code for the conversion of non-stationary Apple revenue data into stationary form using differencing, seasonal adjustment, and log transformation.
