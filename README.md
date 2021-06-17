     Carlos López-Martínez, Ignacio Matías Montorfano, Elena Picazo Gurina, Adrià Valls Sánchez.

# Forecast Tourism in Barcelona 2021

For this project, we will do an exploratory analysis of the variables that affect tourism regulary and data from the COVID-19 pandemic. We will develop different predictive models to make a prediction on the number of tourists that arrive to Barcelona on 2020 (year of the pandemic). We will also compare our predictions with the real values.

Hipothesis: Will we obtain well trained models despite of the pandemic? If not, how do they perform with just COVID-19 data?

For this propourse, we will combine regression and time series analyses so as to help us understand the data behavior and if the COVID-19 pandemic situation "breaks" our predictive models.

We present different models: Simple linear regression, Multiple linear regression, Random Forest and SARIMA. We evaluate their monthly results using Seaborn visualization tools, Scikit-learn library, as well as other toolboxes.

This project is divided by these sections: collect information, merge it, clean it and try to build a well trained model from scratch.

### Sources and variables

We use different real datasets from different sources:
- INE
- AENA
- Ministerio de transporte de España
- OpenData Port Barcelona
- Google trends

**Variables**

All the variables that we collected from different sources are for Barcelona city, except for "Nº total de parados en España".

Variables that we use for our model:
- Mes: time variable from 2015-01 to 2021-04 (year-month)
- Aviones: number of flights coming to Barcelona-El Prat
- Pasajeros en Avion: number of flight passengers coming to Barcelona-El Prat
- Barcos de pasajeros:
- Indice busquedas: number of google search for "hotel Barcelona"
- Temperaturas: average temperature in Barcelona (degree Celsius?)
- Nº total de parados en España: number of unemployed people in Spain
- Total Viajeros Barcelona: number of foreign and spanish residents with at least one overnight stay in a hotel or tourist apartment in Barcelona
- Viajeros Residentes del Extranjero: number of foreign residents with at least one overnight stay in a hotel or tourist apartment in Barcelona
- Viajeros Residentes de España: number of spanish residents with at least one overnight stay in a hotel or tourist apartment in Barcelona
- Facturación: Average price for a night in a hotel in Barcelona.
- Facturación 5 estrellas: Average price for a night in a 5 stars hotel in Barcelona.
- Facturación 4 estrellas: Average price for a night in a 4 stars hotel in Barcelona.
- Facturación 3 estrellas: Average price for a night in a 3 stars hotel in Barcelona.
- Facturación 2 estrellas: Average price for a night in a 2 stars hotel in Barcelona.
- Facturación 1 estrellas: Average price for a night in a 1 star hotel in Spain.
- P. Medio Apartmento: Average price for a night in turistic apartment in Barcelona.
- P. Medio Rural: Average price for a night in a rural house.
- Pernoct. Españoles: Number of tourists from Spain in Barcelona.
- Pernoct. Extranjeros: Number of foreigner tourists in Barcelona.
- Pernoct. Total: Number of tourists in Barcelona.
- Estancia Españoles: Average stay of spanish tourist at hotel in Barcelona.
- Estancia Extranjeros: Average stay of foreigner tourist at hotel in Barcelona.
- Estancia Total: Average stay of tourist at hotel in Barcelona.
- Estancia Apartamentos: Average stay of tourist at apartments in Spain.
- Hoteles Abiertos: Number of open hotels in Barcelona.
- Habitaciones estimadas: Estimate number of available rooms at hotels in BCN.
- Plazas estimadas: Estimate number of available places at hotels in Barcelona.
- Ocupacion: Percentatge of ocupation in hotels in Barcelona.
- Ocupacion fin de semana: Percentatge of ocupation at the weekend in hotels in BCN.
Ocupacion habitación: Percentatge of rooms at hotels ocupated.
- Personal empleado: Number of workers intended to hotel sector.
COVID-19 data: Barcelona city or province?
- CASOS_CONFIRMAT: number of positive COVID-19 cases
- VACUNATS_DOSI_1: number of people vaccinated with first dosis
- VACUNATS_DOSI_2: number of people vaccinated with second dosis
- PCR: number of people who have taken a PCR test
- TAR: number of people who have taken a COVID-19 test different form PCR

## Gathering and Cleaning Data

**COVID-19 Data**

We contacted the Generalitat to get the main and more deagreggate information of the COVID-19 pandemic in Barcelona, such as confirmed cases, vaccinations, PCR's, etc. 

First, we upload the COVID-19 information from https://aquas.gencat.cat/ca/actualitat/ultimes-dades-coronavirus. This dataset contains information about COVID-19 infections, PCRs, vaccination, etc.

We will consider only the data refering to the city of Barcelona. The data are originally provided at a daily basis and higly dissagregated by: 

*   Sex: Male, Female
*   Age group: <15, 15-64, 65-74 >75
* General & Elderly residences COVID-19 cases
* "Area Integral de Salut": Barcelona Esquerra, Barcelona Litoral-Mar, Barcelona Dreta & Barcelona Nord

We create two additional aggregated databases, at weekly and monthly basis, to make them complatible with the following databases of tourist information. In addition we:

*   Agregate COV-19 cases by sex and age group
*   We remove COVID-19 cases in elderly residences, as they do not contribute to tourism in the city of Barcelona
* We remove COVID-19 cases of the "Area Integral de Salut Barcelona Nord" as this area is not contributuing much to the tourist activity in the city of Barcelona.

**Tourism Data**

The source for tourism data in Barcelona ("zona turística" Cataluña:Barcelona") is Instituto Nacional de Estadística (INE):
- For hotels: https://www.ine.es/dynt3/inebase/index.htm?padre=238&capsel=238
- For tourist apartaments: https://www.ine.es/dynt3/inebase/index.htm?padre=231&capsel=231

For rural apartaments and camping sites, there is no tourism data specifically for Barcelona. Therefore, we only consider information from travelers with at least one overnight stay in a hotel and tourist apartment in Barcelona.

**Transportation and others**

In this section we upload the main information about planes, cruises and others source of information that might help us understand the behaviour of the travelers like google trends and unemployment rate.

- Transportation:

     *   Passengers: https://ec.europa.eu/
     *   Planes and aircrafts: https://www.mitma.gob.es/aereo
     *   Cruises and ships: https://opendata.portdebarcelona.cat/

- Others

Other variables that might help us are Google Trends (a website by Google that analyzes the popularity of top search queries in Google Search across various regions and languages. The website uses graphs to compare the search volume of different queries over time), Barcelona's mean temperatures and the unemployment rate.

*   Google trends: https://trends.google.es/trends/
*   Mean temperatures: https://datosclima.es/Aemethistorico/Meteostation.php
*   Unemployment rate: https://www.epdata.es/

## Explanatory Analysis

### COVID-19 Data

COVID-19 is a disease with origin in China. It is a new virus linked to the same family of viruses as Severe Acute Respiratory Syndrome (SARS) and some types of common cold. 

This virus can be spread in many different ways. The rate of spread can easily increase  if people travel across countries for holidays, business trips, etc. That is why most of the countries took political decisions such as lockdowns and borders closing. And, therefore, the tourism industry has been one of the sectors hardest hit by COVID-19.

In this section we will look at how the disease has spread in Barcelona and the correlation between the spread, tourism and transportation data.

### Dependent Variable

Since we are under a forecasting task with time series data, we should expect patterns of seasonality and/or trends, especially for our tourism data. In facr, our dependent variable shows seasonality and trend patterns. It is reasonable to believe that "Viajeros_Tot" has a seasonality pattern because the number of visitors usually increase from spring to summer months. The positive trend might imply that Barcelona becomes more and more popular amongst tourists and, therefore, it receives every year an increase of visitors.

### Main Correlations

We create three different correlation matrices. We believe features do not influence our dependent variable in the same way with the presence of COVID-19 data. Moreover, we check the correlation between the variables to see if we should drop some of them.

## Models and Scenarios

All the different models try to forecast the number of visitors in Barcelona for 2020-2021.

**Simple Linear Regression**

Simple linear regression is a linear regression model with a single explanatory variable. That is, it concerns two-dimensional sample points with one independent variable and one dependent variable and finds a linear function (a non-vertical straight line) that, as accurately as possible, predicts the dependent variable values as a function of the independent variable. The adjective simple refers to the fact that the outcome variable is related to a single predictor.

We will try this model to understand the data behavior and after this, try other models and add more variables to it.

**Multiple Linear Regression**

The use of Multiple Linear Regression tries to exploit multiple variables that where included in the Database we generated to see their relation with the total number of travelers in Barcelona. First, we will consider a model for the Non COVID-19 period from 2105 to 2019, using from 2015 to 2017 as training and 2018 and 2019 as validation of the predicted model. We consider also the extension to a polynomial regresion algorithm of order 3.

**Random Forest**

In order to use Random Forest algorithm, we first convert our time series dataset to a matrix of pairs of input and output sequences. Once this transformation is done, we will be able under a supervised learning problem.

For this section, we decided to drop variables relating to whether tourist establishments are open or not ('HOTELES ABIERTOS', 'APARTAMENTOS DISPONIBLES'). The algorithm might interpret that these variables have a positive effect on "Viajeros_Tot". But, during lockdown periods, many tourist establishments were open but without any visitors. Therefore, it is appropiate to exclude them from the task.

**SARIMA**

A SARIMA model can be understood by outlining each of its components as follows:

*   Seasonality (S): represents the seasonality of the series.
*   Autoregression (AR): refers to a model that shows a changing variable that regresses on its own lagged, or prior, values.
*   Integrated (I): represents the differencing of raw observations to allow for the time series to become stationary (i.e., data values are replaced by the difference between the data values and the previous values).
*   Moving average (MA):  incorporates the dependency between an observation and a residual error from a moving average model applied to lagged observations.

Key points:
- SARIMA models predict future values based on past values.
- SARIMA makes use of lagged moving averages to smooth time series data.
- Autoregressive models implicitly assume that the future will resemble the past. Therefore, they can prove inaccurate under certain conditions, such as crisis or periods of rapid change.

## Conclusions

**Simple Linear Regression**

Linear regression attempts to fit a straight hyperplane to our dataset, in the period previous to pandemia, we have observed a increasing tendence every year and the prediction estimates the same for 2021, probably it would had not failed.

For a COVID-19 period, if we try to estimate the number of travelers by month the result is not correct due to a non-linear relationship, in order to avoid it, we estimate between years, despite being a straight relation due to a short size of dataset. This algorithm is no flexible enough to capture a complex pattern such number of travelers during COVID-19.

-------

**Multiple Linear Regression**

In the case of the multiple linear regression, or multivariate linear regression we consider first, a model for tourists using touristic data. Using training data from 2015 to 2017, we are able to estimate the dependent variable in 2018 and 2019. This model is able to estimate the visitors in the COVID-19 period as it is based on touristic data, which is affected by the pandemics.

In order to avoid this dependence, we propose a model based only on COVID-19 data for the COVID-19 period. In this particulr case we observe that this model is able to predict an increase in the number of visitors for the summer 2021. The prediction depends on how much training data from the non-COVID-19 period is considered. The larger this period, the higher the estimation in the number of visitors.

Consquently, the model need to see the decrease on the number of tourists at the beginning of 2020 in order to predict the increase for the summer 2021. The model predicts the increase on the number of tourists based on the number of vaccines.

-------

**Random Forest**

We decided to implement an ensemble decision tree algorithm because it does not require data to behave normal. In addition, it can handle many features at the same time. For instance, it did a pretty good job forecasting the values in 2018-2019, the model obtained an R-squared of 0.93 (without COVID-19 data) 

However, Random Forest algorithm doesn’t make accurate predictions for time frames outside of the training set nor with the presence of sparse features. On the one hand, the minimum value for the training set of the Random Forest model trained with no COVID-19 is 430539. And the maximum value of "Viajeros_Tot" during 2020-2021 is 238053. This means that this model would have never predicted a value as low as 238053 nor lower than that. 
On the other hand, the R-squared (0.54) of the model trained with COVID-19 data is low since it trained with sparse variables. For instance, features related to COVID-19 were all 0 for the time frame 2015-2019.

-------

**SARIMA**

As we can see, the ARIMA models are not embedded within any underlying structural relationships. As we only see how the only variable beheves during time.
ARIMA models are essentially ‘backward looking’ models. As such, they are generally poor at predicting turning points, unless the turning point represents a return to a long-run equilibrium (as we can clearly see in confidence interval in the "with COVID19 Data" model).

For using this model correctly we would need more data to predict how the tourism will stabilize in the near future.

-------

### Next Steps

Because we have a limited time to do this project, we propose some next stepts to extend this study or refine the models we already propose:

The main limitation for both SARIMA and Random Forest algorithms is the size of the dataset. Therefore, in order to improve the algorithms, we would need a larger dataset. For example, we could start the time frame in 2005 up to end 2021 (maybe also 2022). 

For the case of Random Forest, the training set would have a wider range of values and the model would predict values closer to the expected ones. Moreover, the effect of missing values would be smaller. We could also add other variables related to COVID-19 but with lesss missing values.

On the other hand, with this larger dataset we could try to train a Long Short-term Memory (LSTM) model or try to use SARIMAX (with an exogenous variable) to see how they behave
     
## Appendix: Sources and papers

*   Impact of COVID-19 on the travel and tourism industry: https://www.researchgate.net/profile/Malgorzata-Porada-Rochon/publication/346914362_Impact_of_COVID-19_on_the_travel_and_tourism_industry/links/600ffb55299bf14088c0e545/Impact-of-COVID-19-on-the-travel-and-tourism-industry.pdf
*   Predicting tourism trends with Google Insights
https://www.researchgate.net/publication/265201229_Predicting_tourism_trends_with_Google_Insights

*   Forecasting Tourist Arrivals via Random Forest and Long Short-term Memory https://www.researchgate.net/publication/342451405_Forecasting_Tourist_Arrivals_via_Random_Forest_and_Long_Short-term_Memory
*   Big Data as Input for Predicting Tourist Arrivals:
https://www.researchgate.net/publication/312416184_Big_Data_as_Input_for_Predicting_Tourist_Arrivals

*   Seasonal and Trend Forecasting of Tourist Arrivals: An Adaptive Multiscale Ensemble Learning Approach
https://arxiv.org/ftp/arxiv/papers/2002/2002.08021.pdf

*   Cruises and ferrys to Barcelona:
https://opendata.portdebarcelona.cat/en/dataset/estadistiques-de-trfic-de-vaixells

*   COVID-19 Data: https://aquas.gencat.cat/ca/actualitat/ultimes-dades-coronavirus
*   Hotels and tourists data:
https://www.ine.es/jaxiT3/Tabla.htm?t=2039&L=0
*   Passengers: https://ec.europa.eu/
*   Planes and aircrafts: https://www.mitma.gob.es/aereo

*   Google trends: https://trends.google.es/trends/
*   Mean temperatures: https://datosclima.es/Aemethistorico/Meteostation.php
*   Unemployment rate: https://www.epdata.es/


