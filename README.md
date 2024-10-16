# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
#Import necessary libraries\
import numpy as np\
import pandas as pd\
import matplotlib.pyplot as plt\
import warnings\
from statsmodels.tsa.holtwinters import ExponentialSmoothing

#Suppress warnings\
warnings.filterwarnings('ignore')

#Read the yearly EV data from a CSV file\
file_path = 'ev.csv'  # Replace with the correct file path\
data = pd.read_csv(file_path)

#Focus on 'year' and 'value' columns\
data = data[['year', 'value']]

#Display the shape and the first 20 rows of the dataset\
print("Shape of the dataset:", data.shape)\
print("First 20 rows of the dataset:")\
print(data.head(20))

#Set 'year' as the index\
data.set_index('year', inplace=True)

#Plot Transform Dataset (Original Value Data)\
plt.figure(figsize=(12, 6))\
plt.plot(data['value'], label='Original Value Data', color='blue')\
plt.title('Transform Dataset (Original Value)')\
plt.xlabel('Year')\
plt.ylabel('Value')\
plt.legend()\
plt.grid()\
plt.show()

#Moving Average\
#Perform rolling average transformation with a window size of 3 (or adjust as needed)\
rolling_mean_3 = data['value'].rolling(window=3).mean()

#Plot Moving Average\
plt.figure(figsize=(12, 6))\
plt.plot(data['value'], label='Original Value Data', color='blue')\
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')\
plt.title('Moving Average of Value')\
plt.xlabel('Year')\
plt.ylabel('Value')\
plt.legend()\
plt.grid()\
plt.show()

#Exponential Smoothing\
model = ExponentialSmoothing(data['value'], trend='add', seasonal=None)\
model_fit = model.fit()

#Make predictions for the next 5 periods (adjust as needed)\
future_steps = 5\
predictions = model_fit.predict(start=len(data), end=len(data) + future_steps - 1)

#Create a future index for the predicted years\
future_years = pd.Series(range(data.index[-1] + 1, data.index[-1] + future_steps + 1))

#Plot the original data and Exponential Smoothing predictions\
plt.figure(figsize=(12, 6))\
plt.plot(data['value'], label='Original Value Data', color='blue')\
plt.plot(future_years, predictions, label='Exponential Smoothing Forecast', color='orange')\
plt.title('Exponential Smoothing Predictions for Value')\
plt.xlabel('Year')\
plt.ylabel('Value')\
plt.legend()\
plt.xticks(rotation=45)\
plt.grid(True)\
plt.tight_layout()\
plt.show()

### OUTPUT:

Moving Average

![Screenshot 2024-10-16 105106](https://github.com/user-attachments/assets/b61be0f6-8a77-4775-a486-e1c792bb87c8)

Plot Transform Dataset
![Screenshot 2024-10-16 105039](https://github.com/user-attachments/assets/3e6eef51-eefe-4449-8d0d-e52a0c179749)

Exponential Smoothing

![Screenshot 2024-10-16 105032](https://github.com/user-attachments/assets/eb88e020-31dc-401f-b2ec-451fb504c896)

### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
