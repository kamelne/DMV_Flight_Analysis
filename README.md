# DMV Airport Efficiency Final Project

## Reasoning For Our Project:

As we approach post-pandemic normalcy, we can agree that a vacation (for whatever reason) is long overdue. Making up for lost time, especially while traveling, is something truly important to us. Once we've completed this project, we can use this information to plan trips and share with others outside of academia. Working with our large dataset is also allowing us to use what we've learned thoughout our class to practice real world situations. The findings from our project can help both airports and airlines improve flight efficiency by identifying delays and their reasons.

## Overview: 
For our project we are looking at the efficiency of local DC, Maryland, and Virginia (DMV) Airports for outbound domestic flights. Specifically we will be pulling data across Baltimore Washington International (BWI), Dulles International Airport (IAD), and Ronald Reagan Washington National Airport (DCA) from January 2018 through March 2022. Destinations were seperated by region; NorthEast, SouthEast, MidWest, SouthWest, West. Our group used multiple data points to determine the best run airport. We looked at the day of the week, month and year of flight information. The operating airline, scheduled take off time and actual departure, just to name a few. There are 5 delay categories that we agreed best represented our analysis: Carrier, Late Aircraft, National Aviation System, Weather, and Security. 


![Screen Shot 2022-07-06 at 4 41 07 PM](https://user-images.githubusercontent.com/99618784/182042461-9c97e970-bb0a-418e-9ea5-781c20bec000.png)

## Presentation 
[Presentation](https://docs.google.com/presentation/d/1YszyuInGDuC_et4G8m_60k3zDEPiCfOyu6jOvvO_-Hg/edit#slide=id.gf47a8fbfff_1_0)

[Tableau Dashboard](https://public.tableau.com/shared/NST8W37XT?:display_count=n&:origin=viz_share_link)

## Data Source:

We worked with a couple websites to pull data for our project. The United States Department of Transportation provided statistics on avaiation data that we filtered through to grab specific inputs for our analysis. The National Oceanic and Atomspheric Administration provided daily weather summaries used in our analysis as well, as it coincideds with delays.

[Bureau of Transportation Statistics (BTS)](https://www.transtats.bts.gov/DL_SelectFields.aspx?gnoyr_VQ=FGK&QO_fu146_anzr=b0-gvzr)

* year/month/day of week
* flight date
* Operated_or_Branded_Code_Share_Partners
* Origin
* Dest
* DestStateName
* Crsdeptime
* Deptime
* Depdelay
* Departure delay groups
* Dep time block
* Cancelled
* Diverted
* Carrier delay
* Weather delay
* Nas delay
* Security delay
* Lateaircraft delay

[National Oceanic and Atmospheric Administration (NOAA)](https://www.ncdc.noaa.gov/cdo-web/datasets)

* WSF2 - Fastest 2-minute wind speed
* WSF5 - Fastest 5-second wind speed
* SNOW - Snowfall
* WT03 - Thunder
* WT04 - Ice pellets, sleet, snow pellets, or small hail"
* PRCP - Precipitation
* WT05 - Hail (may include small hail)
* TOBS - Temperature at the time of observation
* WT06 - Glaze or rime
* WT08 - Smoke or haze
* SNWD - Snow depth
* WT09 - Blowing or drifting snow
* WDF2 - Direction of fastest 2-minute wind
* AWND - Average wind speed
* WDF5 - Direction of fastest 5-second wind
* PGTM - Peak gust time
* WT11 - High or damaging winds
* WT01 - Fog, ice fog, or freezing fog (may include heavy fog)
* TMAX - Maximum temperature
* WESD - Water equivalent of snow on the ground
* WT02 - Heavy fog or heaving freezing fog (not always distinguished from fog)
* TAVG - Average Temperature.
* TMIN - Minimum temperature

### Link to data files on AWS:

[Data](data_files.md)

## Description of the Data Exploration Phase:

We began our data exploration with researching online sources of all flights in the U.S. Initially, we started combing through Kaggle and found information but it was limited. To provide an accurate analysis on our selected DMV airports, we needed to find enough avaiaton data for pre-covid, peak covid, post-covid years. To validate our future findings, we considered bringing in general unemployement, Hotel/AirBnB, and pricing data. Ultimately, we decided against pulling inputs from said subjects due to not seeing a direct connection to the questions we want answered. The United States Department of Transportation website proved to be a dependable source for the 3 airports we are preforming our analysis on. The National Oceanic and Atomspheric Administration provided a weather summary that we wanted for our project as well. 

![bts dexterproject](https://user-images.githubusercontent.com/99618784/179411577-4f4184a2-d491-4d2f-aca9-9f6726e91548.PNG)



## Description of the Analysis Phase: 

The information that was provided from our trusted sources had millions of data points. After importing our csv file in Jupyter Notebook, we created a dataframe using Pandas to work with our large dataset. While working with different data types it was necessary to identify what each column was for the analysis going forward. Afterwards we created a seperate dataframe for each airport using the following code:

![dataframe dpcd](https://user-images.githubusercontent.com/99618784/180104535-ed617892-2a0a-49bd-9761-721e36803d32.PNG)

We filled state abreviations with state names and orgainzed each state by region. Our analysis is specifically looking at outbound domestic flights so we simplified the destination to regions, to include Puerto Rico and the U.S Virgin Islands as non-continental regions. Hawaii and Alaska are included as part of the Western region. In order to do so, we had to create a loop that would run through each dataframe and drop the state abreviation column and only show the full state name:

![loop dpcd](https://user-images.githubusercontent.com/99618784/180104416-6be151bb-936e-498b-9fe3-859f15c2988c.PNG)

We checked counts of each flight per year for each airport, origination flights, destination flights per state and null values. Creating our outputs, the delay output column was determined by a flight having a late depature of 15 minutes or longer. Since we are also factoring pre-covid and covid effects, we created a column to define them: 0 being the output for pre-covid and 1 being present times.

![delayoutput dpcd](https://user-images.githubusercontent.com/99618784/180105787-36b6cde1-aaa1-4d84-91e4-5efb0b16abc8.PNG)
![covid dpcd](https://user-images.githubusercontent.com/99618784/180107934-67754b35-208e-46e4-8f45-f2bfc1bab610.PNG)


Satisfied with our dataset, we arranged our flight delay reasoning column to: weather, carrier, late aircraft delay(LAS), security, and national air system(NAS).

* Air Carrier: The cause of the cancellation or delay was due to circumstances within the airline's control (e.g. maintenance or crew problems, aircraft cleaning, baggage loading, fueling, etc.).

* Extreme Weather: Significant meteorological conditions (actual or forecasted) that, in the judgment of the carrier, delays or prevents the operation of a flight such as tornado, blizzard or hurricane.

* National Aviation System (NAS): Delays and cancellations attributable to the national aviation system that refer to a broad set of conditions, such as non-extreme weather conditions, airport operations, heavy traffic volume, and air traffic control.

* Late-arriving aircraft: A previous flight with same aircraft arrived late, causing the present flight to depart late.

* Security: Delays or cancellations caused by evacuation of a terminal or concourse, re-boarding of aircraft because of security breach, inoperative screening equipment and/or long lines in excess of 29 minutes at screening areas.

![delayreason dpcd](https://user-images.githubusercontent.com/99618784/180107458-a4ce4994-a031-4dbe-a96a-d5ca7dbfcd45.PNG)

We repeated the process for the BWI and DCA dataframes. After running a summary on our IAD dataframe, we liked what we saw and continue to lookover our data. 

![iaddataframe dpcd](https://user-images.githubusercontent.com/99618784/180108482-0e8bbd93-af23-4227-88e5-9cb336c34441.PNG)


## Questions We Hoped To Answer and What we did Answer: 
Our main question -which Airport has been most efficient through the volatility of the past 3 years? That being said, we will be looking at what factors make up the answer.

* What month/day of the week is the best? Does month/day of the week matter?
  * From our analysis we learned that flying out on a Saturday is the best day of the week for all 3 airports. Saturday proved to be the day of the week with the least number of delays. Each airport had similar patterns where delays dropped Tuesdays and Wednesdays from Sunday, increased Fridays, and dropped to their lowest on Saturdays. We also found that April was the best month to fly with the least amount of delays and August is the worst with the most delays. These are the trends we found over the course of 4 years from our data. 
* Which airlines preformed the best? Which airline has the most delays over the years?
  * We broke this down by airport, each airline preformed differently. If flying out of IAD, the best airline is Delta and the worst being Allegiant followed closely by Jetblue. DCA shows Hawaiian and Delta Airlines as the best and Jetblue as the worst. Delta Airlines is the best for BWI and Allgiant is the worst for delayed flights.
* How does weather affect delays?
  * Weather is a cause for delay but its not as impactful as we originally thought. Out of our top 5 reasoning for delays it was consistently in the last 2 if not the bottom affect. 
* Does origin airport affect delay?
  * BWI data has shown us that of the 3 airports, it has the most delays. 

### Database:

![Database ERD first draft](https://user-images.githubusercontent.com/99618784/178156404-6ebea7fa-4b84-4da8-b44f-9de8016d30ee.png)

### Machine Learning Model
#### Preprocessing 
First, we had to implement the countries to a higher level of categories (5 U.S Region). 
We also converted the categorical data (Airport, Airline, etc.) into dummy/indicator variables. 
We are dropping the same columns for every model because they overlap with our target variable (DELAYED). The columns that we are dropping are: 
* DATE 
* DEP_TIME
* DEP_DELAY_GROUP
* DEST_STATE_NM
* DEST
* DEP_DELAY
* LATE_AIRCRAFT_DELAY
* CARRIER_DELAY
* WEATHER_DELAY
* SECURITY_DELAY
* NAS_DELAY
* DELAY_REASON
* CRS_DEP_TIME

#### Processing 
* _We separated the feature (x) from the target (y)_ : Our target is “delayed,” while the rest of the columns are our features that might influence the chances of a flight being delayed 
* _Training and Test_ : The y-test value in the logistic regression model has 222,493 on-time flights and 47,885 delayed flights.
* _Scaling_ : Since our X values feature different values, we want to avoid large numbers that can disproportionately impact the model.

#### Insights on Our Machine Learning Models 
* After pre-processing and processing our data, we decided to run our data through 4 different machine learning models: Logistic Regression, Decision Tree, Random Forest, and Neural Network. Below is a file with insights on each model. 

[ML_insights.md](https://github.com/camilabatres/dexter_project/blob/main/ML_insights.md)

#### Comparing All The Models 
![image](https://user-images.githubusercontent.com/100107588/182040092-9f93d890-f130-4f7f-b8c9-677ad2ddb87a.png)
* Accuarcy - All the models have similar accuracy score between the 0.82-0.83 range. Therefore, we need to use other indicators to find out which one is the best model for our data. 
* Precision - The model with the highest precision score is the Logistic Regression. The Neural Network is very close to the Logistic Regression score. The other two models are in the .40s.
* Sensitivity - The Random Forest and Decision Tree models' sensitivity scores are in the .20s. Logistic Regression and Neural Network have way lower scores, close to 0. 

##### Choosing Model 
* We believe the Decision Tree is a better performing model with higher precision and sensitivity.
* Even though Decision Tree has the lowest precision score out of all the models, it has the highest sensitivity score. In this situation, sensitivity is more important than the precision. 
  * False positives can be ruled out by double checking the flight status. It is more important to detect delayed flights.  
  * There is no penalty on misclassifying flights 
* Advantages: 
  * Decision Tree Model is very intuitive and easy to explain to stakeholders
* Disadvantages: 
  * A small change in the data can cause a large change in the structure 
 
 ##### Further Model
 After we decided on the decision tree we went further and incorporated the weather data to see how the model changes. 

 #### Preprocessing 
First, we had use the station ID to add an Origin column to aid in joining the dataframe with the flight data. Columns from the weather data we chose to use for our model are :
* DATE
* ORIGIN
* AWND
* SNOW
* WT03
* PRCP
* TMAX
* TMIN

The weather data only went back to 2019 so the flight data was filtered to exclude the 2018 data. The dataframes were then merges on  date and origin:

![Capture3](https://user-images.githubusercontent.com/57120024/182505305-203a817f-2625-4b9a-9c67-266fb78d562e.PNG)

#### Processing 
The processing step was the same as before


#### Insights on the Decision Tree with Weather Data

When the weather data was added the results were similar accuracy, precision, and sensitivity. The issue we believe the model is now skewd by the weather data. When looking at feature importance, you can see of the top 5 features 3 come from the weather data. We do not belive this is a good model beacuse of this skew.

![Capture](https://user-images.githubusercontent.com/57120024/182505594-5d29b53e-2922-453a-af3f-6913ade06ba6.PNG)

![Capture2](https://user-images.githubusercontent.com/57120024/182505600-543461f9-0944-4a12-870f-ef035a7d8a30.PNG)

Looking forward we belive the next steps would be is to find data for each airport on othe other delay categories, Carrier delay, Nas delay, Security delay, Lateaircraft delay. Incorporate them into the decision tree model and add approtiate weights to each. 

## Dashboard

As we create our dashboard in Tableau, our data begins to tell a story. When booking a flight, one of the first choices you have to make is "When are you traveling". You will also have to decide which airline you'll chose to reach your destination. Wanting to make the most of your time away and spending it at an airport because of a delay is not in the plans. If your wondering what causes these delays, your first thought may be weather and its not even in the top 3. Our dashboard will go over those categories in more depth. These visuals of validating efficiency for our local airports are what we look forward to presenting to our stakeholders.

Total Flights vs. Delays:

![Dashboard 9](https://user-images.githubusercontent.com/99618784/182963242-01a9ec6c-4767-4bee-8537-b3834bad1bb8.png)


While looking at the images below you may notice that Thursdays and Fridays, for outbound domestic flights, are more likely to be delayed out of BWI and DCA over any other day in the week. IAD holds the lowest amount of delayed flights overall for our DMV airports. We would also like to point out that Saturdays are the best days to fly out with a less likely hood for delays. 

![Delays By Weekday (1)](https://user-images.githubusercontent.com/99618784/182730980-4b5cc5b4-1999-4ed3-84cb-45f6b5e3924b.png)

While weather conditions do cause delays, it may surprise you that its not nearly as impactful as a Carrier, Late Aircraft, or NAS delay. These factors are more on the logistical side of running an airport. 

![Airport Delay Reasons](https://user-images.githubusercontent.com/99618784/182731372-8e0bb95b-7e68-4968-a36e-12c565751de3.png)



<img width="1374" alt="Carrier Accountability for Delays by Airport" src="https://user-images.githubusercontent.com/95712234/182051501-8eb532c5-3170-4f16-91fb-6b5fbaf3fbca.png">

The following interactive visual on Tableau shows the daily flight delays for the 3 DMV airports for each year. Here you can view the results for the year 2021:

BWI (2021):

<img width="1388" alt="Delayed Flights by Day per Airport (BWI - 2021)" src="https://user-images.githubusercontent.com/95712234/182051955-b505056e-b680-4680-b661-297546588e2e.png">

DCA (2021):

<img width="1370" alt="Delayed Flights by Day per Airport (DCA - 2021)" src="https://user-images.githubusercontent.com/95712234/182052015-29f49adf-6a0c-49d7-9620-cbda9d1c00ae.png">

IAD (2021):

<img width="1372" alt="Delayed Flights by Day per Airport (IAD - 2021)" src="https://user-images.githubusercontent.com/95712234/182052077-9105f7ba-c8fc-4b95-ac00-19e390ff12f3.png">

## Recommendations and Summary:

To summarize our conclusions, if you’re going to plan a trip within the U.S. and if your local to northern Virginia-Avoid flying out on Thursdays or Fridays, departing from BWI in August. If you’re wanting to make the most of your time away. Fly out on a Saturday, out of DULLES AIRPORT, IN APRIL. The best day to fly out of the year is January 26th and the Worst is August 13th. With that being said Hopefully no one has a trip coming up next week. The highest delay reasoning for BWI was due to circumstances within the carrier like crew problems, fueling or baggage loading. DCA was due to Late Aircrafts which is what it sounds like, A previous flight with same aircraft arrived late, causing the present flight to depart late. IADs highest delay reasoning were due to the National Aviation System such as non-extreme weather conditions, heavy traffic volume, airport operations. As a reminder Dulles is an international airport and our data is only for domestic flights. We recommend Delta airlines and strongly suggest against Jetblue. They recently acquired Spirit Airlines so do with that information what you will. 

### Technology

The technolgies we will be using can be seen [here](technology.md)
