# UB Capstone Project 2021

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

---

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

## Explanatory Analysis

### COVID-19 Data

COVID-19 is a disease with origin in China. It is a new virus linked to the same family of viruses as Severe Acute Respiratory Syndrome (SARS) and some types of common cold. 

This virus can be spread in many different ways. The rate of spread can easily increase  if people travel across countries for holidays, business trips, etc. That is why most of the countries took political decisions such as lockdowns and borders closing. And, therefore, the tourism industry has been one of the sectors hardest hit by COVID-19.

In this section we will look at how the disease has spread in Barcelona and the correlation between the spread, tourism and transportation data.

### Dependent Variable

Since we are under a forecasting task with time series data, we should expect patterns of seasonality and/or trends, especially for our tourism data. In facr, our dependent variable shows seasonality and trend patterns. It is reasonable to believe that "Viajeros_Tot" has a seasonality pattern because the number of visitors usually increase from spring to summer months. The positive trend might imply that Barcelona becomes more and more popular amongst tourists and, therefore, it receives every year an increase of visitors.

## Models and Scenarios

All the different models try to forecast the number of visitors in Barcelona for 2020-2021.
- Simple Linear Regression
- Multiple Linear Regression
- Random Forest
- SARIMA

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

     Carlos López-Martínez, Ignacio Matías Montorfano, Elena Picazo Gurina, Adrià Valls Sánchez.
