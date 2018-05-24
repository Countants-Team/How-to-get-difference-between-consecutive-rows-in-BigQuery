# How to  get difference between consecutive rows in BigQuery
#### This is the table:

 | Row No | Date | Values |
 | :---: | --- | --- |
 | 1 | 2012-10-30 | 10245 |
 | 2 | 2012-10-31 | 25416 |
 | 3 | 2012-11-01 | 84252 |
 | 4 | 2012-11-02 | 21454 |
 | 5 | 2012-11-03 | 54436 |
 | 6 | 2012-11-04 | 49364 |
 | 7 | 2012-11-05 | 42656 |
 
 
 #### This is the result we need:
 
 | Row No | Date | Values | Pre-Value | Diffrence |
 | :---: | --- | --- | --- | --- |
 | 1 | 2012-10-30 | 10245 | - |
 | 2 | 2012-10-31 | 25416 | 10245 | 15171 |
 | 3 | 2012-11-01 | 84252 | 25416 | 58836 |
 | 4 | 2012-11-02 | 21454 | 84252 | -62798 |
 | 5 | 2012-11-03 | 54436 | 21454 | 32982 |
 | 6 | 2012-11-04 | 49364 | 54436 | -5072 |
 | 7 | 2012-11-05 | 42656 | 49364 | -6708 |
 
 ## Syntax:-
 
 ##### Lag() over (order by )
 
 #### For Example:-
 
 ```
 Select 
Date,
Values ,
lag(Values) over (order by date) as Pre_value
From
[project.dataset.table]
 ```
 
 #### We get Output as :
 
 | Row No | Date | Values | Pre-Value |
 | :---: | --- | --- | --- |
 | 1 | 2012-10-30 | 10245 | - |
 | 2 | 2012-10-31 | 25416 | 10245 |
 | 3 | 2012-11-01 | 84252 | 25416 |
 | 4 | 2012-11-02 | 21454 | 84252 |
 | 5 | 2012-11-03 | 54436 | 21454 |
 | 6 | 2012-11-04 | 49364 | 54436 |
 | 7 | 2012-11-05 | 42656 | 49364 |
 
 
 #### Now we want to calculate diffrence:
 
 ```
 Select 
Date,
Values ,
lag(Values) over (order by date) as Pre_value,
(Values-Pre_values) as Difference
From
[project.dataset.table]
 ````
 #### we get final out-put as:
 
 | Row No | Date | Values | Pre-Value | Diffrence |
 | :---: | --- | --- | --- | --- |
 | 1 | 2012-10-30 | 10245 | - |
 | 2 | 2012-10-31 | 25416 | 10245 | 15171 |
 | 3 | 2012-11-01 | 84252 | 25416 | 58836 |
 | 4 | 2012-11-02 | 21454 | 84252 | -62798 |
 | 5 | 2012-11-03 | 54436 | 21454 | 32982 |
 | 6 | 2012-11-04 | 49364 | 54436 | -5072 |
 | 7 | 2012-11-05 | 42656 | 49364 | -6708 |
 
 
