# Pump-it-Up-Data-Mining-the-Water-Table

Project git repository [here](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/).

## Data Cleaning  

The data has several null values, missing values, and redundant characteristics columns. This project has two major challenges: cleaning data and dealing with extremely imbalanced target labels.

Initially, attempted to tackle a cleaning challenge. Some columns that had the same information were removed. Null, incorrect, and missing data were converted to mean, median, or unknown. Some values in features have been gathered and classified.

Under the heading data cleaning it contains detailed data cleaning methods under the headings of important columns. It is mentioned how and why the column was cleaned.

First, I go over each column one by one to see what they're about and what they imply.

        Features
                
        amount_tsh - Amount of water to pump
        date_recorded - Date of data insertion
        funder - Who founded the well
        gps_height - Altitude of the well
        installer - Organization that installed it
        longitude - GPS coordinates
        latitude - GPS coordinates
        wpt_name - Pump name (if it has one)
        num_private - Number
        basin - Geographic basin
        subvillage - Geographical location
        region - Geographic location
        region_code - Geographic location (in code)
        district_code - Geographic location (in code)
        lga - Geographical location
        ward - Geographical location
        population - Population by the well
        public_meeting - True / False
        recorded_by - Group entering this data
        scheme_management - Who manages the pump
        scheme_name - Who runs the pump
        permit - Whether the pump is allowed or not
        construction_year - Year of construction of the pump
        extraction_type - Pump extraction type
        extraction_type_group - Pump extraction type
        extraction_type_class - Pump extraction type
        management - How the pump is managed
        management_group - How the pump is managed
        payment - Cost of water
        payment_type - Cost of water
        water_quality - Water quality
        quality_group - Water quality
        quantity - Amount of water
        quantity_group - Amount of water
        source - Water source
        source_type - Water source
        source_class - Water source
        waterpoint_type - Pump type
        waterpoint_type_group - Pump type
        
        Labels
        
        functional - The pump works and does not need to be repaired
        functional needs repair - Works, but needs repair
        non functional - The water pump does not work

