# Tradingview-Pinescript

This google sheet is meant to convert a basket of stocks into pinescript syntax in order to create a custom indicator for Tradingview software which can track the peformance of a basket of up to 40 stocks. This is useful when trading baskets of stocks because seeing the performance of the entire basket charted out can provide a unique perspective to a trader who is trading more than one stock. We can put the price action of the basket into greater context, looking at things such as ATR and other standard deviation moves in order to determine trends or outsized moves that are ripe for mean reversion. Unfortunataley tradingview does not provide a default method to view an entire basket of stocks that exceeds 10 symbols on their charts, so  creating this custom indicator is the next best thing.

Here is a link to our google sheet:

https://docs.google.com/spreadsheets/d/1JykWh2U27KEBGeGrsSs7nlftnLkPb0Vfyv0BdFlT_yQ/edit?usp=sharing

Here is a screenshot of the sheet in its entirety:

![Screenshot 2024-11-08 160314](https://github.com/user-attachments/assets/e75435c4-6247-4a57-984d-31ef1c97ec0b)


Our sheet begins with Cell A4 which is our capital allocation cell. It simply says how much money we want to allocate to each stock symbol and is the basis for much of our calculations throughout the sheet. Here is a screenshot of that part of the sheet:

![Screenshot 2024-11-08 160331](https://github.com/user-attachments/assets/38305ff2-01c8-4f59-87c0-7d1173345455)


Our longs and shorts are entered in columns D and H respectively. From there, calculations for the number of shares per stock symbol occurr in columns B for longs and F for the shorts. In the case of our longs as an example, the formula we use looks like this:
=round($A$4/GOOGLEFINANCE(D2,"closeyest"), 0). 

Column C and E are then automatically filled with "*" and "+" respectively for the longs, and the same occurs in columns G and I for the shorts. This is to create a sequence of cell values which can then be concatenated into tradingview syntax, which occurs in Column J. Here is a screenshot of what that looks like in our sheet:

![Screenshot 2024-11-08 160347](https://github.com/user-attachments/assets/1d702ff6-4d22-49b9-9c3e-6dca2855b806)


The syntax we use for this can be demonstrated in Row 2 of column J, where we see our formula =CONCATENATE(D2," ", "= request.security(symbol='",D2,"',timeframe=timeframe.period,expression=close)"). 

In this example, MNST is the stock symbol that appears in column D, and this creates a string of text that reads as 
"MNST = request.security(symbol='MNST',timeframe=timeframe.period,expression=close)" This demonstrates the conversion into Pinescript syntax, which can then be applied to tradingview's pinescrtipt editor and used to create a custom indicator. 

In addition to this, in column K, row 30 we have a further concatenation which is also necessary to our pinescript syntax necessary to create our custom indicator in tradingview. The formula is =CONCATENATE("plot((",B2:E21,")-(",F2:I21,"))"). Rows 32 and 34 of column K provide further syntax conversions using concatenate to allow us to break down our custome indicators by strictly longs or short baskets only. Here is a screenshot of what that looks like: 

![Screenshot 2024-11-08 160400](https://github.com/user-attachments/assets/fed8611a-7098-4318-8c20-023fdd1c629d)

In summary, this sheet allows a user to copy and paste stock symbols of their choice into the sheet, which then automatically converts their stock selection into pinescript syntax, ready to be copied and pasted into Tradingview's pinescript editor to create a custom indicator that can track the performance of a basket of stocks via a chart that is displayed within Tradingview itself. The process is easy enough to make quick work of this task and allow a trader to make this essential task part of their daily routine. 





