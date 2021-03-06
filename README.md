# All Stocks Analysis

## Overview of Project

### Purpose

The code for reviewing the history of 12 stocks across two separate years (2017 and 2018) was running successfully. The target moving forward was refactoring the code to run more efficiently and to have a better backbone to refactor for future purposes depending on the size of the data to be observed.
 
## Results

### 2017 Results

11 of 12 stocks being considered yielded a positive return with 9 of them yielding a return that was at least in the double digits. 2017 was indeed a year for growth with these assets. The code used to initially perform the analysis was refactored to yield performance/efficiency of ~80% as seen below.

![2017 Returns](./Resources/Results_2017.png)

Original Code to Perform Analysis

![Original Code to Perform Analysis](./Resources/Old_2017.png)

Refactored Code to Perform Analysis

![Refactored Code to Perform Analysis](./Resources/VBA_Challenge_2017.png)

### 2018 Results

10 of 12 stocks being considered yielded a negative return with 6 of them yielding a return that was at least in the double digits in the negative. 2018 was indeed a year for negative returns for a majority of these assets. The code used to initially perform the analysis was refactored to yield performance/efficiency of ~80% as seen below.

![2018 Returns](./Resources/Results_2018.png)
<sub>ENPH stood to continue to yield positive returns with a decrease from 129.5% to 81.9% between 2017 and 2018.

<sub>RUN not only yielded a positive return both years, but its return increased significantly from 5.5% to 84.0% between 2017 to 2018.

Original Code to Perform Analysis

![Original Code to Perform Analysis](./Resources/Old_2018.png)

Refactored Code to Perform Analysis

![Refactored Code to Perform Analysis](./Resources/VBA_Challenge_2018.png)

### Optimized Analysis Code

	Sub AllStocksAnalysisRefactored()    Dim startTime As Single    Dim endTime  As Single    yearValue = InputBox("What year would you like to run the analysis on?")    startTime = Timer        'Format the output sheet on All Stocks Analysis worksheet    Worksheets("All Stocks Analysis").Activate        Range("A1").Value = "All Stocks (" + yearValue + ")"        'Create a header row    Cells(3, 1).Value = "Ticker"    Cells(3, 2).Value = "Total Daily Volume"    Cells(3, 3).Value = "Return"    'Initialize array of all tickers    Dim tickers(12) As String        tickers(0) = "AY"    tickers(1) = "CSIQ"    tickers(2) = "DQ"    tickers(3) = "ENPH"    tickers(4) = "FSLR"    tickers(5) = "HASI"    tickers(6) = "JKS"    tickers(7) = "RUN"    tickers(8) = "SEDG"    tickers(9) = "SPWR"    tickers(10) = "TERP"    tickers(11) = "VSLR"        'Activate data worksheet    Worksheets(yearValue).Activate        'Get the number of rows to loop over    RowCount = Cells(Rows.Count, "A").End(xlUp).Row        '1a) Create a ticker Index            tickerIndex = 0            '1b) Create three output arrays        Dim tickerVolumes(12) As Long    Dim tickerStartingPrices(12) As Single    Dim tickerEndingPrices(12) As Single            ''2a) Create a for loop to initialize the tickerVolumes to zero.        For i = 0 To 11                tickerVolumes(i) = 0            Next i                ''2b) Loop over all the rows in the spreadsheet.        For i = 2 To RowCount            '3a) Increase volume for current ticker        tickerVolumes(tickerIndex) = tickerVolumes(tickerIndex) + Cells(i, 8).Value                        '3b) Check if the current row is the first row with the selected tickerIndex.        'If  Then                    If Cells(i - 1, 1).Value <> tickers(tickerIndex) Then                tickerStartingPrices(tickerIndex) = Cells(i, 6).Value                                'End If                    End If                '3c) check if the current row is the last row with the selected ticker         'If the next row???s ticker doesn???t match, increase the tickerIndex.        'If  Then                        If Cells(i + 1, 1).Value <> tickers(tickerIndex) Then                tickerEndingPrices(tickerIndex) = Cells(i, 6).Value            '3d Increase the tickerIndex.                        tickerIndex = tickerIndex + 1                    'End If                End If        Next i        '4) Loop through your arrays to output the Ticker, Total Daily Volume, and Return.    For i = 0 To 11                'Be sure activate the sheet where the output is meant to be displayed        Worksheets("All Stocks Analysis").Activate                'for the ticker display, volume display, and return:populate the appointed column based on each row that is governed by the ticker        Cells(4 + i, 1).Value = tickers(i)        Cells(4 + i, 2).Value = tickerVolumes(i)        Cells(4 + i, 3).Value = (tickerEndingPrices(i) / tickerStartingPrices(i)) - 1                    Next i        'Formatting    Worksheets("All Stocks Analysis").Activate    Range("A3:C3").Font.FontStyle = "Bold"    Range("A3:C3").Borders(xlEdgeBottom).LineStyle = xlContinuous    Range("B4:B15").NumberFormat = "#,##0"    Range("C4:C15").NumberFormat = "0.0%"    Columns("B").AutoFit    dataRowStart = 4    dataRowEnd = 15    For i = dataRowStart To dataRowEnd                If Cells(i, 3) > 0 Then                        Cells(i, 3).Interior.Color = vbGreen                    Else                    Cells(i, 3).Interior.Color = vbRed                    End If            Next i     endTime = Timer    MsgBox "This code ran in " & (endTime - startTime) & " seconds for the year " & (yearValue)	End Sub

## Summary

### Advantages/Disadvantages to Refactoring Code
When considering to refactor code, there's a cost benefit analysis that's performed. Making the code more efficient/cleaner can help to speed up the processing speed and to have a code that is easier to modify for future use with similar datasets, but at what cost? How long or tedious will it be to perform the refactoring? Weighing these factors, among others, will determine if it's advantageous to spend the resources to making adjustments to the code.

Pertaining to the VBA code refactored in this project, the code has been enhanced that sped up processing time (immaterial for this dataset, but more viable for larger datasets). The base for this code adds simplicity to being used for similar analysis projects by being able to easily accounts for different variables, for datasets that are laid out differently, and performing additional loops.