*  When I looked at the data distribution, I saw that there are a lot of missing values for the min values of the variables. This refers to the presence of missing values that must be filled in before the models may be used again. I eliminated a couple of them because the aim is unaffected by repeated or similar values, and decreasing the data makes our models quicker to execute. Some of the missing data can be filled up with the mean values.

   ![image1](https://user-images.githubusercontent.com/47825369/133795127-4feee396-d7cf-441b-8b51-a68150831592.JPG)

* The training set contains 59400 observation records  and 41 columns.The label for each pump is displayed in the column **status group**, while the other 40 variables correspond to the attributes, 10 of which are numerical and the rest are categorical.
'id', 'amount_tsh', 'gps_height', 'longitude', 'latitude', 'num_private', 'region_code', 'district_code', 'population', 'construction_year' are numeric values others are categorical values.

* The train data set is labeled as 
          functional - 32259
          non functional - 22824 
          functional needs repair - 4317. 
          So Given data has highly imbalanced target values.
          
* It means that we can start to estimate the 54.31% probability that any one pump in this database will work fine (that is, it is *functional*).This will be used to make future predictions.

* Due to the discrete nature of the target variable, a supervised classification technique must be used, which can be performed after data preprocessing and feature engineering.

* Some columns have data that is comparable and similar meaning. As a result, I must choose the best candidate for model training. I'll go over each column individually.

### scheme_management / management / management_group columns

   * These scheme management and management columns contain nearly identical information. Because "scheme management" refers to who manages the water station, "management" refers to how it is run. I'd rather keep the 'management' column because the 'scheme management' field has 3877 null entries. In the column 'management group,' similar information on how the water point is managed is maintained..

  ![image2](https://user-images.githubusercontent.com/47825369/133795223-b9440cb3-a9e0-4fcf-95d6-28ba618f395e.JPG) 
  
   * I checked the 'user-group' values to locate the subgroups of the 'management_ group' column and discovered that this column is simply the grouped version of 'management'. Despite the fact that the 'management' column includes more detailed information, I choose to remove the 'management group' column. I also categorized it below and saw the numbers of sub-groups to recall and check the sub-groups of the 'management_group' column (management column)
    
  ![image3](https://user-images.githubusercontent.com/47825369/133795316-c30ff2d6-871e-415c-bad3-2679e2577f0b.JPG)

### quantity / quantity_group columns

   * Because these two columns contain the identical data, I decided to remove the 'quantity_group' column..
    
   ![image4](https://user-images.githubusercontent.com/47825369/133799558-e57649d9-9f29-472f-8f8b-5633648703e9.JPG)
   
   ![image5](https://user-images.githubusercontent.com/47825369/133799661-3aebc0a6-3cbe-4cf2-902c-d8d7323aca01.JPG)

   * It is clear that, despite the presence of sufficient water, some wells are non-functional. Dry quantity water points have a strong correlation with non-functionality in this graph. There's a good likelihood the water point is non-functional if it's dry or unknown. If the quantity is enough, however, there is a better probability of finding functional water points.
    
### source / source_type / source_class columns

   * It is self-evident that the information in these three columns is identical. As a result, I've opted to maintain only the 'source' column because it has more detailed information, and I'll omit the others.
    
   ![image6](https://user-images.githubusercontent.com/47825369/133801780-a2305af5-c064-4d50-afdf-88e1f8d3c7bb.JPG)
   
   ![image7](https://user-images.githubusercontent.com/47825369/133801820-f5f5b249-0a28-4984-82e2-e4929834e933.JPG)

   * There is a lot of non-functional ground water when I look at the columns. It's also interesting to note that the functional and non-functional waterpoints for machine dbh and swallow well sources are nearly identical..
    
### water_quality / quality_group columns
        
   * I'll maintain 'water_quality' and drop 'quality_group' because the 'water_quality' column has more unique values.
   
   ![image9](https://user-images.githubusercontent.com/47825369/133802539-804b4f6c-63bb-45b6-a3cc-3c8698692c00.JPG)

   * It can be seen from the graph that many non-functional water sites have soft, good water quality.
     
### payment / payment_type columns
    
   * Because these two columns are identical, I chose to remove one of them.
    
   ![image10](https://user-images.githubusercontent.com/47825369/133802591-74d3888f-777b-46dd-a69f-b2fcbec81f1e.JPG)

   * This feature shows us what the water cost. Mostly, there are lots of non-functioal water points as never paid for them. Repair needed pumps are commonly in never paid category.
    
### extraction_type / extraction_type_group / extraction_type_class columns

   * It is clear that the information in these three columns is identical. As a result, I choose to keep 'extraction_type_group' and remove the others. Although extraction type has more unique values than extraction type group, according to this large dataset, some of these values are quite small. I prefered to use more compact one. Furthermore, extraction_type_class column contains less information. As a result, extraction_type_group has been chosen to be kept.
    
   ![extractiontype](https://user-images.githubusercontent.com/47825369/133803627-578dbf98-0a41-427e-8a33-512f071bba73.JPG)

   * Other and mono extraction kinds, in particular, have a larger chance of being non-functional than functional..
    
### waterpoint_type / waterpoint_type_group columns

   * Despite the fact that both have the identical information, I choose to maintain 'waterpoint_type' because it contains more data.
    
   ![waterpoint](https://user-images.githubusercontent.com/47825369/133803713-628fadc0-4fc2-4151-991f-a286f542f90f.JPG)

   * It can be seen that waterpoint type has correlation with functionality of water points. As a result, communal standpipes have a higher chance of being functional, while communal standpipe multiple and others have a higher chance of being non-functional.
    
### construction_year column
    
   * The dataset now includes a new feature. For future encoding, the year values are changed to decades. The missing values are represented as zero. Because it contains the bulk of the data, it will not be converted to the mean or median and will be retained as a new value for decades.
   
   ![image](https://user-images.githubusercontent.com/46936272/132955254-60247de8-bb7a-42ab-acff-a009220dee01.png)
    
   ![construction year](https://user-images.githubusercontent.com/47825369/133803929-81456050-3f66-4d03-bb30-a35394b3ec4e.JPG)

   * It is clear that missing values and that recent years have shown an increase in the number of functional water points.

### recorded_by column

   ![image](https://user-images.githubusercontent.com/46936272/132998302-5d689438-bdb8-467f-8c7e-c9e3746fd2c1.png)

   * There is only one value in the 'recorded_ by' column. Our model will not receive any information as a result of this. As a result, I also dropped it.

### installer column

   * There are lots of NaN and 0 values in this column. Firstly, I will convert them to unknown and change the spell mistakes in the data. 
    
   * It is interesting that most of water points which central government and district council installed are non-functional. DWE has the majority of functional wells but has also many non-functional wells.
   
   ![installer](https://user-images.githubusercontent.com/47825369/133804126-1fb865bd-cd90-4374-ac1c-7ee62f6af0c7.JPG)

### funder column

   * This is a highly categorized column with thousands of possible values. So, for future encoding, I'll use the 20 most common values.

   ![funder](https://user-images.githubusercontent.com/47825369/133804177-f14e5491-4761-4d0b-8d35-5d67d24ccbeb.JPG)
   
   * From the plots, I realize that most of the water points which funded by government are non-functional.

### longitude,latitude column

   ![long](https://user-images.githubusercontent.com/47825369/133805135-aaecff70-21ce-4fba-b9f0-85373de93959.JPG)

   * When the longitude is unknown, it is evident that it is written as 0. Because the zero points in the graph above outliers and outside of Tanzania are plainly seen. As a result, I converted them to mean, where the median is nearly the same number.

### wpt_name / scheme_name / id/ region/ region_code columns

   * When I checked the wpt_name, scheme_name and id columns, they do not have any information about functionality. So, I decide to drop them. I dropped also region_code column because region column gives more information about the region. Also, before dropping columns i check the dublicated values in dataframe.

   ![image](https://user-images.githubusercontent.com/46936272/132956871-58c2fb27-3e13-4192-bad6-1e9ffe49b6ac.png)

   ![region](https://user-images.githubusercontent.com/47825369/133805248-58cc4bfb-8944-4c42-bf13-216770043806.JPG)

   * Some areas have a better chance of having a functional water well. Between the basins of Klimanjaro and Arusha is the Pangani basin, which has a higher water point. They also have larger parts for functional wells, as can be seen.

### amount_tsh column

   ![image](https://user-images.githubusercontent.com/46936272/132998248-65e08ed1-1ccc-42f7-8008-68c6283e532e.png)

   * I decided to drop this column because 70% of the column has no informative values. So, this column will not give idea to the model and i will drop it.

### gps_height column

   ![image](https://user-images.githubusercontent.com/46936272/132956978-4752da50-4a80-429e-98e9-1baec4b2d6f6.png)

   * The level of the water point from sea level is shown by the GPS height. I don't modify this column because there are 34% zero values, but maybe 34% of the water spots are at sea level.

### population column

   ![image](https://user-images.githubusercontent.com/46936272/132977514-fab8e831-e843-4554-adc4-abd4f628b0de.png)

   * Some functional water points has zero population, it is weird so I will change zero population to mean.
    
   * To see the most populated areas water point functionality , i choose crowded 50 values and did groupby. It shows that higher population areas have more functional water points.

### date_recorded column

   * Between 2011 and 2013, approximately 95% of the water points were reported. As a result, I do not believe it contains necessary functionality information at this time. For the time being, I'm going to drop this column.

### num_private column

   * This column has no information about it and also mostly have zero values. So, i drop this also.

### basin column

   ![basin](https://user-images.githubusercontent.com/47825369/133805302-c624a381-5218-40ec-8ecf-413b59e6e892.JPG)

   * This column gives an idea about there is correlation between functionality and geographical water basin.

### subvillage column

   * This column has location value of water point regions but i already have region column. I will drop this, because it is hard to handle this nunique object values.

### district_code column

   ![district code](https://user-images.githubusercontent.com/47825369/133805353-560f35bd-ed40-470a-a44f-1170610e7e42.JPG)

   * It includes numeric values about districts. Each district has one number.
 
### lga / ward columns

   * Now I decided to  drop this column. Because, there are also other location features .

### public_meeting column

   * There are some null values and I convert them to most common data.

### permit column

   * This column indicates whether or not the water point is permitted. This column contains 3056 null values. I'll switch them to true, which has a higher value.

   * I chose to alter the target value to a numerical number before feeding the data into the model after this Columnwise analysis.

   ![image](https://user-images.githubusercontent.com/46936272/132957171-57a76a9d-ae04-420a-a844-8775661aef2f.png)

 
 
## Feature Engineering Proposal

   -  In the funder and installer columns, there are a number of category values. I have added new columns that are gathered as 'others' if the value in the feature is not in the first common 20 values.
   -  Furthermore, there are several spelling errors in these columns, resulting in new unique values in these fields. I have identified the top 100 most frequent installers and corrected them. After that, I have created a new column with classified values.
   -  The construction years are in integer format, but they aren't continuous data, and the year values aren't appropriate for the model. As a result, I have split them into decades and assigned a category value to each decade.


### Data Preprocessing  

   * Before start the the process I have imported nesssary tools such as libraries and data for the project.

   ![image](https://user-images.githubusercontent.com/46936272/133043808-51f868d3-7f32-4482-9a04-53cc1fefebc4.png)

### Descriptive statistics

   ![image](https://user-images.githubusercontent.com/46936272/133043910-8e5e4d82-bfc1-4edf-b883-35d6766f2cd1.png)

   * I examine the data distribution using these tables. I notice that the min of the feature variables has multiple missing values. This refers to the existence of missing values that must be addressed before moving forward with the models.

   * There are 59400 records in the training set, with 41 columns/features. The column status group displays the label for each pump, while the remaining 40 variables correspond to the attributes, with 10 being numeric and the rest being category. I'll start by looking into the numerical ones.

Since our target variable is discrete, I will need a **supervised classification algorithm**, which I will apply later.

### Extraction of similar variables

As I mentioned previously, I need to handle similar variables in the dataset to get better model.

### The following attributes

    - (extraction_type, extraction_type_group, extraction_type_class),
    - (water_quality, quality_group),
    - (waterpoint_type, waterpoint_type_group)
    - (scheme_name, scheme_management)
    - (source, source_class),
    - (subvillage, region, region_code, district_code, lga, ward),
    - (payment, payment_type),

   * they provide very similar information, which indicates that there is a high correlation between them. By leaving them, would risk an overfitting.
   * What's more:

       - num_private consists of 99% zeros and does not have a clear description, so we cannot interpret it
       - wpt_name is not very informative as it has fewer values than the number of observations

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

## Modelling 
 
I got good results with Random Forest Classifier with suitable format to three-class target.
I have used models with Random Forest and XGBoost. 
I mostly care about balanced accuracy on test set. Because competition metric for success in ternary classification problem is balanced accuracy.

|Accuracy| Random Forest| XGBoost|
|:---|:---|:---|
|**Train accuracy**|0.9632010339081046|0.8917117300955685|
|**Test accuracy**|0.835016835016835|0.8249158249158249|
|**Balanced Train accuracy**|0.9178927855359819|0.7930168611874482|
|**Balanced Test accuracy**|0.6951889733951102|0.6884408871966059|

While submitting the result obtain from the above model in [Data Driven - Pump it up competition](https://www.drivendata.org/competitions/7/pump-it-up-data-mining-the-water-table/page/23/) I have obtained the following accuracy 
 
|Model| Accuracy| 
|:---|:---|
|**Random Forest**|0.8227|
|**XGBoost**|0.8086|



