# Tibber-API-Hubitat

Driver for Tibber API quater prices.

The driver fetches price info from Tibber API once an hour (refresh command), calculates day average price, low/high price and stores the data.
Every quater it updates the current price from the stored data and sets the child devices according to the current price.

Low/high prices.
The spread between the highest and lowest price of the day is calculated and is then multiplied with the factor set in the settings. The result is added to the lowest price and is used as a threshold for low prices. (For high prices it is subtracted from the highest price.)
Example:
Factor is set to 10%
Highest price is 120
Lowest price is 20
The spread is 120-20 = 100 * 10% = 10

Low price threshold = 20 + 10 = 30. Every hour with a price equal to or lower to 30 will be concidered as low price-hour. Stored in attribute lowPrice.
High price threshold = 120 - 10 = 110. Every hour with a price equal to or higher than 110 will be concidered as high price-hour. Stored in attribute highPrice.

The device has four child devices:
- Tibber_lowPrice - turns on when price is equal to or lower than lowPrice.
- Tibber_highPrice - turns on when price is equal to or higher than highPrice.
- Tibber_belowAvg - turns on when price is lower than or equal to day average price. (todayAvg)
- Tibber_aboveAvg - turns on when price is higher than day average price.
