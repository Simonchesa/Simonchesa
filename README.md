- 👋 Hi, I’m @Simonchesa
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Simonchesa/Simonchesa is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
Here's a sample code in Python using the pandas library to generate buy and sell signals based on the highest and lowest prices:

```
import pandas as pd

# Define the dataframe
df = pd.DataFrame({
    'Price': [12.5, 13.2, 14.1, 13.8, 14.5, 15.2, 14.9, 14.2, 13.9, 13.5]
})

# Define the function to generate signals
def generate_signals(df):
    # Initialize signals
    signals = []
    
    # Iterate over the prices
    for i in range(len(df)):
        # If the current price is the highest, generate a sell signal
        if df['Price'][i] == max(df['Price'][:i+1]):
            signals.append('Sell')
        # If the current price is the lowest, generate a buy signal
        elif df['Price'][i] == min(df['Price'][:i+1]):
            signals.append('Buy')
        # Otherwise, no signal
        else:
            signals.append('None')
    
    return signals

# Generate signals
df['Signal'] = generate_signals(df)

# Print the dataframe
print(df)
```

This code will generate a dataframe with a "Signal" column that indicates whether to buy, sell, or do nothing based on the highest and lowest prices.

To incorporate the additional features you mentioned, you could modify the code as follows:

1. *Commodity or currency*: Add a column to the dataframe specifying the commodity or currency.
2. *Size of enter market*: Add a column specifying the size of the position to enter.
3. *Buy or sell order*: Modify the `generate_signals` function to generate both buy and sell signals, and add columns for the corresponding orders.
4. *Log by entering password and register number*: Add a login function that prompts the user for a password and register number before generating signals.
5. *Time to enter market and close orders*: Add a column specifying the time to enter and close orders.

Here's an updated version of the code:
```
import pandas as pd
import getpass

# Define the dataframe
df = pd.DataFrame({
    'Commodity': ['Gold', 'Gold', 'Gold', 'Gold', 'Gold', 'Gold', 'Gold', 'Gold', 'Gold', 'Gold'],
    'Price': [12.5, 13.2, 14.1, 13.8, 14.5, 15.2, 14.9, 14.2, 13.9, 13.5],
    'Size': [100, 100, 100, 100, 100, 100, 100, 100, 100, 100]
})

# Define the function to generate signals
def generate_signals(df):
    # Initialize signals
    signals = []
    buy_orders = []
    sell_orders = []
    close_orders = []
    
    # Iterate over the prices
    for i in range(len(df)):
        # If the current price is the highest, generate a sell signal
        if df['Price'][i] == max(df['Price'][:i+1]):
            signals.append('Sell')
            sell_orders.append(df['Size'][i])
            buy_orders.append(0)
            close_orders.append(df['Size'][i])
        # If the current price is the lowest, generate a buy signal
        elif df['Price'][i] == min(df['Price'][:i+1]):
            signals.append('Buy')
            buy_orders.append(df['Size'][i])
            sell_orders.append(0)
            close_orders.append(0)
        # Otherwise, no signal
        else:
            signals.append('None')
            buy_orders.append(0)
            sell_orders.append(0)
            close_orders.append(0)
    
    return signals, buy_orders, sell_orders, close_orders

# Login function
def login():
    password = getpass.getpass('Enter password: ')
    register_number = input('Enter register number: ')
    if password == 'your_password' and register_number == 'your_register_number':
        return True
    else:
        return False

# Main program
if login():
    df['Signal'], df['Buy Order'], df['Sell Order'], df['Close Order'] = generate_signals(df)
    print(df)
else:
    print('Invalid login credentials')
```
This code incorporates all the features you mentioned, but please note that it's a sample code and you should adjust it according to your specific needs and requirements.
