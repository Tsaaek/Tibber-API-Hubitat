# Tibber-API-Hubitat

Driver for controlling devices based on the current quarter-hour electricity price from the Tibber API
By default, the driver fetches price data from the Tibber API once a day (via the refresh command), calculates the day’s average price and low/high thresholds, and stores the data in the device. You can manually trigger this update at any time using the refresh command.
At the start of every quarter-hour, the driver retrieves the current price from the stored data and updates the child devices according to the price and calculated thresholds.

Getting the code

Copy the code.
Log in to Hubitat and create a new driver (Drivers Code → New Driver).
Paste the code and click Save.


Creating the device

Create a new virtual device (Devices → Add Device → Virtual Device).
Select Tibber quarter-hour prices.
Name the device (e.g., "Tibber").
Assign a room (optional).
View the device details.


Setting up the device

Go to Preferences.
Get your Access Token from Tibber Developer Settings and copy it.
Paste the token into the Tibber API-token field and press Save.
Return to Commands and press Refresh.

The device is now operational.

Child Devices
The driver creates four child devices that update based on the current price level:
Tibber_lowPrice - Activates when price ≤ lowPrice or ≤ fixedLowPrice.
Tibber_highPrice - Activates when price ≥ highPrice or ≥ fixedHighPrice.
Tibber_belowAvg - Activates when price ≤ today’s average (todayAvg).
Tibber_aboveAvg - Activates when price > today’s average.

Price Threshold Calculations
The driver dynamically calculates low/high thresholds using the day’s min/max prices and a factor (default: 10%). You can override these with fixed values.

Dynamic Thresholds
lowPrice:
Lowest price + ((Highest price – Lowest price) × Factor)
Example: 20 öre + ((120 öre – 20 öre) × 0.1) = 30 öre.
→ Any quarter-hour ≤ 30 öre is considered a low price.


highPrice:
Highest price – ((Highest price – Lowest price) × Factor)
Example: 120 öre – ((120 öre – 20 öre) × 0.1) = 110 öre.
→ Any quarter-hour ≥ 110 öre is considered a high price.


Fixed Thresholds (User-Defined)

fixedLowPrice: Always treated as a low price (regardless of dynamic calculation).
fixedHighPrice: Always treated as a high price.


Notes

You can adjust the factor, fixedLowPrice, or fixedHighPrice at any time.
After changes, the driver recalculates thresholds and updates values automatically.


