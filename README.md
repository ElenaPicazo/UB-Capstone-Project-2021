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


Predict Number of Visitors in Barcelona for 2020-2021.

Carlos López-Martínez, Ignacio Matías Montorfano, Elena Picazo Gurina, Adrià Valls Sánchez.
