# How-to-make-Time-Series-Predictions-with-Alteryx-Tableau-and-R

# Method 1 : Prediction in Tableau Desktop. 


# Method 2 : Prediction in Tableau connected to RServe. 


# Method 3 : Prediction in Alteryx connected to Tableau. 

```
Step 1 : Arima Times Series in Alteryx 
-Alteryx has two Time Series models ARIMA and ETS 
-In/Out-Input Data : Bookings Data from 2002 tà 2011 (monthly report)
-Connection with Time Series ARIMA: Write the model name 'ARIMA',
-Select the target field 'Bookings', Target Field Frequency 'Monthly'. 
-Connection with Time Series ARIMA : Other options select 6 months, week format US. 
-Connection "O Output" of ARIMA with Time Series TS Forecast. 
-Select the confidence interval 80% ans 95%. 
-Run the Alteryx File (green arrow) to obtain the bookings forecasts for the 6 next months. 
```

```
Step 2: Create the TDE with the forecast Predictions. 

-Connection "O Output" of TD Forecast with In/out-Output Data 
-Give a name to the .tde. 
-In File Format : select Tableau Data Extract(*.tde)
-Output Options : Create New Extract File
-Run the Alteryx File tro generate the TDE File (native Tableau file). 
-Another Solution : Connection "O Output" of TD Forecast with Tableau/Output Tableau Workbook. 
```

```
Step 3: Create the Dashboard in Tableau Dektop

-Open the TDE file with Tableau Desktop and create the dashboard twbx. 
-You can visualize the forecast for the next 6 months, the confidence intervals. 
```


