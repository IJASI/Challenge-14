
#  machine_learning_trading_bot 


Increasing or decreasing the training window and increasing or decreasing of the SMA windows affects the amount of returns. As you shorten the periods it seems that the returns are greater. Please refer to imigae files below. 



## Usage Examples 

DateOffset(months=5)

Using the .plot and .loc functionalities we can select a specific date and show a graph for the desired dates. 
```python

# Set the short window and long window
short_window = 5
long_window = 60

# Generate the fast and slow simple moving averages (4 and 100 days, respectively)
signals_df['SMA_Fast'] = signals_df['close'].rolling(window=short_window).mean()
signals_df['SMA_Slow'] = signals_df['close'].rolling(window=long_window).mean()

signals_df = signals_df.dropna()

# Review the DataFrame
display(signals_df.head())
display(signals_df.tail())
```

![Actual vs strategy increasing the training window 5 month offset - SMA SW 5 LW 60](/Images/Learning1.PNG)

```python

# Set the short window and long window
short_window = 8
long_window = 90

# Generate the fast and slow simple moving averages (4 and 100 days, respectively)
signals_df['SMA_Fast'] = signals_df['close'].rolling(window=short_window).mean()
signals_df['SMA_Slow'] = signals_df['close'].rolling(window=long_window).mean()

signals_df = signals_df.dropna()

# Review the DataFrame
display(signals_df.head())
display(signals_df.tail())
```

![Actual vs strategy increasing the training window 8 month offset - SMA SW 8 LW 90](/Images/Learning2.PNG)



##Results using AdaBoost

```python
# Select the start of the training period
training_begin = X.index.min()

# Display the training begin date
print(training_begin)

# Select the ending period for the training data with an offset of 3 months
training_end = X.index.min() + DateOffset(months=8)

# Display the training end date
print(training_end)

# Generate the X_train and y_train DataFrames
Xabc_train = X.loc[training_begin:training_end]
yabc_train = y.loc[training_begin:training_end]

# Review the X_train DataFrame
Xabc_train.head()

# Generate the X_test and y_test DataFrames
Xabc_test = X.loc[training_end+DateOffset(hours=1):]
yabc_test = y.loc[training_end+DateOffset(hours=1):]

# Review the X_test DataFrame
Xabc_train.head()

# Scale the features DataFrames

# Create a StandardScaler instance
scaler = StandardScaler()

# Apply the scaler model to fit the X-train data
Xabc_scaler = scaler.fit(Xabc_train)

# Transform the X_train and X_test DataFrames using the X_scaler
Xabc_train_scaled = Xabc_scaler.transform(Xabc_train)
Xabc_test_scaled = Xabc_scaler.transform(Xabc_test)
```



![Actual vs strategy increasing the training window 5 month offset - SMA SW 5 LW 60](/Images/Learning3.PNG)




 



