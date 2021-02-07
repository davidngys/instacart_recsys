# Instacart Recommender System
---

## Preamble
..placeholder..

---

## Contents
* [1. Problem Statement](#chapter1)
    * [1.1 Context & Motivation](#chapter1_1)
    * [1.2 Primary & Secondary Stakeholders](#chapter1_2)
    * [1.3 Business Problem Statement](#chapter1_3)
    * [1.4 Educational Problem Statement](#chapter1_4)
* [2. Data Dictionary](#chapter2)
    * [2.1 Main Trap Data](#chapter2_1)
    * [2.2 Spray Data](#chapter2_2)
    * [2.3 Weather Data](#chapter2_2)
* [3. Executive Summary](#chapter3)
    * [3.1 Context & Initial Assumptions](#chapter3_1)
    * [3.2 Data Science Process](#chapter3_2)
    * [3.3 Key Findings](#chapter3_3)
* [4. Recommendations & Conclusion](#chapter4)
    * [4.1 Addressing Business Problem](#chapter4_1)
    * [4.2 Addressing Education Problem](#chapter4_2)
* [5. Limitations](#chapter5)
    * [5.1 Data Collection](#chapter5_1)
    * [5.2 Spray Effectiveness](#chapter5_2)
    * [5.3 Cost Benefit Analysis Assumptions](#chapter5_3)
* [6. Further Opportunities](#chapter6)
* [7. Citations](#chapter7)

## 1. Problem Statement <a class="anchor" id="chapter1"></a>

### 1.1 Context & Motivation <a class="anchor" id="chapter1_1"></a>
placeholder


### 1.2 Primary & Secondary Stakeholders <a class="anchor" id="chapter1_2"></a>
|Type|Stakeholders|Value Proposition|Problem Type|
|:--|:--|:--|:--|
|Primary||- <br />- ||
|Secondary||- <br />- ||

### 1.3 Business Problem Statement <a class="anchor" id="chapter1_3"></a>
placeholder.

### 1.4 Educational Problem Statement <a class="anchor" id="chapter1_4"></a>
placeholder.

## 2. Data Dictionary <a class="anchor" id="chapter2"></a>
placeholder.

### 2.1 Main Trap Data <a class="anchor" id="chapter2_1"></a>
|Column|Data Type|Train/Test|Description|
|:--|:--|:--|:--|
|`Id`|int64|Test|Index of row|
|`Date`|object|Train/Test|Date of WNV test|
|`Address`|object|Train/Test|Approximate location of trap (sent to GeoCoder)|
|`Species`|object|Train/Test|Species of mosquito|
|`Block`|int64|Train/Test|Block number of address|
|`Street`|object|Train/Test|Street name|
|`Trap`|object|Train/Test|Id of the trap|
|`AddressNumberAndStreet`|object|Train/Test|Approximate address (returned from GeoCoder)|
|`Latitude`|float64|Train/Test|Latitude (returned from GeoCoder)|
|`Longitude`|float64|Train/Test|Longitude (returned from GeoCoder)|
|`AddressAccuracy`|int64|Train/Test|Accuracy score (returned from GeoCoder)|
|`NumMosquitos`|int64|Train|Number of mosquitos caught in the trap|
|`WnvPresent`|int64|Train|1 for WNV present, 0 for no WNV|

### 2.2 Spray Data <a class="anchor" id="chapter2_2"></a>
|Column|Data Type|Description|
|:--|:--|:--|
|`Date`|object|Date of spray|
|`Time`|object|Time of spray|
|`Latitude`|float64|Latitude of the location of the spray|
|`Longitude`|float64|Longitude of the location of the spray|

### 2.3 Weather Data <a class="anchor" id="chapter2_3"></a>
|Column|Data Type|Description|
|:--|:--|:--|
|`Station`|integer|Id number of the weather station|
|`Date`|object|Date of the weather report|
|`Tmax`|integer|Maximum temperature of the day|
|`Tmin`|integer|Minimum temperature of the day|
|`Tavg`|object|Average temperature of the day|
|`Depart`|object|Difference from the normal temperature|
|`DewPoint`|integer|Average dew point|
|`WetBulb`|object|Average wet bulb|
|`Heat`|object|Temperature degrees above base 65F|
|`Cool`|object|Temperature degrees below base 65F|
|`Sunrise`|object|Calculated sunrise|
|`Sunset`|object|Calculated sunset|
|`CodeSum`|object|Encoded weather pheomena|
|`Depth`|object|Snow/ice on the ground in inches|
|`Water1`|object|Water equivalent of Depth|
|`SnowFall`|object|Snowfall in inches and tenths|
|`PrecipTotal`|object|Water equivalent in inches and hundredths/rainfall and melted snow|
|`StnPressure`|object|Average station pressure|
|`SeaLevel`|object|Average sea level pressure|
|`ResultSpeed`|float|Resultant wind speed|
|`ResultDir`|integer|Resultant wind direction|
|`AvgSpeed`|object|Average wind speed|

## 3. Executive Summary <a class="anchor" id="chapter3"></a>

### 3.1 Context & Initial Assumptions <a class="anchor" id="chapter3_1"></a>
placeholder

### 3.2 Data Science Process <a class="anchor" id="chapter3_2"></a>
The target is to predict the presence of the virus, which is a binary classification problem. Classification models will be explored.

1. [Data Cleaning](./code/01_data_cleaning.ipynb)
 - Introduction and Problem Statement
 - Exploring the Data
 - Data Processing
2. [Exploratory Data Analysis](./code/02_eda.ipynb)
 - WNV Distribution
 - Correlation
 - Species
 - WNV/Mosquito Seasonality
 - Traps/Mosquitos Distribution
 - Weather Trends
 - Spray Analysis
 - Location Analysis
 - EDA Conclustion and Takeaway
 - Data Processing for Model
3. [Model Selection and Evaluation](./code/03_model_selection.ipynb)
 - Modeling Strategy
 - Data Preparation
 - Establishing Baseline
 - Fit and Evaluate Models
 - Kaggle Submissions
 - Cost Benefit Analysis
 - Key Takeaways and Recommendations
 
### 3.3 Key Findings <a class="anchor" id="chapter3_3"></a>

#### 3.3.1 Data Cleaning
The data collected is evaluated to be sufficient and appropriate in developing a model to predict the presence of WNV as:
- Location details such as latitude and longitude are found in the main data set, with the corresponding labels of WNV positivity in the train data set.
- Spray data list the locations of where sprays has been conducted and can be used to evaluate the effectiveness of sprays. However, it should not be used as a prediction feature as sprays are a measure to be used in areas that are predicted to have high possibilities of the presence of WNV.
- Weather data provides insights to the effect of weather conditions on the spread of WNV. Certain conditions may prove to be more favourable in the spread of the virus and will be useful as prediction features.
- Only 774 points of data were marked as having a spray within the last 14 days in a 5 mile radius
- Weather data used will be `Tvg`, `TotalPrecip`, `DewPoint`, and a enginerred `R_Humid` datapoint, which computes the relative humidity based on precipitation and dewpoint
- Weather data will also be rolled based on 7 days to observe the effect of past weather on a data collection point in the main data

#### 3.3.2 Exploratory Data Analysis
- Unbalanced distribution of classes (~95% for no virus and 5% for virus)
- Virus only found to be in 2 species, Culex Pipiens and Culex Restuans
![species](./assets/species_dist.png)
- Mosquito numbers seem to be seasonal and spikes in around Aug, similar to trends of the WNV virus. However, this is expected as the higher the number of mosquitos within a trap, the more likely to detect the virus
- Seasonality of mosquitos and virus seems to follow trend of weather, which peaks in virus. However, no significant trends can be ovserved with the relative humidity.
![weather](./assets/weather_trends.png)
- Some traps are more heavily sampled then others, with the top location at the O'Hare International Airport
- No conclusive results can be drawn from the spray data regarding the effectiveness of sprays, due to limited data of sprays
- Areas with presence of the virus tend to be clustered near each other. This is also following our expectation as mosquitos tend to have a flight radius of about 3 miles.
![map](./assets/map_plot.png)

#### 3.3.3 Model Selection and Evaluation
- Baseline of vanilla `Logistic Regression` model returned ROC AUC score of 0.77
- From cross validation, `Bagged Trees`, `Random Forests` and `Adaboost` performed the best
- However, `Decision Trees` had the least false negatives
- After tuning hyperparameters, model that had the best ROC AUC score is `Random Forests`, with `Bagged Trees` producing the least false negatives
- When tested on unseen data, `Random Forests` performed the best with ROC AUC score of 0.72, followed by `Bagged Trees` at 0.70
- However, based on values in confusion matrix, `Bagged Trees` had the best cost benefit analysis
![results](./assets/opt_model.png)

## 4. Recommendations & Conclusion <a class="anchor" id="chapter4"></a>

### 4.1 Addressing Business Problem <a class="anchor" id="chapter4_1"></a>
**Optimising Resources to Curb WNV Spread**
Typically, Type 1 errors (False Positives) are evaluated as worse than Type 2 errors (False Negatives)
- False Positives: Predicted as has WNV but actually has no WNV
- False Negatives: Predicted as no WNV but actually has WNV

Based on the model, sprays will be conducted at all areas predicted as positive but no sprays at locations predicted as negatives. Therefore, a False Negative area would not be sprayed, giving rise to the mosquitos having higher opportunities to spread WNV. Areas which are False Positives would have been sprayed even though they do not have presence of the virus. This still effectively drives down the population of mosquitos which are seen as pests and provides societal benefits. 

Therefore, even though `Random Forests` provides the best ROC AUC score as a prediction model, `Bagged Trees` is the best model to optimise use of resources in curbing the virus.

### 4.2 Addressing Education Problem <a class="anchor" id="chapter4_2"></a>
In our EDA, it has been discovered that mosquito populations typically peak during hot seasons in Jul and Aug. However, there are no conclusive insights into the effect of relative humidity. This could be due to the nature of the data, which only spans from May to Oct of each year. Limited data on the effect of sprays also do not provide any insights into their effectiveness. It is also observed that the presence of the virus only exists within 2 of the species. This information could be useful to investigate if the virus is only capable of spreading through these 2 species of mosquitos in order to develop more measures to curb the virus.

## 5. Limitations <a class="anchor" id="chapter5"></a>
### 5.1 Data Collection <a class="anchor" id="chapter5_1"></a>
The main data that is collected only spans from May to Oct of each year. Furthermore, it was discovered that certain traps were more heavily sampled compared to other traps. This could lead to certain biases being formed when analysing the data. We recommend to collect further data throughout the year if possible and also create a more even distribution of samples of traps to gain further insight into prediction methods and possible trends of the virus.

### 5.2 Spray Effectiveness <a class="anchor" id="chapter5_2"></a>
Spray data is currently limited, and no conclusive results can be drawn on the effectiveness of sprays. We recommend to collect further data to analyse the effect on sprays on the control of mosquito populations and virus trends.

### 5.3 Cost Benefit Analysis Assumptions <a class="anchor" id="chapter5_3"></a>
Certain assumptions were taken based on available data to compute the cost benefit analysis. If other methods are developed that can effectively help to control the spread of the virus, the assumptions should be re-evaluated in order to decide on the best classification models that help optimise cost.

## 6. Further Opportunities <a class="anchor" id="chapter6"></a>
- Explore using time series models to predict, given observed seasonal trends of mosquito populations and the presence of the virus
- Further evaluate effectivenes of sprays in order to determine best practices with regards to curbing mosquito populations (how many consecutive days, optimal time of day etc.)

## 7. Citations <a class="anchor" id="chapter7"></a>
Information on Aerial Spraying | West Nile Virus | CDC. (n.d.). CDC. https://www.cdc.gov/westnile/vectorcontrol/aerial-spraying.html#:%7E:text=Spraying%20larvicides%20kills%20mosquito%20larvae,permanently%20get%20rid%20of%20them

mosquito.org. (n.d.). Mosquito.Org. https://www.mosquito.org/page/faq#How%20fast%20can%20mosquitoes%20fly?

Lee, B. Y. (2018, September 24). West Nile Virus: How Climate Change May Be Contributing To Its Spread. Forbes. https://www.forbes.com/sites/brucelee/2018/09/16/west-nile-virus-how-climate-change-may-be-contributing-to-its-spread/?sh=797f29e93784

Climate of Chicago - Description, Illinois State Climatologist Office, Illinois State Water Survey, U of I. (n.d.). State Climatologist Office for Illinois. https://www.isws.illinois.edu/statecli/general/chicago-climate-narrative.htm#:%7E:text=Chicago’s%20climate%20is%20typically%20continental,to%20be%20the%20most%20pleasant

City to Spray Insecticide Thursday to Kill Mosquitoes. (2020). CDPH. https://www.chicago.gov/city/en/depts/cdph/provdrs/healthy_communities/news/2020/august/city-to-spray-insecticide-thursday-to-kill-mosquitoes.html

Wikipedia contributors. (2020, December 19). Dew point. Wikipedia. https://en.wikipedia.org/wiki/Dew_point

Zenivex E4 (etofenprox) | Central Mass Mosquito Control Project. (n.d.). Central Mass Mosquito Control Project. https://www.cmmcp.org/pesticide-information/pages/zenivex-e4-etofenprox

Economic Cost Analysis of West Nile Virus Outbreak, Sacramento County, California, USA, 2005. (2010, March 1). PubMed Central (PMC). https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3322011/#R6

Final Cumulative Maps and Data | West Nile Virus | CDC. (n.d.). CDC. https://www.cdc.gov/westnile/statsmaps/cumMapsData.html