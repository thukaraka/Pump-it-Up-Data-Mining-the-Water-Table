# Pump-it-Up-Data-Mining-the-Water-Table

## Data Cleaning  

### Cleaning

The data has several null values, missing values, and redundant characteristics columns. This project has two major challenges: cleaning data and dealing with extremely imbalanced target labels.

Initially, attempted to tackle a cleaning challenge. Some columns that had the same information were removed. Null, incorrect, and missing data were converted to mean, median, or unknown. Some values in features have been gathered and classified.

Under the heading data cleaning it contains detailed data cleaning methods under the headings of important columns. It is mentioned how and why the column was cleaned.

### Explorations

  -  In general, higher population regions have a greater number of functional wells.
  -  Some places have a better probablity of finding clean water, especially if they are close to good basins.
  -  Darul es Salaam is one of the most populous towns in Tanzania, but 35% of good water quality sites are non-functional.
  -  Iringa is an important area, although it has several non-functional water sites with soft water.
  -  The majority of government-funded wells are non-functional.
  -  The majority of the water points installed by the central government and district council are non-functional.
  -  Gravity is the most common extraction method, but hand pumps are a close second. Handpumps have a lower efficiency than commercial pumps. It demonstrates that authorities must focus on pumping type. There are numerous non-functional water points that belong to gravity (which is a natural force, so there is no need to do anything expensive) as an extraction type.
  -  Some water points with enough and soft water  are non-functional.
  -  Wells installed in recent years are more functional than earlier ones. And it has been observed that in recent years, several functional but needs of repair wells. It indicates that if they are not repaired soon, they will become non-functional.
  -  There are a number of water wells that have enough water but aren't functional.

### Findings 
 
  -  Although 4272 wells were dry, the water quality was good. They can be functional if a remedy is found to restore the source of these wells. Finding clean water sources is not the only issue; maintaining the ability to feed these sources is also critical.
  -  2226 (7%) wells have adequate and soft water; however, they need to be repaired. Authorities must spend money on repairs. Otherwise, these will be non-functional.
Although 8035 (27%) of the wells have adequate good quality water, they are non-functional. This demonstrates the need for authorities to collaborate and invest in technology to pump these good resources.
  -  Authorities should check repeat the wells they funded.
  -  To feed dry wells and repair wells, new techniques must be developed.

### Feature Engineering

  -  In the funder and installer columns, there are a number of category values. I have added new columns that are gathered as 'others' if the value in the feature is not in the first common 20 values.
  -  Furthermore, there are several spelling errors in these columns, resulting in new unique values in these fields. I have identified the top 100 most frequent installers and corrected them. After that, I have created a new column with classified values.
  -  The construction years are in integer format, but they aren't continuous data, and the year values aren't appropriate for the model. As a result, I have split them into decades and assigned a category value to each decade.

 ## Modelling 
 
We got good results with Random Forest Classifier with suitable format to three-class target.
I have used models with Random Forest and XGBoost. 
I mostly care about balanced accuracy on test set. Because competition metric for success in ternary classification problem is balanced accuracy.

|Accuracy| Random Forest| XGBoost|
|:---|:---|:---|
|**Train accuracy**|0.9632010339081046|0.8917117300955685|
|**Test accuracy**|0.835016835016835|0.8249158249158249|
|**Balanced Train accuracy**|0.9178927855359819|0.7930168611874482|
|**Balanced Test accuracy**|0.6951889733951102|0.6884408871966059|

While submitting the result obtain from the above model in [Data Driven - Pump it up comoetition](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/) I have obtained the following accuracy 
 
|Model| Accuracy| 
|:---|:---|
|**Random Forest**|0.8227|
|**XGBoost**|0.8086|



