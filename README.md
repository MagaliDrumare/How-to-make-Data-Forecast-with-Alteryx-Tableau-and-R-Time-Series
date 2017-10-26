# How-to-make-Time-Series-Predictions-with-Alteryx-Tableau-and-R

# Method 1 : Prediction in Tableau Desktop. 


# Method 2 : Prediction in Tableau connected to RServe. 
```
Step 1 : Install R on your computer : https://cran.r-project.org
-Open an R session : 
-install.packages("Rserve")
-library(Rserve)
-Rserve(args="--no-save")
-library forecast
-install.packages("forecast")
```
```
Step 2 : Open Tableau 
-Go to Help/ Parameters and Performance
-Manage External Service Connection 
-Choose localhost + OK 
-Then ‘Test Connection’
-Successfully connected to the RServe service must appear. 
```
```
Step 3: Create a Calculated Field : Forecast 
SCRIPT_REAL("
library(forecast);
myts <- ts(.arg1, start = c(1896), frequency = 1);
farima<- auto.arima(myts)
fcast <- forecast(farima, h=.arg2[1]);
n <- length(.arg1); 
append(.arg1[(.arg2[1]+1):n],fcast$mean, after = n-.arg2[1])", 
SUM([visits]), 
[Forecast Periods])
```
```
Step 4: Need to adjust the axis : Date New 
-Create Calculated field day : 31 [day ]
-Create Calculated field month : 12  [month ]
-Create Calculate field [Date]: MAKEDATE([year],[month ],[day ])
-Create Date New : DATEADD("year",[Forecast Periods],[Date])
In Column : Date New Continuous 
Rows : Forecast
```
```
Step 5 : Adjust the color : Separate Actual/Forecast Periods 
IF INDEX()<=SIZE()-[Forecast Periods]
Then"Actual" 
ELSE "Forecast"
END
```


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


